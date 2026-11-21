---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: conocimiento general; parcial 1 (API REST del blog)
---
# Comunicaciones II - 06 Capa de aplicación HTTP DNS correo FTP

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 05 Capa de red IP y enrutamiento]]
Siguiente: [[Comunicaciones II - 07 Contenedores Docker y arquitectura cliente-servidor]]

## Contexto y objetivo
La capa de aplicación define protocolos que usan directamente las aplicaciones. Se estudian HTTP/REST, DNS, correo, FTP/SFTP y DHCP, con arquitecturas cliente-servidor y P2P. También se conecta con [[Desarrollo de Aplicaciones Web]].

## Arquitecturas
- **Cliente-servidor**: servidor siempre activo con dirección fija; clientes inician. Escala con balanceadores y réplicas.
- **P2P**: pares actúan como cliente y servidor (BitTorrent). Autoescalable, difícil de gestionar.
- Un proceso se identifica con IP + puerto; la aplicación elige el transporte: HTTP/SMTP/FTP sobre TCP, DNS y DHCP sobre UDP (DNS usa TCP para respuestas grandes).

## HTTP
Protocolo de texto de petición-respuesta (sin estado).
```
GET /api/posts HTTP/1.1
Host: localhost:3000
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 87
```
- **Métodos**: GET (leer, seguro e idempotente), POST (crear), PUT (reemplazar, idempotente), PATCH, DELETE (idempotente).
- **Códigos**: 2xx éxito (200, 201, 204), 3xx redirección (301, 304), 4xx error del cliente (400, 401, 403, 404), 5xx error del servidor (500, 503).
- Versiones: HTTP/1.0 (conexión por objeto), 1.1 (persistente, *pipelining*), 2 (binario, multiplexado en una conexión), 3 (sobre QUIC/UDP).
- **Cookies** y sesiones añaden estado; **caché** con `ETag`/`If-None-Match` y `Cache-Control`.
- **HTTPS** = HTTP sobre TLS (puerto 443).

### REST
Estilo arquitectónico de recursos con URL, verbos HTTP y representaciones (JSON). Ejemplo del blog (parcial 1): `GET /api/posts` lista, `GET /api/posts/:id` obtiene una, `POST /api/posts` crea, `PUT /api/posts/:id` actualiza, `DELETE /api/posts/:id` elimina, `GET /health` estado.

## DNS
Sistema jerárquico distribuido que traduce nombres a IP. Jerarquía: raíz (.), TLD (.ve, .com), dominios autoritativos (unet.edu.ve).
- **Resolución recursiva**: el resolvedor local consulta raíz -> TLD -> autoritativo y guarda en caché según el **TTL**.
- Registros: **A** (IPv4), **AAAA** (IPv6), **CNAME** (alias), **MX** (correo, con prioridad), **NS** (servidores de nombres), **TXT** (SPF, verificaciones), **PTR** (inversa), **SOA**.
- Puerto 53 UDP/TCP. Riesgos: envenenamiento de caché, amplificación DDoS; mitigación: DNSSEC, DoT/DoH.
- Ejemplo: `dig unet.edu.ve MX` devuelve los servidores de correo del dominio.

## Correo electrónico
- **SMTP** (25/587): envío entre servidores y desde clientes (push). Comandos: HELO/EHLO, MAIL FROM, RCPT TO, DATA, QUIT.
- **POP3** (110) y **IMAP** (143): recuperación por el usuario. IMAP mantiene los mensajes en el servidor.
- Seguridad: STARTTLS, SPF, DKIM y DMARC contra suplantación.

## FTP y SFTP
- **FTP** (21 control, 20/efímero datos): dos conexiones; control en **texto plano** (credenciales visibles, ver informe OSINT). Modos activo y pasivo.
- **SFTP**: transferencia sobre SSH (22), cifrada. No confundir con FTPS (FTP sobre TLS).
- El proyecto [[SFTP-U Protocolo sobre UDP]] es un protocolo *propio* inspirado en estas ideas (LIST, GET, PUT, STAT) sobre UDP, no el SFTP estándar.

## DHCP y otros
DHCP (UDP 67/68), NTP (123, sincronización de tiempo), SSH (22), SNMP (161, gestión: v1/v2c con *community* en claro, v3 con autenticación y cifrado), RTP/RTSP (streaming).

## Programación con sockets TCP (esqueleto)
```python
import socket
srv = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
srv.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
srv.bind(("0.0.0.0", 8000)); srv.listen()
conn, addr = srv.accept()          # un socket por cliente
data = conn.recv(4096)             # recv puede devolver menos de lo enviado
conn.sendall(b"HTTP/1.1 200 OK\r\nContent-Length: 2\r\n\r\nok")
conn.close()
```

## Errores comunes
- Confundir método seguro con idempotente (POST no es idempotente).
- Asumir que un `recv` devuelve un mensaje completo.
- Dejar FTP/Telnet/SNMPv1 en producción: credenciales en claro.
- Olvidar el TTL de DNS al planear migraciones.

## Ejercicios propuestos
1. ¿Qué código HTTP devuelve crear un recurso con éxito? *Resp.: 201 Created.*
2. Un registro A con TTL 3600: ¿cuánto tarda en propagarse un cambio? *Resp.: hasta 1 h en cachés ya poblados.*
3. ¿Por qué DNS usa UDP? *Resp.: consulta/respuesta corta, sin overhead de conexión; TCP para respuestas grandes.*

## Conexiones
Transporte: [[Comunicaciones II - 02 Capa de transporte y UDP]], [[Comunicaciones II - 03 TCP conexión flujo y congestión]]. Despliegue de la API: [[Comunicaciones II - 07 Contenedores Docker y arquitectura cliente-servidor]]. Sistemas distribuidos: [[Sistemas Distribuidos]].

## Fuente
Conocimiento general (Kurose-Ross cap. 2; RFC 9110, 1035, 5321) y `~/Documentos/UNET/Comunicaciones 2/parcial 1/README.md` para la API del blog.
