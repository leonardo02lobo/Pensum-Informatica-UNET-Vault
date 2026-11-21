---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 3/ComunicacionProcesos.pdf y Clase 1 Complemento.pdf (§1.6)
---
# Sistemas Distribuidos - 08 Comunicación entre procesos

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 07 Gerencia de procesos y asignación de procesadores]]
Siguiente: [[Sistemas Distribuidos - 09 RPC y RMI]]

## Contexto y objetivo
Sin memoria compartida, todo en un SD depende de **intercambiar mensajes**. La clase (diapositivas "Comunicación entre procesos") presenta el protocolo solicitud/respuesta, el direccionamiento, y las políticas de transferencia de mensajes (bloqueo, buffer, confiabilidad). El complemento de Lafuente añade los modelos de comunicación. Se menciona también la comunicación de grupo.

## 1. Protocolo solicitud/respuesta
El SD se estructura como procesos que cooperan: **servidores** que ofrecen servicios y **clientes** que los usan. La interacción básica es sencilla y **sin conexión**:
1. El cliente envía un mensaje de **solicitud** (p. ej. leer un bloque de un archivo).
2. El servidor hace el trabajo y devuelve los datos o un código de error.
3. La **respuesta sirve como reconocimiento** de la solicitud: no se establece conexión.

Ventaja: la pila de protocolos es corta y eficiente (basta con las capas física, de enlace y la de solicitud/respuesta, evitando la sobrecarga de TCP).

### Paquetes del protocolo (tabla del material)
| Código | Tipo | De -> A | Significado |
|---|---|---|---|
| REQ | Solicitud | Cliente -> Servidor | El cliente desea servicio |
| REP | Respuesta | Servidor -> Cliente | Respuesta del servidor |
| ACK | Reconocimiento | cualquiera | El paquete anterior llegó |
| AYA | ¿Estás vivo? | Cliente -> Servidor | Comprueba si el servidor se cayó |
| IAA | Estoy vivo | Servidor -> Cliente | El servidor no se cayó |
| TA | Inténtalo de nuevo | Servidor -> Cliente | No hay espacio |
| AU | Dirección desconocida | Servidor -> Cliente | Ningún proceso usa esa dirección |

## 2. Direccionamiento
Para enviar, el cliente debe conocer la dirección del servidor. No sirve la dirección física de la máquina (solo habría un proceso por máquina). Tres esquemas:
1. **Machine.process** (`máquina.número`) incrustado en el código del cliente: simple pero no transparente; si la máquina falla, los programas ya compilados quedan con ese ID.
2. **Direcciones aleatorias con difusión (broadcast):** el proceso elige una dirección al azar y el emisor la localiza mediante un paquete de localización ("aquí estoy") a todos los núcleos de la LAN, que comprueban si la dirección es suya.
3. **Servidor de nombres:** el cliente consulta con un nombre ASCII y obtiene la dirección de la máquina; luego envía la solicitud directamente. Es el esquema escalable (como DNS).

## 3. Políticas de transferencia de mensajes
### a) Primitivas con bloqueo vs sin bloqueo
- **Con bloqueo (síncronas):** el emisor queda bloqueado hasta que el mensaje se envía/recibe; un proceso puede bloquearse "para siempre" si el otro no responde.
- **Sin bloqueo:** el control regresa de inmediato antes de enviar; el emisor **no puede reutilizar el buffer** hasta que el mensaje se haya enviado completo. Si no se almacena, no se sabe cuándo se envió.

### b) Primitivas con buffer vs sin buffer
- **Sin buffer:** si el receptor no está listo, el mensaje se pierde; el emisor puede reintentar y concluir erróneamente que el servidor cayó o que la dirección es incorrecta.
- **Con buffer:** el núcleo del receptor guarda los mensajes que llegan prematuramente en un **buzón (mailbox)**. El proceso pide al núcleo crear un buzón y especifica la dirección. En algunos sistemas no se deja enviar si no hay espacio en destino, por lo que el emisor se bloquea hasta recibir el reconocimiento.

### c) Primitivas confiables vs no confiables
- **No confiable:** sin garantía de entrega.
- **Confiable por mensaje:** el núcleo receptor devuelve un ACK por cada mensaje; recién entonces se libera al emisor.
- **Confiable por grupo (solicitud/respuesta):** la **respuesta funciona como ACK**; el emisor se bloquea hasta la respuesta; si tarda, el núcleo reenvía la solicitud (cubre la pérdida).

Los timeouts y reintentos introducen duplicados: el servidor debe ser **idempotente** o detectar repetidos.

## 4. Modelos de comunicación (Lafuente §1.6)
- **Paso de mensajes** (send/receive): nivel más bajo; el programador maneja mensajes explícitamente. Modos: síncrono/asíncrono, confiable/no, uno a uno o **en grupo** (multicast).
- **RPC** (llamada a procedimiento remoto) y **RMI** (invocación de métodos remotos): ocultan el mensaje tras una llamada a función/método (nota 09).
- **Memoria compartida distribuida (DSM):** abstrae un espacio de memoria común sobre memorias físicamente distribuidas.
- **Comunicación de grupo:** un mensaje a un conjunto de procesos (replicación, tolerancia a fallos). Plantea problemas de orden (FIFO, causal, total) y de atomicidad (todos o ninguno), vinculados con relojes lógicos (nota 10).

## 5. Ejemplo resuelto: petición con reintento
Cliente C envía REQ(leer bloque 7) al servidor S con temporizador de 200 ms.
1. REQ se pierde. A los 200 ms C reenvía REQ (mismo identificador).
2. S recibe, procesa y responde REP con datos; REP actúa como ACK.
3. Variante: REP se pierde. C reenvía REQ; S detecta el identificador repetido y reenvía la respuesta almacenada sin ejecutar de nuevo. Si en lugar de "leer bloque" fuera "descontar saldo", ejecutarla dos veces sería un error: por eso hace falta detectar duplicados (semántica *at-most-once*).
4. Si S tarda mucho, C puede enviar AYA; S contesta IAA para indicar que sigue vivo.

## Errores comunes
- Asumir que "sin conexión" significa "confiable".
- Reutilizar el buffer de envío antes de que la operación sin bloqueo termine.
- Reintentar operaciones no idempotentes sin identificadores de petición.

## Ejercicios propuestos
1. ¿Qué desventaja tiene la dirección `máquina.proceso`? *R: no es transparente; ata el programa a una máquina.*
2. ¿Por qué la respuesta puede actuar de ACK? *R: demuestra que el servidor recibió y procesó la solicitud.*
3. ¿Qué es un buzón? *R: estructura del núcleo receptor que almacena mensajes que llegan antes de que el proceso los pida.*

## Conexiones
[[Sistemas Distribuidos - 09 RPC y RMI]]; [[Comunicaciones II]] (UDP/TCP); [[Sistemas Operativos]] (IPC).

## Fuente
ComunicacionProcesos.pdf (956 palabras) y Complemento §1.6.
