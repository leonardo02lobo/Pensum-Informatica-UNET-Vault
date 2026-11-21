---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaIV/materialDeApoyo/Curso de SQL Basico.pdf
---
# Tema 4 - Curso de SQL básico: SELECT, joins y funciones

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 4 SQL Lenguaje de Definición de Datos]]
Siguiente: [[Base de Datos I - Tema 4 SQL DML y transacciones]]

## Contexto y objetivo
Resumen ampliado de las 71 diapositivas "Introducción a SQL" (Oracle). Cubre la consulta de datos con `SELECT`: proyección, selección, operadores, ordenamiento, combinaciones (joins) y la biblioteca de funciones de una fila y de grupo. Es la base del Tema 5 ([[Base de Datos I - Tema 5 Consultas avanzadas SQL]]). Complementa: [[Base de Datos I - Tema 3 Curso de Modelo Relacional]] (SELECT implementa selección, proyección y combinación).

## 1. Contexto técnico
SQL no es sensible a mayúsculas/minúsculas (los **datos** sí); las sentencias pueden ocupar varias líneas; las palabras clave no se abrevian; se recomienda indentar. Se ejecuta desde **SQL\*Plus** (herramienta de Oracle que envía SQL y PL/SQL al servidor y tiene sus propios comandos) o SQL Developer. `DESCRIBE tabla;` muestra nombre, nulabilidad y tipo de cada columna.

## 2. Estructura del SELECT
```sql
SELECT [DISTINCT] {* | columna [alias], ...}   -- QUÉ
FROM   tabla1 [, tabla2 ...]                   -- DE DÓNDE
[WHERE condición(es)]                          -- FILTRO
[ORDER BY exp [ASC | DESC], ...];              -- CLASIFICAR
```
Orden de evaluación lógico (complemento): FROM -> WHERE -> SELECT -> ORDER BY (por eso WHERE no puede usar alias definidos en el SELECT, pero ORDER BY sí).

### Proyección
- Columnas parciales: `SELECT no_dept, loc FROM dept;`
- Todas: `SELECT * FROM dept;`
- **Operadores aritméticos** `* / + -` con precedencia: `*` y `/` antes que `+` y `-`; igual prioridad de izquierda a derecha; paréntesis para alterar. Ejemplo: `SELECT nom_emp, sal, 12*sal + 100 FROM emp;` (Pedro: 5000 -> 60100).
- **DISTINCT** elimina duplicados: `SELECT DISTINCT cargo FROM empleado;`
- **Alias**: `salario*10 bono` o `"Salario Base"` (comillas dobles si hay espacios o mayúsculas mezcladas).
- **Concatenación** con `||`: `SELECT nom_emp || ' es un ' || cargo AS "Detalle de empleado" FROM emp;` -> "Pedro es un Presidente". Es el mismo recurso usado en el caso del Tema 5 ('El Cliente ' || apellido ...).

### Selección (WHERE)
Compara columnas, literales, expresiones o funciones. Cadenas y fechas entre **comillas simples**; las cadenas distinguen mayúsculas ('vendedor' no es 'VENDEDOR'); el formato de fecha por defecto depende de la instalación (DD-MON-YY).
| Operador | Significado |
|---|---|
| `= != <> ^= > >= < <=` | comparación |
| `BETWEEN a AND b` | entre dos valores, inclusive |
| `IN (lista)` | igual a alguno |
| `LIKE` | patrón: `%` cero o más caracteres, `_` un carácter (con escape para buscar literales) |
| `IS NULL / IS NOT NULL` | nulidad |
Ejemplos: `WHERE cargo IN ('SECRETARIA','CHOFER')`; `WHERE salario BETWEEN 10000 AND 20000`; `WHERE nom_emp LIKE '_A%'` (segunda letra A: RAUL, MARTIN, CARLOS); `WHERE jefe IS NULL`.

