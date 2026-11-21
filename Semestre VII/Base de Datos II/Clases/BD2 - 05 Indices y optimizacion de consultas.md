---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: conocimiento general + sql/01_ddl.sql (índices del proyecto)
---
# BD2 - 05 Índices y optimización de consultas

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 04 Recuperacion WAL y respaldo]]
Siguiente: [[BD2 - 06 Data Warehouse OLAP y modelado dimensional]]

## Contexto y objetivo
Una consulta SQL describe *qué* se quiere; el **optimizador** decide *cómo* obtenerlo. Con millones de filas, la diferencia entre un recorrido secuencial y un acceso por índice es de segundos contra milisegundos. Objetivo: conocer las estructuras de índice, leer planes de ejecución y aplicar reglas de optimización.

## Almacenamiento
Los datos se guardan en **páginas** (8 KB en PostgreSQL). El costo se mide sobre todo en páginas leídas de disco. Una tabla sin índice solo admite **recorrido secuencial** (*seq scan*): lee todas las páginas.

## Tipos de índice
- **B-tree** (por defecto): árbol balanceado de orden alto; búsqueda, rango y ordenamiento en $O(\log_m n)$ con $m$ del orden de cientos, por lo que 3–4 niveles bastan para millones de filas. Soporta `=, <, >, BETWEEN, ORDER BY`, `LIKE 'abc%'`.
- **Hash**: solo igualdad.
- **GIN**: valores múltiples (arreglos, JSONB, texto completo). **GiST/SP-GiST**: geometría, rangos. **BRIN**: tablas enormes con correlación física (fechas ordenadas); índice minúsculo.
- **Árbol B+**: variante donde los datos están en hojas enlazadas (recorridos de rango eficientes); ver [[Estructura de Datos]].

### Variantes
- **Compuesto** `(a, b)`: sirve a consultas por `a` o por `a` y `b`, **no** solo por `b` (regla del prefijo izquierdo).
- **Parcial**: `CREATE UNIQUE INDEX ... ON dim_estudiante (cedula) WHERE vigente;`
- **Sobre expresión**: `CREATE INDEX ON t (lower(email));`
- **Cubriente** (`INCLUDE`): permite *index-only scan*.
- **Único**: impone unicidad (las claves primarias lo crean).

### Ejemplo real del proyecto
En `sql/01_ddl.sql` el índice único parcial garantiza una sola versión vigente por cédula (regla SCD2) y sirve al mismo tiempo de acceso rápido:
```sql
CREATE UNIQUE INDEX uq_dim_estudiante_cedula_vigente
    ON dwh.dim_estudiante (cedula) WHERE vigente;
CREATE INDEX ix_dim_estudiante_cedula  ON dwh.dim_estudiante (cedula);
CREATE INDEX ix_dim_estudiante_carrera ON dwh.dim_estudiante (id_carrera);
```
Un índice parcial es más pequeño que uno total y expresa una **restricción de integridad** que un `UNIQUE` normal no puede (la cédula se repite entre versiones históricas, pero no entre vigentes).

## Procesamiento de consultas
Fases: análisis sintáctico → reescritura → **planificación/optimización** → ejecución. El optimizador estima el costo de planes alternativos con **estadísticas** (`ANALYZE`, `pg_statistic`): número de filas, valores más frecuentes, histogramas.

**Selectividad** $s=\frac{\text{filas que cumplen}}{\text{filas totales}}$. Un índice conviene con selectividad alta (pocas filas, $s$ pequeño, típicamente < 5–10 %).

### Algoritmos de acceso y unión
- Acceso: Seq Scan, Index Scan, Index Only Scan, Bitmap Heap Scan.
- **Nested Loop**: para cada fila externa busca en la interna; bueno con pocas filas externas y índice en la interna. Costo $\approx n_e\cdot\log n_i$.
- **Hash Join**: construye tabla hash de la menor y sondea con la mayor; costo lineal $O(n+m)$; solo igualdad.
- **Merge Join**: ordena (o aprovecha orden) ambas y fusiona; bueno con entradas ordenadas.
- Orden de uniones: el optimizador explora (programación dinámica) y usa heurísticas genéticas (GEQO) con muchas tablas.

