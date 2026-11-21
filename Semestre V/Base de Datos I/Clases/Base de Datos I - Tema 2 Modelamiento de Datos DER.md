---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaII/materialDeApoyo/Curso de Modelamiento de Datos DER.pdf
---
# Tema 2 - Modelamiento de datos y Diagrama Entidad-Relación (DER)

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 1 Caso de Estudio Planificación]]
Siguiente: [[Base de Datos I - Tema 2 Oracle SQL Developer Data Modeler]]

## Contexto y objetivo
Apunte reconstruido a partir de las 45 diapositivas "Modelamiento de Datos" del curso. Presenta la técnica con la que se pasa de los **requisitos de datos** (lenguaje natural) a un **modelo conceptual**: el Diagrama Entidad-Relación en la notación tipo *Barker* (la que usa Oracle Designer y Oracle SQL Developer Data Modeler: opcionalidad "debe ser/puede ser", cardinalidad "uno y solamente uno / uno o más", `#` para identificadores, `*` para atributos obligatorios y `o` para opcionales). Objetivo: saber identificar entidades, atributos, relaciones, identificadores, supertipos/subtipos, arcos y restricciones, y documentarlos.

## 1. Modelos esenciales vs. de implantación
- Un **modelo** es una representación gráfica de la realidad.
- **Modelo esencial** (lógico o conceptual): independiente de la implantación; describe *qué hace o debe hacer* el sistema.
- **Modelo de implantación** (tecnológico o físico): muestra además *cómo* se implanta físicamente.
El **modelamiento de datos** organiza y documenta los datos de un sistema; es el primer paso del desarrollo **top-down** de una base de datos y se ejecuta en las etapas de estrategia y análisis. Su producto, el **modelo conceptual**, examina los datos del negocio para determinar la estructura de la información y las reglas que la gobiernan, de forma independiente de la técnica de implementación. Sus ventajas: describe exactamente la información necesaria, facilita la discusión, previene malentendidos, es documentación ideal y sirve de base al diseño físico. El **modelo físico** implementa el conceptual en un entorno de software y hardware específico (se verá en [[Base de Datos I - Tema 3 Curso de Diseño Físico]]).

Flujo del ciclo de vida: *Modelo conceptual (DER) -> Diseño físico (diagrama de tablas) -> implementación*. Se vincula con la **Ingeniería de la Información**: técnica basada en datos pero sensible a los procesos, aplicada a la organización completa o a grandes áreas más que a un proyecto circunstancial.

## 2. Elementos del DER
**Metas del DER**: capturar todos los requerimientos de información; que cada dato aparezca **solo una vez**; no modelar información que pueda **derivarse** de otra ya modelada.

### Entidad
Cualquier ente real o abstracto sobre el que se desea almacenar datos; categoría de cosas significativas para el negocio. Se dibuja como rectángulo y representa **todas las ocurrencias**. Clases típicas: participantes (cliente, empleado), sucesos (pedido, factura), lugares (tienda, ciudad) y bienes tangibles (producto).

### Atributo
Característica común a todas o la mayoría de ocurrencias de la entidad: describe, cuantifica, clasifica o especifica. Diferencias entidad/atributo (de la diapositiva): una entidad es "algo acerca de lo cual debe informarse", posee atributos, puede tener múltiples ocurrencias asociadas por relaciones; un atributo califica a una entidad, **no posee atributos propios** y tiene un **valor simple** por ocurrencia (no hay grupos repetitivos). Si algo "tiene atributos", es entidad; si una entidad no tiene atributos, probablemente es solo un atributo.
- **Obligatorio** (mandatorio): marcado con `*`; siempre debe conocerse.
- **Opcional**: marcado con `o`; puede ser desconocido (NULL).

### Identificador (clave)
Atributo o combinación que identifica unívocamente una ocurrencia. Toda entidad debe tener al menos uno; si hay varios hay uno **principal** (`#`) y secundarios (`(#)`). Cuando no hay atributos suficientes se usa la **relación de llegada**: la entidad hereda el identificador de otra (identificador compuesto, marcado con una raya sobre la relación). Tipos:
1. **Simple**: un atributo (código de producto).
2. **Múltiple**: varios atributos (paquete de software = nombre + versión: Oracle Designer 7.0).
3. **Compuesto**: atributo propio más el identificador de la entidad relacionada (p. ej. *línea de pedido* identificada por número de línea + pedido).
4. **Compuesto en cascada**: se hereda de una entidad que a su vez heredó de una tercera.

