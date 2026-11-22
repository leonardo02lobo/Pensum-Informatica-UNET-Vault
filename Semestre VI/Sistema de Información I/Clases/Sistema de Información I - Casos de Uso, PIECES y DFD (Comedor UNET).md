---
tags: [clase, semestre-VI, analisis, dfd, casos-de-uso]
materia: Sistema de Información I
---
# Sistema de Información I - Casos de Uso, PIECES y DFD (Comedor UNET)

Materia: [[Sistema de Información I]]
Anterior: _Ninguna_
Siguiente: _Ninguna_

## Contexto y objetivo

Material práctico extraído de Google Drive (Diciembre 2025 – Marzo 2026) aplicando técnicas de análisis de sistemas al **Sistema del Comedor Universitario UNET** y a un **Sistema de Gestión de Soporte Técnico** y **Sistema de Compras UNET**.

## 1. Identificación de Actores y Casos de Uso (Comedor UNET)

- **Actores principales:** `Estudiante`, `Personal Obrero`, `Administrador`.
- **Casos de uso clave:**
  - Generación y escaneo de ticket QR / carnet en taquilla.
  - Gestión de menú diario y control de stock/inventario.
  - Registro y seguimiento de incidencias operativas.

## 2. Marco PIECES y Clasificación de Sistemas (Parcial 2)

- **Análisis PIECES** (aplicado a Soporte Técnico): evaluación de **P**erformance (rendimiento), **I**nformation (información), **E**conomics (economía), **C**ontrol (seguridad/control), **E**fficiency (eficiencia) y **S**ervice (servicio).
- **Clasificación de sistemas:** TPS (procesamiento de transacciones), MIS (información gerencial), DSS (soporte a decisiones), Sistemas de Inventarios y Workflow.

## 3. Errores comunes en DFD (Nivel 0 y Nivel 1)

Detectados en el ejercicio del *Sistema de Compras UNET*:
- **Flujos directos entre entidades externas** sin pasar por un proceso.
- **Almacenes de datos conectados directamente** entre sí sin un proceso intermedio.
- **Desbalanceo entre Nivel 0 (Contexto) y Nivel 1:** flujos de entrada/salida que aparecen en el Nivel 1 pero no existen en el Diagrama de Contexto (o viceversa).
- **Procesos "agujero negro"** (tienen entradas pero ninguna salida) o **"milagro"** (producen salidas sin entradas).

## Recursos en Google Drive

- [Técnicas de Identificación de Actores y Casos de Uso (Comedor UNET)](https://docs.google.com/document/d/1yppcSLI5BF4iLSAIksVASMeRn5TUoVAI5D-8OVMT6g8/edit?usp=drivesdk)
- [Sistema de Información I · Parte 2 Parcial (PIECES, DER, DFD)](https://docs.google.com/document/d/1eU-sxqSd0wfCNoHyuilu0sls4dPErha0IuasGdO4yjs/edit?usp=drivesdk)

## Conexiones

- Se conecta con [[Sistema Comedor Universitario UNET (CSC-P 2026)]] y [[Base de Datos I]].
- Prepara el diseño detallado para [[Sistema de Información II]] e [[Ingeniería de Software]].
