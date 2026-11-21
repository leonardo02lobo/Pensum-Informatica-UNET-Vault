---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: ~/Documentos/UNET/Base de datos 2 (sql/02_funciones_scd2.sql, sql/06_migracion_claves_subrogadas.sql, etl/resolver.py)
---
# BD2 - 08 SCD Tipo 2 y claves subrogadas

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 07 DWH Atenciones DDL y modelo estrella]]
Siguiente: [[BD2 - 09 ETL carga inicial y carga diaria]]

## Contexto y objetivo
Los atributos de una dimensión cambian con el tiempo (un estudiante cambia de carrera). El DWH debe decidir si olvida el valor anterior o lo conserva. Esta nota explica los tipos de SCD (*Slowly Changing Dimensions*), la clave subrogada y cómo el proyecto los implementa con PL/pgSQL.

## Tipos de SCD
| Tipo | Estrategia | Historia | Uso |
|---|---|---|---|
| 0 | no cambia nunca | no | fecha de nacimiento |
| 1 | sobrescribe | no | corregir errores; `dim_carrera` |
| 2 | nueva fila con vigencia | completa | `dim_estudiante`, `dim_asesor` |
| 3 | columna "valor anterior" | un solo cambio | comparar antes/después |
| 6 | 1+2+3 híbrido | completa + actual | casos avanzados |

SCD2 añade `fecha_inicio_vigencia`, `fecha_fin_vigencia` y `vigente` (y a veces un `hash` de atributos para detectar cambios rápido).

## Clave subrogada
Entero artificial sin significado de negocio, **propiedad del DWH**. Ventajas: independencia del origen (que puede reutilizar o cambiar códigos), permite varias versiones de la misma entidad, joins rápidos con enteros, y miembro desconocido (-1). La **clave de negocio** (aquí la `cedula`) identifica la entidad; la subrogada identifica una **versión**.

## Implementación del proyecto: `aplicar_scd2_estudiante`
La función recibe cédula, atributos y `p_fecha_cambio` y distingue **cuatro casos**:
1. **No existe la cédula**: inserta primera versión (`vigente = TRUE`, sin fecha fin).
2. **Sin cambios** en nombre, apellido, género, fecha de nacimiento o carrera: devuelve el id actual (idempotente).
3. **Cambio el mismo día (o antes) del inicio de la versión vigente**: es una *corrección*, no una nueva versión; se actualiza en sitio (versionar produciría rangos solapados).
4. **Cambio real**: cierra la versión vigente con `fecha_fin_vigencia = p_fecha_cambio - 1` (el día anterior, para que no haya solape) y `vigente = FALSE`; inserta la nueva versión vigente desde `p_fecha_cambio`.
```sql
UPDATE dwh.dim_estudiante
   SET fecha_fin_vigencia = p_fecha_cambio - 1, vigente = FALSE
 WHERE id_estudiante = v_actual.id_estudiante;
INSERT INTO dwh.dim_estudiante (cedula, ..., fecha_inicio_vigencia, fecha_fin_vigencia, vigente)
VALUES (p_cedula, ..., p_fecha_cambio, NULL, TRUE)
RETURNING id_estudiante INTO v_nuevo_id;
```
Devuelve siempre el `id_estudiante` de la versión vigente resultante. El id lo asigna la secuencia `IDENTITY`, nunca `MAX+1` (que colisionaría con numeraciones del origen).

### Ejemplo resuelto
Estudiante cédula 27800076 está en "Informática" desde 2025-01-10 (id 100). El 2026-03-05 cambia a "Electrónica".
- Antes: fila 100 vigente=TRUE, fin NULL.
- Llamada: `aplicar_scd2_estudiante('27800076', ..., id_carrera_electronica, '2026-03-05')`.
- Después: fila 100 vigente=FALSE, fin=2026-03-04; fila 150 (nueva) vigente=TRUE, inicio=2026-03-05.
- Una atención del 2026-02-01 debe apuntar a 100; una del 2026-04-01 a 150.

## Resolución de la versión correcta para un hecho
`dwh.estudiante_vigente_en(cedula, fecha)` devuelve la versión cuyo rango cubre la **fecha del hecho** (no la vigente hoy). Si no existe, devuelve NULL y el ETL apunta al miembro desconocido (id -1) y lo registra. Esto es lo que mantiene correcta la historia: ver consultas por carrera en [[BD2 - 10 Consultas analiticas vistas y control de calidad]] (una atención pertenece a la carrera que el estudiante cursaba entonces).

`etl/resolver.py` documenta el problema que resolvió: antes el origen traía `id_tiempo` e `id_estudiante` ya calculados, con tres consecuencias: `dim_tiempo` de solo lectura (cualquier fecha posterior se rechazaba), un `id_tiempo` existente pero incorrecto pasaba sin ser detectado, y el SCD2 quedaba inútil (el hecho seguía apuntando a la versión cerrada). Se invirtió la responsabilidad: **el origen entrega claves de negocio, el DWH resuelve las subrogadas**.

También `_normalizar_cedula`: Excel entrega la cédula como entero, CSV como texto, pandas como float ("27800076.0"); todo debe colapsar en la misma cadena o el JOIN falla en silencio. Una cédula ausente queda `None` (rechazo) y no la cadena `"nan"`.

## Asesores (vigencia)
`dwh.dar_baja_asesor(id, fecha)` cierra la vigencia (`vigente = FALSE`) sin borrar: las atenciones históricas siguen vinculadas.

## Migración idempotente (06)
`sql/06_migracion_claves_subrogadas.sql` convierte un DWH ya cargado: crea `calendario_semestre` sembrada desde `dim_tiempo` (`MIN/MAX(fecha)` por semestre), convierte los ids en IDENTITY posicionando la secuencia en el máximo, relaja el CHECK de género para 'N', crea los miembros desconocidos y añade `cedula` al staging. Va dentro de `BEGIN` y usa `IF NOT EXISTS`/`ON CONFLICT`, por lo que puede repetirse. Idea transferible: tras insertar ids explícitos hay que **sincronizar la secuencia** (`db.sincronizar_secuencia`) o el siguiente id generado chocaría.

## Errores comunes
- Usar `fecha_fin = fecha_cambio` (rangos que se tocan: dos versiones vigentes el mismo día).
- Versionar correcciones tipográficas como si fueran cambios reales.
- Unir el hecho a la dimensión por cédula (multiplica filas por versión) en lugar de por clave subrogada.
- `MAX(id)+1` como generador de claves.
- Contar `COUNT(*)` de estudiantes sin `COUNT(DISTINCT cedula)`.

## Ejercicios propuestos
1. ¿Cuántas versiones vigentes por cédula permite el modelo? *Resp.: exactamente una (índice único parcial).*
2. Un cambio de carrera con fecha anterior al inicio de la versión vigente, ¿qué caso? *Resp.: caso 3, corrección en sitio.*
3. Diseñe SCD3 para carrera. *Resp.: columnas `carrera_actual`, `carrera_anterior`, `fecha_cambio`.*

## Conexiones
[[BD2 - 02 PL-pgSQL funciones procedimientos y triggers]], [[BD2 - 06 Data Warehouse OLAP y modelado dimensional]], [[BD2 - 09 ETL carga inicial y carga diaria]].

## Fuente
`sql/02_funciones_scd2.sql`, `sql/06_migracion_claves_subrogadas.sql`, `etl/resolver.py`.
