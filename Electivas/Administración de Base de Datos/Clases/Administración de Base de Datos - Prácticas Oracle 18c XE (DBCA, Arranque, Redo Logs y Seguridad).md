---
tags: [clase, electiva, oracle, dba]
materia: Administración de Base de Datos
---
# Administración de Base de Datos - Prácticas Oracle 18c XE (DBCA, Arranque, Redo Logs y Seguridad)

Materia: [[Administración de Base de Datos]]
Anterior: _Ninguna_
Siguiente: _Ninguna_

## Contexto y objetivo

Compilación de la serie completa de prácticas e informes de **Administración de Bases de Datos (`0423805T`, Lapso 2026-1)** sobre **Oracle Database 18c Express Edition (XE)** en Oracle Linux / contenedor Docker (`gvenzl/oracle-xe:18-slim`, CDB `XE` / PDB `XEPDB1`), tomando como caso de estudio el esquema del **Comedor Universitario UNET** (25 tablas, 169 restricciones, proyección a 3 años de 1.229.674 filas / 257 MB).

## 1. Arranque, Parada y Vistas Dinámicas

- **Fases de inicio:** `STARTUP NOMOUNT` (lee `SPFILE`/`PFILE`, asigna SGA y procesos en segundo plano) → `ALTER DATABASE MOUNT` (lee Control Files) → `ALTER DATABASE OPEN` (abre Datafiles y Redo Logs).
- **Modos de parada:** `SHUTDOWN NORMAL`, `TRANSACTIONAL`, `IMMEDIATE` (recomendado para mantenimiento), `ABORT` (requiere recuperación de instancia al reiniciar) y `STARTUP FORCE`.
- **Vistas dinámicas (`V$`) clave:** `V$INSTANCE`, `V$DATABASE`, `V$PARAMETER`, `V$SGA`, `V$SESSION`, `V$CONTROLFILE`, `V$DATAFILE`, `V$TABLESPACE`, `V$LOG`.

## 2. Creación de BD, Tablespaces, UNDO y TEMP

- **Creación manual (`Informe_Creacion_BD_COMEDOR`):** Archivo `initCOMEDOR.ora`, `orapwd`, `CREATE DATABASE`, construcción del diccionario de datos y 6 tablespaces funcionales con gestión local de extents.
- **UNDO y TEMP (`Informe2`):** Diagnóstico con `DBA_ROLLBACK_SEGS` y `V$UNDOSTAT`; creación de `TS_COMEDOR_UNDO` (`RETENTION GUARANTEE`, `UNDO_RETENTION = 3600`) y `TS_COMEDOR_TEMP` (`UNIFORM SIZE 2M`).

## 3. Multiplexación de Redo Logs y Control Files (Práctica 4)

- **Redo Logs en caliente:** Multiplexación en **4 grupos, 8 miembros y 3 directorios** para evitar pérdida de transacciones ante fallo de disco (`ALTER DATABASE ADD LOGFILE MEMBER ... TO GROUP n`).
- **Control Files en frío:** Actualización de `control_files` en `SPFILE`, parada limpia (`SHUTDOWN IMMEDIATE`), copia física del archivo de control a múltiples rutas (3 copias en 2 directorios) y `STARTUP`.
- **Diccionario de datos:** Diferencia entre `USER_*` (objetos propios), `ALL_*` (objetos accesibles) y `DBA_*` (todos los objetos de la BD).

## 4. Seguridad: Perfiles, Roles y Delegación (Informes 3 y 4)

- Activar límites de recursos: `ALTER SYSTEM SET RESOURCE_LIMIT = TRUE SCOPE=BOTH;`
- Traducción de roles de aplicación (`SUPER_ADMIN`, `ADMIN`, `TAQUILLERO`, `BENEFICIARIO`) a perfiles (`PERF_COMEDOR_*`), roles (`ROL_COMEDOR_*`) y usuarios Oracle.
- **Delegación (`WITH ADMIN OPTION` vs `WITH GRANT OPTION`):**
  - `WITH ADMIN OPTION` aplica a **privilegios de sistema y roles** (revocar no es en cascada).
  - `WITH GRANT OPTION` aplica a **privilegios de objeto** (revocar sí es en cascada; no puede otorgarse a un rol, error `ORA-01926`).

## Errores Oracle frecuentes observados

- `ORA-01926`: no se puede otorgar un privilegio con `GRANT OPTION` a un rol.
- `ORA-01931`: no se puede otorgar ciertos privilegios/roles bajo condiciones de rol no válido.
- `ORA-01932`: la opción `ADMIN` no fue otorgada para el rol.
- `ORA-01031`: privilegios insuficientes (verificar contenedor `XEPDB1` vs `CDB$ROOT` y `SYSDBA`).

## Recursos en Google Drive

- [Guia_Didáctica_ABD 2026-1](https://docs.google.com/document/d/1Yn4HezsWIOopVc7X4lgDFIjB6nF7JGsZrYxPTz_qhLE/edit?usp=drivesdk)
- [Practica_DBA_Oracle_Arranque_y_Parada](https://docs.google.com/document/d/1FTjiEjYtCyD9QbeEoBUAtlyegsi-dkVC5zRbvMrG3lI/edit?usp=drivesdk)
- [Informe_Practica4_PasoAPaso](https://docs.google.com/document/d/14krY8KfmF-P4dp4ZqLuWUGwqjGhJa_-dYtyxPm9hMM8/edit?usp=drivesdk)
- [Informe 4: Seguridad y Delegación](https://docs.google.com/document/d/1NdM5oKCJ-wzetu4UE_0w_0OhTAthgEK9RrsejFldKWE/edit?usp=drivesdk)

## Conexiones

- Amplía [[Base de Datos I]] y [[Base de Datos II]].
- Usa como caso de estudio el [[Sistema Comedor Universitario UNET (CSC-P 2026)]].
