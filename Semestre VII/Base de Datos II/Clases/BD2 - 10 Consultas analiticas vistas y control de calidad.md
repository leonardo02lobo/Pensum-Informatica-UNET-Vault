---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: ~/Documentos/UNET/Base de datos 2 (sql/03, sql/04, sql/05, docs/powerbi.md)
---
# BD2 - 10 Consultas analíticas, vistas, control de calidad y Power BI

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 09 ETL carga inicial y carga diaria]]
Siguiente: [[BD2 - 11 Bases de datos distribuidas NoSQL y teorema CAP]]

## Contexto y objetivo
Fase 3 del proyecto: responder **ocho preguntas de negocio** con SQL sobre el esquema estrella, exponer vistas limpias para Power BI y verificar la integridad con controles que deben devolver **0 filas**.

## Las ocho preguntas
| # | Pregunta | Técnica |
|---|---|---|
| 1 | Atenciones por semestre | `COUNT`, `SUM(COUNT(*)) OVER ()` para % |
| 2 | Top 5 carreras | `GROUP BY ... ORDER BY ... LIMIT 5`, `COUNT(DISTINCT cedula)` |
| 3 | Satisfacción promedio por tipo de apoyo (indicador) | `AVG`, `STDDEV_SAMP`, `FILTER` |
| 3b | Igual por servicio, con `HAVING COUNT(*) >= 20` | umbral de muestra |
| 4 | Top 5 asesores por satisfacción y semestre | CTE + `RANK() OVER (PARTITION BY semestre ...)`, mínimo 10 atenciones |
| 5 | Duración promedio por tipo de apoyo (indicador) | `AVG` |
| 6 | Carreras con más apoyo psicológico | filtro por `tipo`, más % dentro de cada carrera |
| 7 | Distribución presencial/virtual | `modalidad` de `dim_tipo_modalidad` |
| 8 | Proporción socioeconómico vs académico | `tipo` |

### Detalles reales y por qué importan
- **Receso excluido** (`WHERE semestre_academico <> 'Receso'`) para que el resultado siga siendo correcto si llegase un dato en receso.
- **SCD2 en pregunta 2**: se agrupa por la carrera de la *versión* del estudiante vigente el día de la atención; quien cambió de carrera aporta atenciones a ambas carreras, cada una en su período. Se usa `COUNT(DISTINCT e.cedula)` para contar personas (no versiones).
- **Pregunta 3**: se reporta además dispersión y `pct_satisfechos = 100.0*COUNT(*) FILTER (WHERE satisfaccion >= 4)/COUNT(*)`, porque el promedio esconde la dispersión.
- **Pregunta 4 (top N por grupo)**: la CTE `promedio_asesor_semestre` calcula promedio y conteo con `HAVING COUNT(*) >= 10` (un asesor con una única atención de 5 estrellas no debe encabezar); la CTE `ranking` aplica `RANK() OVER (PARTITION BY semestre_academico ORDER BY satisfaccion_promedio DESC, atenciones DESC)`; la consulta final filtra `puesto <= 5`.
- **Pregunta 6**: el conteo absoluto casi siempre favorece a la carrera con más estudiantes; el porcentaje relativo corrige el sesgo.

## Vistas para Power BI (`04_vistas_powerbi.sql`)
Vistas: `v_dim_estudiante` (nombre completo, edad con `AGE`, carrera), `v_dim_asesor`, `v_dim_apoyo`, `v_dim_tiempo` (nombre de mes/día con `TO_CHAR`, y **`orden_semestre`** numérico: `anio*10 + número de semestre`, 0 para receso), `v_hecho_atenciones` y `v_atenciones_completo` (versión aplanada). Se crea el rol `powerbi` de **solo lectura** (SELECT). Las vistas ocultan claves técnicas, dan nombres legibles y desacoplan al informe del esquema físico.

### Conexión (docs/powerbi.md)
- Requiere el proveedor Npgsql ("Npgsql GAC Installation").
- Servidor `localhost:5433`, base `dwh_atenciones`, usuario `powerbi`.
- Modo **Importar** (5.520 hechos: volumen pequeño); DirectQuery solo si hace falta ver la carga de las 23:30 sin refrescar.
- Importar `v_hecho_atenciones` y las cuatro `v_dim_*`; **no** importar `v_atenciones_completo` junto con las demás (duplica datos).
- Relaciones muchos-a-uno desde el hecho a cada dimensión, dirección simple. Ordenar `semestre_academico` por `orden_semestre`, o Power BI los ordena alfabéticamente.

## Control de calidad (`05_control_calidad.sql`)
Cada consulta debe devolver 0 filas. Ejemplos revisados:
1. Huérfanos: FK del hecho sin dimensión (LEFT JOIN ... WHERE dim IS NULL).
2. Más de una versión vigente por cédula.
3. Rangos de vigencia solapados (autounión con `a.inicio <= COALESCE(b.fin,'9999-12-31') AND b.inicio <= COALESCE(a.fin,...)`).
4. Atención apuntando a una versión no vigente ese día.
5. Asesor y apoyo con distinto tipo/modalidad.
6 a 11: calendario, desconocidos, discrepancia de semestre con `calendario_semestre`, etc. (no revisados en detalle; ver el archivo). El README habla de 11 controles y el MANUAL de 7 en una sección: documentación desactualizada, verificar.

Técnica útil: el anti-join `LEFT JOIN ... IS NULL` para detectar huérfanos y la autounión con `id_a < id_b` para detectar pares solapados sin duplicados.

## Ejemplo resuelto: detectar solape
Versiones de cédula X: A (2025-01-01 a 2026-03-04), B (2026-03-05 a NULL). `a.inicio <= b.fin` (2025-01-01 <= 9999-12-31) cierto; `b.inicio <= a.fin` (2026-03-05 <= 2026-03-04) falso: no hay solape, el control no devuelve filas. Si A terminara el 2026-03-05, daría cierto: solape.

## Errores comunes
- Importar la vista aplanada y las dimensiones a la vez en Power BI.
- Conectar el informe con el usuario administrador.
- Rankings sin umbral mínimo de muestra.
- Contar filas del hecho cuando se pide contar personas.

## Ejercicios propuestos
1. Escriba la pregunta 7 (distribución presencial/virtual con porcentaje). *Resp.: join hecho-apoyo-tipo_modalidad, `GROUP BY modalidad`, `100.0*COUNT(*)/SUM(COUNT(*)) OVER ()`.*
2. Proponga un control de calidad nuevo. *Resp.: satisfacción fuera de 1-5 o duración <= 0 (debe dar 0 filas).*
3. ¿Por qué un rol de solo lectura? *Resp.: principio de mínimo privilegio.*

## Conexiones
[[BD2 - 01 SQL avanzado CTE y funciones de ventana]], [[BD2 - 07 DWH Atenciones DDL y modelo estrella]], [[Sistema de Información II]] (KPIs y BI), [[Estadística I]].

## Fuente
`sql/03_queries_preguntas.sql` (preguntas 1-4 leídas completas; 5-8 por el README), `sql/04_vistas_powerbi.sql` (parcial), `sql/05_control_calidad.sql` (parcial), `docs/powerbi.md`.
