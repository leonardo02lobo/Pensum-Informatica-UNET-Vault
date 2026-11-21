---
tags: [materia, semestre-VII]
semestre: VII
---
# Comunicaciones II

**Semestre:** [[Semestre VII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Comunicaciones I]]

## Desbloquea
- [[Sistemas Distribuidos]]

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Comunicaciones 2`

## Apuntes

### Descripción general y objetivos
Comunicaciones II profundiza sobre [[Comunicaciones I]]: la **pila TCP/IP desde la capa de transporte hasta la de aplicación**, diseño de protocolos, servicios de red, seguridad básica y despliegue de aplicaciones en contenedores. Es prerrequisito de [[Sistemas Distribuidos]]. Contenido oficial exacto: verificar con el programa sinóptico UNET. Los trabajos guardados (parciales 1 a 3) sugieren tres ejes: **despliegue multi-contenedor con Docker**, **reconocimiento pasivo OSINT** y **diseño de un protocolo confiable sobre UDP** (ver [[SFTP-U Protocolo sobre UDP]]).

### Contenido programático (orientativo)
1. **Capa de transporte**: multiplexación por puertos, UDP, TCP (establecimiento de conexión de tres vías, control de flujo con ventana, control de congestión: slow start, AIMD), sockets.
2. **Confiabilidad**: ARQ (Stop-and-Wait, Go-Back-N, Selective Repeat), temporizadores, checksum/CRC.
3. **Capa de aplicación**: HTTP/HTTPS, DNS, correo (SMTP/IMAP), FTP/SFTP, DHCP; REST y APIs.
4. **Arquitecturas cliente/servidor y contenedores**: Docker, Docker Compose, redes y volúmenes, proxys inversos (Nginx).
5. **Seguridad en redes**: criptografía básica, TLS, firewalls, OSINT y reconocimiento pasivo, ética y alcance.
6. **Diseño de protocolos**: formato de mensajes, máquina de estados, tolerancia a pérdida, duplicación, reordenamiento y corrupción.

### Conceptos clave
- **Socket**: extremo de comunicación (IP, puerto, protocolo).
- **Handshake TCP**: SYN, SYN-ACK, ACK.
- **Ventana deslizante**: cantidad de segmentos en vuelo sin ACK; **Go-Back-N** retransmite desde el primer no confirmado.
- **RTT y RTO**: tiempo de ida y vuelta; temporizador de retransmisión (retroceso exponencial al fallar).
- **CRC32 / SHA-256**: detección de errores por trama / integridad de archivo completo.
- **Google Hacking (dorks)**: operadores `site:`, `filetype:`, `inurl:`, `intitle:` para reconocimiento pasivo.
- **Contenedor**: proceso aislado con su propio sistema de archivos y red, ligero frente a una VM.

### Fórmulas y código de ejemplo
Eficiencia de Stop-and-Wait: U = (L/R) / (RTT + L/R). Con ventana N: U = N·(L/R) / (RTT + L/R).
Temporizador adaptativo: EstimatedRTT = (1-α)·EstimatedRTT + α·SampleRTT, α = 0.125; RTO = EstimatedRTT + 4·DevRTT.

```yaml
# docker-compose.yml (blog de 3 servicios)
services:
  database: { image: postgres:16, volumes: [pgdata:/var/lib/postgresql/data] }
  backend:  { build: ./backend,  ports: ["3000:3000"], depends_on: [database] }
  frontend: { build: ./frontend, ports: ["8080:80"],   depends_on: [backend] }
volumes: { pgdata: {} }
```

```python
# Envío UDP con ACK y reintentos (esqueleto Stop-and-Wait)
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM); s.settimeout(0.5)
for intento in range(5):
    s.sendto(paquete, destino)
    try:
        ack, _ = s.recvfrom(1024)
        if ack == esperado: break
    except socket.timeout:
        continue  # retransmitir
```

### Ejemplo resuelto breve
Enlace de 1 Mbps, RTT = 40 ms, paquete de 1000 bytes. L/R = 8000/10^6 = 8 ms. Stop-and-Wait: U = 8/(40+8) = 16.7%. Con ventana N = 6: U = 48/48 = 100%. Es decir, hacen falta ~6 paquetes en vuelo para llenar la tubería.

### Cómo se relaciona con otras materias
[[Comunicaciones I]] (modelo en capas, enlace y red), [[Introducción a las Telecomunicaciones]], [[Sistemas Operativos]] (sockets, procesos), [[Administración de Redes]] y [[Desarrollo de Aplicaciones Web]]; habilita [[Sistemas Distribuidos]].

### Evaluación y consejos de estudio
Los materiales muestran evaluación por **proyectos prácticos** (parcial 1: despliegue Docker; parcial 2: informe OSINT pasivo; parcial 3: protocolo sobre UDP con fases de línea base, adversidad y robustecimiento). Verificar ponderaciones oficiales. Consejos: capture tráfico con Wireshark/tshark, pruebe con pérdida simulada (`tc netem`), documente alcance ético en toda auditoría.

### Bibliografía
- Kurose y Ross. *Redes de computadoras: un enfoque descendente*.
- Tanenbaum y Wetherall. *Redes de computadoras*.
- Stevens, W. R. *TCP/IP Illustrated*.
- RFC 768 (UDP), RFC 793/9293 (TCP), documentación de Docker.

### Recursos (fuera del vault)
`~/Documentos/UNET/Comunicaciones 2`: `parcial 1/` (blog Astro + Express + PostgreSQL en Docker Compose, `start.sh`/`stop.sh`), `parcial 2/` (informe OSINT sobre `unet.edu.ve` en .md/.pdf/.html con capturas censuradas), `parcial 3/` (protocolo SFTP-U v1/v2), `markitdown/`. No hay `Material/` en el vault.