### Lógica trivaluada
Con NULL, las condiciones tienen tres valores: verdadero, falso, desconocido.
| AND | V | F | N |   | OR | V | F | N |
|---|---|---|---|---|---|---|---|---|
| V | V | F | N |   | V | V | V | V |
| F | F | F | F |   | F | V | F | N |
| N | N | F | N |   | N | V | N | N |
`NOT NULL` = nulo. WHERE solo devuelve filas cuya condición es **verdadera**. Precedencia: operadores de comparación, `NOT`, `AND`, `OR`. Ejemplo clásico:
```sql
WHERE (cargo = 'Vendedor' OR cargo = 'Presidente') AND sal > 1500   -- paréntesis cambian el resultado
```
Trampa: `WHERE columna NOT IN (1, NULL)` nunca devuelve filas (comparar con NULL da desconocido).

### Ordenamiento
`ORDER BY cargo DESC, nombre ASC` (ascendente por defecto; se puede usar alias o posición de columna: `ORDER BY 2`). Los NULL se ordenan al final en ASC en Oracle.

## 3. Combinaciones (joins)
| Tipo | Descripción |
|---|---|
| Simple: **equijoin** | condición de igualdad PK = FK |
| Simple: **non-equijoin** | condiciones distintas de igualdad (rangos) |
| **Externo** (outer) | incluye filas sin correspondencia |
| **Self join** | une una tabla consigo misma |

Reglas: se pueden unir tantas tablas como se desee; las columnas homónimas se califican `tabla.columna`; el criterio de unión va en el WHERE (sintaxis tradicional de Oracle); para N tablas se necesitan **al menos N-1 condiciones**, o se produce producto cartesiano.
```sql
-- equijoin
SELECT emp.nro_emp, emp.nom_emp, dept.loc
FROM emp, dept WHERE emp.no_dept = dept.no_dept;
-- non-equijoin: rangos salariales
SELECT e.nom_emp, e.sal, s.rango
FROM emp e, rangosal s WHERE e.sal BETWEEN s.salmin AND s.salmax;
-- outer join con (+) : el (+) va del lado deficiente en datos
SELECT e.nom_emp, d.dept, d.nom_dep
FROM emp e, depart d WHERE e.dep(+) = d.dep;   -- todos los departamentos, incluso sin empleados (ej. 'Servicio')
SELECT e.nom_emp, d.dept, d.nom_dep
FROM emp e, depart d WHERE e.dep = d.dep(+);   -- todos los empleados, incluso sin departamento (ej. 'Jesus')
-- self join
SELECT trabajador.nom_emp || ' trabaja para ' || gerente.nom_emp
FROM emp trabajador, emp gerente WHERE trabajador.jefe = gerente.nro_emp;
```
Equivalente ANSI (el que se usa en el caso de estudio): `FROM emp e LEFT JOIN depart d ON e.dep = d.dep`. En ANSI, `A LEFT JOIN B` conserva todas las filas de A; `RIGHT` las de B; `FULL` ambas.

## 4. Funciones SQL
Cinco tipos: aritméticas (valor simple, grupo, lista), cadena, fecha, conversión y varias.

**Numéricas (una fila)**: `NVL(n,m)` (si n es nulo devuelve m), `MOD(n,m)` residuo, `SQRT`, `ROUND(n,m)`, `TRUNC(n,m)`, `SIGN`, `POWER`, `ABS`, `CEIL` (menor entero >= n), `FLOOR`, `GREATEST/LEAST` (de una lista).

**Grupo**: `SUM`, `COUNT` (ignora nulos; `COUNT(*)` cuenta filas), `MAX`, `MIN`, `AVG` (ignora nulos). Ej.: `SELECT TO_CHAR(AVG(salario),'999G999D99') "Salario Medio", COUNT(comision) "Comisiones no nulas" FROM emple;`

**Fecha**: `ADD_MONTHS(n,m)`, `LAST_DAY`, `NEXT_DAY(n,c)`, `MONTHS_BETWEEN(n,m)`, `SYSDATE`. Aritmética: fecha1 - fecha2 = días (base del caso del Tema 5: `fecha_entrega - fecha_factura > 10`).