## EXPLAIN y EXPLAIN ANALYZE
```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT c.nombre_carrera, COUNT(*)
FROM dwh.hecho_atenciones h
JOIN dwh.dim_estudiante e USING (id_estudiante)
JOIN dwh.dim_carrera c USING (id_carrera)
GROUP BY 1;
```
Leer el plan de adentro hacia afuera. Campos: `cost=inicial..total`, `rows` (estimado) vs `actual rows` (real), `loops`, `Buffers`. **Una gran diferencia entre filas estimadas y reales** indica estadísticas desactualizadas (`ANALYZE`).

### Ejemplo resuelto
Tabla `pedido(id, id_cliente, fecha)` con 1 000 000 filas. `SELECT * FROM pedido WHERE id_cliente = 42;` sin índice: Seq Scan sobre ~6 000 páginas. Se crea `CREATE INDEX ON pedido(id_cliente)`; con 20 filas por cliente, el plan pasa a Bitmap/Index Scan leyendo unas decenas de páginas: mejora de ~100x. Pero `WHERE fecha::text LIKE '2026%'` **no** usa un índice sobre `fecha` (función aplicada a la columna): reescribir como `fecha >= '2026-01-01' AND fecha < '2027-01-01'`.

## Reglas de optimización
1. **Empujar selecciones** (filtrar antes de unir) y **proyecciones** (traer solo columnas necesarias; evitar `SELECT *`).
2. Evitar funciones sobre columnas indexadas en el `WHERE` (*sargability*).
3. Preferir `EXISTS` a `IN` con subconsultas grandes y `JOIN` frente a subconsultas correlacionadas.
4. Indexar claves foráneas (PostgreSQL no lo hace automáticamente) y columnas de `JOIN/WHERE/ORDER BY` frecuentes.
5. No sobre-indexar: cada índice cuesta espacio y ralentiza `INSERT/UPDATE/DELETE`. En cargas masivas de DWH conviene cargar y luego indexar.
6. Particionamiento por rango (fecha) en tablas de hechos grandes.
7. Mantenimiento: `VACUUM`, `ANALYZE`, `REINDEX`.

Algebra relacional: $\sigma_{p_1\wedge p_2}(R)=\sigma_{p_1}(\sigma_{p_2}(R))$; $\sigma_p(R\bowtie S)=\sigma_p(R)\bowtie S$ si $p$ solo usa atributos de $R$.

## Errores comunes
- Crear un índice y esperar que se use siempre (con baja selectividad el optimizador prefiere seq scan, y hace bien).
- Índice compuesto con columnas en orden incorrecto.
- Comparar tipos distintos (cast implícito que anula el índice).
- Optimizar sin medir: usar siempre `EXPLAIN ANALYZE`.

## Ejercicios propuestos
1. ¿Sirve un índice `(a,b)` para `WHERE b = 5`? *Resp.: normalmente no (prefijo izquierdo).*
2. Elija join para dos tablas grandes desordenadas con igualdad. *Resp.: Hash Join.*
3. ¿Qué índice acelera `WHERE lower(nombre) = 'ana'`? *Resp.: sobre expresión `(lower(nombre))`.*
4. Si el plan estima 10 filas y devuelve 100 000, ¿qué hacer? *Resp.: `ANALYZE`, revisar estadísticas/correlaciones.*

## Conexiones
[[BD2 - 01 SQL avanzado CTE y funciones de ventana]], [[BD2 - 07 DWH Atenciones DDL y modelo estrella]], [[Estructura de Datos]] (árboles B, hashing), [[Administración de Base de Datos]].

## Fuente
Conocimiento general (documentación de PostgreSQL, Silberschatz) e índices reales de `sql/01_ddl.sql`.
