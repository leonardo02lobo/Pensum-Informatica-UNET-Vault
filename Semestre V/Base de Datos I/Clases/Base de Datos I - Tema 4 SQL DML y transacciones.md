---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaIV/materialDeApoyo/Curso de SQL Basico (DML) Parte IV.pdf
---
# Tema 4 - SQL DML: INSERT, UPDATE, DELETE, MERGE y transacciones

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 4 Curso de SQL Básico]]
Siguiente: [[Base de Datos I - Tema 4 Introducción a Oracle9i SQL]]

## Contexto y objetivo
Reconstrucción de las 22 diapositivas "Lenguaje de Manipulación de Datos (DML)" (Parte IV del curso de SQL básico). Explica cómo se modifican los datos y cómo el motor garantiza consistencia mediante **transacciones**, **commit/rollback/savepoint**, **consistencia de lectura** y **bloqueos**. Es la base de las pruebas de restricciones del caso del Tema 4 ([[Base de Datos I - Tema 4 Caso de Estudio Diseño e Implementación]]).

## 1. Qué es una instrucción DML de actualización
Se ejecuta al insertar, actualizar o eliminar filas. Una **transacción** es una colección de instrucciones DML que forman una **unidad lógica de trabajo** (todo o nada; propiedad de atomicidad de ACID).

## 2. INSERT
```sql
INSERT INTO departamento (numdept, nombre) VALUES (50, 'TRANSPORTE');   -- lista de columnas explícita
INSERT INTO departamento VALUES (50, 'TRANSPORTE', NULL);               -- orden de definición, todas las columnas
INSERT INTO emp_investigacion (empno, nombre, cargo, numdept)
  SELECT empno, nombre, cargo, numdept FROM empleado WHERE numdept = 4; -- desde subconsulta (varias filas, sin VALUES)
```
Con VALUES se inserta **una** fila; las columnas omitidas quedan en NULL (o su DEFAULT). Con subconsulta, número y tipos de columnas deben coincidir. Si falta una columna NOT NULL, o se viola PK/FK/CHECK, la sentencia **falla completa** (ORA-00001, ORA-02291, ORA-02290...).

## 3. UPDATE
```sql
UPDATE empleado SET numdept = 3 WHERE empno = 100;
UPDATE emp_investigacion
   SET numdept = (SELECT numdept FROM departamento WHERE nombre = 'Contabilidad')
 WHERE (empno, nombre) = (SELECT empno, nombre FROM empleado WHERE empno = 100);
UPDATE tabla SET (c1, c2) = (SELECT ...) WHERE condición;
```
Sin WHERE se actualizan **todas** las filas. Si la subconsulta devuelve más de una fila donde se espera una, ocurre error (ORA-01427).

## 4. DELETE
```sql
DELETE FROM empleado
 WHERE numdept = (SELECT numdept FROM departamento WHERE nombre = 'OPERACION');
DELETE FROM departamento WHERE nombre = 'ADMINISTRACION';
DELETE departamento;      -- sin WHERE: borra TODAS las filas
```
Si hay FK que referencian la fila, el borrado falla salvo `ON DELETE CASCADE` (borra hijos) o `ON DELETE SET NULL`. Alternativa de diseño usada en el caso de estudio: **borrado lógico** (`UPDATE ... SET estado = 'I'`).

## 5. MERGE (upsert)
Actualiza o inserta según haya coincidencia de join, en una sola sentencia:
```sql
MERGE INTO emp_investigacion A
USING empleado B
ON (A.emp_no = B.emp_no)
WHEN MATCHED THEN
  UPDATE SET A.cargo = B.cargo
WHEN NOT MATCHED THEN
  INSERT (emp_no, nombre, cargo, numdept)
  VALUES (B.emp_no, B.nombre, B.cargo, B.numdept);
```
(La diapositiva muestra `MERGE INTO tabla AS alias`; en Oracle no se usa `AS` para alias de tabla.) Útil para sincronizar tablas de carga con tablas finales.

