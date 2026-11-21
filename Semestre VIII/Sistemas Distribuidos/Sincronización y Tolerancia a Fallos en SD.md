---
tags: [tema, semestre-VIII]
semestre: VIII
---
# Sincronización y Tolerancia a Fallos en SD

Nota hija de [[Sistemas Distribuidos]] (Clase 4 del material).

## Sincronización
- **Relojes físicos**: deriva y sincronización (Cristian, Berkeley, NTP).
- **Relojes lógicos**: Lamport (orden parcial causal) y vectoriales (distinguen causalidad de concurrencia).
- **Exclusión mutua distribuida**: centralizada (coordinador), Ricart-Agrawala (2(N−1) mensajes), anillo con testigo.
- **Elección de coordinador**: algoritmos Bully y de anillo.
- **Transacciones distribuidas**: compromiso en dos fases (2PC): votación y decisión; bloqueo si cae el coordinador; 3PC y consenso como alternativas.

## Tolerancia a fallos
- Tipos: parada (*crash*), omisión, temporización, arbitrarios (bizantinos).
- Técnicas: **redundancia** (información, tiempo, física), replicación activa y pasiva, *checkpointing* y recuperación, detección de fallos con *heartbeats*.
- **Consenso** con tolerancia a f fallos: n ≥ 2f+1 (parada) o n ≥ 3f+1 (bizantinos); Paxos y Raft.
- Disponibilidad: A = MTBF/(MTBF + MTTR). En paralelo: A = 1 − Π(1 − Aᵢ).

## Ejemplo
Tres réplicas con A = 0,99 cada una: A_sistema = 1 − 0,01³ = 0,999999.

Ver también [[Base de Datos II]] y [[Sistemas Operativos]].
