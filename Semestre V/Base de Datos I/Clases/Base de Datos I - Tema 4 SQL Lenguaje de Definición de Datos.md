---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaIV/materialDeApoyo/SQL Lenguaje de Definicion de Datos v1.pdf
---
# Tema 4 - SQL: Lenguaje de Definición de Datos (DDL) en Oracle

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 3 Caso de Estudio Diseño Físico]]
Siguiente: [[Base de Datos I - Tema 4 Curso de SQL Básico]]

## Contexto y objetivo
Con el diseño físico listo (Tema 3) se crea el esquema en el motor. Este apunte reconstruye las 50 diapositivas "Introducción a SQL - Lenguaje de Definición de Datos (DDL)": qué es SQL, tipos de sentencias, objetos de base de datos, CREATE/ALTER/DROP/TRUNCATE/RENAME/COMMENT, restricciones, diccionario de datos, vistas, secuencias, índices, sinónimos y privilegios, todo con sintaxis **Oracle**.

## 1. Conceptos previos
- **RDBMS**: datos organizados e integrados lógicamente más el software de definición y manipulación. Ventajas: control de redundancia y consistencia, datos integrados y compartidos, control de integridad, estándares, desarrollo de aplicaciones más fácil, seguridad uniforme, independencia datos-programas, menor costo de mantenimiento.
- **SQL (Structured Query Language)**: adoptado por ANSI en octubre de 1986 y por ISO en 1987. Es **no procedimental**: se indica *qué* se quiere, no *dónde* ni *cómo*. **PL/SQL** es la extensión procedimental de Oracle (Tema 6, [[Base de Datos I - Tema 6 Curso de PL/SQL Básico]]). Las sentencias se guardan en el *SQL buffer* hasta la siguiente.

### Categorías de sentencias
| Categoría | Sentencias | Función |
|---|---|---|
| DDL | CREATE, ALTER, DROP, RENAME, TRUNCATE (y COMMENT) | crear y mantener la estructura |
| DML | SELECT, INSERT, UPDATE, DELETE | manipular datos |
| Control de transacciones | COMMIT, ROLLBACK, SAVEPOINT | confirmar o deshacer cambios DML |
| DCL | GRANT, REVOKE | privilegios |
Detalle técnico importante (complemento): en Oracle cada sentencia DDL hace **COMMIT implícito** antes y después, por eso no se puede deshacer un DROP o TRUNCATE.

## 2. Objetos de la base de datos
Tabla (unidad básica de almacenamiento), vista (subconjunto lógico de datos), secuencia (números consecutivos), índice (rendimiento) y sinónimo (nombre alternativo). **Convenciones de nombres**: empezar por letra; 1 a 30 caracteres; solo letras, dígitos, `_`, `$`, `#`; sin duplicados en el mismo esquema; no ser palabra reservada.

## 3. CREATE TABLE
Requisitos: privilegio `CREATE TABLE` y espacio (tablespace). Se especifica nombre, columnas, tipos y tamaños y, opcionalmente, restricciones.

### Tipos de datos Oracle
| Tipo | Descripción |
|---|---|
| VARCHAR2(t) | cadena variable, 1 a 4000 |
| CHAR(t) | cadena fija, hasta 2000 |
| NUMBER(p,s) | numérico; p = dígitos totales (1-38), s = dígitos decimales |
| DATE | fecha y hora |
| LONG, RAW, LONG RAW, BLOB, BFILE | texto largo, binarios, objetos grandes |
Ejemplo: `NUMBER(12,2)` guarda hasta 10 dígitos enteros y 2 decimales (montos).

### Restricciones (constraints)
Reglas impuestas a una tabla para evitar datos inconsistentes: `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY` (con `ON DELETE CASCADE` opcional) y `CHECK`. Se pueden dar nombre (si no, Oracle asigna `SYS_Cn`), se crean al crear la tabla o después, y se definen **a nivel de columna o de tabla** (las compuestas solo a nivel de tabla). Se consultan en el diccionario.

