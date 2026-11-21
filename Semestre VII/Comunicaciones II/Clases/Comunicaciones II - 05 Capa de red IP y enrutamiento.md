---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: conocimiento general
---
# Comunicaciones II - 05 Capa de red IP y enrutamiento

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 04 Confiabilidad ARQ y ventana deslizante]]
Siguiente: [[Comunicaciones II - 06 Capa de aplicación HTTP DNS correo FTP]]

## Contexto y objetivo
Por debajo del transporte, la capa de red lleva paquetes de host a host a través de múltiples redes. Se repasan direccionamiento IP, subredes, NAT, ICMP y los algoritmos y protocolos de enrutamiento (RIP, OSPF, BGP). Es el fundamento de [[Administración de Redes]].

## Datagrama IPv4
Cabecera de 20 B (sin opciones): versión (4), IHL, DSCP/ECN, longitud total, identificación, banderas (DF, MF), desplazamiento de fragmento, **TTL**, protocolo (6 = TCP, 17 = UDP, 1 = ICMP), checksum de cabecera, IP origen, IP destino. El TTL decrece en cada router; al llegar a 0 se descarta y se envía ICMP "Time Exceeded" (así funciona `traceroute`).

### Fragmentación
Si el paquete excede la MTU del enlace, el router lo fragmenta (si DF = 0). Ejemplo: paquete de 4000 B (3980 B de datos) por MTU 1500: fragmentos de 1480 B de datos (desplazamientos 0, 185, 370 en unidades de 8 B) y uno final de 1040 B; MF = 1 salvo el último.

## Direccionamiento y subredes
- 32 bits en notación decimal con puntos. **CIDR**: prefijo `a.b.c.d/n`; máscara con n unos.
- Subred: dirección de red (host todo ceros), broadcast (todo unos), hosts útiles = $2^{32-n} - 2$.
- **Ejemplo**: 192.168.10.0/26. Máscara 255.255.255.192; 64 direcciones; hosts 192.168.10.1-.62; broadcast .63. Siguiente subred: 192.168.10.64/26.
- **VLSM**: subredes de distinto tamaño. Para 100, 50 y 20 hosts desde 10.0.0.0/24: /25 (126 hosts) para 100; /26 (62) para 50; /27 (30) para 20: 10.0.0.0/25, 10.0.0.128/26, 10.0.0.192/27.
- Rangos privados (RFC 1918): 10/8, 172.16/12, 192.168/16. IPv6 usa 128 bits (`2001:db8::/32`), sin fragmentación en routers ni checksum de cabecera.

## NAT y DHCP
**NAT/PAT** traduce (IP privada, puerto) a (IP pública, puerto distinto) y mantiene una tabla de traducciones; rompe el principio extremo a extremo (dificulta servidores detrás de NAT: requiere reenvío de puertos). **DHCP** asigna IP, máscara, gateway y DNS mediante DORA (Discover, Offer, Request, Ack) sobre UDP 67/68.

## ICMP y ARP
ICMP (protocolo 1) informa errores y diagnósticos (`ping` = Echo Request/Reply). ARP resuelve IP -> MAC en una LAN mediante broadcast; es sin autenticación (base de ARP spoofing).

## Reenvío (forwarding) y enrutamiento (routing)
- **Reenvío**: acción local por paquete: consultar la tabla y elegir interfaz de salida por **coincidencia del prefijo más largo** (*longest prefix match*).
- **Enrutamiento**: construcción de las tablas mediante algoritmos distribuidos.

### Ejemplo de prefijo más largo
Tabla: 10.0.0.0/8 -> A; 10.1.0.0/16 -> B; 10.1.2.0/24 -> C; 0.0.0.0/0 -> D. Destino 10.1.2.7 -> C (/24). 10.1.9.9 -> B. 10.200.0.1 -> A. 8.8.8.8 -> D (ruta por defecto).

## Algoritmos de enrutamiento
1. **Vector de distancias (Bellman-Ford)**: cada nodo comparte su vector con los vecinos; $d_x(y) = \min_v \{c(x,v) + d_v(y)\}$. Problema: *cuenta al infinito*; mitigaciones: horizonte dividido, envenenamiento de ruta. Protocolo: **RIP** (métrica = saltos, máximo 15, actualización cada 30 s).
2. **Estado de enlace (Dijkstra)**: cada nodo inunda el estado de sus enlaces; todos tienen el mapa completo y calculan el árbol de rutas más cortas. Protocolo: **OSPF** (áreas, costo inversamente proporcional al ancho de banda: costo = 10^8 / BW en bps por defecto).
3. **Vector de rutas (BGP)**: enrutamiento entre **sistemas autónomos** (AS); decide por política (AS-PATH, preferencia local), no solo por costo.

### Dijkstra, ejemplo
Grafo: A-B 2, A-C 5, B-C 1, B-D 4, C-D 1. Desde A: dist(A)=0; B=2; C=min(5, 2+1)=3; D=min(2+4, 3+1)=4 vía C. Ruta A->D: A-B-C-D, costo 4.

## IGP vs EGP
Dentro de un AS: IGP (RIP, OSPF, EIGRP). Entre AS: EGP (BGP-4). Jerarquía de Internet: ISPs de nivel 1, 2, 3 y puntos de intercambio (IXP).

## Errores comunes
- Olvidar restar 2 (red y broadcast) al contar hosts.
- Aplicar prefijo "más corto" en lugar de "más largo".
- Confundir reenvío con enrutamiento.
- Pensar que NAT es un mecanismo de seguridad: solo oculta direccionamiento, no filtra por estado por sí mismo.

## Ejercicios propuestos
1. ¿Cuántos hosts admite /21? *Resp.: 2^11 - 2 = 2046.*
2. ¿A qué red pertenece 172.16.37.200/20? *Resp.: 172.16.32.0/20.*
3. Con tabla 192.168.0.0/16 -> X y 192.168.4.0/22 -> Y, ¿destino 192.168.5.1? *Resp.: Y (/22 cubre 4.0-7.255).*

## Conexiones
Capas inferiores: [[Comunicaciones I - 11 Modelos de capas y redes LAN]]. Seguridad (firewalls, ACL): [[Comunicaciones II - 08 Seguridad en redes criptografía y TLS]]. El informe OSINT ([[Comunicaciones II - 09 OSINT reconocimiento pasivo y Google Hacking]]) discute paneles de routers expuestos.

## Fuente
Conocimiento general (Kurose-Ross cap. 4-5; RFC 791, 1918, 2328, 4271).
