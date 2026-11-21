---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaII/CasoEstudioII/ (Caso de Estudio Tema 2 2025-1.pdf, Formato de Requisito de Datos Tema 2 2024-3.docx, ZAMBRANO9008.docx, Equipo 9 - Tema 2 - 2025-1.zip y carpeta homónima con DiagramaLogicoTeorico.pdf/.sql)
---
# Tema 2 - Caso de estudio: requisitos de datos y diseño conceptual (DER)

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 2 Oracle SQL Developer Data Modeler]]
Siguiente: [[Base de Datos I - Tema 3 Curso de Modelo Relacional]]

## Contexto
Segunda entrega del proyecto "Gestión de Ventas de Productos de Entretenimiento" (lapso 2025-1, tema "Análisis de base de datos"). Se continúa el informe del Tema 1 ([[Base de Datos I - Tema 1 Caso de Estudio Planificación]]) y se añaden las secciones 6 (definición de requisitos) y 7 (diseño conceptual o lógico) usando [[Base de Datos I - Tema 2 Oracle SQL Developer Data Modeler]]. La teoría necesaria está en [[Base de Datos I - Tema 2 Modelamiento de Datos DER]].

## 1. Enunciado
Además del contexto del Tema 1 (caída de ventas, aplicación web, presupuesto de 10.000 $), el enunciado entrega un **documento en lenguaje natural** de requerimientos de datos acordado entre usuarios y analistas, con 12 puntos:
1. La BD cubre solo ventas de productos de entretenimiento.
2. Del **cliente**: nombre, estado marital, género, correo, ingreso anual, ocupación, ciudad y dirección.
3. **Promociones**: promoción, descuento, tipo, categoría de la promoción, fecha inicio y fin.
4. **Productos**: nombre, fabricante, marca, color, costo unitario, precio unitario, categoría. Las categorías tienen subcategorías, que pueden ser de dos tipos (software o equipo), y una categoría tiene una sola subcategoría.
5. Los productos se facturan: un producto aparece **una sola vez en una factura** pero puede estar en varias facturas; un producto es fabricado por **un solo fabricante** y un fabricante fabrica varios productos.
6. **Tienda**: nombre, estatus, fecha de apertura, ZIP, teléfono, ciudad, dirección 1 y 2, cantidad de empleados, área de venta. Una tienda genera muchas facturas; cada factura pertenece a una sola tienda.
7. La ciudad de la tienda no es necesariamente la del cliente: **las ciudades son una sola entidad**.
8. Los montos deben ser mayores a cero.
9. En rangos de fechas o valores, el "desde" debe ser menor al "hasta".
10. Plataforma: Oracle en la nube (AWS), Linux.
11. Volumen: ~500.000 facturas por año.
12. Tiempos de respuesta: transacción de recepción ~10 s; consulta ~5 s.

**Se solicita**: (1) fase de definición de requisitos: *documento de requisitos de datos*; (2) fase de diseño conceptual: identificar entidades, matriz de relaciones, modelo conceptual y documentar cada entidad; con la herramienta Data Modeler. El informe añade las secciones 6 y 7, cada una con una pregunta DAMA-DMBOK (qué funciones del marco son análogas a las actividades realizadas) y los entregables.

## 2. Enfoque de solución
### Paso 1: documento de requisitos de datos
El formato de la cátedra ("Documento de requisitos de datos", control de versiones incluido) tiene las secciones:
- **Nombre del esquema y siglas**.
- **Objetivos de la BD** (claros y medibles).
- **Alcance** (qué procesos cubre y qué queda fuera).
- **Requisitos de datos**: tabla por entidad con *descripción, atributos, descripción de atributos y tipo de entidad (dominio o transaccional)*.
- **Reglas del negocio y restricciones**.
- **Requisitos de infraestructura** (hardware, software, nivel de servicio, performance, seguridad, volúmenes).
El ejemplo adjunto en el formato lista 16 entidades (Cliente, Producto, CategoríaProducto con jerarquía recursiva, Tienda, Ciudad, Promoción, Pedido, DetallePedido, Factura, Pago, Despacho, Transportista, RutaDespacho, Inventario, PrecioLista, Empleado), reglas de negocio como: un producto no se repite en una factura; `TotalFactura = Σ(precio·cantidad) - descuentos + impuestos`; cantidad solicitada <= stock; no transferibilidad del ID de factura; una sola promoción activa por pedido; fechas consistentes (pedido <= factura <= despacho); y requisitos de infraestructura (Oracle 19c en AWS RDS Multi-AZ, RPO <= 15 min, RTO <= 30 min, particionamiento mensual, cifrado). Importante: **son cifras de ejemplo del formato**, no del enunciado oficial; el enunciado solo fija Oracle/AWS/Linux, 500.000 facturas/año y los tiempos de respuesta.

Cómo derivar entidades del texto (técnica nombre/verbo): los sustantivos con atributos propios son entidades candidatas (cliente, promoción, producto, categoría, subcategoría, fabricante, factura, tienda, ciudad); los verbos dan relaciones ("se factura", "fabrica", "genera"); los sustantivos sin atributos propios son atributos (color, marca). Los puntos 8 y 9 son **reglas de dominio** (CHECK: monto > 0; fecha_desde < fecha_hasta). El punto 5 implica una entidad asociativa **ítem de factura** con clave compuesta (factura, producto) para garantizar "un producto una sola vez por factura".

