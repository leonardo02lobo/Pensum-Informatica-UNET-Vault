---
tags: [clase, semestre-VI]
materia: Multimedia
---
# Multimedia - Audio Digital, Muestreo, Cuantificación y MIDI

Materia: [[Multimedia]]
Anterior: [[Multimedia - Imagen Digital, Modelos de Color y Formatos Gráficos]]
Siguiente: [[Multimedia - Video Digital, Animación, Códecs y Contenedores]]

## Contexto y objetivo
El sonido es una onda acústica continua (analógica) que varía en presión y tiempo. Para procesarlo, almacenarlo y transmitirlo en un computador, es necesario convertirlo en una secuencia discreta de números binarios. Este proceso conecta directamente los conceptos de señales vistos en [[Comunicaciones I]] con la ingeniería multimedia.

Al finalizar esta clase, el estudiante comprenderá el proceso de digitalización (muestreo, cuantificación y codificación), aplicará el Teorema de Nyquist-Shannon, calculará tasas de bits y tamaños de audio PCM, y distinguirá entre audio digitalizado y representación simbólica MIDI.

## 1. Digitalización del audio (PCM: Pulse Code Modulation)
Convertir una señal analógica $x(t)$ en audio digital consta de tres pasos:
1. **Muestreo (Sampling)**: tomar valores de la señal a intervalos regulares de tiempo $T_s$. La frecuencia de muestreo es $f_s = \frac{1}{T_s}$ (en Hz).
   - *Ejemplos estándar:* Telefonía ($8\text{ kHz}$), CD de audio ($44.1\text{ kHz}$), audio profesional/video ($48\text{ kHz}$).
2. **Cuantificación (Quantization)**: redondear la amplitud continua de cada muestra a uno de $2^b$ niveles discretos, donde $b$ es la **profundidad de bits** (*bit depth*).
   - El error de redondeo introduce **ruido de cuantificación**. La relación señal a ruido máxima teórica es aproximadamente:
     $$\text{SNR}_{\text{dB}} \approx 6.02\, b + 1.76\text{ dB}$$
   - Para audio de $16\text{ bits}$ (CD), $\text{SNR} \approx 98\text{ dB}$.
3. **Codificación**: representar cada nivel cuantificado como una palabra binaria.

## 2. Teorema de Muestreo de Nyquist-Shannon
Para reconstruir fielmente una señal limitada en banda cuya frecuencia máxima es $f_{\max}$ sin sufrir distorsión por solapamiento (**aliasing**), la frecuencia de muestreo debe cumplir:

$$f_s \ge 2 \cdot f_{\max}$$

- La frecuencia $f_N = 2 f_{\max}$ se denomina **tasa de Nyquist**.
- Dado que el oído humano percibe aproximadamente hasta $20\text{ kHz}$, la industria eligió $f_s = 44.1\text{ kHz}$ ($> 2 \times 20\text{ kHz}$, dejando margen para filtros antialiasing).

## 3. Tasa de bits y tamaño de audio sin comprimir
Para audio PCM sin comprimir:

$$\text{Tasa de bits (bps)} = f_s \times b \times c$$
$$\text{Tamaño (bytes)} = \frac{f_s \times b \times c \times t}{8}$$

donde $c$ es el número de canales ($1$ = mono, $2$ = estéreo) y $t$ la duración en segundos.

**Ejemplo resuelto (Audio calidad CD):** $f_s = 44\,100\text{ Hz}$, $b = 16\text{ bits}$, $c = 2$ (estéreo):
$$\text{Tasa de bits} = 44\,100 \times 16 \times 2 = 1\,411\,200\text{ bps} \approx 1.41\text{ Mbps}$$
En 1 minuto ($t = 60\text{ s}$):
$$\text{Tamaño} = \frac{1\,411\,200 \times 60}{8} = 10\,584\,000\text{ bytes} \approx 10.58\text{ MB}$$

## 4. Formatos de audio y protocolo MIDI
- **WAV / AIFF**: contenedores sin compresión (PCM lineal). Máxima fidelidad, gran tamaño; ideales para edición.
- **FLAC**: compresión **sin pérdida** (~50% de ahorro manteniendo bit a bit el audio original).
- **MP3 / AAC / OGG Vorbis**: compresión **con pérdida** basada en modelos psicoacústicos (enmascaramiento frecuencial y temporal); reducen el tamaño 8–12 veces (p. ej., $128\text{–}320\text{ kbps}$).
- **MIDI (Musical Instrument Digital Interface)**: **no almacena sonido grabado**, sino instrucciones simbólicas de eventos musicales (*qué nota tocar, con qué instrumento, cuándo inicia, cuánto dura y con qué intensidad/velocidad*). Un archivo `.mid` de 3 minutos puede pesar apenas $20\text{–}50\text{ KB}$, pero su timbre final depende del sintetizador que lo reproduzca.

## Errores comunes
- **Muestrear por debajo de $2 f_{\max}$ sin filtro paso-bajo previo**: genera frecuencias fantasma (*aliasing*) imposibles de eliminar después.
- **Confundir MIDI con MP3/WAV**: no se puede convertir directamente una grabación de voz humana a MIDI como si fuera un simple cambio de formato.
- **Recodificar de MP3 a WAV pensando que mejora la calidad**: la información descartada por el modelo psicoacústico nunca se recupera; solo aumenta el tamaño del archivo.

## Ejercicios propuestos
1. Una señal de voz telefónica se limita a $f_{\max} = 3.4\text{ kHz}$. ¿Cuál es la frecuencia mínima de muestreo según Nyquist? Si se muestrea a $8\text{ kHz}$, con $8\text{ bits}$ y 1 canal, ¿cuál es la tasa de bits?
   - *Respuesta esperada:* Nyquist mínimo: $2 \times 3.4\text{ kHz} = 6.8\text{ kHz}$. Con $8\text{ kHz}$: $8000 \times 8 \times 1 = 64\,000\text{ bps} = 64\text{ kbps}$.
2. Calcula el tamaño sin comprimir de una grabación estéreo de 3 minutos a $48\text{ kHz}$ y $24\text{ bits}$.
   - *Respuesta esperada:* $\frac{48\,000 \times 24 \times 2 \times 180}{8} = 51\,840\,000\text{ bytes} \approx 51.84\text{ MB}$.

## Conexiones
- Materia principal: [[Multimedia]]
- Anterior: [[Multimedia - Imagen Digital, Modelos de Color y Formatos Gráficos]]
- Siguiente: [[Multimedia - Video Digital, Animación, Códecs y Contenedores]]
- Relación con señales: [[Comunicaciones I]], [[Interfaces Digitales Biomédicas]]

## Fuente
Basado en el programa típico de la asignatura y en Li & Drew (*Fundamentals of Multimedia*) y Fluckiger (*Understanding Networked Multimedia*).
