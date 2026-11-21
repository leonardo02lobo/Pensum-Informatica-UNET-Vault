---
tags: [clase, electiva]
materia: Administración de Redes
fuente: "conocimiento general"
---
# ADR 04 - Servicios DNS y DHCP

Materia: [[Administración de Redes]]
Anterior: [[ADR 03 - Enrutamiento y NAT]]
Siguiente: [[ADR 05 - Servicios web, correo, proxy y directorio]]

## Contexto y objetivo
DHCP entrega configuración IP automáticamente y DNS traduce nombres a direcciones. Casi todo falla si alguno de los dos cae. Objetivo: configurar un servidor DHCP (dnsmasq/ISC) y DNS (BIND o dnsmasq) y diagnosticar con `dig`.

## Teoría

### DHCP
Proceso DORA sobre UDP 67 (servidor) y 68 (cliente): Discover (difusión), Offer, Request, Acknowledge. Entrega: dirección, máscara, puerta de enlace, DNS y **tiempo de concesión** (*lease*). Renovación a $T_1 = 50\,\%$ de la concesión y reenlace a $T_2 = 87{,}5\,\%$. Reservas por MAC; **relay** (`ip helper-address`) para atender varias subredes desde un servidor. Riesgo: servidores DHCP falsos (mitigación: *DHCP snooping*).

### DNS
Sistema jerárquico distribuido (raíz, TLD, dominio). Actores: **resolver recursivo**, servidores autoritativos, raíz. Consultas sobre UDP/TCP 53; DNSSEC añade firmas. Registros:
| Tipo | Contenido |
|---|---|
| A / AAAA | Nombre a IPv4 / IPv6 |
| CNAME | Alias |
| MX | Servidor de correo (con prioridad) |
| NS | Servidores de la zona |
| PTR | Inverso (IP a nombre) |
| TXT | Texto (SPF, DKIM, verificaciones) |
| SOA | Parámetros de la zona (serie, refresco, TTL negativo) |
Zonas y transferencia (AXFR/IXFR) entre primario y secundario; **TTL** controla el caché.

## Ejemplo resuelto
Red 192.168.20.0/24, dominio interno `lab.local`. Servidor 192.168.20.2.

1. DHCP + DNS ligero con dnsmasq (`/etc/dnsmasq.conf`):
```
interface=eth0
domain=lab.local
local=/lab.local/
dhcp-range=192.168.20.100,192.168.20.200,255.255.255.0,12h
dhcp-option=option:router,192.168.20.1
dhcp-option=option:dns-server,192.168.20.2
dhcp-host=aa:bb:cc:dd:ee:01,impresora,192.168.20.50
address=/web.lab.local/192.168.20.10
```
```bash
sudo systemctl restart dnsmasq
journalctl -u dnsmasq -f           # ver DORA en vivo
cat /var/lib/misc/dnsmasq.leases   # concesiones
```
2. Zona autoritativa en BIND9 (`/etc/bind/named.conf.local`):
```
zone "lab.local" {
    type master;
    file "/etc/bind/db.lab.local";
    allow-transfer { 192.168.20.3; };
};
```
Archivo de zona `/etc/bind/db.lab.local`:
```
$TTL 3600
@   IN SOA ns1.lab.local. admin.lab.local. (
        2026112001 ; serie AAAAMMDDnn
        3600 ; refresco
        900  ; reintento
        604800 ; expira
        300 )  ; TTL negativo
@       IN NS   ns1.lab.local.
@       IN MX 10 correo.lab.local.
ns1     IN A    192.168.20.2
web     IN A    192.168.20.10
correo  IN A    192.168.20.11
www     IN CNAME web
```
```bash
named-checkconf && named-checkzone lab.local /etc/bind/db.lab.local
sudo systemctl reload bind9
```
3. Diagnóstico con `dig`:
```bash
dig @192.168.20.2 web.lab.local A +short       # 192.168.20.10
dig @192.168.20.2 lab.local MX
dig -x 192.168.20.10                           # PTR (requiere zona inversa)
dig +trace example.org                         # recorrido desde la raíz
resolvectl status                              # DNS que usa el cliente
```
Cálculo: concesión de 12 h = 43.200 s; renovación a 6 h (21.600 s), reenlace a 10,5 h.

## Errores comunes
- Olvidar incrementar la serie SOA: los secundarios no se actualizan.
- Falta de punto final en nombres de zona (`ns1.lab.local` sin punto se le añade el origen).
- CNAME en el ápice de la zona o junto a otros registros.
- Rango DHCP que incluye direcciones estáticas.
- Resolver abierto a todo Internet (usable para amplificación DDoS): restringir con `allow-recursion`.

## Ejercicios propuestos
1. ¿Qué mensaje DHCP se envía en difusión primero? *Respuesta: Discover.*
2. ¿Qué registro necesita un dominio para recibir correo? *Respuesta: MX (y el A del servidor).*
3. ¿Cuándo se renueva una concesión de 8 h? *Respuesta: a las 4 h (T1).*

## Conexiones
[[Comunicaciones II]] (aplicaciones de red), [[Sistemas Operativos]] (resolución de nombres, systemd), [[Sistemas Distribuidos]] (descubrimiento de servicios), [[Administración de Redes]] (nota principal).

## Fuente
Conocimiento general: RFC 1034/1035 (DNS), 2131 (DHCP); documentación de BIND9 y dnsmasq.
