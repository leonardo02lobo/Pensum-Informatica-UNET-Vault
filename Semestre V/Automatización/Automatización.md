---
tags: [materia, semestre-V]
semestre: V
---
# Automatización

**Semestre:** [[Semestre V]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Fundamentos de Lógica Digital]]

## Desbloquea
- _Ninguna_

## Notas en el vault
- [[Charla automatizacion]]
- [[Investigacion_NodeRED_ThingsBoard]]
- [[Investigacion_ThingsBoard_IoT]]
- [[Practica 1]]
- [[Practica para tercer parcial]]
- [[Proyecto HIDRA - Arquitectura n8n y Ciberseguridad]]

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Automatizacion Industrial`

## Apuntes

### Descripción general y objetivos
Automatización (en el aula, *Automatización Industrial*) introduce el control automático de procesos mediante PLC, lógica de contactos (ladder), sensores/actuadores, redes industriales e IoT, y en la versión cursada aquí se integra con **IA agéntica orquestada en n8n**, plataformas IoT (Node-RED, ThingsBoard) y despliegue web (Vercel). Objetivos: modelar un proceso automatizado, programar su lógica secuencial (contadores, temporizadores), comunicar dispositivos y plataformas con protocolos estándar y documentar requisitos, riesgos y seguridad del sistema. Verificar con el programa oficial el sinóptico exacto.

### Contenido programático
1. **Fundamentos de automatización**: sistemas de lazo abierto y cerrado, sensores, actuadores, señales digitales/analógicas.
2. **Lógica programable (PLC)**: ciclo de scan (leer entradas, ejecutar programa, escribir salidas), lenguaje Ladder, bobinas Set/Reset, contactos NA/NC, marcas internas (M), contadores (C) y temporizadores (T: TON/TOF).
3. **Prácticas de lógica secuencial** (ver [[Practica 1]]): contador de pulsos que enciende una luz al primer clic, ignora el segundo y al tercero arranca un ventilador tras 10 s; parada con retardo de 10 s; variante con luz intermitente.
4. **IoT e integración**: protocolos MQTT, HTTP, CoAP, Modbus, OPC-UA; Node-RED (programación por flujos) y ThingsBoard (telemetría, dashboards, alarmas, Rule Engine, gemelos digitales). Ver [[Investigacion_NodeRED_ThingsBoard]], [[Investigacion_ThingsBoard_IoT]] y [[Practica para tercer parcial]].
5. **Proyecto integrador**: arquitectura IA agéntica con proceso de aplicación web (comunicación bidireccional), flujos en n8n, capas PM / IA agéntica / Planta, roles y entregables (ver [[Charla automatizacion]]).
6. **Ciberseguridad de sistemas automatizados**: auditoría, frontera de confianza, aprobación humana de recomendaciones de la IA.

### Conceptos clave
- **PLC**: computadora industrial robusta con ejecución cíclica determinista.
- **Rung**: línea de lógica ladder; **Set/Reset**: enclavamiento de una salida.
- **TON**: temporizador a la conexión; activa su salida tras el tiempo preset con la entrada activa.
- **Telemetría**: datos enviados por un dispositivo a una plataforma.
- **MQTT**: protocolo publicador/suscriptor ligero sobre TCP con broker y tópicos.
- **Edge computing**: procesar cerca de la fuente de datos.
- **IA agéntica**: modelo de lenguaje con herramientas que toma pasos intermedios; en el proyecto solo recomienda y un humano aprueba.

### Ejemplo de lógica (Práctica 1, estructura ladder en texto)
```
RUNG1: X0(pulso) -> C1 cuenta
RUNG2: C1=1 -> SET M1 -> Y0 (luz ON)
RUNG3: C1=3 -> TON T1 (10 s) -> SET Y1 (ventilador ON)
RUNG4: STOP -> RESET M1 -> TON T2 (10 s) -> RESET Y0, Y1, C1
```

### Proyecto del Material (HIDRA)
El informe del líder de proyecto del Grupo 4 documenta requisitos, riesgos y alcance de un sistema de bombeo con HMI, frontera de confianza en el servidor y despliegue en Vercel, más cinco flujos de IA en n8n: F1 diagnóstico causal de alarmas, F2 informe de turno, F3 vigilancia de bitácora, F4 recomendación de consignas y un quinto flujo adicional (ver el docx). Toda salida del agente es recomendación sujeta a aprobación humana (RF-A-07). Reparto de puntos de la charla: líder de proyecto 20, planta 60 (nota grupal), ciberseguridad 10, presentación 10.

### Relación con otras materias
Prelada por [[Fundamentos de Lógica Digital]] (álgebra booleana, secuenciales). Se relaciona con [[Organización del Computador]], [[Comunicaciones I]] (protocolos), [[Sistemas Operativos]] (tiempo real) y [[Gerencia de Proyectos]] (requisitos y riesgos).

### Evaluación y consejos
- Parciales con prácticas (ladder, flujos) y proyecto grupal; la fecha de presentación indicada en la charla es 19/08/2026.
- Documenta con diagramas (mermaid) y checklist de cierre; versiona los flujos JSON de Node-RED/n8n.
- Prioriza la seguridad: no expongas credenciales en los flujos.

### Bibliografía recomendada
- Bolton, W. *Mecatrónica*. Alfaomega.
- Ogata, K. *Ingeniería de Control Moderna*. Pearson.
- Documentación oficial de n8n, Node-RED, ThingsBoard y MQTT.

### Recursos del Material/
- [Informe-Lider-Proyecto-HIDRA.docx](Material/Informe-Lider-Proyecto-HIDRA.docx): informe de requisitos, riesgos y alcance con capas, flujos F1-F5 y requisitos.
