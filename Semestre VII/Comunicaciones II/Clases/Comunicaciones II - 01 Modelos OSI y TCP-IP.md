---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: conocimiento general
---
# Comunicaciones II - 01 Modelos OSI y TCP-IP

Materia: [[Comunicaciones II]]
Siguiente: [[Comunicaciones II - 02 Capa de transporte y UDP]]

## Contexto y objetivo
Comunicaciones II comienza donde terminó [[Comunicaciones I]]: ya se conocen señales, medios y enlace; ahora se estudia cómo **procesos** en máquinas distintas intercambian datos de forma útil. Para ello se organiza la complejidad en **capas**. Esta nota fija el vocabulario (modelo OSI, modelo TCP/IP, encapsulación, PDU) que usan todas las demás notas de la materia. Contenido oficial exacto: verificar con el programa sinóptico de la UNET.

## Idea central: arquitectura en capas
Una **capa** ofrece un *servicio* a la capa superior usando los servicios de la inferior y comunicándose con su **par** (capa homóloga en el otro extremo) mediante un **protocolo**. Ventajas: modularidad, intercambiabilidad (HTTP funciona igual sobre Wi-Fi o fibra), interoperabilidad por estándares. Costo: duplicación de funciones y cabeceras (*overhead*).

### Modelo OSI (ISO/IEC 7498) de 7 capas
| N.º | Capa | PDU | Función | Ejemplos |
|---|---|---|---|---|
| 7 | Aplicación | Datos/mensaje | Servicios de red al usuario/aplicación | HTTP, DNS, SMTP |
| 6 | Presentación | Datos | Formato, compresión, cifrado | TLS (parcialmente), JSON, ASN.1 |
| 5 | Sesión | Datos | Diálogo, sincronización | RPC, NetBIOS |
| 4 | Transporte | Segmento/datagrama | Comunicación proceso a proceso, fiabilidad | TCP, UDP |
| 3 | Red | Paquete | Direccionamiento lógico y enrutamiento | IP, ICMP |
| 2 | Enlace | Trama | Acceso al medio, detección de errores | Ethernet, Wi-Fi |
| 1 | Física | Bit | Señales sobre el medio | Cables, radio |

### Modelo TCP/IP (4 capas, RFC 1122)
1. **Aplicación** (absorbe OSI 5-7).
2. **Transporte** (TCP, UDP, hoy también QUIC).
3. **Internet** (IP, ICMP, enrutamiento).
4. **Acceso a la red / Enlace** (OSI 1-2). Muchos textos separan física y enlace y hablan de 5 capas (Kurose-Ross).

OSI es un modelo de **referencia**; TCP/IP es la pila **implementada** en Internet. En la práctica se usa la numeración OSI para hablar ("un switch es de capa 2", "un firewall de capa 7").

## Encapsulación y desencapsulación
Al enviar, cada capa añade su cabecera (y a veces cola) al PDU recibido de arriba:

```
Datos de aplicación
[Cab. TCP | Datos]                      -> segmento
[Cab. IP  | Cab. TCP | Datos]           -> paquete
[Cab. Eth | Cab. IP | Cab. TCP | Datos | CRC]  -> trama
```
El receptor desencapsula en orden inverso. Cada capa solo interpreta *su* cabecera.

### Ejemplo con tamaños
Se envía un bloque de 1000 bytes por TCP sobre IPv4 y Ethernet, sin opciones:
- TCP: 20 B de cabecera, IP: 20 B, Ethernet: 14 B + 4 B de FCS = 18 B.
- Total en el cable: 1000 + 20 + 20 + 18 = 1058 B. Eficiencia = 1000/1058 ≈ 94.5 %.
- Si el dato fuera de 10 B: 10/68 ≈ 14.7 %. Por eso los mensajes pequeños son ineficientes.

## Direccionamiento por capa
- **Enlace**: dirección MAC (48 bits), alcance local.
- **Red**: dirección IP (32 bits IPv4 / 128 bits IPv6), alcance global.
- **Transporte**: número de **puerto** (16 bits), identifica el proceso.
- Un *socket* queda identificado por (IP, puerto, protocolo); una conexión TCP por la 4-tupla (IP origen, puerto origen, IP destino, puerto destino).

## Dónde viven los dispositivos
- Hub/repetidor: capa 1. Switch: capa 2 (aprende MAC por trama). Router: capa 3. Firewall de estado: capas 3-4; WAF/proxy: capa 7.
- Los *hosts* implementan las cinco/siete capas; los equipos intermedios solo las inferiores. Esto es el **principio extremo a extremo**: la fiabilidad se coloca en los extremos (TCP), la red solo hace "mejor esfuerzo".

## Servicios: orientados a conexión vs sin conexión
- **Orientado a conexión**: establece estado antes de enviar (TCP). Ofrece orden, fiabilidad, control de flujo/congestión.
- **Sin conexión**: cada datagrama es independiente (UDP, IP). Menor latencia y sobrecarga; la aplicación decide cómo manejar pérdidas (el caso del proyecto [[SFTP-U Protocolo sobre UDP]]).
- **Fiable vs no fiable** es una propiedad distinta: IP es sin conexión y no fiable; TCP es con conexión y fiable.

## Errores comunes
- Decir "TCP es de la capa de red" o confundir **segmento** (transporte) con **paquete** (red) con **trama** (enlace).
- Pensar que el puerto identifica a la máquina; la identifica la IP.
- Creer que OSI describe lo que está implementado; las capas 5 y 6 casi no existen como capas separadas en Internet.
- Olvidar que el enlace cambia en cada salto (MAC distinta) mientras que las IP origen/destino se mantienen (salvo NAT).

## Ejercicios propuestos
1. Una aplicación genera 1460 B; calcule el tamaño de la trama Ethernet (TCP/IPv4, sin opciones). *Resp.: 1460+20+20+18 = 1518 B.*
2. ¿En qué capa opera un switch administrable con VLAN? *Resp.: capa 2 (con funciones L3 si es "multicapa").*
3. Clasifique: DNS sobre UDP, ARP, ICMP, TLS. *Resp.: aplicación (sobre transporte), enlace/red, red, entre transporte y aplicación.*

## Conexiones
- Base física y de enlace: [[Comunicaciones I - 11 Modelos de capas y redes LAN]].
- Siguiente tema: [[Comunicaciones II - 02 Capa de transporte y UDP]].
- Aplicaciones prácticas en [[Administración de Redes]] e [[Introducción a las Telecomunicaciones]].

## Fuente
Conocimiento general (Kurose y Ross; Tanenbaum; RFC 1122). Sin documento específico en el material del estudiante.
