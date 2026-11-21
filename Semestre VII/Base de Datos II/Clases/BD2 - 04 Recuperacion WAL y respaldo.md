---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: conocimiento general
---
# BD2 - 04 Recuperación ante fallos, WAL y respaldo

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 03 Transacciones ACID y control de concurrencia]]
Siguiente: [[BD2 - 05 Indices y optimizacion de consultas]]

## Contexto y objetivo
Los fallos son inevitables: caída de energía, error de software, disco dañado. El SGBD debe garantizar **atomicidad** y **durabilidad** (la A y la D de ACID, ver [[BD2 - 03 Transacciones ACID y control de concurrencia]]). Objetivo: entender el registro de transacciones, el protocolo WAL, los puntos de control, REDO/UNDO y las estrategias de respaldo.

## Clasificación de fallos
1. **De transacción**: error lógico (división por cero) o aborto del sistema (deadlock). Solo requiere deshacer esa transacción.
2. **Del sistema**: se pierde la memoria volátil (buffers) pero no el disco. Requiere recuperación al reiniciar.
3. **De medio** (disco): se pierden datos persistentes. Requiere restaurar un respaldo y reaplicar el registro.

## Gestión de buffers y políticas
Las páginas se modifican en memoria (buffer pool) y se escriben a disco después.
- **Steal**: se permite escribir al disco páginas con cambios no confirmados (necesita UNDO).
- **No-force**: al confirmar no se obliga a escribir las páginas modificadas (necesita REDO).
- La combinación **steal/no-force** es la más eficiente y es la que usan los SGBD modernos; exige registro con REDO y UNDO.

## Write-Ahead Logging (WAL)
Regla: **el registro de un cambio debe llegar al disco antes que la página modificada** (y todos los registros de una transacción antes de su `COMMIT`). Cada registro lleva: LSN (número de secuencia), id de transacción, página, valor anterior (before image, para UNDO) y posterior (after image, para REDO).

Tipos de registros: `<T, inicio>`, `<T, X, antes, después>`, `<T, commit>`, `<T, abort>`, `<checkpoint, activas>`.

En PostgreSQL el WAL vive en `pg_wal/`; el parámetro `synchronous_commit` controla si el `COMMIT` espera el volcado (durabilidad estricta vs rendimiento); `fsync` nunca debería desactivarse en producción.

## Puntos de control (checkpoints)
Periódicamente se escriben a disco las páginas sucias y se anota un registro de checkpoint. En la recuperación solo hay que examinar el log **desde el último checkpoint**. Parámetros PostgreSQL: `checkpoint_timeout`, `max_wal_size`.

## Algoritmo de recuperación (estilo ARIES simplificado)
1. **Análisis**: leer el log desde el último checkpoint; determinar transacciones activas al momento de la falla y páginas sucias.
2. **REDO**: repetir historia; reaplicar todos los cambios desde el punto más antiguo necesario (incluidos los de transacciones que luego abortarán).
3. **UNDO**: deshacer los cambios de las transacciones no confirmadas, escribiendo registros de compensación (CLR).

### Ejemplo resuelto
Log: `T1 inicio; T1,A,10→20; T2 inicio; T2,B,5→8; T1 commit; CHECKPOINT; T2,C,1→2; ` *caída*.
- Confirmadas: T1. No confirmadas: T2.
- REDO: se reaplica todo lo posterior al checkpoint (C=2) y lo necesario antes.
- UNDO de T2: C vuelve a 1, B vuelve a 5.
- Estado final: A=20 (T1 confirmada), B=5, C=1.

## Respaldo y restauración
| Tipo | Descripción | Herramienta PostgreSQL |
|---|---|---|
| Lógico | Exporta SQL/datos | `pg_dump`, `pg_dumpall`; restaurar con `psql`/`pg_restore` |
| Físico en frío | Copia de archivos con el servidor detenido | copia de `PGDATA` |
| Físico en caliente | `pg_basebackup` + archivado del WAL | `archive_mode`, `archive_command` |
| Incremental / diferencial | Solo cambios desde el último respaldo | herramientas externas (pgBackRest, Barman) |

**PITR (Point-In-Time Recovery)**: restaurar un respaldo base y reproducir el WAL archivado hasta un instante concreto (por ejemplo, justo antes de un `DROP TABLE` accidental) con `recovery_target_time`.

**Replicación**: un servidor *standby* recibe el WAL en streaming; sirve como alta disponibilidad (ver [[BD2 - 11 Bases de datos distribuidas NoSQL y teorema CAP]]).

Métricas: **RPO** (cuántos datos se pueden perder) y **RTO** (cuánto se tarda en volver a operar). Regla 3-2-1: 3 copias, 2 medios, 1 fuera del sitio.

```bash
pg_dump -h localhost -p 5433 -U dwh_admin -Fc dwh_atenciones > dwh.dump
pg_restore -d dwh_nuevo dwh.dump
```
(El proyecto del DWH corre PostgreSQL 17 en Docker en el puerto 5433; ver [[BD2 - 07 DWH Atenciones DDL y modelo estrella]].)

## Errores comunes
- Nunca probar la restauración: un respaldo no verificado no es un respaldo.
- Confundir replicación con respaldo (un `DROP` se replica).
- Desactivar `fsync` por rendimiento.
- No monitorear el crecimiento de `pg_wal` cuando falla el archivado.

## Ejercicios propuestos
1. ¿Por qué steal necesita UNDO y no-force necesita REDO? *Resp.: steal deja cambios no confirmados en disco; no-force puede dejar confirmados sin escribir.*
2. Calcule RPO si se hace respaldo nocturno sin archivado de WAL. *Resp.: hasta 24 h.*
3. ¿Qué se necesita para PITR? *Resp.: respaldo base más WAL archivado continuo.*

## Conexiones
[[BD2 - 03 Transacciones ACID y control de concurrencia]], [[Administración de Base de Datos]], [[Sistemas Operativos]] (sistemas de archivos y caché).

## Fuente
Conocimiento general (ARIES, documentación de PostgreSQL). Material del proyecto: puerto y versión de `README.md`.
