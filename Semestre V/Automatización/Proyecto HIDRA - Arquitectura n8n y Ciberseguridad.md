---
tags: [proyecto, semestre-V, automatizacion, n8n, ciberseguridad]
materia: Automatización
---
# Proyecto HIDRA · Arquitectura n8n y Ciberseguridad

Materia: [[Automatización]]

## Resumen del proyecto

El **Proyecto HIDRA** (Grupo 4, Automatización Industrial, Agosto 2026) implementa la supervisión y operación de un sistema de bombeo industrial combinando lógica de control determinista, una interfaz HMI web y una capa de **IA agéntica en n8n** bajo el principio estricto *human-in-the-loop* (`RF-A-07`: *"la IA propone, el humano dispone"*).

## 1. Arquitectura en 3 capas

1. **Capa PM (Gestión):** Especificación de **63 requisitos** (50 funcionales: `RF-P` proceso, `RF-S` seguridad, `RF-A` IA agéntica, `RF-H` interfaz HMI; y 13 no funcionales `RNF`), gestión de riesgos y alcance.
2. **Capa IA Agéntica (n8n + LLM):** Orquestada en **n8n** con 5 flujos especializados:
   - `F1`: Diagnóstico causal de alarmas.
   - `F2`: Informe automático de turno.
   - `F3`: Vigilancia periódica de bitácora (cada 15 min).
   - `F4`: Recomendación de consignas (siempre requiere aprobación humana).
   - `F5`: Consulta operativa en lenguaje natural.
3. **Capa Planta (Web / Vercel):** Simulación de bombeo con paso fijo de **50 ms**, temporizadores `TON`/`TOF`/`TP` conformes a **IEC 61131-3**, e interfaz HMI en Canvas diseñada bajo estándares **ISA-101** y accesibilidad **WCAG 2.2 AA**.

## 2. Controles de Ciberseguridad y Auditoría

Según `Auditoria-Ciberseguridad-Hidra`:
- **Autenticación y sesiones:** Contraseñas con **Argon2id** (y comparación segura `crypto.timingSafeEqual`), cookies `HttpOnly`, `Secure` y `SameSite=Strict`, y control de acceso **RBAC** en servidor.
- **Integridad de comandos y auditoría:** Gateway de comandos firmado (nonce con `crypto.randomBytes` + secuencia), webhooks/callbacks firmados servidor-a-servidor y bitácora encadenada por hashes.
- **Escaneo DAST:** Auditoría con **OWASP ZAP v2.17.0** sobre `https://hidra-seven.vercel.app` (0 alertas críticas o altas).

## Recursos en Google Drive

- [Informe-Lider-Proyecto-HIDRA.docx](https://docs.google.com/document/d/1s2DUp0DWsFLfGwXQpeVLDCm6vNU1mdxP/edit?usp=drivesdk)
- [Auditoria-Ciberseguridad-Hidra](https://docs.google.com/document/d/1VnX8nrE5jgpvMCPlf3uQWgMVRaMXH5c8rRwcMM57yl4/edit?usp=drivesdk)

## Conexiones

- Complementa [[Charla automatizacion]], [[Investigacion_NodeRED_ThingsBoard]] y [[Practica 1]].
- Se relaciona con [[Sistemas Operativos]] (tiempo real y procesos) y [[Gerencia de Proyectos]].
