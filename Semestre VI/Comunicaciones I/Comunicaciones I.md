---
tags: [materia, semestre-VI]
semestre: VI
---
# Comunicaciones I

**Semestre:** [[Semestre VI]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Organización del Computador]]

## Desbloquea
- [[Comunicaciones II]]

## Apuntes

### Descripción general y objetivos
Comunicaciones I introduce los fundamentos de la transmisión de información: señales, medios, modulación, multiplexación, codificación y los principios de las redes de datos y los protocolos que conectan computadores. Objetivo: comprender cómo se representa, transmite y protege la información a través de un canal y cómo se organiza la comunicación en capas. No hay Material del estudiante; el contenido sigue el programa típico (verificar con el programa oficial).

### Contenido programático
1. **Conceptos básicos**: modelo de comunicación (emisor, canal, receptor), ruido, simplex/half/full duplex, redes y topologías.
2. **Señales y análisis de Fourier**: señales analógicas y digitales, ancho de banda, serie de Fourier, espectro.
3. **Medios de transmisión**: par trenzado, coaxial, fibra óptica, inalámbrico; atenuación, distorsión, diafonía.
4. **Límites del canal**: teorema de Nyquist, capacidad de Shannon.
5. **Codificación y modulación**: codificación de línea (NRZ, Manchester), ASK, FSK, PSK, QAM; conversión analógico-digital (PCM, muestreo).
6. **Multiplexación**: FDM, TDM, WDM.
7. **Detección y corrección de errores**: paridad, CRC, códigos de Hamming.
8. **Control del enlace y modelos de capas**: tramas, control de flujo, ARQ, modelo OSI y TCP/IP.

### Conceptos clave
- **Ancho de banda (Hz)** y **tasa de datos (bps)**; **baudios** = símbolos por segundo.
- **SNR** = potencia de señal / potencia de ruido; `SNR_dB = 10 log10(S/N)`.
- **Modulación**: variar amplitud, frecuencia o fase de una portadora.
- **Eficiencia espectral** (bps/Hz).

### Fórmulas
```
Nyquist (canal sin ruido):  C = 2 B log2(M)
Shannon (canal con ruido):  C = B log2(1 + SNR)
Muestreo (Nyquist):         f_s >= 2 f_max
Hamming: 2^r >= m + r + 1
```
Ejemplo de CRC con generador x^3+x+1 (1011), datos 1101: se agregan 3 ceros (1101000) y se divide módulo 2 entre 1011; el resto (001) es el CRC, trama enviada 1101001.

### Ejemplos resueltos
- Canal telefónico B=3100 Hz, SNR=30 dB (=1000): `C = 3100·log2(1001) ≈ 30.9 kbps`.
- Voz muestreada a 8000 Hz con 8 bits: 64 kbps (PCM).

### Relación con otras materias
Prelada por [[Organización del Computador]]; desbloquea [[Comunicaciones II]]. Se relaciona con [[Introducción a las Telecomunicaciones]], [[Administración de Redes]], [[Sistemas Distribuidos]], [[Sistemas Operativos]] y [[Automatización]] (protocolos industriales y MQTT).

### Evaluación y consejos
- Parciales con problemas numéricos (Shannon, Nyquist, PCM, CRC) y teoría de capas.
- Aprende las fórmulas con sus unidades y practica conversiones dB.
- Dibuja las formas de onda de codificaciones y modulaciones.

### Bibliografía recomendada
- Stallings, W. *Comunicaciones y Redes de Computadores*. Pearson.
- Tanenbaum, A. *Redes de Computadoras*.
- Forouzan, B. *Transmisión de Datos y Redes de Comunicaciones*. McGraw-Hill.

### Recursos del Material/
No hay carpeta `Material/` en esta materia.
