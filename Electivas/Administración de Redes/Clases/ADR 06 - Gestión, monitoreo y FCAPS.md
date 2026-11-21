---
tags: [clase, electiva]
materia: Administración de Redes
fuente: "conocimiento general"
---
# ADR 06 - Gestión, monitoreo y FCAPS

Materia: [[Administración de Redes]]
Anterior: [[ADR 05 - Servicios web, correo, proxy y directorio]]
Siguiente: [[ADR 07 - Seguridad de red, firewalls y VPN]]

## Contexto y objetivo
No se puede administrar lo que no se mide. Esta clase presenta el modelo FCAPS, SNMP, syslog, las herramientas de monitoreo (Nagios, Zabbix) y el análisis de paquetes con Wireshark/tcpdump, además de buenas prácticas ITIL. Objetivo: consultar dispositivos por SNMP, calcular utilización de enlaces y capturar tráfico para diagnosticar.

## Teoría

### FCAPS (ISO)
**F**allas, **C**onfiguración, **C**ontabilidad, **P**restaciones (*performance*), **S**eguridad. Marco para clasificar tareas de gestión: detectar y corregir fallas, versionar configuraciones, medir uso, vigilar rendimiento, proteger.

### ITIL
Marco de buenas prácticas de servicios de TI: gestión de incidentes, problemas, cambios, configuración (CMDB) y niveles de servicio (SLA). Disponibilidad:
$$A = \frac{MTBF}{MTBF + MTTR}$$
Con 99,9 % se admiten unas 8,76 h de caída al año.

### SNMP
Arquitectura gestor, agente y **MIB** (árbol de objetos con **OID**, p. ej. `1.3.6.1.2.1.1.5.0` = sysName). Operaciones: GET, GETNEXT, GETBULK, SET, TRAP/INFORM (avisos). Versiones: v1 y v2c (comunidad en claro, inseguras), **v3** (autenticación y cifrado). UDP 161 (consultas) y 162 (traps). Contadores de 32 bits (`ifInOctets`) se desbordan; usar 64 bits (`ifHCInOctets`).

### Syslog
Mensajes centralizados (UDP/TCP 514) con *facility* y *severidad* (0 emergencia a 7 depuración). Útil junto a rsyslog/journald y pilas como ELK.

### Monitoreo
Nagios/Icinga (comprobaciones activas, alertas), Zabbix (agentes, plantillas, gráficos), Prometheus + Grafana, LibreNMS. Buen monitoreo: umbrales con histéresis, dependencias entre alertas, línea base.

### Análisis de paquetes
Wireshark (interfaz) y `tcpdump` (consola). Filtros de captura (BPF) y de visualización.

## Ejemplo resuelto
Estimar la utilización de una interfaz con dos lecturas de contador SNMP.

1. Lecturas de `ifHCInOctets`: $C_1 = 5\,200\,000\,000$ en $t_1$ y $C_2 = 5\,950\,000\,000$ a los 300 s; enlace de 100 Mb/s.
2. Octetos en el intervalo: $\Delta C = 750\,000\,000$.
3. Velocidad media: $\dfrac{750\,000\,000 \times 8}{300} = 20\,000\,000$ b/s $= 20$ Mb/s.
4. Utilización: $20/100 = 20\,\%$.

Comandos:
```bash
# v2c (solo laboratorio)
snmpwalk -v2c -c public 192.168.1.1 system
snmpget  -v2c -c public 192.168.1.1 1.3.6.1.2.1.1.5.0
snmpget  -v2c -c public 192.168.1.1 IF-MIB::ifHCInOctets.2
# v3 con autenticación y cifrado
snmpget -v3 -l authPriv -u monitor -a SHA -A 'claveAuth123' -x AES -X 'clavePriv123' 192.168.1.1 sysUpTime.0
```
Agente en un servidor Linux (`/etc/snmp/snmpd.conf`):
```
rocommunity secreto 192.168.20.0/24
syslocation Laboratorio
sysservices 72
```
Cálculo automático (Python):
```python
def utilizacion(c1, c2, seg, bps, bits=64):
    delta = (c2 - c1) % (2 ** bits)       # tolera desbordamiento
    return delta * 8 / seg / bps * 100

print(utilizacion(5_200_000_000, 5_950_000_000, 300, 100_000_000))   # 20.0
```
Syslog remoto con rsyslog:
```
# cliente: /etc/rsyslog.d/50-remoto.conf
*.warning  @@192.168.20.5:514
# servidor: habilitar imtcp en puerto 514
```
`logger -p auth.warning "prueba de alerta"` genera un mensaje.

Captura y análisis:
```bash
sudo tcpdump -i eth0 -nn 'host 192.168.20.10 and tcp port 443' -w captura.pcap
sudo tcpdump -i eth0 -nn udp port 53            # ver consultas DNS
sudo tcpdump -i eth0 -nn 'port 67 or port 68'   # ver DORA de DHCP
```
Filtros de visualización en Wireshark: `ip.addr == 192.168.20.10`, `tcp.flags.syn == 1 && tcp.flags.ack == 0`, `dns.flags.rcode != 0`, `tcp.analysis.retransmission`.

Diagnóstico guiado: usuarios se quejan de lentitud; (1) utilización del enlace, (2) errores y descartes en la interfaz (`ip -s link`), (3) retransmisiones TCP en la captura, (4) tiempo de respuesta DNS con `dig`.

## Errores comunes
- Dejar la comunidad `public` o SNMPv1 expuesta.
- Usar contadores de 32 bits en enlaces rápidos.
- Alertar por cada pico breve (fatiga de alertas).
- Capturar tráfico con datos personales sin autorización.
- No sincronizar relojes (NTP): los registros pierden valor.

## Ejercicios propuestos
1. Disponibilidad de un servicio con MTBF 1000 h y MTTR 2 h. *Respuesta: 1000/1002 = 99,80 %.*
2. ¿Qué diferencia hay entre GET y TRAP? *Respuesta: GET lo inicia el gestor (sondeo); el TRAP lo envía el agente al ocurrir un evento.*
3. Filtro `tcpdump` para tráfico SSH desde 10.0.0.5. *Respuesta: `tcpdump -nn 'src host 10.0.0.5 and tcp port 22'`.*

## Conexiones
[[Comunicaciones II]] (protocolos de red), [[Sistemas Operativos]] (registros, procesos, NTP), [[Sistemas Distribuidos]] (observabilidad), [[Ingeniería de Software]] (operaciones y calidad de servicio).

## Fuente
Conocimiento general: RFC 3411-3418 (SNMPv3), 5424 (syslog), recomendación ISO FCAPS, ITIL; documentación de Wireshark, Zabbix y Net-SNMP.
