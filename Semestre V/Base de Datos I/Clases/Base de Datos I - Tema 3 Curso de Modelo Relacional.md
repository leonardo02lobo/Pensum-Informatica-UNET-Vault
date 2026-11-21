---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaIII/materialApoyo/Curso de Modelo Relacional.pdf
---
# Tema 3 - El modelo relacional y el álgebra relacional

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 2 Caso de Estudio Requisitos y DER]]
Siguiente: [[Base de Datos I - Tema 3 Curso de Diseño Físico]]

## Contexto y objetivo
Tras el DER (modelo conceptual) se necesita un formalismo matemático para representar y consultar datos: el **modelo relacional**. Este apunte reconstruye las 31 diapositivas "El Modelo Relacional": definición, elementos (relación, atributo, dominio, tupla), claves, y **álgebra relacional** con ejemplos sobre facturas y productos. Es el fundamento teórico de SQL (Temas IV-V) y de la sección 8b del caso de estudio ([[Base de Datos I - Tema 3 Caso de Estudio Diseño Físico]]).

## 1. Origen y ventajas
En 1970 E. F. Codd (IBM) publicó "Un modelo relacional de datos para grandes bancos de datos compartidos". El modelo usa **tablas bidimensionales** para la representación **lógica** de datos y relaciones (no es una representación física) y se basa en la teoría matemática de relaciones. Ventajas citadas: visión conceptual simple, comprensible por usuarios no expertos, **independencia física** (el usuario no necesita saber dónde están los datos), posibilidad de ampliar el esquema conceptual sin modificar los programas, eliminación de redundancia y minimización de cálculos derivados almacenados (ver [[Base de Datos I - Tema 1 Fundamentos de Base de Datos]]).

## 2. Elementos formales
- **Relación (tabla)**: conjunto de tuplas. Cada fila representa una asociación entre valores. Hay correspondencia directa con la relación matemática.
- **Atributo**: propiedad de los datos almacenados (columna).
- **Dominio**: conjunto **nominado, finito y homogéneo de valores atómicos**; atómico = indivisible. Existe independientemente de las tablas.
- **Tupla**: ocurrencia de la relación (fila).
- **Producto cartesiano**: una relación de $n$ atributos es un subconjunto de $D_1 \times D_2 \times \dots \times D_n$.

Ejemplo del curso: tabla Cuenta(numero_cuenta, nombre_sucursal, saldo) con dominios $D_1$ (números de cuenta), $D_2$ (sucursales), $D_3$ (saldos). La tabla contiene solo un subconjunto de todas las combinaciones posibles: Cuenta $\subseteq D_1 \times D_2 \times D_3$. Con 7 tuplas, p. ej. (C-101, Centro, 500), (C-102, Navacerrada, 400), (C-201, Galapagar, 900)... Se escribe $t \in r$ para decir que la tupla $t$ pertenece a la relación $r$.

- **Esquema de relación**: $R(A_1, \dots, A_n)$ con sus dominios; ejemplo `Esquema_cuenta(numero_cuenta, nombre_sucursal, saldo)`.
- **Instancia (ejemplar)**: el contenido en un instante; el esquema es el diseño lógico y casi no cambia.
- **Grado**: número de columnas; **cardinalidad**: número de filas; **valor**: celda; **NULL**: ausencia de dato (no es cero ni cadena vacía).

## 3. Claves y restricciones
- **Clave primaria (PK)**: columna(s) que identifican cada fila; no admite NULL.
- **Clave foránea (FK)**: columnas cuyos valores corresponden a los de la PK de otra tabla; implementan las relaciones y garantizan la **integridad referencial**.
- **Clave única (UK)**: no puede haber dos filas con los mismos valores en esas columnas (admite NULL en la mayoría de motores).
- **Dominios**: generales o restringidos (CHECK).
- **Vista**: tabla ficticia derivada de otras; solo se almacena su definición.
Tabla de ejemplo EMPLEADOS(Nro_Emp PK, Nombre UK, Dirección, Fecha_Nacim, Nro_Dept FK): 1011 Pérez Carlos...; 1210 Chacon María...; 1416 Colmenares José.

## 4. Álgebra relacional
Lenguaje procedimental formal cuyos operandos son tablas y cuyo resultado es otra tabla (propiedad de **clausura**). Es la base teórica de las consultas SQL y de los planes de ejecución del optimizador.

### Operaciones básicas
| Operación | Símbolo | Condición | Descripción |
|---|---|---|---|
| Selección | $\sigma_{cond}(R)$ | -- | filtra **filas** con todas las columnas |
| Proyección | $\pi_{A_1,\dots,A_k}(R)$ | -- | elige **columnas**; elimina duplicados |
| Unión | $R \cup S$ | mismo número de columnas y dominios compatibles | filas de ambas; sin duplicados |
| Diferencia | $R - S$ | compatibles | filas de $R$ que no están en $S$ |
| Producto cartesiano | $R \times S$ | nombres de columnas distintos | todas las combinaciones; $|R|\cdot|S|$ filas |

