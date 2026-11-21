---
tags: [tema, semestre-VII]
semestre: VII
---
# SFTP-U Protocolo sobre UDP

Nota hija de [[Comunicaciones II]]. Resume el Parcial III (`~/Documentos/UNET/Comunicaciones 2/parcial 3`).

## Idea
Diseño, adversidad y robustecimiento de un protocolo de **capa de aplicación** para transferir archivos sobre UDP. El proyecto contiene dos versiones deliberadas:

- **v1 (ingenua)**: sin checksum, sin números de secuencia, sin confirmaciones. Es la línea base y **debe fallar** ante pérdida, duplicación, reordenamiento o corrupción. Es vulnerable a propósito (solo uso académico).
- **v2 (robusta)**: CRC32 por paquete, SHA-256 del archivo, ACK/NACK, temporizadores con **retroceso exponencial** y ventana deslizante **Go-Back-N**.

## Piezas
- Servidor en Python 3.11+ (biblioteca estándar), cliente en Node.js 18+, un **adversario** en Python con YAML que simula pérdida, duplicados, reordenamiento y corrupción, y captura opcional con `tshark`.
- La lógica de confiabilidad (ARQ, temporizadores, ventana) es código propio porque es el objeto de la evaluación.

## Fases (resumen)
1. Diseño del protocolo (formato de mensaje y máquina de estados).
2. Medición de v1 bajo adversidad (falla).
3. Robustecimiento (v2).
4. Comparación v1 vs v2 con métricas (tasa de éxito, retransmisiones, tiempo).

## Conceptos
Checksum vs hash; ARQ; Go-Back-N frente a Selective Repeat; idempotencia ante duplicados; retroceso exponencial para evitar congestión.
