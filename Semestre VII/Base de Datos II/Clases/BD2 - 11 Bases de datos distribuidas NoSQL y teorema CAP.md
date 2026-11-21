---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: conocimiento general
---
# BD2 - 11 Bases de datos distribuidas, NoSQL y teorema CAP

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 10 Consultas analiticas vistas y control de calidad]]

## Contexto y objetivo
Cuando los datos o la carga superan un solo servidor, se **distribuyen**. Esta nota presenta fragmentación, replicación, consistencia y los modelos NoSQL. El alcance exacto en el programa de la UNET debe verificarse con el programa oficial.

## Fragmentación (sharding/particionamiento)
- **Horizontal**: subconjuntos de filas (por rango, hash o lista). Ej. clientes por región.
- **Vertical**: subconjuntos de columnas (separar datos pesados).
- **Mixta**.
Reglas: completitud (todo dato en algún fragmento), reconstrucción (unión/join recompone la relación) y disyunción (horizontal).
Particionamiento por **hash** reparte uniforme pero rompe consultas por rango; por **rango** favorece rangos pero puede crear puntos calientes. **Hashing consistente** minimiza la reubicación al añadir nodos.

## Replicación
- **Maestro-réplica** (primary-standby): escrituras en un nodo, lecturas en réplicas; síncrona (sin pérdida, mayor latencia) o asíncrona (rápida, posible pérdida y **retraso de réplica**).
- **Multi-maestro**: escrituras en varios nodos; requiere resolución de conflictos (último gana, CRDT).
- **Quórum**: con $N$ réplicas, lecturas de $R$ y escrituras de $W$ nodos, hay consistencia fuerte si $R+W>N$.

## Transacciones distribuidas
**Commit en dos fases (2PC)**: (1) *prepare*: el coordinador pregunta, cada participante vota sí/no y persiste; (2) *commit* si todos dijeron sí, si no *abort*. Problema: bloqueante si cae el coordinador. **3PC** y **Paxos/Raft** mitigan. Alternativa en microservicios: patrón **Saga** (compensaciones). Ver [[Sistemas Distribuidos]].

## Teorema CAP (Brewer)
Un sistema distribuido solo puede garantizar dos de tres: **C**onsistencia (todos ven el mismo dato), **A**disponibilidad (toda petición recibe respuesta), tolerancia a **P**articiones de red. Como las particiones ocurren, la elección real es **CP** (rechaza peticiones para no divergir: HBase, MongoDB por defecto, ZooKeeper) o **AP** (responde con datos posiblemente viejos: Cassandra, DynamoDB). **PACELC**: además, sin partición, se elige entre latencia y consistencia.

**ACID vs BASE**: BASE = *Basically Available, Soft state, Eventually consistent*. **Consistencia eventual**: si cesan las escrituras, las réplicas convergen.

## Modelos NoSQL
| Modelo | Ejemplo | Uso |
|---|---|---|
| Clave-valor | Redis, DynamoDB | caché, sesiones |
| Documento | MongoDB | datos semiestructurados (JSON) |
| Columnar ancho | Cassandra, HBase | series de tiempo, alto volumen de escritura |
| Grafo | Neo4j | relaciones (redes sociales, recomendaciones) |
| Columnar analítico | ClickHouse, Redshift | OLAP (ver [[BD2 - 06 Data Warehouse OLAP y modelado dimensional]]) |
PostgreSQL también soporta `JSONB` (híbrido relacional-documento).

## Ejemplo resuelto: elegir quórum
$N=3$. Con $W=2,R=2$: $R+W=4>3$, lectura siempre ve la última escritura confirmada. Con $W=1,R=1$: $2\le3$, puede leerse una réplica atrasada (más rápido, consistencia eventual). Tolera la caída de 1 nodo en el primer caso.

## Errores comunes
- Pensar que NoSQL significa "sin transacciones" o que reemplaza siempre a SQL.
- Elegir shard key con baja cardinalidad (puntos calientes).
- Confundir replicación con respaldo ([[BD2 - 04 Recuperacion WAL y respaldo]]).
- Creer que CAP aplica "cuando todo funciona": solo describe el comportamiento ante partición.

## Ejercicios propuestos
1. Clasifique Cassandra en CAP. *Resp.: AP con consistencia ajustable.*
2. ¿Qué pasa en 2PC si el coordinador cae tras el prepare? *Resp.: los participantes quedan bloqueados.*
3. Elija modelo para un catálogo con atributos variables. *Resp.: documento.*

## Conexiones
[[Sistemas Distribuidos]], [[Administración de Base de Datos]], [[BD2 - 03 Transacciones ACID y control de concurrencia]].

## Fuente
Conocimiento general (Brewer, Kleppmann, Silberschatz).
