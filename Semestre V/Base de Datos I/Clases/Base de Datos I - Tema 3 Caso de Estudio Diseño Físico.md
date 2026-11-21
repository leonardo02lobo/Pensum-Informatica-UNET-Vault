---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaIII/casoEstudio/ (Caso de Estudio Tema 3 2025-1.pdf, Equipo 9 - Tema 3 - 2025-1 - Caso Estudio.pdf/.docx, Planilla Descripción Casos de Prueba.docx)
---
# Tema 3 - Caso de estudio: diseño físico y álgebra relacional

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 3 Caso Práctico Ejemplo Servicios Informáticos]]
Siguiente: [[Base de Datos I - Tema 4 SQL Lenguaje de Definición de Datos]]

## Contexto
Tercera entrega del proyecto "Gestión de Ventas de Productos de Entretenimiento" (2025-1). Continúa los temas anteriores ([[Base de Datos I - Tema 2 Caso de Estudio Requisitos y DER]]) y añade la **sección 8: diseño físico**, con ayuda de [[Base de Datos I - Tema 3 Curso de Diseño Físico]] y [[Base de Datos I - Tema 3 Curso de Modelo Relacional]].

## 1. Enunciado
Repite el contexto del negocio y los 13 puntos de requisitos (los del Tema 2 más: "las facturas se identifican por un número de factura, poseen fecha y se desea conocer la **cantidad facturada por producto**"). Tras la presentación del diseño lógico el gerente **anexa requisitos físicos**:
1. La entidad de **ciudades** se implementa como **supertipo** y las subcategorías (software o equipo) como **arco**.
2. Una vez insertado el cliente en la factura, **la factura no puede reasignarse a otro cliente** (no transferibilidad).

**Entregables**: (a) diseño físico (diagrama de tablas) **normalizado hasta 3FN**; (b) documentar en el diseño los **CHECK** o validaciones. Se exige SQL Developer Data Modeler, creando tablas, relaciones, PK y FK **una a una en el modelo relacional** (no por ingeniería directa del lógico), en un **archivo nuevo sin el diseño lógico**. El informe añade el punto 8: (a) funciones DAMA-DMBOK análogas a la fase; (b) requerimientos con álgebra relacional; (c) entregables más el archivo `.dmd`.

Requerimientos de álgebra (8b): esquema matemático de CLIENTES, PRODUCTOS, PROMOCIONES, TIENDAS, FACTURAS e ITEMS FACTURA; clientes de Venezuela/Táchira; tiendas en Caracas; facturas con datos de cliente, ciudad, productos y cantidades; tiendas con facturas y promociones; productos facturados de subcategoría software con precio total. Cada uno "explicando el tipo de operación".

## 2. Solución: modelo físico normalizado
Del enunciado resultan, en 3FN, tablas CIUDAD, CLIENTES, TIENDAS, CATEGORIA, SUBCATEGORIA, PRODUCTOS, PROMOCIONES, FACTURAS e ITEMFACTURA (9 tablas en el informe del equipo). Decisiones a justificar:
- **Ciudad como supertipo**: una tabla con columna discriminadora de nivel/tipo (ciudad, estado, país) y relaciones opcionales; así clientes y tiendas apuntan a la misma entidad (requisito 8 del enunciado).
- **Subcategoría como arco**: software y equipo son entidades distintas, cada una con FK a categoría; el arco se representa en el físico con dos FK opcionales y un CHECK de exclusividad (ver [[Base de Datos I - Tema 3 Curso de Diseño Físico]]). El informe del equipo simplificó con una columna `TipoSubcat IN ('Software','Equipo')`, solución equivalente funcional pero que no es literalmente el arco pedido.
- **Factura no reasignable**: la FK `cliente_id` de FACTURAS se marca como *no transferible* y se refuerza con un trigger `BEFORE UPDATE` que rechaza el cambio.
- **ITEMFACTURA**: PK compuesta (factura, producto), garantiza "un producto una sola vez por factura"; atributo `cantidad`.
- **Fabricante** como entidad aparte (un fabricante fabrica varios productos).
- Claves FK con integridad referencial; CHECK: montos > 0, `fecha_inicio < fecha_fin` en promociones, `tipo IN (...)`.