### Relación
Asociación natural o lógica entre una o más entidades. Es **bidireccional**: entre dos entidades o de una entidad consigo misma (recursiva). Cada dirección tiene un **nombre** (dirigido por, asignado a), una **opcionalidad/orden** ("debe ser" / "puede ser") y un **grado/cardinalidad** ("uno y solamente uno" / "uno o más").

Ejemplo de la diapositiva: INSTRUCTOR-CURSO.
- Cada CURSO **debe ser** dictado por **uno y solamente un** INSTRUCTOR.
- Cada INSTRUCTOR **puede ser** asignado a **uno o más** CURSOS.
Es una relación 1:N (un instructor, muchos cursos).

### Tipos de relación (con los ejemplos del curso)
| Tipo | Definición | Ejemplo |
|---|---|---|
| 1:M (uno a muchos) | grado "uno o más" en un sentido y "uno y solo uno" en el otro | REPRESENTANTE DE VENTAS - CLIENTE |
| M:M (muchos a muchos) | "uno o más" en ambos sentidos | ESTUDIANTE - CURSO |
| 1:1 | "uno y solo uno" en ambos sentidos | MICROCOMPUTADOR - TARJETA MADRE |
| Recursiva M:1 | una entidad consigo misma | EMPLEADO - JEFE (columna `supervisor` apunta al número de empleado) |

Ejemplo recursivo en tabla: Empleados(num_emp, cédula, nombre, teléfono, supervisor): el supervisor de María (1211) es el empleado 1010 (Pedro). La clave foránea `supervisor` referencia a la propia tabla.

**Mandatoriedad en ambas direcciones**: las instancias no pueden existir una sin la otra ("chicken-and-egg"); al implementarlo físicamente crea problemas para insertar las primeras filas. Se evita o se resuelve con una de las dos direcciones opcional.

### Matriz de relaciones
Herramienta de análisis: todas las entidades se colocan en filas y columnas; en la intersección se escribe el nombre de la relación si existe o una línea si no. La celda simétrica contiene la relación inversa (la "imagen"); las relaciones recursivas están en la diagonal. Sirve para no olvidar relaciones antes de dibujar. Ejemplo (ventas): fila CLIENTE, columna PEDIDO = "realiza"; fila PEDIDO, columna CLIENTE = "realizado por".

### Entidad asociativa
Cuando la cardinalidad es "muchos" en ambas direcciones, la relación suele tener atributos propios (cantidad, fecha). Se resuelve con una **entidad asociativa** (intersección) cuyos atributos describen la asociación y que se relaciona con **una y solo una** ocurrencia de cada entidad fundamental. Ejemplo: PRODUCTO M:M PEDIDO -> DETALLE_PEDIDO(cantidad, precio) con dos relaciones 1:M. Es el equivalente a la tabla puente.

### Redundancia en relaciones y no transferibilidad
- **Relaciones redundantes**: dos caminos que informan lo mismo (PERSONA vive en PUEBLO, PUEBLO localizado en PAÍS, y PERSONA también ligada a PAÍS). Si el segundo camino se deriva del primero, se elimina. Excepción: cuando representan hechos distintos (hogar vs. lugar de nacimiento).
- **No transferibilidad**: la conexión no puede cambiar una vez hecha (un MENSAJE escrito por un USUARIO no cambia de autor). Se dibuja con un diamante sobre la línea y en implementación significa que la clave foránea **no se actualiza** (se implementa con trigger o permisos).

### Supertipos y subtipos
Un **supertipo** agrupa atributos y relaciones comunes; los **subtipos** heredan todos sus atributos y relaciones y añaden los propios. Se dibujan *dentro* del supertipo, nunca existen aislados y pueden tener sus propios subtipos. Los subtipos de una misma entidad deben ser **exhaustivos** (toda instancia del supertipo pertenece a algún subtipo) y **mutuamente exclusivos** (a uno solo). Ejemplo: CUENTAHABIENTE = PERSONA o COMPAÑÍA, relacionado con CUENTA BANCARIA. En el caso de estudio: CATEGORÍA con subtipos de subcategoría "software" o "equipo".

