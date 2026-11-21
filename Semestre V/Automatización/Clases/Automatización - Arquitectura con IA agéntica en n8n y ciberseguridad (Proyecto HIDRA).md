---
tags: [clase, semestre-V]
materia: Automatización
---
# Automatización - Arquitectura con IA agéntica en n8n y ciberseguridad (Proyecto HIDRA)

Materia: [[Automatización]]
Anterior: [[Automatización - Plataformas IoT: Node-RED y ThingsBoard]]
Siguiente: —

## Contexto y objetivo

Esta clase sintetiza la arquitectura del proyecto integrador de [[Automatización]] (**Sistema de bombeo HIDRA**): una arquitectura de **tres capas** que conecta una planta automatizada con HMI/aplicación web desplegada en Vercel y un módulo de **IA agéntica orquestada en n8n**, bajo estrictos controles de **ciberseguridad** y supervisión humana (*human-in-the-loop*).

## 1. Arquitectura de tres capas y comunicación bidireccional

El proyecto se organiza en tres capas jerárquicas con separación clara de responsabilidades:

```
┌───────────────────────────────────────────────────────────┐
│  Capa 1: PM / Gestión (Requisitos, riesgos, métricas)     │
└──────────────────────────┬────────────────────────────────┘
                           ▼
┌───────────────────────────────────────────────────────────┐
│  Capa 2: IA Agéntica en n8n (Flujos F1–F5, análisis LLM)  │
│  [ Frontera de confianza en servidor — Solo recomienda ]  │
└──────────────────────────┬────────────────────────────────┘
                           ▲  Aprobación humana (RF-A-07)
                           ▼
┌───────────────────────────────────────────────────────────┐
│  Capa 3: Planta / HMI / App Web (Vercel + PLC / IoT)      │
└───────────────────────────────────────────────────────────┘
```

- **Comunicación bidireccional:** la planta envía telemetría, alarmas y bitácoras hacia la aplicación web y n8n; las consignas o acciones correctivas viajan de vuelta hacia la planta **únicamente** después de pasar por validación en el servidor y aprobación del operador humano.

## 2. Flujos de IA agéntica en n8n (F1–F5)

**n8n** actúa como orquestador de flujos de trabajo que conecta webhooks de la HMI/backend con modelos de lenguaje (LLM) y herramientas de consulta:

1. **F1 — Diagnóstico causal de alarmas:** al dispararse una alarma crítica (ej. sobrepresión o cavitación), el agente consulta el historial reciente de telemetría y propone causas raíz probables y pasos de verificación.
2. **F2 — Informe de turno:** consolida eventos, consumo energético, horas de operación de bombas y anomalías del turno en un reporte estructurado para supervisión.
3. **F3 — Vigilancia de bitácora:** analiza continuamente registros de eventos para detectar patrones anómalos o secuencias de fallas recurrentes antes de que escalen.
4. **F4 — Recomendación de consignas:** sugiere ajustes óptimos de operación (ej. alternancia de bombas o puntos de consigna) según demanda y estado del sistema.
5. **F5 — Flujo adicional de soporte:** automatiza la asistencia operativa o notificación contextual según las necesidades definidas en el proyecto (ver informe HIDRA en `Material/`).

## 3. Ciberseguridad y frontera de confianza

Integrar IA generativa y aplicaciones web con procesos físicos industriales introduce riesgos críticos (inyección de *prompts*, comandos no autorizados, exposición de secretos). Para mitigarlos se establecen tres reglas de oro:

1. **Principio de aprobación humana obligatoria (RF-A-07):** *toda salida de la IA agéntica es una recomendación, nunca una ejecución directa sobre actuadores físicos.* Un operador autenticado debe aprobar explícitamente cualquier cambio de consigna.
2. **Frontera de confianza en el servidor:** el frontend (desplegado en Vercel) jamás se comunica directamente con credenciales de planta o llaves de API del LLM; todas las peticiones pasan por endpoints autenticados en el backend.
3. **Auditoría y trazabilidad:** cada recomendación del agente, cada aprobación humana y cada cambio en la planta quedan registrados en bitácora inmutable con marca de tiempo y usuario responsable.

## Errores comunes

- **Permitir que el LLM ejecute comandos directamente sobre la planta (`auto-actuate`):** una alucinación del modelo o un *prompt injection* podría causar daños físicos o paradas peligrosas.
- **Guardar API keys o tokens de webhook en el cliente web o en JSON exportados a Git:** compromete la frontera de seguridad del sistema.

## Ejercicios propuestos

1. **¿Por qué el requisito RF-A-07 prohíbe que la IA agéntica actúe de forma autónoma sobre las bombas?**
   - *Respuesta:* Porque los modelos probabilísticos pueden cometer errores o alucinaciones; mantener al humano en el lazo (*human-in-the-loop*) garantiza seguridad operacional y responsabilidad legal.
2. **¿Qué función cumple la frontera de confianza en el servidor?**
   - *Respuesta:* Validar autenticación, autorización, esquemas de datos y proteger credenciales antes de reenviar comandos hacia la planta o hacia n8n.

## Conexiones

- Documenta la estructura descrita en [[Charla automatizacion]] y el informe HIDRA en `Material/`.
- La gestión de requisitos, riesgos y alcance se vincula con [[Gerencia de Proyectos]] y [[Ingeniería de Software]].
- La supervisión ética de la IA conecta con [[Ciencia y Sociedad I]].
- Anterior: [[Automatización - Plataformas IoT: Node-RED y ThingsBoard]].

## Fuente

- Basado en `Material/Informe-Lider-Proyecto-HIDRA.docx`, [[Automatización]] y [[Charla automatizacion]].