**Cadena**: `INITCAP`, `UPPER`, `LOWER`, `SUBSTR(c,n1,n2)`, `LENGTH`, `TRANSLATE(c1,c2,c3)` (ej. TRANSLATE('HOLA','AHOL','OCHA') = CHAO), `LPAD/RPAD(c,n,[relleno])`, `REPLACE`. `SUBSTR(NOMBRE,3,5)` de INVESTIGACION da VESTI; `LPAD(NOMBRE,15,'*')` rellena a la izquierda. `INITCAP` aparece en los triggers del caso del Tema 4.

**Conversión**: `TO_CHAR(d,[fmt])`, `TO_DATE(c,[fmt])`, `TO_NUMBER`, `CONVERT`. Formatos de número: `9` (ancho), `0` (ceros a la izquierda), `$`, `G` y `D` (separadores de miles y decimal según NLS), coma y punto. Formatos de fecha: `YYYY`, `YY`, `MM`, `MON`, `MONTH`, `D`, `DD`, `DDD`, `HH`, `MI`, `SS`. Ej.: `TO_CHAR(TO_DATE('01052021','ddmmyyyy'),'MONTH')` = MAYO.

**Varias**: `DECODE(c,n1,r1,n2,r2,...,d)` (un CASE simple), `USER`, `VSIZE`, `CONCAT`/`||`, `NVL2(n,m,p)` (m si n no es nulo, p si lo es), `NULLIF(a,b)` (null si iguales), `COALESCE` (primer no nulo).
```sql
SELECT numdept,
       DECODE(numdept, 1,'DEPARTAMENTO UNO', 2,'DEPARTAMENTO DOS', 'OTRO DEPARTAMENTO') nombre_dept
FROM empleado;
```

## 5. Ejemplo resuelto paso a paso
Pedido: "empleados con salario integral (12*sal + comisión, tratando nulos como 0), nombre del departamento, de mayor a menor".
```sql
SELECT e.nombre "Empleado",
       d.nombre "Departamento",
       12*e.salario + NVL(e.comision, 0) "Salario Integral"
FROM   empleado e, departamento d
WHERE  e.numdept = d.numdept
ORDER BY 3 DESC;
```
Pasos: (1) tablas y condición de join (N-1 = 1); (2) alias para claridad; (3) `NVL` evita que NULL contamine la suma (NULL + n = NULL); (4) orden por la tercera columna.

## Errores comunes
- Join sin condición (producto cartesiano).
- `= NULL` en vez de `IS NULL`.
- Comparar cadenas ignorando mayúsculas.
- Mezclar columnas agregadas y no agregadas sin GROUP BY (Tema 5).
- Poner el `(+)` en el lado equivocado del join.
- Usar `LIKE '%_%'` esperando buscar un guion bajo literal sin escape.

## Ejercicios propuestos
1. Liste los nombres que tengan la letra A en cualquier posición, sin duplicados. (`SELECT DISTINCT nombre FROM empleado WHERE UPPER(nombre) LIKE '%A%';`)
2. Muestre departamentos sin empleados. (outer join con `e.dep IS NULL`.)
3. Muestre años de antigüedad. (`TRUNC(MONTHS_BETWEEN(SYSDATE, fingreso)/12)`.)
4. Clasifique salarios en 'BAJO' (<10000), 'MEDIO', 'ALTO' (>30000) con DECODE/CASE.

## Conexiones
[[Base de Datos I - Tema 4 SQL DML y transacciones]], [[Base de Datos I - Tema 5 Curso Consultas Avanzadas SQL]], [[Administración de Base de Datos]].

## Fuente
`Material/baseDatosI/temaIV/materialDeApoyo/Curso de SQL Basico.pdf`. La tabla de verdad, el orden de evaluación y las advertencias sobre NOT IN/NULL son complemento.
