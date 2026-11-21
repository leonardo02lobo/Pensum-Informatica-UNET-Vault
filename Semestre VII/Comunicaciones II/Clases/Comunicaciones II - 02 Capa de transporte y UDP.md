---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: conocimiento general; ejemplos de ~/Documentos/UNET/Comunicaciones 2/parcial 3
---
# Comunicaciones II - 02 Capa de transporte y UDP

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 01 Modelos OSI y TCP-IP]]
Siguiente: [[Comunicaciones II - 03 TCP conexión flujo y congestión]]

## Contexto y objetivo
La capa de red (IP) entrega paquetes **entre hosts** con "mejor esfuerzo". La capa de transporte extiende esa entrega a **entre procesos**. Objetivo: entender multiplexación por puertos, la API de sockets y el protocolo más simple, **UDP**, que además es la base del proyecto SFTP-U.

## Multiplexación y demultiplexación
- **Multiplexación** (emisor): reúne datos de varios sockets, añade cabecera con puerto origen/destino.
- **Demultiplexación** (receptor): usa los campos de la cabecera para dirigir cada segmento al socket correcto.
- UDP demultiplexa solo por **(IP destino, puerto destino)**: dos clientes distintos que escriben al mismo puerto llegan al mismo socket.
- TCP demultiplexa por la **4-tupla**: cada conexión tiene su propio socket en el servidor.
- Rangos de puertos: 0-1023 bien conocidos (80 HTTP, 443 HTTPS, 53 DNS, 22 SSH); 1024-49151 registrados; 49152-65535 efímeros.

## UDP (RFC 768)
Servicio mínimo: sin conexión, sin garantía de entrega, orden ni duplicados, pero **conserva límites de mensaje** (un `sendto` = un datagrama).

Cabecera de 8 bytes:
```
 0      15 16     31
+---------+---------+
| Puerto  | Puerto  |
| origen  | destino |
+---------+---------+
| Longitud| Checksum|
+---------+---------+
```
- **Longitud**: cabecera + datos (mín. 8, máx. 65 535 teórico; 65 507 B de datos sobre IPv4).
- **Checksum**: suma en complemento a uno de 16 bits sobre un *pseudo-encabezado* (IP origen, IP destino, protocolo 17, longitud), la cabecera y los datos. Opcional en IPv4, obligatorio en IPv6.

### Checksum de Internet: ejemplo
Palabras de 16 bits: 0x4500 y 0x0073. Suma = 0x4573 (sin acarreo). Complemento a uno: 0xBA8C. El receptor suma todo incluido el checksum y debe obtener 0xFFFF. Si hay acarreo fuera de 16 bits se suma de vuelta al bit menos significativo ("end-around carry").

### ¿Por qué usar UDP?
- Sin retraso de establecimiento de conexión; ideal para consultas de una sola ida y vuelta (DNS, DHCP).
- Sin estado en el servidor; atiende a muchos clientes con pocos recursos.
- Cabecera pequeña (8 B frente a 20 B de TCP).
- Control fino por la aplicación: streaming, VoIP, juegos, QUIC y protocolos propios como SFTP-U.
- Limitación: **no hay control de congestión**; una aplicación UDP agresiva puede saturar la red (debe implementar el suyo).

## Sockets en Python (UDP)
```python
import socket
# Servidor
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)   # SOCK_DGRAM = UDP
s.bind(("0.0.0.0", 9001))                               # asocia IP:puerto
datos, origen = s.recvfrom(2048)                        # bloquea hasta recibir un datagrama
s.sendto(b"eco:" + datos, origen)                       # responde al remitente

# Cliente
c = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
c.settimeout(0.5)                                       # evita bloqueo eterno ante pérdida
c.sendto(b"hola", ("127.0.0.1", 9001))
try:
    r, _ = c.recvfrom(2048)
except socket.timeout:
    r = None                                            # decidir: reintentar o abortar
```
Detalles: `recvfrom` con búfer menor que el datagrama **trunca** el sobrante; el cliente recibe un puerto efímero en el primer `sendto`.

## Tamaño de datagrama y fragmentación
La MTU de Ethernet es 1500 B. Un datagrama UDP de 4000 B se fragmenta en IP (3 fragmentos) y se pierde completo si se pierde un fragmento. Buena práctica: mantener datagramas ≤ ~1200-1400 B. SFTP-U usa un máximo de 536 B por datagrama (24 B de cabecera + 512 B de datos) para evitar fragmentación incluso con rutas de MTU reducida.

## Errores comunes
- Suponer que `sendto` exitoso significa entrega: solo significa que el SO aceptó el datagrama.
- No poner *timeout*: un datagrama perdido bloquea `recvfrom` para siempre.
- Asumir orden: datagramas pueden llegar desordenados o duplicados.
- Olvidar que el checksum UDP solo detecta (no corrige) errores y es débil; protocolos serios añaden CRC32 o hash (ver [[Comunicaciones II - 10 SFTP-U Diseno del protocolo y trama]]).

## Ejercicios propuestos
1. ¿Cuántos bytes de datos caben en un datagrama UDP sobre IPv4 sin fragmentar en Ethernet? *Resp.: 1500 - 20 - 8 = 1472 B.*
2. Dos clientes envían al puerto 5000 del servidor UDP. ¿Cuántos sockets necesita el servidor? *Resp.: uno.*
3. Calcule el checksum de 0x1234 y 0xF0F0. *Resp.: suma 0x10324 -> 0x0325; complemento 0xFCDA.*

## Conexiones
TCP agrega fiabilidad (siguiente nota); [[Comunicaciones II - 03 TCP conexión flujo y congestión]]. Sockets y procesos: [[Sistemas Operativos]]. Uso en RPC y mensajería: [[Sistemas Distribuidos]].

## Fuente
Conocimiento general (RFC 768, Kurose-Ross cap. 3). Fragmentos de código ilustrativos propios; el diseño de SFTP-U proviene de `~/Documentos/UNET/Comunicaciones 2/parcial 3/server/protocol.py`.