**A nivel de columna:**
```sql
CREATE TABLE departamento (
  numdept   NUMBER(2)    NOT NULL CONSTRAINT depar_pk PRIMARY KEY,
  nombre    VARCHAR2(14) NOT NULL CONSTRAINT depar_ck CHECK (nombre = UPPER(nombre)),
  ubicacion VARCHAR2(13) DEFAULT 'LOCAL'
);
```
**A nivel de tabla (preferible, más legible):**
```sql
CREATE TABLE empleado (
  num_emp   NUMBER(4)    NOT NULL,
  cedula    VARCHAR2(12) NOT NULL,
  nombre    VARCHAR2(30) NOT NULL,
  direccion VARCHAR2(40) NOT NULL,
  telef     VARCHAR2(12),
  numdept   NUMBER(2)    NOT NULL,
  CONSTRAINT emple_pk PRIMARY KEY (num_emp),
  CONSTRAINT emple_uk UNIQUE (cedula),
  CONSTRAINT emple_ck CHECK (nombre = UPPER(nombre)),
  CONSTRAINT emple_fk FOREIGN KEY (numdept)
      REFERENCES departamento (numdept) ON DELETE CASCADE
);
```
(Observación: la diapositiva con restricciones por columna reutiliza el nombre `emple_uk` para la FK, lo que fallaría por nombre duplicado; es un error del original que debe evitarse.)

**Desde una subconsulta (CTAS):**
```sql
CREATE TABLE departamento30 AS
  SELECT nombre, ubicacion FROM departamento WHERE numdept = 30;
```
Copia estructura y datos, pero **no** copia restricciones salvo NOT NULL.

## 4. ALTER TABLE, DROP, RENAME, TRUNCATE, COMMENT
```sql
ALTER TABLE departamento ADD (clasificacion VARCHAR2(30));      -- columna nueva al final
ALTER TABLE departamento MODIFY (nombre VARCHAR2(60));          -- tipo, tamaño o DEFAULT; afecta solo nuevas inserciones
ALTER TABLE empleado ADD CONSTRAINT empno_pk PRIMARY KEY (empno);
ALTER TABLE empleado ADD CONSTRAINT fk_jefe FOREIGN KEY (jefe) REFERENCES empleado(empno);
ALTER TABLE empleado DISABLE CONSTRAINT fk_jefe;                -- con CASCADE para dependientes
ALTER TABLE empleado ENABLE  CONSTRAINT fk_jefe;
DROP TABLE departamento3 CASCADE CONSTRAINTS;                   -- borra datos, estructura e índices; no reversible
RENAME departamento2 TO copia_depa2;                            -- tabla, vista, secuencia o sinónimo
TRUNCATE TABLE departamento2;                                   -- borra todas las filas y libera espacio; sin reverso
COMMENT ON TABLE departamento IS 'Unidades de la empresa';
COMMENT ON COLUMN departamento.nombre IS 'Nombre en mayúsculas';
```
Diferencia clave **DELETE vs TRUNCATE**: DELETE es DML, admite WHERE y ROLLBACK, no libera espacio; TRUNCATE es DDL, borra todo, libera espacio y no admite rollback. (La diapositiva escribe `COMMENT ON TABLE tabla.columna`; la sintaxis correcta es `COMMENT ON COLUMN`.)

## 5. Diccionario de datos
Tablas del sistema mantenidas por el servidor con metadatos. Prefijos: `USER_` (objetos del usuario), `ALL_` (a los que tiene acceso), `DBA_` (toda la base; solo DBA), `V$_` (rendimiento y estado; DBA).
```sql
SELECT * FROM user_tables;
SELECT DISTINCT object_type FROM user_objects;
SELECT * FROM user_catalog;                        -- tablas, vistas, sinónimos y secuencias
SELECT * FROM user_constraints WHERE table_name = 'EMPLEADO';
SELECT * FROM user_cons_columns;
SELECT * FROM user_tab_comments;  -- user_col_comments
```
Utilidad práctica: verificar tras la ejecución de un script que todas las tablas y restricciones existen (se usa en el caso de estudio).

## 6. Vistas
Tabla lógica basada en otras tablas (o vistas); solo se almacena la definición. Usos: restringir acceso, simplificar consultas complejas, independencia de datos y distintas versiones de los mismos datos.
| Característica | Vista simple | Vista compleja |
|---|---|---|
| Tablas | una | una o más |
| Funciones | no | sí |
| Grupos | no | sí |
| DML | sí | no siempre |
```sql
CREATE OR REPLACE VIEW v_empleados_ventas AS
  SELECT num_emp, nombre FROM empleado WHERE numdept = 30;
```

