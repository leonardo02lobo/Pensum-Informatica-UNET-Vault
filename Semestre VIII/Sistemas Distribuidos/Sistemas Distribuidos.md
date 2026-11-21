---
tags: [materia, semestre-VIII]
semestre: VIII
---
# Sistemas Distribuidos

**Semestre:** [[Semestre VIII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Comunicaciones II]]

## Desbloquea
- [[Ingeniería de Software]]

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Sistema Distribuidos`

## Apuntes

### Descripción general y objetivos
Sistemas Distribuidos (prof. Dahyana Nimo en el material de 2012-1) estudia sistemas formados por **computadores autónomos conectados por una red que se presentan al usuario como un sistema coherente**. Cubre modelos, gestión de procesos, comunicación entre procesos, sincronización y tolerancia a fallos. Prerrequisito: [[Comunicaciones II]]; desbloquea [[Ingeniería de Software]]. Programa oficial: verificar con la UNET. Detalle en [[Sincronización y Tolerancia a Fallos en SD]].

### Contenido programático (según las clases del material)
- **Clase 1: Introducción**: motivación, tipos de sistemas, definición, perspectivas; ventajas (escalabilidad, disponibilidad, compartición de recursos) y desafíos (transparencia, heterogeneidad, fallos parciales).
- **Clase 2: Modelos**: multiprocesadores (MIMD, memoria compartida vs distribuida, simétrico/asimétrico), **cliente/servidor** (tareas repartidas entre proveedores y demandantes), **peer-to-peer** (elementos y arquitecturas), **SOA y servicios web** (modelo de referencia OASIS, reutilización de componentes).
- **Clase 3: Gerencia de procesos y comunicación**: organización de procesadores (pila, grupo de procesadores), asignación y migración de procesos, hilos; paso de mensajes, RPC, sockets, comunicación en grupo.
- **Clase 4: Sincronización y tolerancia a fallos**: relojes físicos y lógicos, exclusión mutua distribuida, elección de líder, transacciones, replicación, consenso, programas distribuidos tolerantes a fallos.

### Conceptos clave
- **Transparencia**: acceso, ubicación, migración, replicación, concurrencia, fallos.
- **Fallo parcial**: un nodo o enlace falla mientras el resto funciona.
- **RPC**: llamada a procedimiento remoto con *stubs* y serialización.
- **Reloj lógico de Lamport**: a→b implica L(a) < L(b).
- **Reloj vectorial**: detecta causalidad y concurrencia.
- **Teorema CAP**: no se garantizan a la vez consistencia, disponibilidad y tolerancia a particiones.
- **Consenso**: acuerdo de nodos sobre un valor (Paxos, Raft).
- **Ley de Amdahl**: S = 1/((1−p) + p/n).

### Algoritmos y código
```
Lamport:  al enviar, L = L + 1 y adjuntar L.
          al recibir m con sello Lm: L = max(L, Lm) + 1.
Ricart-Agrawala (exclusión mutua): enviar REQUEST(t,i) a todos;
          entrar en la sección crítica al recibir REPLY de los N-1 nodos;
          diferir respuestas si se está en la sección o se tiene prioridad.
Bully (elección): el nodo que detecta fallo envía ELECTION a mayores ID;
          si nadie responde, se proclama COORDINATOR.
```
```python
import socket, json
# Cliente RPC mínimo con sockets y JSON
def llamar(host, metodo, *args):
    with socket.create_connection((host, 9000)) as s:
        s.sendall(json.dumps({"m": metodo, "a": args}).encode())
        return json.loads(s.recv(4096))["r"]
```

### Ejemplo resuelto breve
Aceleración: programa con 80 % paralelizable en 8 nodos: S = 1/(0,2 + 0,8/8) = 3,33. Con infinitos nodos el límite es 5.
Relojes de Lamport: P1 envía m con L=3; P2 tiene L=1; al recibir fija L = max(1,3)+1 = 4.

### Cómo se relaciona con otras materias
[[Comunicaciones II]] (sockets, TCP/UDP), [[Sistemas Operativos]] (procesos, hilos, sincronización), [[Base de Datos II]] (transacciones y replicación), [[Estructura de Datos]], [[Administración de Redes]]; alimenta [[Ingeniería de Software]] (arquitecturas, microservicios) y [[Desarrollo de Aplicaciones Web]].

### Evaluación y consejos
El material corresponde al primer parcial (P1) de clases 1 a 4; verificar ponderaciones con el programa oficial. Consejos: dibuje diagramas de tiempo para los algoritmos, practique relojes lógicos y exclusión mutua a mano, y construya un pequeño servicio replicado para sentir los fallos parciales.

### Bibliografía recomendada
- Tanenbaum, A. y Van Steen, M. *Sistemas Distribuidos: principios y paradigmas*.
- Coulouris, Dollimore, Kindberg. *Sistemas Distribuidos: conceptos y diseño*.
- Kleppmann, M. *Designing Data-Intensive Applications*.
- Lamport, L. (1978). *Time, Clocks, and the Ordering of Events*.

### Recursos (fuera del vault)
`~/Documentos/UNET/Sistema Distribuidos/P1`: Clase 1 (`Clase 1.pdf`, `Clase 1 Complemento.pdf`), Clase 2 (`Clase 2.pdf`, `CS.pdf`, `P2P.pdf`, `Soa_WS.pdf`, `Multiprocesador.pdf`), Clase 3 (`GerenciaProcesos.pdf`, `ComunicacionProcesos.pdf`), Clase 4 (`Sincronizacion.pdf`, `Tolerancia.pdf`). No hay `Material/` en el vault.