## 3. Restricciones (reglas del negocio)
- **Arcos (arco exclusivo)**: restricción sobre dos o más relaciones de una misma entidad: una ocurrencia solo puede tener **una** relación válida a la vez (un OR exclusivo). Reglas: pertenece a una entidad; puede incluir más de dos relaciones; no todas las relaciones de la entidad entran en el arco; una entidad puede tener varios arcos; las relaciones del arco deben tener la **misma opcionalidad**; pueden tener distinta cardinalidad. Ejemplo: una DIRECCION pertenece a un CLIENTE o a una TIENDA, nunca a ambos.
- **Dominios**: conjunto de valores permitidos de un atributo (género: varón/hembra/desconocido; días hábiles). En el modelo conceptual pueden representarse como entidades de dos atributos (código, descripción): *entidades de dominio*, muy referenciadas pero con pocas relaciones propias.
- **Constraints especiales**: reglas que el DER no puede expresar (dominio condicionado a otro atributo; chequeo de rango contra una instancia relacionada). Se listan en un documento y se programan (CHECK, triggers).
- **Limitantes**: reglas impuestas por fuentes externas (casa matriz, legislación). Deben ir **en una tabla de parámetros** y no codificadas en programas, para que un cambio de regla sea solo actualizar valores.

## 4. Ejemplo resuelto
Enunciado: "Los clientes realizan pedidos; cada pedido incluye productos con cantidad; cada producto pertenece a una categoría".
1. Entidades: CLIENTE, PEDIDO, PRODUCTO, CATEGORÍA, y por M:M entre pedido y producto la asociativa DETALLE_PEDIDO.
2. Relaciones (leer en ambos sentidos): Cada PEDIDO debe ser realizado por uno y solamente un CLIENTE; cada CLIENTE puede realizar uno o más PEDIDOS. Cada PRODUCTO debe pertenecer a una y solo una CATEGORÍA; cada CATEGORÍA puede agrupar uno o más PRODUCTOS.
3. Identificadores: #cliente_id, #pedido_id, #producto_id, #categoria_id; DETALLE_PEDIDO se identifica por pedido + producto (compuesto).
4. Atributos: cliente(* nombre, o teléfono); pedido(* fecha); detalle(* cantidad, * precio_aplicado).
5. Verificar metas: ¿algún dato repetido? (precio unitario vive en PRODUCTO; el aplicado vive en detalle, porque puede variar en el tiempo, es un hecho distinto). ¿Algún dato derivable? (total del pedido: se puede calcular; solo se guarda si hay razón de rendimiento o de congelar un valor).

## Errores comunes
- Modelar atributos de atributos (si "dirección" tiene calle, ciudad, zip, puede ser varios atributos o una entidad).
- Dejar relaciones M:M sin resolver.
- Entidades sin identificador.
- Guardar datos derivados (edad y fecha de nacimiento) sin necesidad.
- Mandatoriedad en ambas direcciones sin analizar el orden de inserción.
- Poner nombres de relación vagos ("tiene"), que no permiten leer la regla de negocio.

## Ejercicios propuestos
1. Escribir en lenguaje natural la relación EMPLEADO-JEFE recursiva. (Cada empleado puede ser supervisado por un jefe; cada jefe puede supervisar uno o más empleados.)
2. Una factura puede ser pagada con tarjeta o con transferencia, nunca ambas. ¿Qué construcción del DER aplica? (Arco exclusivo.)
3. Identifique supertipo y subtipos en "vehículo: automóvil, camión, moto". (Vehículo supertipo; atributos comunes placa, marca; subtipos con atributos propios, p. ej. capacidad de carga en camión.)
4. ¿Por qué "total_pedido" puede violar la meta "no modelar información derivable"? (Se calcula sumando detalles.)

## Conexiones
Siguiente paso: pasar el DER a tablas ([[Base de Datos I - Tema 3 Curso de Modelo Relacional]]). Herramienta: [[Base de Datos I - Tema 2 Oracle SQL Developer Data Modeler]]. Entregable: [[Base de Datos I - Tema 2 Caso de Estudio Requisitos y DER]]. Visión de requisitos de software: [[Ingeniería de Software]].

## Fuente
`Material/baseDatosI/temaII/materialDeApoyo/Curso de Modelamiento de Datos DER.pdf`. Los ejemplos resueltos y los ejercicios de esta nota se añaden como complemento de conocimiento general.