## 7. Secuencias
Generan números consecutivos automáticamente.
```sql
CREATE SEQUENCE dep INCREMENT BY 1 START WITH 11 MAXVALUE 99 NOCYCLE NOCACHE;
SELECT dep.NEXTVAL FROM dual;    -- siguiente valor (incrementa)
SELECT dep.CURRVAL FROM dual;    -- valor actual (no altera; requiere un NEXTVAL previo en la sesión)
INSERT INTO depart (dept_no, dnombre, loc) VALUES (dep.NEXTVAL, '&nombre_dep', '&ubica');
ALTER SEQUENCE dep MAXVALUE 200;  DROP SEQUENCE dep;
SELECT sequence_name, min_value, max_value, increment_by, last_number FROM user_sequences;
```
Las secuencias **no garantizan ausencia de huecos** (un rollback no devuelve el número). En Oracle 12c+ existe la alternativa `GENERATED ALWAYS AS IDENTITY`, usada en el caso de estudio ([[Base de Datos I - Tema 4 Caso de Estudio Diseño e Implementación]]).

## 8. Índices
Estructura que acelera el acceso. Se crean **automáticamente** (por PK y UNIQUE) o manualmente: `CREATE INDEX ind_nombre_emp ON empleado(nombre);` y `DROP INDEX ind_nombre_emp;`. Vistas: `USER_INDEXES`, `USER_IND_COLUMNS`.
**Crear** cuando: la columna se usa en WHERE o joins, tiene amplio rango de valores o muchos nulos, la tabla es grande y las consultas recuperan ~2-4 % de filas. **No crear** si: tabla pequeña, columna no usada en joins, consultas que recuperan gran parte de la tabla, o tabla con actualización frecuente (cada DML debe mantener el índice).

## 9. Sinónimos
Nombre alternativo para simplificar acceso a objetos de otro usuario o remotos.
```sql
CREATE [PUBLIC] SYNONYM persona FOR scott.empleado;
DROP SYNONYM persona;     -- consulta: USER_SYNONYMS
```

## 10. Control de acceso (DCL)
- **Privilegios de sistema** (más de 80): crear usuarios, objetos, respaldar, etc. (DBA).
- **Privilegios de objeto**: ALTER, DELETE, EXECUTE, INDEX, INSERT, REFERENCES, SELECT, UPDATE según el tipo de objeto. El propietario tiene todos y puede otorgarlos.
```sql
GRANT select, insert ON departamento TO scott WITH GRANT OPTION;
GRANT select ON departamento TO PUBLIC;
REVOKE select, insert ON departamento FROM scott;
-- diccionario: USER_ROLE_PRIVS, USER_TAB_PRIVS_MADE, USER_TAB_PRIVS_RECD, USER_COL_PRIVS_MADE/RECD
```
Esquema = colección de objetos de un usuario.

## Errores comunes
- Crear la tabla hija antes que la padre (la FK falla); orden de creación: padres primero, y de borrado: hijas primero o `CASCADE CONSTRAINTS`.
- Nombres de constraints repetidos.
- Pensar que `TRUNCATE` o `DROP` se pueden revertir con ROLLBACK.
- Usar `CHAR` para textos de longitud variable (relleno con espacios que rompe comparaciones).
- `MODIFY` a un tamaño menor con datos existentes que no caben.
- Indexar todo "por si acaso".

## Ejercicios propuestos
1. Escriba el DDL de `producto(codigo PK, nombre NOT NULL único, precio > 0, categoria_id FK)`.
2. Cree una secuencia que empiece en 1000 y avance de 5 en 5 sin ciclo. (`CREATE SEQUENCE s START WITH 1000 INCREMENT BY 5 NOCYCLE;`)
3. ¿Cómo listaría todas las FK de su esquema? (`SELECT * FROM user_constraints WHERE constraint_type = 'R';`)
4. Dé el privilegio de solo lectura sobre `producto` a un rol `ROL_READONLY`. (`GRANT SELECT ON producto TO rol_readonly;`)

## Conexiones
[[Base de Datos I - Tema 4 Curso de SQL Básico]] (DML), [[Base de Datos I - Tema 3 Curso de Diseño Físico]] (origen de las restricciones), [[Administración de Base de Datos]] (privilegios, tablespaces, índices).

## Fuente
`Material/baseDatosI/temaIV/materialDeApoyo/SQL Lenguaje de Definicion de Datos v1.pdf`. Correcciones y detalles sobre COMMIT implícito, CTAS e IDENTITY son complemento de conocimiento general.
