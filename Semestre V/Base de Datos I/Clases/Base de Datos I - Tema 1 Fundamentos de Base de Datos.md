---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaI/materialApoyo/Curso Base de Datos I 2021.pdf
---
# Tema 1 - Fundamentos de Base de Datos

Materia: [[Base de Datos I]]
Siguiente: [[Base de Datos I - Tema 1 Metodología DAMA-DMBOK y ciclo de vida]]

## Contexto y objetivo
Este apunte reconstruye y amplía las diapositivas "Fundamentos de Base de Datos" (curso de Base de Datos I, 2021). Es la base conceptual de todo el semestre: antes de modelar (Tema II), pasar al modelo relacional (Tema III) o escribir SQL (Temas IV a VI) hay que entender qué es un dato, qué es un sistema de base de datos, qué niveles de abstracción maneja y cómo está organizado internamente un gestor (DBMS).

## 1. Dato, información y conocimiento
- **Dato**: representación abstracta de hechos (eventos, ocurrencias, transacciones) u objetos (personas, lugares). Por sí solo no tiene significado: "25" es un dato.
- **Información**: datos ordenados o colocados en un contexto mediante un procesamiento, con valor para quien los usa y que reducen su incertidumbre: "Pedro Pérez tiene 25 años y es del departamento de Ventas".
- **Conocimiento**: información que, interpretada, sirve para decidir y actuar ("el departamento de Ventas tiene el personal más joven; planificar capacitación"). La cadena es *dato -> información -> conocimiento -> decisión -> acción -> ventaja competitiva*.

En una organización, la función de la información es **apoyar la toma de decisiones**: permitir al usuario comprender lo que ocurrió, lo que ocurre y lo que puede ocurrir.

### Procesamiento de datos
Se distinguen dos actividades:
1. **Procesamiento de transacciones**: eventos y entidades del mundo real generan datos que se almacenan (alta de un pedido, pago de una factura).
2. **Procesamiento de información**: los datos almacenados se procesan y se entregan a un elemento receptor (reportes, consultas, estadísticas).

## 2. Sistema de información (SI)
Conjunto de componentes interrelacionados que **capturan, almacenan, procesan y distribuyen** información para apoyar la toma de decisiones y el control de las operaciones. Incluye personas, actividades, datos, redes y tecnología integrados. Cada unidad funcional de la organización tiene tres centros:
- **Centro de decisiones** (gerente),
- **Centro de actividades** (empleados),
- **Centro de información** (el SI), que captura y procesa los datos originados por las transacciones del centro de actividades y alimenta a los demás mediante canales de información.

La arquitectura del SI se concibe entonces como una red de centros de información asociados a las unidades funcionales y conectados por canales por los que fluyen datos. Esto enlaza con la materia [[Sistema de Información I]] y con la visión sistémica de [[Teoría General de Sistemas]].

### Los datos como activo y la ciencia de datos
Las empresas tratan hoy los datos como uno de sus activos más importantes. Los sistemas de soporte (operativos, gerenciales, de apoyo a decisiones y analíticos en línea) transforman los datos en conocimiento para obtener **ventaja competitiva**. El *científico de datos* encuentra patrones, hace descubrimientos y comunica sus implicaciones al negocio.

## 3. Jerarquía de la organización de datos
De lo más pequeño a lo más grande:
1. **Bit** (0/1);
2. **Carácter / byte** (8 bits; 1000 0001 = 'A');
3. **Elemento de dato / campo** (caracteres en un contexto: "Pedro Pérez");
4. **Registro** (campos relacionados lógicamente: nombre, edad, estado civil, departamento);
5. **Archivo** (conjunto de registros del mismo tipo: archivo de ventas, de clientes);
6. **Base de datos** (archivos integrados lógicamente).

## 4. Sistema de base de datos y DBMS
- Un **sistema de base de datos** es una colección de archivos interrelacionados y un conjunto de programas que permiten acceder y modificarlos. Su propósito principal es dar una **visión abstracta** de los datos, ocultando cómo se almacenan.
- Un **DBMS/SGBD (Sistema Administrador de Base de Datos)** es la colección de datos organizados e integrados lógicamente más el software que permite su definición y manipulación.
- Ventaja central: **centraliza los datos y minimiza la redundancia**, sirviendo a muchas aplicaciones (ventas, producción, inventario, pedidos) con un único repositorio, a diferencia del enfoque de archivos aislados por aplicación (duplicación, inconsistencia, dificultad de compartir).

## 5. Niveles de abstracción
| Nivel | Qué describe |
|---|---|
| Físico | Cómo se almacenan realmente los datos (estructuras de bajo nivel, archivos, índices). |
| Lógico / conceptual | Qué datos se almacenan y qué relaciones existen entre ellos, en pocas estructuras simples (tablas). |
| Vistas | Solo la parte de la base de datos relevante para un usuario o aplicación (subesquemas). |

### Independencia de datos
- **Independencia física**: se puede cambiar el almacenamiento (índices, particiones, ubicación de archivos) sin tocar el esquema lógico ni los programas.
- **Independencia lógica/conceptual**: se puede cambiar el esquema conceptual (agregar una columna o tabla) sin alterar los subesquemas (vistas) existentes.

Ejemplo: en Oracle, crear un índice sobre `cliente(apellido)` no requiere cambiar ninguna consulta (independencia física); crear una vista `v_clientes_activos` protege a las aplicaciones si luego se agrega una columna a `cliente` (independencia lógica).

