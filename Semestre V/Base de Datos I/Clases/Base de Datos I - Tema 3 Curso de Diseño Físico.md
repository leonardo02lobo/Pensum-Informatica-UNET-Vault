---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaIII/materialApoyo/Curso de Diseño Fisico.pdf
---
# Tema 3 - Diseño físico relacional: mapeo, supertipos, arcos y normalización

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 3 Curso de Modelo Relacional]]
Siguiente: [[Base de Datos I - Tema 3 Caso Práctico Ejemplo Servicios Informáticos]]

## Contexto y objetivo
El **diseño físico relacional** transforma el modelo lógico (DER), orientado al **QUÉ**, en una estructura de tablas orientada al **CÓMO**: nombres de tablas y columnas, claves primarias, foráneas y únicas. Estas diapositivas (38) son la guía de transformación del curso: notación de diagrama de tablas, reglas de mapeo (relaciones 1:M, M:M, 1:1, identificador compuesto, arcos, supertipo/subtipo) y **normalización hasta 3FN** con un ejemplo de facturas. Se aplica en el Tema 3 del caso ([[Base de Datos I - Tema 3 Caso de Estudio Diseño Físico]]) y se implementa en SQL en el Tema 4.

## 1. Notación del diagrama de tablas
Cada tabla se dibuja con nombre y **nombre corto de 3 letras** entre paréntesis (EMPLEADOS (EPO)). Cada columna lleva prefijos:
- `pk` clave primaria, `fk` clave foránea (con número `fk1`, `fk2`), `uk` clave única (`uk1`, `uk2` para claves únicas compuestas).
- `*` columna obligatoria (NOT NULL), `o` columna opcional.
- Las relaciones se nombran con el patrón `fk = <tabla_hija>_<tabla_padre>_fk` (por ejemplo `epo_dpo_fk`, `ite_fta_fk`).
Esta es la notación que genera Oracle SQL Developer Data Modeler en el modelo relacional ([[Base de Datos I - Tema 2 Oracle SQL Developer Data Modeler]]).

## 2. Mapeo de entidades a tablas
Una entidad EMPLEADO con identificador primario `# Nro.Emp`, secundario `(#) Nombre, (#) Fecha nacim` y opcional `o Direccion` produce la tabla EMPLEADOS (EPO) con:
- `pk * Nro_Emp`;
- `uk1 * Nombre`, `uk1 * Fecha_Nacim` (clave única **compuesta**: ambas columnas con el mismo `uk1`);
- `o Direccion`.
Reglas: identificador primario -> PK; secundarios -> UK; atributos obligatorios -> NOT NULL; opcionales -> NULL; el nombre de entidad se pluraliza como nombre de tabla (convención del curso).

## 3. Mapeo de relaciones
- **1:M**: la FK va en la tabla del lado "muchos". Ejemplo: DEPARTAMENTO 1:M EMPLEADO -> EMPLEADOS recibe `fk1 * Dept_id` (obligatoria porque cada empleado debe pertenecer a un departamento), con `fk1 = epo_dpo_fk`. Una relación recursiva (jefe) agrega `fk2 o Emp_id` (opcional, el jefe puede no existir) con `epo_epo_fk`. La obligatoriedad de la FK refleja la opcionalidad del DER: "debe ser" -> NOT NULL; "puede ser" -> NULL.
- **M:M**: se crea una **tabla de intersección** (asociativa) cuya PK es la combinación de las dos FK (`Pk,fk1` y `Pk,fk2`) más los atributos de la asociación. Ejemplo: PEDFAC(N_ped, N_prod, Cantidad_pedida).
- **1:1**: la FK (única) va en la tabla del lado obligatorio o se fusionan las tablas si ambos lados son obligatorios.
- **Identificador único compuesto (en cascada)**: la PK de la tabla hija incluye la FK del padre (`Pk,fk`): ITEMS(Nro_Factura PK-FK, Código_producto PK-FK).

