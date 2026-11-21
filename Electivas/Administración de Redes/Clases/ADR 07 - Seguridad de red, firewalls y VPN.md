---
tags: [clase, electiva]
materia: Administración de Redes
fuente: "conocimiento general"
---
# ADR 07 - Seguridad de red, firewalls y VPN

Materia: [[Administración de Redes]]
Anterior: [[ADR 06 - Gestión, monitoreo y FCAPS]]
Siguiente: (fin de la serie)

## Contexto y objetivo
Una red administrada debe controlar quién entra, qué sale y qué circula entre segmentos. Objetivo: aplicar defensa en profundidad con segmentación, cortafuegos con estado (iptables/nftables), VPN (WireGuard, IPsec) e IDS/IPS.

## Teoría

### Principios
Confidencialidad, integridad, disponibilidad (tríada CIA); mínimo privilegio; defensa en profundidad; denegar por defecto. Modelo de amenazas: escaneo, suplantación ARP, ataques DoS, fuerza bruta, malware.

### Cortafuegos
- **Sin estado** (filtra por paquete) vs **con estado** (conntrack: estados NEW, ESTABLISHED, RELATED, INVALID).
- Linux: **netfilter**, gestionado con `iptables` (clásico) o `nftables` (actual). Cadenas INPUT, OUTPUT, FORWARD; políticas por defecto.
- Cortafuegos de aplicación (WAF) y de nueva generación (inspección profunda).
- Orden de reglas: la primera coincidencia gana.

### Segmentación y DMZ
Separar usuarios, servidores y servicios expuestos (DMZ) con reglas entre zonas. Las VLAN (ADR 02) más ACL/cortafuegos limitan el movimiento lateral.

### VPN
- **IPsec** (IKE + ESP): túnel sitio a sitio estándar.
- **WireGuard**: moderno, simple, basado en pares de claves públicas (UDP, puerto típico 51820).
- **OpenVPN**: TLS, flexible.
Modos: acceso remoto y sitio a sitio.

### IDS/IPS
Sistemas de detección o prevención de intrusiones: Snort, Suricata (firmas y anomalías). Colocación en puntos de espejo (SPAN). Fail2ban bloquea IP tras intentos fallidos leyendo registros. Seguridad de capa 2: *port security*, DHCP snooping, ARP inspection, 802.1X.

## Ejemplo resuelto
Servidor Linux con SSH y web. Política: denegar todo entrante salvo SSH desde la LAN administrativa, HTTP y HTTPS.

1. Reglas con nftables (`/etc/nftables.conf`):
```
table inet filtro {
  chain entrada {
    type filter hook input priority 0; policy drop;
    ct state established,related accept
    ct state invalid drop
    iif "lo" accept
    ip protocol icmp icmp type echo-request limit rate 5/second accept
    ip saddr 192.168.20.0/26 tcp dport 22 accept
    tcp dport { 80, 443 } accept
    counter log prefix "DROP-IN: " limit rate 3/minute
  }
  chain reenvio {
    type filter hook forward priority 0; policy drop;
    ct state established,related accept
    iifname "eth1" oifname "eth0" accept
  }
}
```
```bash
sudo nft -c -f /etc/nftables.conf      # verificar sintaxis
sudo nft -f /etc/nftables.conf
sudo nft list ruleset
```
Equivalente iptables:
```bash
sudo iptables -P INPUT DROP
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A INPUT -p tcp -s 192.168.20.0/26 --dport 22 -j ACCEPT
sudo iptables -A INPUT -p tcp -m multiport --dports 80,443 -j ACCEPT
```
Precaución: aplicar con acceso por consola o con un temporizador que revierta, para no cortar la propia sesión SSH.

2. Prueba desde otra máquina: `nmap -Pn -p 22,80,443,3306 192.168.20.10` debe mostrar 22 filtrado fuera de la LAN administrativa, 80/443 abiertos y 3306 filtrado.

3. VPN WireGuard sitio a servidor:
```bash
umask 077
wg genkey | tee priv.key | wg pubkey > pub.key
```
Servidor `/etc/wireguard/wg0.conf`:
```
[Interface]
Address = 10.8.0.1/24
ListenPort = 51820
PrivateKey = <clave privada del servidor>

[Peer]
PublicKey = <clave pública del cliente>
AllowedIPs = 10.8.0.2/32
```
Cliente:
```
[Interface]
Address = 10.8.0.2/32
PrivateKey = <clave privada del cliente>

[Peer]
PublicKey = <clave pública del servidor>
Endpoint = vpn.example.org:51820
AllowedIPs = 192.168.20.0/24, 10.8.0.0/24
PersistentKeepalive = 25
```
```bash
sudo wg-quick up wg0
sudo wg show           # handshake reciente indica túnel activo
```
`AllowedIPs` actúa como tabla de enrutamiento y filtro por par.

4. Fail2ban para SSH (`/etc/fail2ban/jail.local`):
```
[sshd]
enabled = true
maxretry = 5
findtime = 10m
bantime = 1h
```
Estado: `sudo fail2ban-client status sshd`.

## Errores comunes
- Política ACCEPT por defecto con reglas de bloqueo parciales.
- Bloquear todo ICMP (rompe descubrimiento de MTU, sobre todo en IPv6).
- Olvidar reglas IPv6 mientras se protege solo IPv4.
- Claves privadas con permisos amplios o en repositorios.
- Confiar en NAT como protección.
- Probar reglas en producción sin plan de reversión.

## Ejercicios propuestos
1. ¿Por qué `ESTABLISHED,RELATED` va primero? *Respuesta: acepta respuestas de conexiones legítimas rápidamente y reduce el procesamiento de reglas.*
2. Regla para permitir DNS entrante UDP desde la LAN 192.168.20.0/24. *Respuesta: `iptables -A INPUT -p udp -s 192.168.20.0/24 --dport 53 -j ACCEPT`.*
3. Diferencia entre IDS e IPS. *Respuesta: el IDS detecta y alerta; el IPS está en línea y puede bloquear.*

## Conexiones
[[Comunicaciones II]] (seguridad en redes), [[Sistemas Operativos]] (netfilter, usuarios y servicios), [[Sistemas Distribuidos]] (autenticación y confianza entre servicios), [[Introducción a las Telecomunicaciones]] (medios inalámbricos y cifrado de enlaces).

## Fuente
Conocimiento general: documentación de nftables/netfilter y WireGuard, RFC 4301 (IPsec), Stallings; OWASP/NIST SP 800-41 para cortafuegos. Verificar con el programa oficial.
