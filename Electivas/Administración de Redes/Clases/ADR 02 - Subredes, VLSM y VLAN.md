---
tags: [clase, electiva]
materia: Administración de Redes
fuente: "conocimiento general"
---
# ADR 02 - Subredes, VLSM y VLAN

Materia: [[Administración de Redes]]
Anterior: [[ADR 01 - Modelos OSI, TCP-IP y direccionamiento IP]]
Siguiente: [[ADR 03 - Enrutamiento y NAT]]

## Contexto y objetivo
Una organización recibe un bloque de direcciones y debe repartirlo entre departamentos sin desperdicio ni solapamientos, y separar lógicamente el tráfico en la capa 2. Objetivo: aplicar VLSM (máscaras de longitud variable) y configurar VLAN con troncales 802.1Q.

## Teoría

### Subredes y VLSM
Con **máscara fija** todas las subredes tienen el mismo tamaño, lo que desperdicia direcciones. **VLSM** asigna a cada subred el prefijo justo. Procedimiento:
1. Ordenar los requisitos de mayor a menor número de hosts.
2. Para cada uno, hallar el menor $n$ con $2^{n}-2 \ge H$ (hosts necesarios); prefijo $=32-n$.
3. Asignar bloques consecutivos alineados al tamaño del bloque, empezando por el inicio del espacio.
4. Reservar los enlaces punto a punto con /30 (2 hosts) o /31.

Resumen:
$$H \le 2^{32-p}-2 \quad\Rightarrow\quad p = 32-\lceil \log_2 (H+2)\rceil$$
Agregación (*supernetting*): reunir bloques contiguos en un prefijo más corto para resumir rutas.

### VLAN
Una VLAN es un dominio de difusión lógico definido en el conmutador. Ventajas: segmentación, seguridad, menos difusión. Puertos **de acceso** (una VLAN, sin etiqueta) y **troncales** (varias VLAN con etiqueta IEEE 802.1Q de 4 bytes, ID de 12 bits: 1 a 4094). La VLAN nativa viaja sin etiqueta. Entre VLAN se necesita enrutamiento capa 3: *router-on-a-stick* (subinterfaces) o conmutador capa 3 (SVI).

## Ejemplo resuelto
Bloque 192.168.20.0/24 para: Docentes 100 hosts, Estudiantes 50, Laboratorio 25, Administración 10 y dos enlaces punto a punto.

1. Docentes: $2^7-2=126 \ge 100$, /25. Bloque 192.168.20.0/25 (0-127), útiles .1-.126.
2. Estudiantes: $2^6-2=62\ge 50$, /26. 192.168.20.128/26 (128-191).
3. Laboratorio: $2^5-2=30\ge 25$, /27. 192.168.20.192/27 (192-223).
4. Administración: $2^4-2=14 \ge 10$, /28. 192.168.20.224/28 (224-239).
5. Enlaces: /30 cada uno: 192.168.20.240/30 y 192.168.20.244/30.
6. Sobra 192.168.20.248/29 para crecer.

Tabla final:
| Subred | Prefijo | Red | Rango útil | Difusión |
|---|---|---|---|---|
| Docentes | /25 | .0 | .1-.126 | .127 |
| Estudiantes | /26 | .128 | .129-.190 | .191 |
| Laboratorio | /27 | .192 | .193-.222 | .223 |
| Administración | /28 | .224 | .225-.238 | .239 |
| Enlace 1 | /30 | .240 | .241-.242 | .243 |
| Enlace 2 | /30 | .244 | .245-.246 | .247 |

Verificación programada:
```python
import ipaddress
total = ipaddress.ip_network("192.168.20.0/24")
reqs = [("Docentes",100),("Estudiantes",50),("Lab",25),("Admin",10),("E1",2),("E2",2)]
libre = total.network_address
for nombre, h in sorted(reqs, key=lambda x: -x[1]):
    p = 32 - (h + 2 - 1).bit_length()
    red = ipaddress.ip_network((libre, p))
    print(nombre, red, red.num_addresses - 2)
    libre = red.broadcast_address + 1
```

VLAN en Linux (iproute2) y conmutador estilo Cisco:
```bash
# Linux: subinterfaz VLAN 10
sudo ip link add link eth0 name eth0.10 type vlan id 10
sudo ip addr add 192.168.20.1/25 dev eth0.10
sudo ip link set eth0.10 up
```
```
! Conmutador (sintaxis tipo Cisco IOS)
vlan 10
 name DOCENTES
vlan 20
 name ESTUDIANTES
interface fastEthernet0/1
 switchport mode access
 switchport access vlan 10
interface gigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
! Router-on-a-stick
interface gigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.20.1 255.255.255.128
```
Prueba: un equipo en VLAN 10 no alcanza a uno en VLAN 20 hasta que exista el enrutamiento entre VLAN; `show vlan brief` y `show interfaces trunk` verifican.

## Errores comunes
- Asignar primero las subredes pequeñas y fragmentar el espacio.
- Bloques no alineados (un /26 que no empieza en múltiplo de 64).
- VLAN nativa distinta en ambos extremos del troncal.
- Olvidar permitir la VLAN en el troncal.
- Dejar la VLAN 1 para administración y datos.

## Ejercicios propuestos
1. Prefijo para 500 hosts. *Respuesta: /23 (510 útiles).*
2. ¿Por qué un /30 para enlaces punto a punto? *Respuesta: solo se necesitan 2 direcciones útiles.*
3. ¿Cuántas VLAN identifica 802.1Q? *Respuesta: 4094 utilizables (12 bits).*

## Conexiones
[[Comunicaciones II]] (conmutación, Ethernet), [[Sistemas Operativos]] (configuración de interfaces), [[Sistemas Distribuidos]] (segmentación de servicios).

## Fuente
Conocimiento general: Kurose y Ross; Cisco Networking Academy (sintaxis de ejemplo); IEEE 802.1Q. Verificar con el programa oficial el equipo usado en laboratorio.
