---
tags: [materia, semestre-VII]
semestre: VII
---
# Base de Datos II

**Semestre:** [[Semestre VII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Sistema de Información I]]

## Desbloquea
- [[Sistema de Información II]]

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Base de datos 2`
- `~/Documentos/UNET/Base de datos 2.zip`

## Apuntes

### Descripción general y objetivos
Base de Datos II continúa [[Base de Datos I]] y [[Sistema de Información I]] con temas de **bases de datos avanzadas**: programación del lado del servidor (procedimientos, funciones, disparadores), transacciones y control de concurrencia, optimización de consultas, recuperación ante fallos, y -según el proyecto trabajado en el vault- **almacenes de datos (Data Warehouse), modelado dimensional y ETL**. El objetivo es que el estudiante diseñe, implemente y ajuste sistemas de datos más allá del modelo relacional básico. (Contenido programático oficial: verificar con el programa sinóptico de la UNET.)

Nota hija con el proyecto práctico: [[Data Warehouse Atenciones Estudiantiles]].

### Contenido programático (por unidades)
1. **SQL avanzado y programación en el servidor**
   - Subconsultas correlacionadas, CTE (`WITH`), funciones de ventana (`OVER`, `RANK`, `SUM() OVER`), `GROUP BY ROLLUP/CUBE`.
   - Vistas y vistas materializadas; esquemas y roles/privilegios.
   - Procedimientos almacenados, funciones, *triggers*, cursores (PL/pgSQL en PostgreSQL).
2. **Transacciones y concurrencia**
   - Propiedades ACID; niveles de aislamiento (Read Uncommitted, Read Committed, Repeatable Read, Serializable).
   - Anomalías: lectura sucia, lectura no repetible, fantasma.
   - Bloqueos (2PL), deadlock, MVCC, planificaciones serializables.
3. **Recuperación**: registro de transacciones (WAL), *checkpoints*, REDO/UNDO, respaldo y restauración.
4. **Indexación y optimización**: B-tree, hash, índices compuestos y parciales, planes de ejecución (`EXPLAIN ANALYZE`), estadísticas, selectividad, reordenamiento de joins.
5. **Almacenes de datos y BI**: OLTP vs OLAP, modelo estrella/copo de nieve, tabla de hechos y dimensiones, granularidad, ETL, dimensiones lentamente cambiantes (SCD), cubos y tableros (Power BI).
6. **Bases de datos distribuidas / NoSQL (introducción)**: fragmentación, replicación, teorema CAP, modelos documento/clave-valor/grafo. (Verificar alcance con el programa oficial.)

### Conceptos clave y definiciones
- **Transacción**: unidad lógica de trabajo que se ejecuta completa o no se ejecuta (atomicidad).
- **ACID**: Atomicidad, Consistencia, Aislamiento (*Isolation*), Durabilidad.
- **MVCC**: cada transacción ve una instantánea; lectores no bloquean escritores.
- **Plan de ejecución**: estrategia elegida por el optimizador (seq scan, index scan, hash join, nested loop, merge join).
- **OLTP**: procesamiento transaccional, muchas escrituras cortas, normalizado. **OLAP**: análisis, lecturas agregadas masivas, desnormalizado.
- **Tabla de hechos**: eventos medibles (métricas); **dimensión**: contexto descriptivo (quién, cuándo, dónde).
- **Grano (*grain*)**: qué representa exactamente una fila de la tabla de hechos; se define **antes** de diseñar.
- **Clave subrogada**: identificador artificial propiedad del DWH, independiente de la clave de negocio.
- **SCD Tipo 1 / 2 / 3**: sobrescribir / nueva versión con vigencia / columna con valor anterior.
- **ETL**: Extract, Transform, Load; carga **inicial** vs **incremental (diaria)**.

### Código de ejemplo
```sql
-- Función de ventana: ranking de carreras por atenciones
SELECT c.nombre_carrera,
       COUNT(*) AS total,
       RANK() OVER (ORDER BY COUNT(*) DESC) AS posicion
FROM dwh.hecho_atenciones h
JOIN dwh.dim_estudiante e ON e.id_estudiante = h.id_estudiante
JOIN dwh.dim_carrera   c ON c.id_carrera    = e.id_carrera
GROUP BY c.nombre_carrera;

-- Trigger de auditoría (PL/pgSQL)
CREATE OR REPLACE FUNCTION auditar() RETURNS trigger AS $$
BEGIN
  INSERT INTO bitacora(tabla, operacion, fecha) VALUES (TG_TABLE_NAME, TG_OP, now());
  RETURN NEW;
END $$ LANGUAGE plpgsql;
CREATE TRIGGER t_aud AFTER INSERT OR UPDATE ON cliente
FOR EACH ROW EXECUTE FUNCTION auditar();

-- Transacción con aislamiento fuerte
BEGIN ISOLATION LEVEL SERIALIZABLE;
UPDATE cuenta SET saldo = saldo - 100 WHERE id = 1;
UPDATE cuenta SET saldo = saldo + 100 WHERE id = 2;
COMMIT;
```

### Ejemplo resuelto breve
*¿Cuándo usar SCD Tipo 2?* Un estudiante cambia de carrera en 2025. Con Tipo 1 se perdería el historial y las atenciones previas se atribuirían a la carrera nueva. Con Tipo 2 se cierra la fila vieja (`fecha_fin`, `vigente = false`) y se inserta una nueva con otra clave subrogada; cada hecho apunta a la versión vigente el día de la atención.

### Relación con otras materias
- Prerrequisito directo: [[Sistema de Información I]]; fundamentos de [[Base de Datos I]].
- Habilita [[Sistema de Información II]] y se conecta con [[Administración de Base de Datos]] y [[Análisis y Procesamiento de Datos]].
- Usa [[Estructura de Datos]] (árboles B, hashing) y [[Estadística I]] para métricas.

### Evaluación y consejos de estudio
- Practique en un PostgreSQL real (Docker) y lea siempre `EXPLAIN ANALYZE`.
- Entienda el grano antes de escribir el DDL del DWH; la mayoría de errores nacen ahí.
- Practique ejercicios de planificaciones serializables y de deadlock a mano.
- Evaluación (verificar con el programa oficial): pruebas, proyecto de DWH/ETL con defensa.

### Bibliografía recomendada
- Elmasri, R. y Navathe, S. *Fundamentos de Sistemas de Bases de Datos*.
- Silberschatz, Korth, Sudarshan. *Fundamentos de Bases de Datos*.
- Kimball, R. y Ross, M. *The Data Warehouse Toolkit*.
- Documentación oficial de PostgreSQL.

### Recursos (material pesado fuera del vault)
Proyecto práctico en `~/Documentos/UNET/Base de datos 2` (README, MANUAL, `sql/`, `etl/`, `scheduler/`, `docs/powerbi.md`, modelos Excel) y el comprimido `Base de datos 2.zip`. No hay carpeta `Material/` dentro del vault. Resumen en [[Data Warehouse Atenciones Estudiantiles]].
