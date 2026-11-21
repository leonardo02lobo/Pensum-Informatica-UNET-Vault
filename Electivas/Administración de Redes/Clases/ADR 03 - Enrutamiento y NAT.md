---
tags: [clase, electiva]
materia: Administración de Redes
fuente: "conocimiento general"
---
# ADR 03 - Enrutamiento y NAT

Materia: [[Administración de Redes]]
Anterior: [[ADR 02 - Subredes, VLSM y VLAN]]
Siguiente: [[ADR 04 - Servicios DNS y DHCP]]

## Contexto y objetivo
El enrutador decide por qué interfaz reenviar cada paquete. Objetivo: configurar rutas estáticas, comprender RIP, OSPF y BGP, y aplicar NAT/PAT para compartir una dirección pública.

## Teoría

### Tabla de enrutamiento y reenvío
Cada entrada: destino/prefijo, siguiente salto, interfaz, métrica. Se aplica la **coincidencia de prefijo más largo**. Ruta por defecto: 0.0.0.0/0. Distancia administrativa (Cisco): conectada 0, estática 1, OSPF 110, RIP 120, eBGP 20.

### Enrutamiento estático vs dinámico
Estático: simple, sin tráfico de control, no se adapta a fallas. Dinámico: los routers intercambian información.
- **RIP** (vector de distancia): métrica en saltos, máximo 15, actualización cada 30 s; converge lento; bucles mitigados con horizonte dividido.
- **OSPF** (estado de enlace): cada router construye el mapa de la red (LSDB) y ejecuta Dijkstra; métrica = costo $\approx \dfrac{10^{8}}{\text{ancho de banda en bps}}$ por defecto en Cisco; áreas (área 0 es la troncal); converge rápido; DR/BDR en redes de difusión.
- **BGP**: protocolo entre sistemas autónomos (AS), vector de rutas con atributos (AS-PATH, LOCAL_PREF, MED); eBGP entre AS, iBGP dentro; usa TCP 179; define el enrutamiento de Internet por políticas.

### NAT
Traduce direcciones privadas a públicas. Tipos: estático (1 a 1), dinámico (pool), **PAT/masquerade** (muchas a una usando puertos). Efecto: oculta direcciones internas, pero rompe conectividad de extremo a extremo (se resuelve con reenvío de puertos). No sustituye a un cortafuegos. IPv6 reduce la necesidad.

## Ejemplo resuelto
Topología: LAN A 192.168.1.0/24 (R1) y LAN B 192.168.2.0/24 (R2), enlace R1-R2 10.0.0.0/30 (R1 .1, R2 .2).

1. Rutas estáticas en Linux (con reenvío habilitado):
```bash
sudo sysctl -w net.ipv4.ip_forward=1
# En R1: alcanzar LAN B vía R2
sudo ip route add 192.168.2.0/24 via 10.0.0.2
# En R2: alcanzar LAN A vía R1
sudo ip route add 192.168.1.0/24 via 10.0.0.1
ip route get 192.168.2.10     # verifica la ruta elegida
```
2. Equivalente en Cisco IOS con OSPF:
```
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
 passive-interface gigabitEthernet0/1
! verificación
show ip route ospf
show ip ospf neighbor
```
Costo OSPF de un enlace Gigabit con referencia 100 Mbps: $10^8/10^9 = 0{,}1$, que se redondea a 1 (por eso se cambia `auto-cost reference-bandwidth`). Un enlace Fast Ethernet cuesta $10^8/10^8 = 1$ y uno de 10 Mbps cuesta 10. Ruta preferida: la de menor suma de costos.

3. PAT con nftables en el router de salida (`eth0` WAN, `eth1` LAN):
```bash
sudo nft add table ip nat
sudo nft add chain ip nat postrouting '{ type nat hook postrouting priority 100 ; }'
sudo nft add rule ip nat postrouting oifname "eth0" masquerade
# Reenvío de puerto: servidor web 192.168.1.10
sudo nft add chain ip nat prerouting '{ type nat hook prerouting priority -100 ; }'
sudo nft add rule ip nat prerouting iifname "eth0" tcp dport 8080 dnat to 192.168.1.10:80
```
Con iptables: `sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`. Verificación: `traceroute`, `conntrack -L`, `ip route`.

Diagnóstico típico: ping de LAN A a LAN B falla; revisar (a) ruta de ida y de vuelta, (b) `ip_forward`, (c) puerta de enlace del host, (d) filtros.

## Errores comunes
- Ruta de ida sin ruta de retorno.
- Olvidar `ip_forward` en un router Linux.
- Mala wildcard en OSPF.
- Costo de referencia de OSPF que iguala Fast y Gigabit Ethernet.
- Anunciar prefijos propios o ajenos por error en BGP (fugas de rutas).
- Creer que NAT es seguridad.

## Ejercicios propuestos
1. ¿Qué ruta se usa para 10.1.1.9 si hay 10.0.0.0/8, 10.1.0.0/16 y 10.1.1.0/24? *Respuesta: la /24 (prefijo más largo).*
2. ¿Máximo de saltos alcanzables en RIPv2? *Respuesta: 15; 16 significa inalcanzable.*
3. Diferencia entre masquerade y SNAT. *Respuesta: masquerade toma la IP actual de la interfaz (útil si es dinámica); SNAT usa una dirección fija.*

## Conexiones
[[Comunicaciones II]] (enrutamiento, protocolos de red), [[Sistemas Operativos]] (reenvío IP, netfilter), [[Sistemas Distribuidos]] (balanceo, alta disponibilidad de red).

## Fuente
Conocimiento general: Kurose y Ross; RFC 2328 (OSPF), 2453 (RIPv2), 4271 (BGP-4), 3022 (NAT). Sintaxis Cisco indicativa; verificar con el programa oficial.
