---
tags: [electiva]
---
# Administración de Redes

Opción de [[Electivas]].

## Descripción
Gestión operativa de redes de computadores: configuración de servicios, monitoreo, seguridad y resolución de fallas. Extiende [[Comunicaciones I]] y [[Comunicaciones II]].

## Temario típico (verificar con el programa oficial)
1. Modelo OSI y TCP/IP, direccionamiento IPv4/IPv6, subredes (VLSM), VLAN.
2. Enrutamiento: estático, RIP, OSPF, BGP (introducción); NAT.
3. Servicios: DNS, DHCP, correo, web, proxy, directorio (LDAP, Active Directory).
4. Gestión y monitoreo: SNMP, syslog, Nagios/Zabbix, análisis con Wireshark.
5. Seguridad: firewalls (iptables, nftables), VPN, IDS/IPS, segmentación.
6. Modelo FCAPS y buenas prácticas ITIL.

## Fórmulas y comandos
```
Hosts utilizables por subred = 2^(32 - prefijo) - 2     # /26 -> 62 hosts
```

```bash
ip addr; ip route
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
snmpwalk -v2c -c public 192.168.1.1 system
```

## Relación con el pensum
[[Comunicaciones I]], [[Comunicaciones II]], [[Sistemas Operativos]], [[Sistemas Distribuidos]], [[Introducción a las Telecomunicaciones]].

## Recursos y bibliografía
- Tanenbaum y Wetherall. *Redes de Computadoras*.
- Kurose y Ross. *Computer Networking: A Top-Down Approach*.
- Cisco Networking Academy; Packet Tracer, GNS3.
- Limoncelli. *The Practice of System and Network Administration*.
