---
tags: [clase, electiva]
materia: Administración de Base de Datos
fuente: "conocimiento general; comandos básicos de ~/Documentos/UNET/administracion DB/COMANDOS_DBA_REFERENCIA.md"
---
# ADBD 07 - Respaldo y recuperación con RMAN

Materia: [[Administración de Base de Datos]]
Anterior: [[ADBD 06 - Roles, privilegios y auditoría]]
Siguiente: [[ADBD 08 - Afinamiento y alta disponibilidad]]

## Contexto y objetivo
El trabajo central de un DBA es que los datos sobrevivan a fallas. Esta clase presenta los tipos de falla, el modo ARCHIVELOG, **RMAN** (Recovery Manager) y flashback. Objetivo: diseñar una estrategia de respaldo y ejecutar una recuperación completa y una a un punto en el tiempo.

## Teoría

### Tipos de falla
Falla de sentencia, de proceso, de usuario (borrado accidental), de instancia (corte de energía; la recupera SMON automáticamente), de medio (pérdida de datafile o disco; exige restaurar).

### NOARCHIVELOG vs ARCHIVELOG
- **NOARCHIVELOG**: los redo se sobrescriben; solo se recupera al último respaldo frío completo. Aceptable en desarrollo.
- **ARCHIVELOG**: los redo llenos se archivan; permite respaldo en caliente y recuperación hasta un punto en el tiempo (PITR). Obligatorio en producción.

### Métricas de diseño
$$RPO = \text{pérdida máxima de datos tolerable},\qquad RTO = \text{tiempo máximo de restauración}$$
La frecuencia de respaldo y el archivado de redo determinan el RPO; el hardware y la estrategia (incremental, copia de imagen) determinan el RTO.

### RMAN
Herramienta cliente; guarda metadatos en el control file (o un catálogo). Conceptos: *backup set* (formato propietario, comprimible), *image copy*, respaldo **incremental** nivel 0 (base) y 1 (cambios; diferencial o acumulativo), *fast recovery area* (`DB_RECOVERY_FILE_DEST`), políticas de retención (`CONFIGURE RETENTION POLICY`).

### Flashback
Revierte cambios lógicos sin restaurar: `FLASHBACK TABLE ... TO TIMESTAMP`, consultas `AS OF TIMESTAMP` (usan undo) y `FLASHBACK DATABASE` (requiere flashback logs). Complementa, no sustituye, al respaldo.

## Ejemplo resuelto
Escenario: el 15 de noviembre a las 10:00 se ejecuta por error `DELETE FROM consumptions` y se confirma; hay respaldo nocturno y ARCHIVELOG.

1. Activar ARCHIVELOG (una vez):
```sql
SHUTDOWN IMMEDIATE
STARTUP MOUNT
ALTER DATABASE ARCHIVELOG;
ALTER DATABASE OPEN;
ARCHIVE LOG LIST
```
2. Configuración y respaldo:
```bash
rman target /
```
```
CONFIGURE RETENTION POLICY TO RECOVERY WINDOW OF 7 DAYS;
CONFIGURE CONTROLFILE AUTOBACKUP ON;
BACKUP DATABASE PLUS ARCHIVELOG;
# Estrategia incremental: domingo nivel 0, resto nivel 1
BACKUP INCREMENTAL LEVEL 0 DATABASE;
BACKUP INCREMENTAL LEVEL 1 DATABASE;
LIST BACKUP SUMMARY;
REPORT NEED BACKUP;
DELETE OBSOLETE;
```
3. Opción rápida, sin restaurar nada (si el undo alcanza):
```sql
-- ¿Cuántas filas había antes del error?
SELECT COUNT(*) FROM comedor.consumptions
  AS OF TIMESTAMP TO_TIMESTAMP('2026-11-15 09:59:00','YYYY-MM-DD HH24:MI:SS');
ALTER TABLE comedor.consumptions ENABLE ROW MOVEMENT;
FLASHBACK TABLE comedor.consumptions
  TO TIMESTAMP TO_TIMESTAMP('2026-11-15 09:59:00','YYYY-MM-DD HH24:MI:SS');
```
4. Si el undo ya no alcanza, recuperación a un punto en el tiempo (en una PDB o clon):
```
RUN {
  SET UNTIL TIME "TO_DATE('2026-11-15 09:59:00','YYYY-MM-DD HH24:MI:SS')";
  RESTORE DATABASE;
  RECOVER DATABASE;
}
ALTER DATABASE OPEN RESETLOGS;
```
Recuperación completa de un datafile perdido: `RESTORE DATAFILE n; RECOVER DATAFILE n;` con la base montada o el tablespace offline.

Verificación de respaldos: `RESTORE DATABASE VALIDATE;` y `CROSSCHECK BACKUP;`.

## Errores comunes
- Nunca probar la restauración: un respaldo no verificado no es un respaldo.
- Guardar respaldos en el mismo disco que los datafiles.
- NOARCHIVELOG en producción.
- Olvidar respaldar el control file y los archive logs; borrar archive logs con el sistema operativo en vez de RMAN.
- Confundir flashback (cambios lógicos recientes) con recuperación de medio.

## Ejercicios propuestos
1. RPO de 15 minutos: ¿qué debe configurarse? *Respuesta: ARCHIVELOG con archivado frecuente/transporte de redo (p. ej. Data Guard) y respaldos de archive logs cada pocos minutos.*
2. Diferencia entre incremental diferencial y acumulativo. *Respuesta: el diferencial respalda cambios desde el último nivel 0 o 1; el acumulativo, desde el último nivel 0.*
3. ¿Qué comando abre la base tras recuperación incompleta? *Respuesta: `ALTER DATABASE OPEN RESETLOGS;`.*

## Conexiones
[[Sistemas Operativos]] (sistemas de archivos, copias de seguridad), [[Base de Datos II]] (recuperación y logging), [[Organización del Computador]] (RAID y almacenamiento), [[Sistemas Distribuidos]] (replicación).

## Fuente
Conocimiento general (Oracle Backup and Recovery User's Guide); los comandos `rman target /`, `BACKUP DATABASE PLUS ARCHIVELOG`, `LIST BACKUP SUMMARY` y `RESTORE/RECOVER DATABASE` aparecen en `~/Documentos/UNET/administracion DB/COMANDOS_DBA_REFERENCIA.md`. Verificar con el programa oficial el alcance de RMAN en el curso.
