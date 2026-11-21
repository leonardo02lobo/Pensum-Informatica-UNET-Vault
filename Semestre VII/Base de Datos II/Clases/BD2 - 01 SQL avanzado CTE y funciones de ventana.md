---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: conocimiento general + sql/03_queries_preguntas.sql de ~/Documentos/UNET/Base de datos 2
---
# BD2 - 01 SQL avanzado: subconsultas, CTE y funciones de ventana

Materia: [[Base de Datos II]]
Siguiente: [[BD2 - 02 PL-pgSQL funciones procedimientos y triggers]]

## Contexto y objetivo
[[Base de Datos I]] cubre `SELECT`, `JOIN`, `GROUP BY`. En Base de Datos II el SQL se usa para **analizar**: rankings, acumulados, porcentajes del total, comparaciones contra el período anterior. Estas consultas son la base de los informes de un almacén de datos (ver [[BD2 - 10 Consultas analiticas vistas y control de calidad]]). El objetivo es dominar tres herramientas: subconsultas (correlacionadas y no), expresiones de tabla comunes (CTE) y funciones de ventana.

## Subconsultas
Una subconsulta es un `SELECT` dentro de otro. Tipos:
- **Escalar**: devuelve una fila y una columna; se usa donde iría un valor. `WHERE precio > (SELECT AVG(precio) FROM producto)`.
- **De lista** (`IN`, `ANY`, `ALL`): `WHERE id IN (SELECT id_cliente FROM pedido)`.
- **De tabla** (en `FROM`): una *tabla derivada* con alias obligatorio.
- **Correlacionada**: referencia columnas de la consulta externa y se reevalúa por cada fila externa. `EXISTS` es su uso más eficiente.

```sql
-- Estudiantes con más atenciones que el promedio de su carrera (correlacionada)
SELECT e.cedula, COUNT(*) AS n
FROM dwh.hecho_atenciones h JOIN dwh.dim_estudiante e USING (id_estudiante)
GROUP BY e.cedula, e.id_carrera
HAVING COUNT(*) > (
   SELECT AVG(x.n) FROM (
      SELECT COUNT(*) AS n FROM dwh.hecho_atenciones h2
      JOIN dwh.dim_estudiante e2 USING (id_estudiante)
      WHERE e2.id_carrera = e.id_carrera GROUP BY e2.cedula) x);
```
Observación: `NOT IN` con `NULL` en la lista devuelve vacío (lógica de tres valores); prefiera `NOT EXISTS`.

## CTE (`WITH`)
Una CTE nombra una subconsulta para reutilizarla y mejorar la legibilidad.
```sql
WITH por_carrera AS (
   SELECT c.nombre_carrera, COUNT(*) AS total
   FROM dwh.hecho_atenciones h
   JOIN dwh.dim_estudiante e USING (id_estudiante)
   JOIN dwh.dim_carrera c USING (id_carrera)
   GROUP BY c.nombre_carrera)
SELECT nombre_carrera, total,
       ROUND(100.0*total/SUM(total) OVER (),2) AS pct
FROM por_carrera ORDER BY total DESC;
```
En PostgreSQL 12+ las CTE no recursivas se "inlinean" salvo que se use `MATERIALIZED`.

### CTE recursivas
Sirven para jerarquías (organigramas, categorías) y series.
```sql
WITH RECURSIVE dias AS (
  SELECT DATE '2026-01-01' AS d
  UNION ALL
  SELECT d + 1 FROM dias WHERE d < DATE '2026-01-10')
SELECT * FROM dias;
```
Estructura: parte ancla + `UNION ALL` + parte recursiva con condición de parada. Sin condición de parada hay bucle infinito.

## Funciones de ventana
Calculan un valor **por fila** usando un conjunto de filas relacionadas (la *ventana*) **sin colapsar** filas como hace `GROUP BY`.

Sintaxis: `función(...) OVER ([PARTITION BY ...] [ORDER BY ...] [marco])`.

| Familia | Funciones | Uso |
|---|---|---|
| Ranking | `ROW_NUMBER`, `RANK`, `DENSE_RANK`, `NTILE` | Top-N por grupo |
| Agregadas | `SUM/AVG/COUNT ... OVER` | Acumulados, % del total |
| Desplazamiento | `LAG`, `LEAD`, `FIRST_VALUE`, `LAST_VALUE` | Comparar con fila anterior |

