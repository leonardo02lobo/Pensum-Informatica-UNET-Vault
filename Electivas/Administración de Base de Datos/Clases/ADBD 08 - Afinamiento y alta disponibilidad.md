---
tags: [clase, electiva]
materia: Administración de Base de Datos
fuente: "conocimiento general; consultas de diagnóstico de ~/Documentos/UNET/administracion DB/COMANDOS_DBA_REFERENCIA.md"
---
# ADBD 08 - Afinamiento y alta disponibilidad

Materia: [[Administración de Base de Datos]]
Anterior: [[ADBD 07 - Respaldo y recuperación con RMAN]]
Siguiente: (fin de la serie)

## Contexto y objetivo
Una base de datos que funciona pero es lenta o cae es una base mala. Esta clase ve el método de afinamiento (medir, hallar el cuello de botella, corregir) y una introducción a la alta disponibilidad (Data Guard, RAC). Objetivo: leer un plan de ejecución, decidir un índice y entender qué protege cada tecnología de HA.

## Teoría

### Método
1. Definir el problema con una métrica (tiempo de respuesta, lecturas lógicas).
2. Localizar: sesiones (`v$session`), esperas (`wait_class`), SQL costoso (`v$sql`), informes AWR/ASH (requieren licencia Diagnostics Pack; en XE no disponibles, usar `v$` y `EXPLAIN PLAN`).
3. Corregir una cosa a la vez y volver a medir.

### El optimizador basado en costos
Elige el plan de menor costo estimado usando **estadísticas** (`DBMS_STATS`): número de filas, valores distintos, histogramas. Estadísticas obsoletas producen planes malos.

### Índices
- **B-tree**: igualdad y rangos; selectivo (pocas filas por valor). Una consulta que devuelve más del ~5-15 % de la tabla suele preferir `TABLE ACCESS FULL`.
- **Bitmap**: baja cardinalidad, DSS (no para OLTP concurrente).
- **Compuestos**: el orden de columnas importa (la primera debe estar en el predicado).
- **Función**: `CREATE INDEX ... (UPPER(nombre))`.
Costo: cada índice penaliza `INSERT/UPDATE/DELETE` y ocupa espacio (en el comedor, 63 % del volumen).

Selectividad: $$S = \frac{\text{valores distintos}}{\text{filas totales}}$$ Cuanto más cercana a 1, más útil el índice B-tree.

### Alta disponibilidad (introducción)
| Tecnología | Protege de | Idea |
|---|---|---|
| Multiplexar control files y redo | Pérdida de un archivo | Copias en discos distintos |
| Data Guard | Pérdida del sitio, error humano (con retardo) | Base *standby* que aplica el redo del primario |
| RAC | Caída de un nodo | Varias instancias sobre la misma base compartida |
| Respaldo + RMAN | Todo lo anterior, más lento | Ver ADBD 07 |
Data Guard: modos de protección Maximum Performance (asíncrono), Availability y Protection (síncrono). Switchover (planificado) y failover (falla).

## Ejemplo resuelto
Consulta lenta: consumos de un beneficiario.

```sql
-- 1. Plan antes de tocar nada
EXPLAIN PLAN FOR
  SELECT * FROM comedor.consumptions WHERE beneficiary_id = 4821;
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);
-- Se observa: TABLE ACCESS FULL CONSUMPTIONS (1,6 millones de filas)

-- 2. Estadísticas al día y selectividad
EXEC DBMS_STATS.GATHER_TABLE_STATS('COMEDOR','CONSUMPTIONS');
SELECT COUNT(DISTINCT beneficiary_id)/COUNT(*) AS selectividad
  FROM comedor.consumptions;          -- por ejemplo 0.02 (ver nota)

-- 3. Índice en el tablespace de índices
CREATE INDEX comedor.ix_cons_benef ON comedor.consumptions (beneficiary_id)
  TABLESPACE ts_comedor_idx;

-- 4. Nuevo plan
EXPLAIN PLAN FOR
  SELECT * FROM comedor.consumptions WHERE beneficiary_id = 4821;
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);
-- INDEX RANGE SCAN IX_CONS_BENEF + TABLE ACCESS BY INDEX ROWID
```
Paso a paso: (1) el plan con full scan sobre 1,6 M filas para recuperar pocas filas es la señal; (2) la selectividad global es baja pero la consulta por un `beneficiary_id` concreto devuelve pocas filas (aprox. filas/valores distintos), por lo que el índice sigue siendo efectivo; (3) el índice va en `TS_COMEDOR_IDX`; (4) se mide de nuevo. Nota: los números son ilustrativos del método, no medidos en el proyecto.

Diagnóstico de sesiones y bloqueos (de la referencia del estudiante):
```sql
SELECT sid, serial#, username, status, program FROM v$session;
SELECT blocking_session, sid, wait_class FROM v$session
 WHERE blocking_session IS NOT NULL;
SELECT sql_id, executions, ROUND(elapsed_time/1e6,2) seg
  FROM v$sql ORDER BY elapsed_time DESC FETCH FIRST 5 ROWS ONLY;
```
Alta disponibilidad, comprobaciones básicas:
```sql
SELECT name, value FROM v$parameter WHERE name IN ('log_archive_dest_1','db_recovery_file_dest');
SELECT database_role, protection_mode FROM v$database;   -- PRIMARY / STANDBY
```

## Errores comunes
- Indexar todo: degrada la escritura.
- Usar funciones sobre la columna indexada en el `WHERE` (`WHERE TRUNC(fecha)=...` anula el índice normal).
- Cambiar parámetros de instancia sin medir.
- Confundir Data Guard (réplica de la base) con RAC (varias instancias de una misma base: no protege contra pérdida de los datos).
- Creer que HA reemplaza el respaldo (un `DELETE` se replica).

## Ejercicios propuestos
1. ¿Qué indica `TABLE ACCESS FULL` en una consulta que devuelve 3 filas de 10 millones? *Respuesta: probable falta de índice o estadísticas desactualizadas.*
2. ¿Qué tecnología cubre la pérdida total del centro de datos? *Respuesta: Data Guard con standby remoto.*
3. ¿Por qué un índice B-tree no ayuda en una columna con dos valores distintos? *Respuesta: selectividad muy baja; leer casi toda la tabla por índice es más costoso que un full scan.*

## Conexiones
[[Base de Datos II]] (optimización de consultas, índices), [[Sistemas Distribuidos]] (replicación, tolerancia a fallos), [[Sistemas Operativos]] (E/S, memoria), [[Administración de Redes]] (latencia entre sitios para Data Guard).

## Fuente
Conocimiento general (Oracle Performance Tuning Guide, Data Guard Concepts); consultas de sesiones en `~/Documentos/UNET/administracion DB/COMANDOS_DBA_REFERENCIA.md`; cifras del comedor de `punto4_tablespaces.md`. Verificar con el programa oficial el alcance de Data Guard/RAC.
