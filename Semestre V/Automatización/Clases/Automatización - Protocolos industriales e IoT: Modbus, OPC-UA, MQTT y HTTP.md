---
tags: [clase, semestre-V]
materia: Automatización
---
# Automatización - Protocolos industriales e IoT: Modbus, OPC-UA, MQTT y HTTP

Materia: [[Automatización]]
Anterior: [[Automatización - Lógica secuencial con temporizadores y contadores]]
Siguiente: [[Automatización - Plataformas IoT: Node-RED y ThingsBoard]]

## Contexto y objetivo

La automatización moderna conecta el piso de planta (**OT**, *Operational Technology*) con los sistemas informáticos, la nube y la analítica (**IT**, *Information Technology*). Esta clase compara los protocolos clásicos de campo (**Modbus**, **OPC-UA**) con los protocolos estándar del Internet de las Cosas (**MQTT**, **HTTP/REST**, **CoAP**).

## 1. Pirámide de automatización e integración IT/OT

```
Nivel 4: ERP / Nube / Analítica / IA      (HTTP, MQTT, REST)
Nivel 3: MES / Supervisión de planta      (OPC-UA, SQL, MQTT)
Nivel 2: SCADA / HMI                      (OPC-UA, Modbus TCP)
Nivel 1: Controladores (PLC, RTU, Edge)   (Modbus RTU/TCP, Profinet)
Nivel 0: Sensores y Actuadores            (4-20 mA, 24 V DC, IO-Link)
```

## 2. Protocolos industriales clásicos

### Modbus (RTU y TCP)
Protocolo maestro-esclavo (cliente-servidor) abierto y muy extendido desde 1979:
- **Modbus RTU:** opera sobre enlace serial **RS-485** (robusto ante ruido, hasta ~1200 m).
- **Modbus TCP:** encapsula tramas Modbus sobre **TCP/IP** (puerto estándar `502`).
- **Modelo de datos simple:** cuatro tablas de direcciones: *Coils* (salidas digitales R/W), *Discrete Inputs* (entradas digitales RO), *Input Registers* (registros analógicos 16-bit RO) y *Holding Registers* (registros 16-bit R/W).
- *Limitación:* carece de cifrado nativo y de tipado semántico (el cliente debe saber manualmente qué significa el registro `40001`).

### OPC-UA (*Open Platform Communications Unified Architecture*)
Estándar moderno independiente de plataforma para interoperabilidad industrial:
- **Modelado semántico:** organiza variables como objetos con metadatos, unidades de ingeniería y jerarquías.
- **Seguridad integrada:** soporta autenticación mediante certificados X.509, firma y cifrado TLS.
- Opera en arquitectura cliente-servidor y también en modo publicador/suscriptor.

## 3. Protocolos IoT: MQTT, HTTP y CoAP

| Característica | **MQTT** | **HTTP / REST** | **CoAP** |
| :--- | :--- | :--- | :--- |
| **Patrón** | Publicador / Suscriptor (*Pub/Sub*) | Petición / Respuesta | Petición / Respuesta (estilo REST) |
| **Transporte** | TCP (puerto `1883` / TLS `8883`) | TCP (puerto `80` / TLS `443`) | UDP (puerto `5683` / DTLS) |
| **Sobrecarga** | Muy baja (cabecera mínima de 2 bytes) | Alta (cabeceras de texto repetitivas) | Muy baja (diseñado para microcontroladores) |
| **Uso típico** | Telemetría en tiempo real hacia brokers | APIs web, integración con backend y n8n | Sensores restringidos de muy bajo consumo |

### Funcionamiento de MQTT
En MQTT los dispositivos no se comunican directamente entre sí, sino a través de un **Broker** central (como Mosquitto o EMQX):
- **Tópicos (*Topics*):** cadenas jerárquicas separadas por `/` (ej. `planta/bomba1/presion`). Comodines: `+` (un nivel) y `#` (multinivel).
- **QoS (*Quality of Service*):**
  - `QoS 0`: a lo sumo una vez (*fire and forget*).
  - `QoS 1`: al menos una vez (con confirmación `PUBACK`, posible duplicado).
  - `QoS 2`: exactamente una vez (handshake de 4 pasos, mayor latencia).
- **Retained message & LWT:** el *Last Will and Testament* permite al broker notificar automáticamente si un dispositivo pierde conexión abruptamente.

## Errores comunes

- **Usar HTTP polling cada segundo desde decenas de sensores:** desperdicia ancho de banda y batería; para telemetría continua es mucho más eficiente **MQTT**.
- **Suscribirse a `#` en producción sin filtros:** puede saturar el cliente o el broker si hay miles de mensajes por segundo.
- **Exponer Modbus TCP directamente a Internet:** al no tener autenticación ni cifrado, cualquiera en la red podría escribir en los registros del PLC.

## Ejercicios propuestos

1. **¿Qué tópico con comodín captura la temperatura de cualquier bomba en cualquier planta** si la estructura es `<planta>/<equipo>/temperatura`?
   - *Respuesta:* `+/+/temperatura`.
2. **¿Qué ventaja clave ofrece OPC-UA frente a Modbus TCP?**
   - *Respuesta:* Seguridad integrada (cifrado y certificados) y un modelo de información semántico con estructura de objetos y unidades.

## Conexiones

- Se relaciona con capas de transporte y red estudiadas en [[Comunicaciones I]].
- Base para la integración de plataformas en [[Automatización - Plataformas IoT: Node-RED y ThingsBoard]].
- Véase también [[Investigacion_NodeRED_ThingsBoard]] e [[Investigacion_ThingsBoard_IoT]].
- Anterior: [[Automatización - PLC, ciclo de scan y lenguaje Ladder]].

## Fuente

- Basado en [[Automatización]], [[Investigacion_NodeRED_ThingsBoard]] y [[Investigacion_ThingsBoard_IoT]].
