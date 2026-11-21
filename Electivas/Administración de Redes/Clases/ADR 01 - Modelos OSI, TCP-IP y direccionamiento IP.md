---
tags: [clase, electiva]
materia: Administración de Redes
fuente: "conocimiento general"
---
# ADR 01 - Modelos OSI, TCP-IP y direccionamiento IP

Materia: [[Administración de Redes]]
Anterior: (inicio de la serie)
Siguiente: [[ADR 02 - Subredes, VLSM y VLAN]]

## Contexto y objetivo
Administrar una red exige un vocabulario común: capas, protocolos y direcciones. Objetivo: ubicar cada protocolo en su capa, leer y escribir direcciones IPv4 e IPv6, y usar los comandos básicos de diagnóstico en Linux.

## Teoría

### Modelos de capas
| OSI | TCP/IP | Unidad | Ejemplos |
|---|---|---|---|
| 7 Aplicación, 6 Presentación, 5 Sesión | Aplicación | Mensaje | HTTP, DNS, SMTP, SSH |
| 4 Transporte | Transporte | Segmento/datagrama | TCP, UDP |
| 3 Red | Internet | Paquete | IP, ICMP, OSPF |
| 2 Enlace | Acceso a red | Trama | Ethernet, Wi-Fi, ARP, VLAN 802.1Q |
| 1 Física | | Bit | Cables, fibra, radio |

Encapsulamiento: cada capa agrega su cabecera al bajar y la retira al subir.

### IPv4
Dirección de 32 bits en notación decimal con puntos. Se divide en red y host mediante la **máscara** o prefijo CIDR (`/24` = 255.255.255.0). Rangos privados (RFC 1918): 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16. Especiales: 127.0.0.0/8 (loopback), 169.254.0.0/16 (APIPA), 224.0.0.0/4 (multicast). Con $n$ bits de host:
$$\text{direcciones} = 2^{n},\qquad \text{hosts utilizables} = 2^{n}-2$$
(se descuentan la dirección de red y la de difusión).

### IPv6
128 bits en hexadecimal (ocho grupos de 16 bits). Se abrevia omitiendo ceros a la izquierda y una sola secuencia de grupos nulos con `::`. Tipos: unicast global (2000::/3), enlace local (fe80::/10), único local (fc00::/7), multicast (ff00::/8). Prefijo típico de subred: /64. Autoconfiguración SLAAC y NDP sustituyen a ARP; no hay difusión.

### Transporte
TCP: orientado a conexión, confiable, control de flujo y congestión (saludo de tres vías SYN, SYN-ACK, ACK). UDP: sin conexión, bajo costo (DNS, VoIP). Puertos: 22 SSH, 53 DNS, 80 HTTP, 443 HTTPS, 25 SMTP, 67/68 DHCP.

## Ejemplo resuelto
Dada la dirección 192.168.10.77/26, hallar red, difusión, rango y hosts.

1. /26 deja 6 bits de host: $2^6 = 64$ direcciones por subred; máscara 255.255.255.192.
2. Salto en el último octeto: 64. Subredes: .0, .64, .128, .192.
3. 77 cae en el bloque .64: red 192.168.10.64.
4. Difusión: 64 + 63 = 192.168.10.127.
5. Rango utilizable: 192.168.10.65 a 192.168.10.126.
6. Hosts: $2^6-2 = 62$.

Con binario: 77 = 01001101; máscara 192 = 11000000; AND = 01000000 = 64. Se verifica igual.

IPv6: `2001:0db8:0000:0000:0000:ff00:0042:8329` se abrevia `2001:db8::ff00:42:8329`.

Comandos en Linux:
```bash
ip addr                      # direcciones de interfaces
ip -6 addr
ip route                     # tabla de rutas, puerta de enlace
ip neigh                     # caché ARP / NDP
ping -c 4 192.168.10.1       # ICMP echo
traceroute -n 8.8.8.8        # ruta salto a salto (o tracepath)
ss -tulpn                    # puertos en escucha y procesos
ipcalc 192.168.10.77/26      # cálculo rápido (si está instalado)
```
Cálculo programable (Python, módulo estándar):
```python
import ipaddress
r = ipaddress.ip_interface("192.168.10.77/26").network
print(r, r.broadcast_address, r.num_addresses - 2)
# 192.168.10.64/26 192.168.10.127 62
print(ipaddress.ip_address("2001:db8::1").exploded)
```

## Errores comunes
- Olvidar restar red y difusión al contar hosts.
- Confundir máscara con wildcard (inversa, usada en OSPF y ACL de Cisco).
- Usar `::` más de una vez en una dirección IPv6.
- Suponer que ping fallido implica host caído (un cortafuegos puede bloquear ICMP).
- Mezclar direcciones privadas entre sitios que se van a interconectar.

## Ejercicios propuestos
1. ¿Cuántos hosts admite un /27? *Respuesta: 30.*
2. Red y difusión de 10.4.17.200/20. *Respuesta: red 10.4.16.0, difusión 10.4.31.255.*
3. Abrevia `fe80:0000:0000:0000:0202:b3ff:fe1e:8329`. *Respuesta: `fe80::202:b3ff:fe1e:8329`.*

## Conexiones
[[Comunicaciones I]] y [[Comunicaciones II]] (capas, protocolos), [[Sistemas Operativos]] (pila de red y sockets), [[Introducción a las Telecomunicaciones]] (capa física), [[Sistemas Distribuidos]] (TCP/UDP en servicios).

## Fuente
Conocimiento general: Tanenbaum y Wetherall; Kurose y Ross; RFC 791, 4291, 1918.