## 4. Implementación de un arco
Un **arco** (OR exclusivo entre relaciones) se implementa con **una FK por cada relación del arco, todas opcionales**, más una restricción **CHECK** que garantiza que **exactamente una** (el curso dice "por lo menos una"; para exclusividad estricta se exige una y solo una) sea NOT NULL. Ejemplo: entidad X con arco hacia Y y Z -> tabla XS con `FK1 o Y_Id`, `FK2 o Z_Id`:
```sql
ALTER TABLE xs ADD CONSTRAINT xs_arco_ck CHECK (
  (y_id IS NOT NULL AND z_id IS NULL) OR
  (y_id IS NULL     AND z_id IS NOT NULL)
);
```
Se usa en el caso de estudio para las subcategorías (software/equipo), implementadas como arco.

## 5. Implementación de supertipos y subtipos
Hay dos estrategias en las diapositivas:

### a) Como supertipo (una sola tabla)
- **Tablas**: una sola, sin importar el número de subtipos.
- **Columnas**: las del supertipo con su opcionalidad original; las de **cada subtipo como opcionales**; más una columna **discriminadora obligatoria** (`tipo_prod`) que indica el subtipo.
- **Identificadores**: se trasladan como PK y UK.
- **Relaciones**: las del supertipo normales; las de los subtipos como FK **opcionales**.
- **Integridad**: para cada subtipo las columnas que provienen de atributos obligatorios se validan con CHECK ("si tipo = 'X' entonces columna NOT NULL").
Ventajas: consultas simples, sin joins; desventajas: muchas columnas NULL, restricciones más complejas. Ejemplo del curso: PRODUCTOS con columna Tipo_prod.

### b) Como subtipos (una tabla por subtipo)
- Una tabla por cada subtipo con todas las columnas del supertipo + las propias, con su opcionalidad original.
- La PK del supertipo se crea como PK en cada tabla; las secundarias como UK.
- Las relaciones del supertipo se replican como FK en **cada** tabla.
- No requiere chequeos adicionales.
Ventajas: sin NULL artificiales; desventajas: para consultar "todos" hay que usar UNION y la relación con otras tablas se duplica.
En el enunciado del Tema 3 se pide que la entidad de ciudades se implemente como **supertipo** y las subcategorías (software o equipo) como **arco**.

## 6. Normalización
**Normalizar** es aplicar a un conjunto de tablas reglas que garanticen estructuras simples, útiles, flexibles y estables. Razones: minimiza redundancia; la redundancia causa problemas de integridad (anomalías de actualización, inserción y borrado); ayuda a identificar entidades y relaciones.

### Formas normales (definiciones del curso)
- **1FN**: sin columnas repetitivas o multivaluadas; cada celda un solo valor atómico.
- **2FN**: en 1FN y toda columna no clave depende **de toda** la clave primaria (no solo de una parte). Solo aplica a claves compuestas.
- **3FN**: en 2FN y ninguna columna no clave depende de otra no clave (no hay **dependencias transitivas**).
Formalmente, con dependencias funcionales $X \to Y$: 2FN prohíbe $A \to C$ cuando $A \subsetneq$ PK; 3FN prohíbe $PK \to B \to C$ con $B$ no clave. (La BCNF, más estricta, exige que todo determinante sea superclave; se menciona como refuerzo, verificar con el programa oficial si se evalúa.)

### Ejemplo resuelto del curso: facturas
Datos sin normalizar: FACTURAS(Nro_Factura, Fecha, Cliente, Dirección, Código_producto, Descripción, Cantidad, Precio) con facturas como 3698 (cliente María Carrillo) que tiene 3 productos en la misma fila repetida.

**Paso 1 - 1FN (eliminar grupos repetidos)**:
1. Quitar de FACTURAS el grupo repetido (Código producto, Descripción, Cantidad, Precio).
2. Crear ITEM_PRODUCTOS con la PK de la tabla base (Nro_Factura) y las columnas repetidas.
3. Agregar a la PK una columna que garantice unicidad (Código_producto).
4. Crear la FK (`ipo_fta_fk`).
Resultado: FACTURAS(Nro_Factura PK, Cliente, Fecha, Dirección) e ITEM_PRODUCTOS(Nro_Factura PK-FK, Código_producto PK, Descripción, Cantidad, Precio).