### Paso 2: identificar entidades y matriz de relaciones
Entidades mínimas del enunciado: Ciudad, Cliente, Categoría, Subcategoría (supertipo/subtipos software y equipo), Producto, Fabricante (si se separa de producto), Promoción, Tienda, Factura, Ítem de factura. Matriz parcial:
| | Cliente | Factura | Tienda | Ciudad | Producto | Promoción |
|---|---|---|---|---|---|---|
| Cliente | - | realiza | - | reside en | - | - |
| Factura | emitida a | - | generada en | - | contiene (vía ítem) | aplica |
| Tienda | - | genera | - | ubicada en | - | - |

### Paso 3: el modelo conceptual en Data Modeler
El informe del equipo dice haber modelado **17 entidades** con subtipos (Empleado -> Vendedor/Repartidor), la entidad asociativa DetallePedido y arcos exclusivos (factura genera pago o nota de crédito), y haber ejecutado la comprobación de reglas de diseño. Como entregable técnico del equipo se adjuntó el script `DiagramaLogicoTeorico.sql`, un volcado de 17 tablas con sus FK: Ciudad, CategoriaProducto (con autorreferencia CategoriaPadreID), Producto, Tienda, Promocion, Transportista, PrecioLista, Empleado, Cliente, Pedido, DetallePedido (PK compuesta pedido+producto), Factura, Pago, Despacho, RutaDespacho, Inventario y EventoTracking. Observaciones didácticas:
```sql
CREATE TABLE "DetallePedido" (
  "PedidoID" int NOT NULL,
  "ProductoID" int NOT NULL,
  "Cantidad" int NOT NULL,
  "PrecioAplicado" decimal(12,2),
  "Subtotal" decimal(12,2),
  PRIMARY KEY ("PedidoID", "ProductoID")   -- identificador compuesto: un producto una vez por pedido
);
ALTER TABLE "CategoriaProducto" ADD FOREIGN KEY ("CategoriaPadreID")
  REFERENCES "CategoriaProducto" ("CategoriaID");   -- relación recursiva (jerarquía de categorías)
```
- `Subtotal` es un dato derivado (cantidad x precio): choca con la meta del DER de no modelar información derivable; se justifica solo si se congela el valor.
- Este volcado usa sintaxis genérica (`int`, `datetime`, `json`), propia de una herramienta de diagramas tipo dbdiagram, y no de Oracle (`NUMBER`, `DATE`, `VARCHAR2`); sirve como diagrama lógico teórico, no como DDL ejecutable en Oracle.
- Las tablas del enunciado "oficial" (fabricante, subcategoría, ítem de factura) no coinciden uno a uno con este modelo ampliado del equipo; el modelo que sí sigue el enunciado se implementa en el Tema 4 ([[Base de Datos I - Tema 4 Caso de Estudio Diseño e Implementación]]).

### Paso 4: documentar cada entidad
Para cada entidad: nombre, descripción, atributos con tipo/obligatoriedad/descripción, identificador, relaciones (en ambos sentidos con opcionalidad y cardinalidad), reglas de negocio asociadas y volumen estimado. Con 500.000 facturas/año y ~N ítems por factura se justifica estimar el tamaño de la tabla de ítems (por ejemplo, 3 ítems por factura = 1,5 millones de filas al año; supuesto de ejemplo).

## 3. Sección DAMA-DMBOK de las secciones 6 y 7
El informe responde mapeando actividades a funciones del marco: *Modelado y diseño* (descubrimiento de datos, entidades, diccionario), *Gobernanza* (glosario, convención de nombres, aprobación del modelo), *Arquitectura* (plataforma Oracle/AWS, claves, particiones), *Metadatos* (repositorio y linaje), *Calidad* (reglas -> CHECK, UNIQUE, NOT NULL), *Seguridad* (clasificación de atributos, cifrado), *Operaciones* (volumen, índices) e *Integración* (vistas lógicas y contratos de interfaz). La idea evaluada es entender que cada actividad de diseño tiene un dominio de gestión que la respalda.

## Errores comunes
- Incluir entidades sin respaldo en el enunciado (por ejemplo logística avanzada) olvidando una que sí está (fabricante, subcategoría).
- No modelar el subtipo de subcategoría (software/equipo) ni la cardinalidad "una categoría, una subcategoría".
- Olvidar la restricción de unicidad producto-factura.
- Confundir entregable lógico con físico: el DER no lleva tipos de Oracle ni secuencias.
- Dejar relaciones sin nombre ni opcionalidad.

## Ejercicios propuestos
1. Dibuje el DER de los puntos 2 a 7 del enunciado y liste identificadores. (Ciudad, Cliente, Categoría, Subcategoría, Producto, Fabricante, Promoción, Tienda, Factura, ÍtemFactura.)
2. Escriba las reglas 8 y 9 como restricciones CHECK. (`CHECK (monto > 0)`, `CHECK (fecha_desde < fecha_hasta)`.)
3. ¿Cómo se garantiza que un producto aparezca una sola vez en una factura? (PK compuesta (factura_id, producto_id) en la tabla de ítems.)

## Conexiones
[[Base de Datos I - Tema 3 Curso de Modelo Relacional]] (siguiente transformación), [[Base de Datos I - Tema 1 Metodología DAMA-DMBOK y ciclo de vida]].

## Fuente
Archivos de `Material/baseDatosI/temaII/CasoEstudioII/`. El `.zip` contiene copias del informe, del formato y del diagrama lógico (leído sin descomprimir en el vault). No se reproducen nombres de autores.
