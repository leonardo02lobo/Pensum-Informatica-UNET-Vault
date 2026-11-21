---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaII/materialDeApoyo/oracle-sql-developer-data-modeler-users-guide.pdf
---
# Tema 2 - Guía de Oracle SQL Developer Data Modeler

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 2 Modelamiento de Datos DER]]
Siguiente: [[Base de Datos I - Tema 2 Caso de Estudio Requisitos y DER]]

## Contexto y objetivo
El material de apoyo incluye el *Oracle SQL Developer Data Modeler User's Guide* (release 19.4, diciembre 2019, 245 páginas, en inglés). Es la herramienta que exige el caso de estudio para el modelado conceptual (Tema 2), el relacional y el físico (Temas 3 y 4, ingeniería directa e inversa). Esta nota resume los conceptos y el flujo de trabajo útiles para el curso; no traduce las ~245 páginas de cuadros de diálogo (capítulo 3) ni los detalles de versionado con Git/Subversion, que son referencia.

## 1. Estructura de un diseño
Data Modeler trabaja con **un diseño abierto**, formado por:
- un **modelo lógico** (el diagrama entidad-relación),
- uno o más **modelos relacionales** derivados del lógico,
- uno o más **modelos físicos** derivados de cada relacional,
- opcionalmente un modelo de tipos de datos, un modelo de procesos (diagramas de flujo de datos), un modelo multidimensional y **información de negocio** (contactos, documentos, correos, ubicaciones, responsables).
Al guardar se genera un archivo XML con extensión `.dmd` (los casos de los Temas IV y V incluyen carpetas de diseño con su `.dmd`) y subcarpetas con la información (logical, rel, datatypes, etc.). Por eso un diseño se entrega como la carpeta completa y no solo el `.dmd`.

## 2. Los modelos
### Modelo lógico
Es el corazón de la herramienta: vista independiente de la implementación de la información empresarial. Contiene **entidades**, **atributos**, **identificadores únicos (UID)**, **herencias** (supertipo/subtipo), **relaciones**, **arcos** y vistas. Soporta dos notaciones: **Bachman** y **Barker** (se alterna en View > Logical Diagram Notation). Se pueden crear **subvistas** (subject areas) que muestran un subconjunto de entidades; un cambio en una subvista se refleja en el modelo completo.
Correspondencia lógico -> relacional: entidad -> tabla; atributo -> columna; UID -> clave primaria/única; relación -> clave foránea; herencia -> tabla(s) según estrategia; arco -> columnas FK con restricción.

### Modelo relacional
Tablas, columnas, índices, claves foráneas y vistas relacionales; se genera por **ingeniería directa** ("Engineer to Relational Model"). El diálogo *Engineering* permite filtrar qué objetos pasan, conservar coordenadas del diagrama, aplicar traducción de nombres (nombres formales a abreviados) y usar abreviaturas preferidas para nombres de tablas/columnas.

### Modelo físico
Objetos específicos de un SGBD (para Oracle: tablespaces, secuencias, sinónimos, roles, usuarios, segmentos, tablas externas, procedimientos almacenados, etc.). De él se genera el **DDL** (opciones en *DDL Generation Options*).

## 3. Enfoques de modelado
- **Top-down**: diseñar una base nueva. Pasos: información de negocio -> modelo de procesos (DFD) -> **modelo lógico** (crear entidades con atributos y UID; crear relaciones M:N, 1:N, 1:N identificante, 1:1; aplicar *Design Rules*; ingeniería directa a relacional) -> (opcional multidimensional) -> relacional (dividir/unir tablas) -> físico -> generar DDL.
- **Bottom-up**: partir de una base existente: importar el diccionario de datos o un archivo DDL (ingeniería inversa) y obtener los modelos. Es el procedimiento del Tema 5, donde se obtiene el diseño físico por ingeniería inversa de las tablas ya cargadas en Oracle XE ([[Base de Datos I - Tema 5 Caso Práctico Gestión de Ventas]]).
- **Targeted**: adaptar una base existente a nuevos requisitos (comparar modelos y fusionar cambios).

