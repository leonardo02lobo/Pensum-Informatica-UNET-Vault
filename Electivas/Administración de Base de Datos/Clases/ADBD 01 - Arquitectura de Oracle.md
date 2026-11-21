---
tags: [clase, electiva]
materia: Administración de Base de Datos
fuente: "~/Documentos/UNET/administracion DB (COMANDOS_DBA_REFERENCIA.md, CONFIGURACION_INICIAL_DBA_COMEDOR.md) y conocimiento general"
---
# ADBD 01 - Arquitectura de Oracle

Materia: [[Administración de Base de Datos]]
Anterior: (inicio de la serie)
Siguiente: [[ADBD 02 - Tablespaces y almacenamiento]]

## Contexto y objetivo
Un DBA no puede administrar lo que no entiende. Esta clase describe las piezas de un servidor Oracle (instancia, memoria, procesos, archivos) y el modelo multitenant (CDB/PDB), que es el que usa el proyecto del comedor universitario en Oracle 18c XE. Objetivo: poder explicar qué ocurre desde que un usuario envía un `UPDATE` hasta que el cambio es durable, y moverse entre CDB y PDB desde SQL*Plus.

## Teoría

### Base de datos vs. instancia
- **Base de datos**: conjunto de archivos en disco (datafiles, control files, redo logs).
- **Instancia**: estructuras de memoria (SGA) más procesos en segundo plano. Una instancia abre una base de datos (en RAC, varias instancias abren la misma).

### Memoria
- **SGA** (System Global Area), compartida: *database buffer cache* (bloques leídos), *shared pool* (planes SQL y caché del diccionario), *redo log buffer*, *large pool*, *java pool*.
- **PGA** (Program Global Area), privada de cada proceso servidor: áreas de ordenamiento, variables de sesión.

### Procesos de segundo plano principales
| Proceso | Función |
|---|---|
| DBWn | Escribe bloques sucios del buffer cache a los datafiles |
| LGWR | Escribe el redo log buffer a los redo logs (en cada COMMIT) |
| CKPT | Señala checkpoints, actualiza cabeceras de archivos |
| SMON | Recuperación de instancia, limpieza de segmentos temporales |
| PMON | Limpia procesos de usuario fallidos |
| ARCn | Copia redo logs llenos a archivo (modo ARCHIVELOG) |

### Archivos físicos
- **Control file**: metadatos de la estructura física (nombres de datafiles, SCN, historial de respaldo). Se multiplexa.
- **Datafiles**: contienen los datos, agrupados en tablespaces.
- **Redo logs (online)**: bitácora circular de cambios; se organizan en grupos con miembros multiplexados.
- **Archived redo logs**: copias de los redo llenos; necesarios para recuperación a un punto en el tiempo.
- **Parameter file (SPFILE)**, **alert log** y trazas.

### Multitenant
Desde 12c, un **CDB** (Container Database, `CDB$ROOT`) aloja una o más **PDB** (Pluggable Databases) más la `PDB$SEED`. Cada PDB tiene sus propios tablespaces, usuarios y objetos; comparte con el CDB la instancia, los redo y el undo (en 18c). En XE 18c existe la PDB `XEPDB1`.

### Ciclo de una transacción
1. El proceso servidor lee el bloque al buffer cache (si no está).
2. Genera datos de *undo* y registros de *redo* en el log buffer.
3. Modifica el bloque en memoria (bloque "sucio").
4. En `COMMIT`, LGWR escribe el redo a disco: la transacción es durable aunque DBWn aún no haya escrito el bloque.
5. DBWn escribe el bloque después (checkpoint). Si la instancia cae, SMON reaplica el redo (*roll forward*) y deshace lo no confirmado con undo (*roll back*).

## Ejemplo resuelto: moverse y diagnosticar
Del material del estudiante (`COMANDOS_DBA_REFERENCIA.md`), contenedor Docker `oracomedor`:

```bash
# Entrar como SYSDBA al contenedor
docker exec -it oracomedor sqlplus / as sysdba
```
```sql
-- Estamos en el CDB raíz. Ver contenedores:
SHOW CON_NAME
SELECT con_id, name, open_mode FROM v$pdbs;

-- Cambiar a la PDB de la aplicación
ALTER SESSION SET CONTAINER = XEPDB1;
SHOW CON_NAME          -- ahora XEPDB1

-- Estado de la instancia y de la base
SELECT status FROM v$instance;                    -- OPEN
SELECT open_mode, log_mode FROM v$database;       -- READ WRITE, NOARCHIVELOG/ARCHIVELOG

-- Dónde está el alert log
SELECT * FROM v$diag_info WHERE name = 'Diag Trace';
```
Paso a paso: `SHOW CON_NAME` confirma que se arranca en `CDB$ROOT`; `v$pdbs` lista `PDB$SEED` y `XEPDB1`; la sentencia `ALTER SESSION SET CONTAINER` es la que usan todos los scripts del proyecto antes de crear tablespaces o usuarios.

Parámetros de memoria:
```sql
SHOW PARAMETER sga_target
SHOW PARAMETER pga_aggregate_target
SELECT name, value/1048576 AS mb FROM v$sga;
```

## Errores comunes
- Crear usuarios o tablespaces en `CDB$ROOT` en lugar de en la PDB (usuarios comunes deben llamarse `C##...`; ORA-65096).
- Confundir instancia con base de datos: apagar la instancia no borra datos.
- Creer que COMMIT escribe en los datafiles; escribe el redo.
- Olvidar que la PDB debe estar abierta (`ALTER PLUGGABLE DATABASE ... OPEN`).

## Ejercicios propuestos
1. ¿Qué proceso garantiza la durabilidad en un COMMIT? *Respuesta: LGWR.*
2. ¿Por qué es seguro que DBWn no haya escrito el bloque al confirmar? *Respuesta: el redo ya está en disco y permite rehacer el cambio en la recuperación de instancia.*
3. Escribe la consulta para saber en qué contenedor estás y qué PDB están abiertas. *Respuesta: `SHOW CON_NAME` y `SELECT name, open_mode FROM v$pdbs;`.*

## Conexiones
[[Base de Datos II]] (transacciones y recuperación), [[Sistemas Operativos]] (procesos y memoria compartida), [[Organización del Computador]] (jerarquía de memoria y E/S), [[Sistemas Distribuidos]] (RAC y réplica).

## Fuente
Material del estudiante: `~/Documentos/UNET/administracion DB/COMANDOS_DBA_REFERENCIA.md` y `CONFIGURACION_INICIAL_DBA_COMEDOR.md`. Teoría general: Oracle Database Concepts / Administrator's Guide; Kyte, *Expert Oracle Database Architecture*. Verificar con el programa oficial el alcance exacto.
