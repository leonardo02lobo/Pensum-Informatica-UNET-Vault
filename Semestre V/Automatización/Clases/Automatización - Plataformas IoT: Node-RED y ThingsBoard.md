---
tags: [clase, semestre-V]
materia: Automatización
---
# Automatización - Plataformas IoT: Node-RED y ThingsBoard

Materia: [[Automatización]]
Anterior: [[Automatización - Protocolos industriales e IoT: Modbus, OPC-UA, MQTT y HTTP]]
Siguiente: [[Automatización - Arquitectura con IA agéntica en n8n y ciberseguridad (Proyecto HIDRA)]]

## Contexto y objetivo

Una vez que los sensores y PLCs exponen sus datos mediante protocolos como Modbus o MQTT, se necesitan herramientas para **orquestar flujos** en el borde (*edge*) y **visualizar, almacenar y reaccionar** ante la telemetría en la nube. Esta clase aborda el uso integrado de **Node-RED** y **ThingsBoard**.

## 1. Node-RED: programación visual por flujos

**Node-RED** es una herramienta de desarrollo basada en flujos (*flow-based programming*) sobre Node.js, ideal para prototipado rápido, pasarelas (*gateways*) Edge y transformación de datos entre protocolos OT e IT.

### Conceptos centrales en Node-RED
- **Nodos:** bloques funcionales conectados por cables virtuales:
  - *Entrada (Input):* `inject`, `mqtt in`, `http in`, `modbus read`.
  - *Procesamiento (Function):* `function` (código JavaScript), `switch` (enrutamiento condicional), `change` (modificación de propiedades), `json` (parseo/serialización).
  - *Salida (Output):* `debug`, `mqtt out`, `http request`, `dashboard`.
- **Mensaje (`msg`):** objeto JavaScript que viaja entre nodos; su campo principal es `msg.payload` (donde suele viajar el JSON de telemetría) y `msg.topic`.

### Flujo típico Edge-to-Cloud
```
[ Modbus Read ] ──▶ [ Function: escalar 4-20 mA a bar ] ──▶ [ MQTT Out ] ──▶ Broker / ThingsBoard
```

## 2. ThingsBoard: plataforma IoT integral

**ThingsBoard** es una plataforma IoT de código abierto para gestión de dispositivos, recolección de telemetría, visualización y automatización de reglas.

### Componentes principales
1. **Dispositivos (*Devices*) y Activos (*Assets*):** representan sensores, PLCs o instalaciones físicas. Cada dispositivo se autentica mediante un **Access Token** (o certificados X.509).
2. **Telemetría vs. Atributos:**
   - *Telemetría (Time-series):* series temporales continuas (ej. `{"presion": 3.4, "caudal": 12.1}`).
   - *Atributos:* propiedades estáticas o de configuración (ej. `ubicacion`, `umbral_alarma` compartido desde el servidor).
3. **Dashboards:** tableros interactivos en tiempo real con medidores (*gauges*), gráficas históricas, mapas y widgets de control RPC (*Remote Procedure Call*) para enviar comandos hacia el dispositivo.
4. **Rule Engine (Motor de Reglas):** cadenas visuales de procesamiento que evalúan condiciones sobre la telemetría entrante:
   - *Ejemplo:* si `temperatura > 80 °C`, crear una **Alarma** crítica, registrar en base de datos y disparar un webhook hacia n8n o correo.
5. **Gemelos digitales (*Digital Twins*):** representación virtual sincronizada del estado actual e histórico de un activo físico para monitoreo y simulación.

## 3. Integración Node-RED + ThingsBoard

Node-RED suele actuar como **adaptador de campo**: lee un PLC vía Modbus/OPC-UA o simula sensores, formatea el JSON al formato esperado por ThingsBoard (`v1/devices/me/telemetry` vía MQTT o `/api/v1/$ACCESS_TOKEN/telemetry` vía HTTP POST) y lo envía. A su vez, puede suscribirse a comandos RPC de ThingsBoard (`v1/devices/me/rpc/request/+`) para accionar salidas en el PLC.

## Errores comunes

- **Enviar cadenas de texto mal formadas en `msg.payload`:** ThingsBoard espera un objeto JSON válido con pares clave-valor numéricos o booleanos para poder graficar series temporales.
- **Hardcodear el `ACCESS_TOKEN` dentro de múltiples nodos:** conviene centralizar credenciales en variables de entorno o nodos de configuración seguros y no incluirlos al exportar flujos JSON al repositorio.

## Ejercicios propuestos

1. **¿Qué diferencia hay en ThingsBoard entre telemetría y atributos compartidos?**
   - *Respuesta:* La telemetría son series de datos variables en el tiempo enviadas por el dispositivo; los atributos compartidos son parámetros de configuración definidos en el servidor (como consignas o umbrales) que el dispositivo consulta o recibe al actualizarse.
2. **¿Qué nodo de Node-RED usarías** para convertir una lectura cruda `0..4095` del ADC en una presión `0..10 bar` antes de publicarla?
   - *Respuesta:* Un nodo `function` (o `range`) que aplique `msg.payload = { presion: (msg.payload / 4095) * 10 }; return msg;`.

## Conexiones

- Desarrolla las prácticas descritas en [[Investigacion_NodeRED_ThingsBoard]], [[Investigacion_ThingsBoard_IoT]] y [[Practica para tercer parcial]].
- Anterior: [[Automatización - Protocolos industriales e IoT: Modbus, OPC-UA, MQTT y HTTP]].
- Siguiente: [[Automatización - Arquitectura con IA agéntica en n8n y ciberseguridad (Proyecto HIDRA)]].

## Fuente

- Basado en [[Automatización]], [[Investigacion_NodeRED_ThingsBoard]], [[Investigacion_ThingsBoard_IoT]] y [[Practica para tercer parcial]].