## 6. Transacciones
**Inicio**: la primera sentencia SQL. **Fin** cuando ocurre: `COMMIT` o `ROLLBACK`; una sentencia DDL o DCL (commit automático); el usuario cierra la sesión (commit en salida normal); falla del sistema (rollback).
- `COMMIT`: guarda cambios permanentemente. `ROLLBACK`: deshace desde el último commit. Sirven para asegurar consistencia, hacer cambios temporales antes de hacerlos permanentes y agrupar operaciones relacionadas.
- `SAVEPOINT nombre`: marca; `ROLLBACK TO nombre` deshace hasta la marca sin terminar la transacción.

Esquema del curso:
```
INSERT (1) ; SAVEPOINT A ; DELETE (2) ; ROLLBACK TO A   -> se reversa solo el cambio 2
UPDATE (3) ; INSERT (4) ; COMMIT                         -> se guardan 1, 3 y 4
```
Ejemplo de transferencia bancaria (complemento):
```sql
UPDATE cuenta SET saldo = saldo - 100 WHERE id = 1;
UPDATE cuenta SET saldo = saldo + 100 WHERE id = 2;
COMMIT;   -- ambos o ninguno
```

### Estado de los datos
| Momento | Efecto |
|---|---|
| Antes de COMMIT/ROLLBACK | el estado previo se puede recuperar; el usuario ve sus cambios con SELECT; **otros usuarios no los ven**; las filas afectadas están **bloqueadas** |
| Después de COMMIT | cambios permanentes; todos los ven; se liberan bloqueos; se borran SAVEPOINT; el estado previo se pierde |
| Después de ROLLBACK | estado previo restablecido; se liberan bloqueos |
**Alcance**: si una sentencia DML falla, solo **esa sentencia** se reversa (Oracle crea un SAVEPOINT implícito por sentencia) y los demás cambios de la transacción se mantienen.

## 7. Consistencia de lectura y bloqueos
- **Consistencia de lectura**: cada usuario ve una imagen consistente; "las lecturas no esperan escrituras ni las escrituras esperan lecturas" (Oracle usa multiversión con segmentos de undo).
- **Bloqueo de filas**: previene interacción destructiva entre transacciones concurrentes; es automático, usa el nivel más bajo de restricción y dura lo que la transacción. Modos: **exclusivo** (solo la transacción que bloquea accede; para cambios) y **compartido** (varias transacciones, normalmente lectura).
Ejemplo: sesión A hace `UPDATE ... WHERE id=1` sin commit; la sesión B puede leer la fila (valor antiguo) pero su `UPDATE` de la misma fila queda esperando hasta que A haga COMMIT o ROLLBACK.

## Errores comunes
- UPDATE o DELETE sin WHERE.
- Olvidar COMMIT y creer que otros usuarios ven los datos; o dejar transacciones abiertas bloqueando filas.
- Ejecutar DDL a mitad de una transacción esperando poder hacer rollback (commit implícito).
- Insertar sin lista de columnas y que el orden cambie luego del ALTER TABLE.
- Suponer que ROLLBACK deshace un TRUNCATE.

## Ejercicios propuestos
1. Duplique en una tabla de respaldo los empleados del departamento 1. (`INSERT INTO resp SELECT * FROM empleado WHERE numdept = 1;`)
2. ¿Qué queda tras: INSERT a; SAVEPOINT s; INSERT b; ROLLBACK TO s; COMMIT? (Solo a.)
3. Escriba un MERGE para actualizar precios de `producto` desde `precios_nuevos` e insertar los productos que no existan.
4. Explique por qué DELETE sin WHERE y TRUNCATE no son equivalentes. (rollback, espacio, triggers.)

## Conexiones
[[Base de Datos I - Tema 4 SQL Lenguaje de Definición de Datos]], [[Base de Datos I - Tema 4 Curso de SQL Básico]], [[Administración de Base de Datos]], [[Base de Datos II]] (transacciones y concurrencia a fondo).

## Fuente
`Material/baseDatosI/temaIV/materialDeApoyo/Curso de SQL Basico (DML) Parte IV.pdf`. Códigos de error ORA y ejemplos de transferencia son complemento.