Fragmento ilustrativo en Oracle (del tipo que se generará en el Tema 4):
```sql
CREATE TABLE facturas (
  factura_nro   NUMBER(12) PRIMARY KEY,
  fecha_factura DATE NOT NULL,
  cliente_id    NUMBER(10) NOT NULL REFERENCES clientes(cliente_id),
  tienda_id     NUMBER(10) NOT NULL REFERENCES tiendas(tienda_id)
);
CREATE TABLE itemfactura (
  factura_nro NUMBER(12) REFERENCES facturas(factura_nro),
  producto_id NUMBER(10) REFERENCES productos(producto_id),
  cantidad    NUMBER(8)  NOT NULL CHECK (cantidad > 0),
  PRIMARY KEY (factura_nro, producto_id)
);
```
El informe del equipo detalla además, desde DAMA-DMBOK, decisiones de arquitectura (Oracle 19c en AWS RDS Multi-AZ, tablespaces separados para transaccional y maestras, particionamiento mensual por rango de `FechaFactura`, tipos NUMBER(10)/NUMBER(12,2)/VARCHAR2/TIMESTAMP), secuencias con triggers, índices B-tree, roles (`ROL_APP`, `ROL_READONLY`), seguridad a nivel de fila (VPD con `DBMS_RLS`), CHECK de calidad, comentarios de columna (`COMMENT ON COLUMN`) como diccionario y vistas lógicas para el portal. Son decisiones de ejemplo del equipo; las cifras (IOPS, RPO/RTO) son supuestos, no del enunciado.

## 3. Álgebra relacional (8b)
Esquema (PK y FK):
`CLIENTES(ClienteID PK, Nombre, Genero, EstadoMarital, Email, Direccion, Ocupacion, IngresoAnual, CiudadID FK)`, `PRODUCTOS(ProductoID PK, NombreProducto, Marca, Color, CostoUnitario, PrecioUnitario, SubcatID FK)`, `PROMOCIONES(PromoID PK, TipoPromocion, Descuento, FechaInicio, FechaFin)`, `TIENDAS(TiendaID PK, NombreTienda, Estatus, CantidadEmpleados, AreaVenta, Telefono, FechaApertura, CiudadID FK)`, `FACTURAS(FacturaNro PK, FechaFactura, ClienteID FK, TiendaID FK)`, `ITEMFACTURA(FacturaNro PK-FK, ProductoID PK-FK, Cantidad, PrecioUnitario, DescuentoAplicado, PromoID FK)`.

Consultas (patrón join -> selección -> proyección):
1. Clientes en Táchira: $\sigma_{Pais='VENEZUELA' \wedge Estado='TÁCHIRA'}(CLIENTES \bowtie_{CiudadID} CIUDAD)$. Operaciones: combinación y selección; sin proyección (todas las columnas).
2. Tiendas en Caracas: $\sigma_{NombreCiudad='CARACAS'}(TIENDAS \bowtie CIUDAD)$.
3. Facturas con cliente, ciudad y productos: $\pi_{ClienteID,Nombre,Genero,NombreCiudad,FacturaNro,FechaFactura,ProductoID,Cantidad}\big(((FACTURAS \bowtie CLIENTES)\bowtie CIUDAD)\bowtie ITEMFACTURA\big)$. Tres combinaciones y una proyección.
4. Tiendas con facturas y promociones: join TIENDAS-FACTURAS-ITEMFACTURA-PROMOCIONES y proyección de tienda, factura, producto, promoción, tipo y descuento.
5. Software facturado: join de FACTURAS, CLIENTES, ITEMFACTURA, PRODUCTOS, SUBCATEGORIA y CATEGORIA, selección $TipoSubcat='Software'$ y proyección con columna calculada $PrecioTotal = Cantidad \cdot PrecioUnitario$.
Observación: en la consulta 4, al ser un join interno, solo salen ítems con promoción; los sin promoción (PromoID nulo) quedan fuera.

## 4. Planilla de casos de prueba
El Material incluye la "Planilla Descripción de Caso de Prueba de Base de Datos" (formato CPBDnn): tabla(s), descripción de la transacción, **escenarios normales** (sentencias INSERT/UPDATE/DELETE que cumplen las restricciones y deben ejecutarse) y **escenarios de restricciones** (sentencias que violan alguna restricción y deben fallar, indicando la restricción). Se usa a partir del Tema 4 ([[Base de Datos I - Tema 4 Caso de Estudio Diseño e Implementación]]).

## Errores comunes
- Generar el físico por ingeniería directa del lógico cuando se exige crearlo manualmente en un archivo nuevo.
- Subcategorías sin arco o con CHECK incorrecto.
- No normalizar a 3FN (guardar precio total de ítem, o ciudad como texto en cliente).
- Álgebra sin explicar las operaciones.

## Ejercicios propuestos
1. Escriba el álgebra de "facturas de la tienda 5 en 2025". (Join FACTURAS-TIENDAS, selección TiendaID=5 y fecha en rango.)
2. Escriba el CHECK de arco para SUBCATEGORIA si se usara una sola tabla con FK a software y equipo. (XOR de las dos FK.)

## Conexiones
[[Base de Datos I - Tema 4 SQL Lenguaje de Definición de Datos]] (implementación DDL), [[Administración de Base de Datos]].

## Fuente
Archivos de `Material/baseDatosI/temaIII/casoEstudio/`. Se omiten nombres de autores y de data stewards del informe de ejemplo.
