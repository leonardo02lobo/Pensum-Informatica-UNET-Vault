---
tags: [tema, semestre-V]
---
# SQL avanzado - ROLLUP CUBE y casos de estudio

Nota hija de [[Base de Datos I]] (Tema V).

## Requisitos del caso práctico "Gestión de Ventas"
1. Importar tablas desde Excel a Oracle XE con SQL Developer.
2. Crear restricciones (PK, FK, UNIQUE) desde las funcionalidades gráficas.
3. Obtener el diseño físico por ingeniería inversa en Data Modeler.
4. Resolver consultas SQL por partes con objetivos de aprendizaje: SELECT/FROM/WHERE, DISTINCT, expresiones, joins.

## Tipos de consulta del caso
- Proyección filtrada (ciudades y continente de Estados Unidos).
- Salida con formato mediante concatenación `||`: `'El Cliente ' || apellido || ' ' || nombre || ' es un ' || genero ...`.
- Agregaciones con `COUNT`, `ORDER BY` ascendente/descendente.
- Filtros por intervalo de fechas (`fecha_entrega - fecha_factura > 10`).

## GROUP BY con ROLLUP y CUBE
```sql
-- Subtotales jerárquicos
SELECT continente, tienda, SUM(monto)
FROM ventas GROUP BY ROLLUP (continente, tienda);

-- Todas las combinaciones
SELECT continente, tienda, SUM(monto), GROUPING(tienda) g
FROM ventas GROUP BY CUBE (continente, tienda);

-- Conjuntos de agrupación a medida
SELECT continente, tienda, SUM(monto)
FROM ventas GROUP BY GROUPING SETS ((continente), (tienda), ());
```
`ROLLUP(a,b)` produce (a,b), (a), (); `CUBE(a,b)` produce (a,b), (a), (b), (). `GROUPING()` devuelve 1 si la fila es un total de esa columna.