## 4. Tutorial del manual: base de datos de una biblioteca
El capítulo 2 construye paso a paso un modelo con tres entidades. Es un buen ejemplo mínimo del flujo:
1. **Dominios** (Tools > Domains Administration): Person Name VARCHAR(25), Address Line VARCHAR(40), City VARCHAR(25), State VARCHAR(2), Zip VARCHAR(10), Book Id VARCHAR(20), Numeric Id NUMERIC(7,0), Title VARCHAR(50). Los dominios dan tipos reutilizables y consistentes (se guardan en `defaultdomains.xml`).
2. **Entidad Books**: book_id (UID primario), title (obligatorio), author_last_name (obligatorio), author_first_name, rating NUMERIC(2,0).
3. **Entidad Patrons**: patron_id (UID), last_name (obligatorio), first_name, street_address, city, state, zip y `location` (tipo estructurado SDO_GEOMETRY).
4. **Entidad Transactions**: transaction_id, transaction_date (obligatorio), transaction_type (obligatorio). No se definen patron_id ni book_id a mano: **se agregan como claves foráneas** al crear las relaciones.
5. **Relaciones 1:N**: Books -> Transactions y Patrons -> Transactions (un libro tiene muchas transacciones; un usuario también).
6. **Ingeniería directa** a modelo relacional y **generación de DDL** (CREATE TABLE con PK y FK), y guardado del diseño.
La lección: *primero dominios, luego entidades, luego relaciones; las FK las deduce la herramienta*.

## 5. Reglas de diseño y reportes
- **Tools > Design Rules** revisa violaciones (entidad sin UID, atributos sin tipo, relaciones inconsistentes, nombres reservados). El informe del equipo del caso de estudio ejecutó "Comprobar reglas de diseño" antes de pasar a físico.
- **Reports**: se pueden generar reportes RTF, HTML o PDF del diseño (útil para el "documentar cada entidad" del caso) y exportar a un esquema de reportes.
- **Preferencias** (DDL, diagrama, modelo) y atajos de teclado se configuran en Tools > Preferences.
- **Importar**: archivos DDL, Erwin, Oracle Designer, diccionario de datos; **exportar** DDL, imágenes, XMLA.
- **Versionado** con Subversion o Git integrado (referencia; el curso no lo evalúa).

## 6. Flujo recomendado para el curso
1. Abrir Data Modeler, File > New Design; poner nombre.
2. Crear dominios que reflejen el diccionario de datos.
3. Dibujar entidades y definir atributos, tipos y obligatoriedad; marcar el UID primario.
4. Crear relaciones con el icono correcto (1:N, 1:N identificante, M:N, 1:1); editar nombres y opcionalidad en ambos sentidos.
5. Crear herencias/arcos si aplican.
6. Ejecutar Design Rules.
7. Engineer to Relational Model; revisar nombres y claves; ajustar al estándar (prefijos de tabla, nombres de PK/FK).
8. Crear modelo físico para Oracle y generar el DDL (Tema 4).

## Errores comunes
- Crear la FK a mano en el modelo lógico: se duplican columnas al hacer la ingeniería directa. Debe nacer de la relación.
- Olvidar marcar UID en alguna entidad: la ingeniería falla o genera tabla sin PK.
- Relación M:N dejada en el lógico: se convierte en tabla de resolución con nombres automáticos; es preferible modelar la asociativa explícita cuando tiene atributos.
- Entregar solo el `.dmd` sin las subcarpetas.

## Ejercicios propuestos
1. Reproducir el tutorial de la biblioteca y verificar el DDL de `Transactions` contiene las dos FK. (Debe incluir patron_id y book_id con REFERENCES.)
2. ¿Qué diferencia hay entre una relación 1:N y una 1:N identificante? (En la identificante la FK forma parte de la PK de la entidad hija.)
3. Describa cuándo usaría ingeniería inversa. (Cuando solo hay una base existente o un script DDL sin diagrama.)

## Conexiones
[[Base de Datos I - Tema 2 Modelamiento de Datos DER]] (teoría de notación), [[Base de Datos I - Tema 3 Curso de Modelo Relacional]] (reglas de transformación), [[Base de Datos I - Tema 3 Curso de Diseño Físico]].

## Fuente
`Material/baseDatosI/temaII/materialDeApoyo/oracle-sql-developer-data-modeler-users-guide.pdf` (se leyó el capítulo 1 conceptual y el tutorial del capítulo 2; el capítulo 3, de diálogos, se consultó solo en las partes de Engineering y Design Rules). Los archivos `.dmd` de los casos de los Temas IV y V son diseños XML; se explican en las notas de esos temas.