**Paso 2 - 2FN**: en ITEM_PRODUCTOS la PK es (factura, producto) pero Descripción y Precio dependen **solo** del producto. Se crea PRODUCTOS(Código_producto PK, Descripción, Precio) y ITEMS(Nro_Factura PK-FK, Código_producto PK-FK, Cantidad). FK `ite_fta_fk` e `ite_pdo_fk`.

**Paso 3 - 3FN**: en FACTURAS, Cliente y Dirección dependen de la **cédula del cliente** (columna no clave): dependencia transitiva Nro_Factura -> Cédula -> (Cliente, Dirección). Se crea CLIENTES(Cédula PK, Cliente, Dirección) y FACTURAS(Nro_Factura PK, Fecha, Cédula FK).
Resultado final (4 tablas): FACTURAS (FTA), ITEMS (ITE), CLIENTES (CTE), PRODUCTOS (PDO), con relaciones `ite_fta_fk`, `ite_pdo_fk`, `fta_cte_fk`.

Nota: en `ITEMS` el precio vigente al facturar suele guardarse también como `precio_unitario` (copia histórica), porque el precio del catálogo cambia; no es violación de 3FN sino otro hecho (precio *aplicado*).

### Ejercicio del curso: reservación de hotel
RESERVACIONES(Localizador PK, Fecha reservación, Nombre cliente, Teléfono cliente, Nombre hotel, Lugar hotel, Costo noche, Categoría hotel, Código carro, Fecha reserva carro, Modelo carro). Solución: separar CLIENTES(cliente), HOTELES(nombre, lugar, costo noche, categoría), CARROS (código, modelo) y las reservas de hotel y de carro como relaciones (la fecha de reserva del carro es un hecho de la reserva del carro). Las columnas de hotel dependen del hotel y las del carro dependen del carro, ambas transitivas respecto de la clave Localizador; el cliente determina nombre y teléfono. Resultado: RESERVACIONES(Localizador, Fecha, Cliente_id FK, Hotel_id FK), CLIENTES, HOTELES, RESERVA_CARRO(Localizador FK, Código_carro FK, Fecha), CARROS.

## Errores comunes
- Poner la FK en el lado "uno" de una relación 1:M.
- Olvidar el CHECK del arco o dejar las FK del arco como NOT NULL (imposible cumplir el OR exclusivo).
- Implementar supertipo sin columna discriminadora.
- Normalizar "de más" separando datos que forman un solo hecho atómico (p. ej. partir un teléfono en tres tablas).
- Creer que 3FN exige no repetir ningún valor: solo exige no repetir **hechos** dependientes de no claves.

## Ejercicios propuestos
1. Dado PEDIDOS(Nro_ped, Cod_cliente, Nombre_cliente, Cod_producto, Cant), normalice a 3FN. (PEDIDOS(Nro_ped, Cod_cliente), CLIENTES(Cod_cliente, Nombre), ITEMS(Nro_ped, Cod_producto, Cant).)
2. Implemente como arco: una DIRECCION pertenece a CLIENTE o a TIENDA. (Dos FK opcionales + CHECK.)
3. ¿Qué estrategia elegiría para PERSONA con subtipos ESTUDIANTE y PROFESOR si casi todo el tiempo se consulta a ambos juntos? (Una sola tabla con discriminador.)

## Conexiones
[[Base de Datos I - Tema 2 Modelamiento de Datos DER]] (origen del modelo), [[Base de Datos I - Tema 4 SQL Lenguaje de Definición de Datos]] (CREATE TABLE y restricciones), [[Administración de Base de Datos]] (tablespaces, índices).

## Fuente
`Material/baseDatosI/temaIII/materialApoyo/Curso de Diseño Fisico.pdf`. Se complementan con conocimiento general el CHECK del arco, las ventajas/desventajas de cada estrategia y la solución del ejercicio del hotel.