## 6. Esquema e instancia
- **Esquema**: diseño completo de la BD (estructura); cambia rara vez. Hay esquema físico, lógico y subesquemas.
- **Instancia (ejemplar)**: colección de datos almacenados en un instante dado; cambia con cada inserción o borrado.
Analogía de programación: el esquema es la declaración de tipos y la instancia es el valor de las variables ([[Programación II]]).

## 7. Modelos de datos
Un modelo de datos es un conjunto de herramientas conceptuales para describir datos, relaciones, asociaciones, reglas y restricciones. Tres grupos:
1. **Modelos lógicos basados en objetos** (niveles conceptual y de vistas): Entidad-Relación y orientado a objetos. Son flexibles y permiten expresar restricciones explícitamente. Se verán en el Tema II.
2. **Modelos lógicos basados en registros** (niveles conceptual y físico): **relacional**, de red y jerárquico. El relacional se estudia en el Tema III.
3. **Modelos físicos**: describen los datos en el nivel más bajo.

## 8. El enfoque relacional
Representa datos y relaciones mediante **tablas** de columnas con nombre único:
- **Tabla**: arreglo bidimensional de filas y columnas.
- **Columna**: valores del mismo tipo (atributo).
- **Fila**: conjunto de datos relacionados (tupla/registro).
- **Campo**: valor en la intersección fila-columna.
Las tablas se relacionan mediante valores comunes (por ejemplo, `cliente_id` en `cuenta_cliente`).

## 9. Lenguajes de base de datos
- **DDL (Data Definition Language)**: especifica el esquema. Su compilación produce metadatos almacenados en el **diccionario de datos** (datos sobre los datos). Ejemplo del curso:
```sql
create table cuentas (numero_cuenta char(10), saldo integer);
```
- **DML (Data Manipulation Language)**: recuperar, insertar, borrar y modificar información. SQL es el lenguaje de consulta relacional. Ejemplo:
```sql
select cliente.nombre_cliente
from cliente
where cliente.id_cliente = '19-283-746';

select cuenta.saldo
from cuenta_cliente, cuenta
where cuenta_cliente.id_cliente = '19-283-746'
  and cuenta_cliente.numero_cuenta = cuenta.numero_cuenta;
```
La segunda consulta navega desde el cliente hasta sus cuentas con una condición de unión (join), idea que se profundiza en [[Base de Datos I - Tema 5 Consultas avanzadas SQL]].

## 10. Estructura de un DBMS
Dos grandes componentes:

**Gestor de almacenamiento**: interfaz entre los datos de bajo nivel y las aplicaciones/consultas. Traduce el DML a órdenes del sistema de archivos. Incluye:
- gestor de autorización e integridad (verifica restricciones y permisos);
- gestor de transacciones (consistencia ante fallos y concurrencia sin conflictos);
- gestor de archivos (reserva espacio en disco y estructuras para representar la información);
- gestor de memoria intermedia (buffer: trae datos del disco a memoria y decide qué mantener en caché).
Implementa estructuras físicas: archivos de datos, diccionario de datos e índices.

**Procesador de consultas**: traduce consultas y actualizaciones escritas en lenguaje no procedimental (nivel lógico) a una secuencia de operaciones físicas. Incluye el intérprete del DDL (registra definiciones en el diccionario), el compilador/precompilador del DML y el motor de evaluación de consultas con optimización.

## 11. Arquitectura de aplicaciones
- **Dos capas**: la aplicación (lógica de negocio) corre en el cliente y llama al servidor de BD con sentencias del lenguaje de consultas.
- **Tres capas**: el cliente es solo frontal (formularios), no habla directamente con la BD; se comunica con un **servidor de aplicaciones** que a su vez accede a la BD. Es más apropiada para aplicaciones grandes y para la Web (el caso de estudio del Tema I plantea justamente una aplicación web de ventas). Nota: las diapositivas rotulan "cliente (back end)" y "servidor (front end)", lo cual está invertido respecto del uso habitual (front end = cliente, back end = servidor); conviene usar la terminología estándar.

## Errores comunes
- Confundir **dato** con **información** o **esquema** con **instancia**.
- Pensar que independencia física significa que "no hay almacenamiento": lo que significa es que las aplicaciones no dependen de él.
- Creer que DBMS y base de datos son lo mismo: el DBMS es el software; la base de datos son los datos.
- Mezclar DDL con DML: `CREATE/ALTER/DROP` definen estructura; `SELECT/INSERT/UPDATE/DELETE` manipulan datos.

## Ejercicios propuestos
1. Clasifique como dato, información o conocimiento: "17", "El pedido 17 se entregó tarde", "Los pedidos a Mérida se retrasan 3 días en promedio, hay que cambiar de transportista". (Dato / información / conocimiento.)
2. Un DBA mueve una tabla a otro tablespace. ¿Qué tipo de independencia se evidencia? (Física.)
3. Explique por qué un trigger de validación pertenece al gestor de autorización e integridad y no al de archivos. (Verifica restricciones; el gestor de archivos solo gestiona el espacio.)
4. ¿Qué capa de una arquitectura de tres capas habla con el DBMS? (El servidor de aplicaciones.)

## Conexiones
- Continuación metodológica: [[Base de Datos I - Tema 1 Metodología DAMA-DMBOK y ciclo de vida]].
- Modelado: [[Base de Datos I - Tema 2 Modelamiento de Datos DER]].
- Administración posterior: [[Administración de Base de Datos]], [[Base de Datos II]].

## Fuente
`Material/baseDatosI/temaI/materialApoyo/Curso Base de Datos I 2021.pdf` (37 diapositivas, Ing. Silverio Bonilla Sánchez).