Diferencia de ranking con empates en los valores (10, 10, 8): `ROW_NUMBER` = 1,2,3; `RANK` = 1,1,3; `DENSE_RANK` = 1,1,2.

### Marcos
`ROWS BETWEEN 2 PRECEDING AND CURRENT ROW` (promedio móvil de 3). Con `ORDER BY` y sin marco el valor por defecto es `RANGE UNBOUNDED PRECEDING .. CURRENT ROW` (acumulado).

### Ejemplo del proyecto (real)
La pregunta 1 del proyecto calcula el porcentaje respecto al total usando `SUM(COUNT(*)) OVER ()`: primero se agrupa y luego la ventana suma los conteos de todos los grupos.
```sql
SELECT t.semestre_academico, COUNT(*) AS total_atenciones,
       ROUND(100.0 * COUNT(*) / SUM(COUNT(*)) OVER (), 2) AS porcentaje_del_total
FROM dwh.hecho_atenciones h JOIN dwh.dim_tiempo t ON t.id_tiempo = h.id_tiempo
WHERE t.semestre_academico <> 'Receso'
GROUP BY t.semestre_academico ORDER BY 1;
```
Para el ranking de asesores por semestre (pregunta 4) se emplea `RANK() OVER (PARTITION BY semestre ORDER BY satisfaccion DESC)` y luego se filtra `rk <= 5` en una consulta externa o CTE (no se puede filtrar una ventana en el mismo `WHERE`, porque `WHERE` se evalúa antes).

## Otros operadores analíticos
- `FILTER (WHERE ...)`: agregado condicional. `COUNT(*) FILTER (WHERE satisfaccion >= 4)` (usado en el proyecto para el % de satisfechos).
- `GROUPING SETS`, `ROLLUP`, `CUBE`: subtotales en una sola consulta. `GROUP BY ROLLUP(anio, mes)` produce filas por (año, mes), por año y total general.
- `STDDEV_SAMP`, `PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY x)` para mediana.
- `LATERAL`: subconsulta que ve columnas de tablas anteriores del `FROM` (útil para "top 3 por grupo").

## Ejemplo resuelto: variación mensual
Tabla `ventas(mes, monto)`: (1,100), (2,120), (3,90).
```sql
SELECT mes, monto,
       monto - LAG(monto) OVER (ORDER BY mes) AS delta,
       ROUND(100.0*(monto-LAG(monto) OVER (ORDER BY mes))/LAG(monto) OVER (ORDER BY mes),1) AS pct
FROM ventas;
```
Resultado: mes 1 delta NULL; mes 2 delta 20 (20.0%); mes 3 delta -30 (-25.0%).

## Errores comunes
1. Filtrar por una función de ventana en `WHERE` (usar CTE/subconsulta).
2. Usar `RANK` creyendo que no deja huecos.
3. `NOT IN` con NULL.
4. Olvidar `PARTITION BY` y obtener un ranking global.
5. Dividir enteros (`100*a/b` con enteros trunca): use `100.0*`.
6. `LAST_VALUE` sin ajustar el marco devuelve la fila actual.

## Ejercicios propuestos
1. Escriba el top 3 de productos por categoría. *Resp.: `ROW_NUMBER() OVER (PARTITION BY cat ORDER BY ventas DESC)` y filtrar `<=3`.*
2. Calcule el acumulado de atenciones por mes. *Resp.: `SUM(COUNT(*)) OVER (ORDER BY mes)` tras agrupar.*
3. ¿Qué devuelve `DENSE_RANK` para (5,5,4,3)? *Resp.: 1,1,2,3.*
4. Genere los días de febrero con CTE recursiva. *Resp.: ancla `DATE '2026-02-01'`, parar en el 28.*

## Conexiones
Estas técnicas se aplican en [[BD2 - 10 Consultas analiticas vistas y control de calidad]] y se optimizan con [[BD2 - 05 Indices y optimizacion de consultas]]. Relación con [[Análisis y Procesamiento de Datos]].

## Fuente
Conocimiento general (documentación de PostgreSQL) y consultas reales de `sql/03_queries_preguntas.sql` del proyecto en `~/Documentos/UNET/Base de datos 2`.