### Operaciones derivadas
- **Intersección** $R \cap S = R - (R - S)$.
- **Combinación (join)**: $R \bowtie_{cond} S = \sigma_{cond}(R \times S)$. Con condición de igualdad PK = FK se llama equijoin/join natural.

### Ejemplos del curso
Datos: PRODUCTO(codigo, descripcion, existencia, precio) con (5100 Patatas 500 78) y (5200 Cebollas 250 90); FACTURA(nro_fac, fecha); ITEMS_FACTURA(nro_fac, codigo, cantidad).
1. Código, descripción y existencia: $\pi_{codigo,descripcion,existencia}(producto)$.
2. Productos con existencia menor a 500: $\pi_{codigo,existencia}(\sigma_{existencia<500}(producto))$ -> (5200, 250).
3. Facturas con sus ítems: $\pi_{f.nro\_fac,\ f.fecha,\ i.codigo,\ i.cantidad}(\sigma_{f.nro\_fac=i.nro\_fac}(factura \times items))$.
4. Facturas del producto 5200: se añade `and items.codigo = 5200` en la selección -> facturas 1 (150 unidades) y 2 (80).

### Ejemplo detallado del producto cartesiano y el join
VENTAS(codi, fecha, cantidad) con 3 filas x ARTICULOS(codigo, descripcion, existencia, precio) con 2 filas da 6 filas. La selección $\sigma_{ventas.codi=articulos.codigo}$ deja solo 3 filas coherentes (las que emparejan código con código); la proyección final quita la columna duplicada. Esto muestra por qué un join "ingenuo" sin condición es un error grave: genera filas basura multiplicando tablas (ver errores comunes).

### Correspondencia con SQL
| Álgebra | SQL |
|---|---|
| $\sigma$ | `WHERE` |
| $\pi$ | lista del `SELECT` (con `DISTINCT` para eliminar duplicados) |
| $\times$ | `FROM t1, t2` o `CROSS JOIN` |
| $\bowtie$ | `JOIN ... ON` |
| $\cup,\cap,-$ | `UNION`, `INTERSECT`, `MINUS` (Oracle) |
Ejemplo: $\pi_{codigo,existencia}(\sigma_{existencia<500}(producto))$ equivale a `SELECT DISTINCT codigo, existencia FROM producto WHERE existencia < 500;`. Nota: SQL trabaja con bolsas (multiconjuntos) y conserva duplicados si no se pide DISTINCT; el álgebra clásica trabaja con conjuntos.

## 5. Ejercicios del curso con solución propuesta
Con las tres relaciones anteriores:
1. Descripción y precio de productos con existencia > 100: $\pi_{descripcion,precio}(\sigma_{existencia>100}(producto))$.
2. Nro. de factura, fecha, cantidad y precio unitario: $\pi_{f.nro\_fac, f.fecha, i.cantidad, p.precio}(\sigma_{f.nro\_fac=i.nro\_fac \wedge i.codigo=p.codigo}(f \times i \times p))$.
3. Facturados el 18/06/2021: añadir $f.fecha = '18/06/2021'$ en la selección y proyectar nro_fac, código, cantidad.
4. Con descripción del producto: igual que (2) agregando p.descripcion y código.
5. Cantidad < 100: añadir $i.cantidad < 100$.
6. Precio pagado por ítem: proyección extendida con $i.cantidad \cdot p.precio$ (columna calculada; muchos textos la escriben como extensión del álgebra).

## Errores comunes
- Olvidar la condición de join (producto cartesiano accidental).
- Confundir $\sigma$ (filas) con $\pi$ (columnas); la letra griega no indica orden sino función.
- Aplicar unión o diferencia a tablas con distinto número de columnas o dominios incompatibles.
- Pensar que una FK puede apuntar a una columna no única.
- Tratar NULL como un valor comparable con `=`; en SQL se usa `IS NULL`.

## Conexiones
- Diseño físico y normalización: [[Base de Datos I - Tema 3 Curso de Diseño Físico]].
- Ejemplo guiado completo: [[Base de Datos I - Tema 3 Caso Práctico Ejemplo Servicios Informáticos]].
- SQL: [[Base de Datos I - Tema 4 Curso de SQL Básico]], [[Base de Datos I - Tema 5 Consultas avanzadas SQL]].
- Teoría de [[Estructura de Datos]]: conjuntos y relaciones.

## Fuente
`Material/baseDatosI/temaIII/materialApoyo/Curso de Modelo Relacional.pdf`. Las soluciones de los ejercicios y la correspondencia con SQL son complemento de conocimiento general.
