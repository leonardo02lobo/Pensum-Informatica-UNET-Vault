---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: conocimiento general
---
# BD2 - 03 Transacciones, ACID y control de concurrencia

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 02 PL-pgSQL funciones procedimientos y triggers]]
Siguiente: [[BD2 - 04 Recuperacion WAL y respaldo]]

## Contexto y objetivo
Un SGBD atiende muchos usuarios a la vez. Sin control, dos operaciones simultáneas pueden corromper datos (saldos erróneos, reservas duplicadas). La teoría de transacciones garantiza corrección bajo concurrencia y fallos. Objetivo: entender ACID, anomalías, niveles de aislamiento, bloqueos, deadlock, MVCC y serializabilidad.

## Transacción y ACID
**Transacción**: secuencia de operaciones que forma una unidad lógica de trabajo. Se delimita con `BEGIN` ... `COMMIT` / `ROLLBACK`.
- **A**tomicidad: todo o nada (lo garantiza el registro de recuperación, ver [[BD2 - 04 Recuperacion WAL y respaldo]]).
- **C**onsistencia: lleva la BD de un estado válido a otro (restricciones, reglas).
- **A**islamiento (*Isolation*): el resultado equivale a ejecutarlas en serie.
- **D**urabilidad: lo confirmado sobrevive a caídas (WAL en disco).

Estados: activa, parcialmente confirmada, confirmada, fallida, abortada.

## Anomalías de concurrencia
1. **Lectura sucia** (*dirty read*): leer datos no confirmados de otra transacción.
2. **Lectura no repetible**: releer una fila y ver otro valor (otra transacción hizo `UPDATE` y confirmó).
3. **Fantasma**: repetir una consulta por rango y aparecen filas nuevas.
4. **Actualización perdida** (*lost update*): dos transacciones leen el mismo valor y ambas escriben, perdiéndose una.
5. **Anomalía de escritura sesgada** (*write skew*): dos transacciones leen datos solapados y actualizan filas distintas rompiendo una regla global (dos médicos de guardia se dan de baja a la vez).

## Niveles de aislamiento (estándar SQL)
| Nivel | Sucia | No repetible | Fantasma |
|---|---|---|---|
| Read Uncommitted | posible | posible | posible |
| Read Committed | no | posible | posible |
| Repeatable Read | no | no | posible (en el estándar) |
| Serializable | no | no | no |

En **PostgreSQL**: Read Uncommitted se comporta como Read Committed; Repeatable Read es *snapshot isolation* (no hay fantasmas, pero sí write skew); Serializable usa SSI (*Serializable Snapshot Isolation*) que detecta ciclos y aborta una transacción con error `40001` (la aplicación debe reintentar).
```sql
BEGIN ISOLATION LEVEL SERIALIZABLE;
UPDATE cuenta SET saldo = saldo - 100 WHERE id = 1;
UPDATE cuenta SET saldo = saldo + 100 WHERE id = 2;
COMMIT;
```

## MVCC (control de concurrencia multiversión)
Cada escritura crea una **nueva versión** de la fila; cada transacción ve una instantánea. Los lectores no bloquean a los escritores y viceversa. En PostgreSQL cada tupla tiene `xmin` (transacción creadora) y `xmax` (borradora); las versiones muertas se limpian con `VACUUM`. Costo: espacio extra y mantenimiento (*bloat*).

## Bloqueo en dos fases (2PL)
Protocolo: fase de **crecimiento** (se adquieren bloqueos, no se liberan) y de **decrecimiento** (se liberan, no se adquieren). Garantiza planificaciones serializables. **2PL estricto**: mantener bloqueos exclusivos hasta `COMMIT` (evita lecturas sucias y aborto en cascada).

Modos: compartido (S, lectura), exclusivo (X, escritura). Compatibilidad: S-S sí; S-X, X-X no. Bloqueos con intención (IS, IX) para jerarquías (tabla, página, fila). En SQL: `SELECT ... FOR UPDATE` (bloqueo de fila), `FOR SHARE`, `LOCK TABLE`.

## Deadlock (interbloqueo)
T1 bloquea A y pide B; T2 bloquea B y pide A: espera circular.
- **Detección**: grafo de espera; un ciclo indica deadlock; se aborta una víctima (PostgreSQL lo hace tras `deadlock_timeout`, 1 s por defecto).
- **Prevención**: ordenar adquisición de recursos; esquemas *wait-die* y *wound-wait* con marcas de tiempo.
- Buena práctica: acceder siempre a las tablas/filas en el mismo orden y mantener transacciones cortas.

## Serializabilidad
Una planificación (*schedule*) es **serializable** si equivale a alguna ejecución serie. **Seriabilidad por conflicto**: dos operaciones están en conflicto si son de transacciones distintas, sobre el mismo dato y al menos una es escritura. Se construye el **grafo de precedencia**: nodo por transacción, arco Ti→Tj si una operación de Ti en conflicto precede a la de Tj. Serializable por conflicto sii el grafo es **acíclico**.

### Ejemplo resuelto
Planificación: R1(A) W1(A) R2(A) W2(A) R1(B) W1(B) R2(B) W2(B).
Conflictos sobre A: W1(A) antes de R2(A) → T1→T2. Sobre B: W1(B) antes de R2(B) → T1→T2. Grafo: solo T1→T2, acíclico: equivalente a la serie T1,T2. Serializable.

Otra: R1(A) W2(A) W1(A). R1(A)→W2(A) da T1→T2; W2(A)→W1(A) da T2→T1: ciclo, **no** serializable (actualización perdida).

## Control optimista y por marcas de tiempo
**Timestamp ordering**: cada transacción recibe un sello; una operación fuera de orden provoca aborto. **Optimista (OCC)**: leer/calcular sin bloquear, validar al confirmar; bueno con pocos conflictos.

## Errores comunes
- Creer que `Read Committed` evita la lectura no repetible.
- No reintentar ante errores de serialización o deadlock.
- Mantener transacciones abiertas con interacción de usuario (bloquea `VACUUM`, retiene bloqueos).
- Hacer `SELECT` y luego `UPDATE` sin `FOR UPDATE` (condición de carrera "leer-modificar-escribir"); alternativa: `UPDATE ... SET saldo = saldo - 100`.

## Ejercicios propuestos
1. T1 y T2 leen saldo=500; T1 resta 100, T2 resta 50, ambas confirman. ¿Anomalía y saldo final posible? *Resp.: actualización perdida; 400 o 450 en lugar de 350.*
2. Dibuje el grafo de espera de T1(A,B) y T2(B,A). *Resp.: T1→T2 y T2→T1; ciclo.*
3. ¿Qué nivel evita fantasmas en PostgreSQL? *Resp.: Repeatable Read (snapshot) ya lo evita; Serializable además evita write skew.*

## Conexiones
La programación de procedimientos con `COMMIT` está en [[BD2 - 02 PL-pgSQL funciones procedimientos y triggers]]. Los conceptos de sección crítica de [[Sistemas Operativos]] y la exclusión mutua en [[Sistemas Distribuidos]] son análogos. La idempotencia del ETL ([[BD2 - 09 ETL carga inicial y carga diaria]]) evita duplicados bajo reintentos.

## Fuente
Conocimiento general (Silberschatz, Elmasri; documentación de PostgreSQL).
