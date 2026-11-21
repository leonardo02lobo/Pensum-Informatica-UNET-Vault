---
tags: [clase, semestre-VI]
materia: Multimedia
---
# Multimedia - Video Digital, Animación, Códecs y Contenedores

Materia: [[Multimedia]]
Anterior: [[Multimedia - Audio Digital, Muestreo, Cuantificación y MIDI]]
Siguiente: [[Multimedia - Compresión de Datos Multimedia sin Pérdida y con Pérdida]]

## Contexto y objetivo
El video digital combina la complejidad espacial de las imágenes con la exigencia temporal continua del sonido. Sin técnicas avanzadas de compresión, transmitir o almacenar video en alta definición sería inviable por su enorme volumen de datos.

Al finalizar esta clase, el estudiante comprenderá cómo se forma la ilusión de movimiento, calculará tasas de bits de video sin comprimir, distinguirá claramente entre **códec** y **contenedor**, y conocerá los fundamentos de la animación 2D/3D y el uso práctico de herramientas como `ffmpeg`.

## 1. Fundamentos del video digital
El video aprovecha el fenómeno de la **persistencia retiniana** y el movimiento aparente: una sucesión rápida de imágenes fijas (**fotogramas** o *frames*) se percibe como movimiento continuo.
- **Tasa de fotogramas (FPS - *Frames Per Second*)**:
  - Cine tradicional: $24\text{ fps}$.
  - Televisión / Web estándar: $25\text{ fps}$ (PAL) o $29.97/30\text{ fps}$ (NTSC).
  - Videojuegos, deportes y fluidez alta: $60\text{ fps}$ o más.
- **Exploración progresiva vs. entrelazada**: el video progresivo (`1080p`) dibuja todas las líneas de cada fotograma en orden; el entrelazado (`1080i`, heredado de TV analógica) alterna líneas pares e impares en campos sucesivos.

### Cálculo de tasa de bits sin comprimir
$$\text{Bitrate video (bps)} = W \times H \times b \times \text{fps}$$

**Ejemplo resuelto:** Video Full HD ($1920 \times 1080$) a $24\text{ bits}$ y $30\text{ fps}$ sin comprimir:
$$\text{Bitrate} = 1920 \times 1080 \times 24 \times 30 = 1\,492\,992\,000\text{ bps} \approx 1.49\text{ Gbps}$$
Un solo minuto ocuparía $\frac{1.493 \times 10^9 \times 60}{8} \approx 11.2\text{ GB}$, lo que demuestra por qué la compresión es obligatoria.

## 2. Submuestreo de crominancia (YCbCr 4:4:4, 4:2:2, 4:2:0)
El ojo humano es mucho más sensible a los cambios de **luminancia** ($Y$, brillo) que a los cambios de **crominancia** ($C_b, C_r$, color). Los estándares de video aprovechan esto reduciendo la resolución espacial del color:
- **4:4:4**: sin submuestreo (máxima fidelidad, edición de cine).
- **4:2:2**: la crominancia se muestrea a la mitad en horizontal.
- **4:2:0**: la crominancia se muestrea a la mitad en horizontal y vertical (ahorra el **50%** de datos antes de comprimir; es el estándar de YouTube, Netflix, H.264 y Blu-ray).

## 3. Códec vs. Contenedor
Es un error común confundir la extensión del archivo con el algoritmo de compresión:
- **Códec (*Codificador-Decodificador*)**: algoritmo matemático que comprime y descomprime una pista individual de video o audio.
  - *Códecs de video:* H.264 (AVC), H.265 (HEVC), VP9, AV1.
  - *Códecs de audio:* AAC, Opus, MP3, AC-3.
- **Contenedor (Formato de archivo)**: "caja" o empaquetado que agrupa múltiples pistas (video, audio, subtítulos, capítulos, metadatos) sincronizadas por marcas de tiempo.
  - *Contenedores comunes:* **MP4** (`.mp4`, estándar web universal), **MKV** (`.mkv`, Matroska, muy flexible), **WebM** (`.webm`, abierto para web con VP9/AV1 + Opus).

```bash
# Ejemplo práctico con ffmpeg: recodificar video a H.264 + audio AAC en contenedor MP4
ffmpeg -i entrada.mkv -c:v libx264 -crf 23 -c:a aac -b:a 128k salida.mp4
```

## 4. Principios de Animación 2D y 3D
A diferencia del video capturado por cámara, la animación genera imágenes sintéticas:
- **Animación por fotogramas clave (*Keyframing*)**: el animador define poses principales en instantes clave y el software calcula los cuadros intermedios (**interpolación / *tweening***).
- **Animación 2D**: capas vectoriales, *sprites*, esqueletos 2D (*rigging*).
- **Animación 3D**: modelado poligonal, texturizado, *rigging* (huesos), iluminación y **renderizado** (rasterización en tiempo real o *ray tracing* para cine).

## Errores comunes
- **Llamar "códec" al MP4**: MP4 es un contenedor; dentro puede tener H.264, H.265 o MPEG-4 Part 2, por lo que dos archivos `.mp4` pueden tener compatibilidad distinta.
- **Subir video sin comprimir o con bitrate excesivo a plataformas web**: genera tiempos de espera largos sin mejora visual perceptible para el usuario final.

## Ejercicios propuestos
1. Calcula la tasa de bits (en Mbps) de un video HD ($1280 \times 720$) a $24\text{ bits}$ y $60\text{ fps}$ sin comprimir.
   - *Respuesta esperada:* $1280 \times 720 \times 24 \times 60 = 1\,327\,104\,000\text{ bps} \approx 1327.1\text{ Mbps}$.
2. Explica la diferencia entre un códec (p. ej. H.264) y un contenedor (p. ej. MKV).
   - *Respuesta esperada:* El códec comprime y descomprime el flujo de video o audio; el contenedor empaqueta y sincroniza en un solo archivo las pistas de video, audio, subtítulos y metadatos.

## Conexiones
- Materia principal: [[Multimedia]]
- Anterior: [[Multimedia - Audio Digital, Muestreo, Cuantificación y MIDI]]
- Siguiente: [[Multimedia - Compresión de Datos Multimedia sin Pérdida y con Pérdida]]

## Fuente
Basado en el programa típico de la asignatura y en Li & Drew (*Fundamentals of Multimedia*).
