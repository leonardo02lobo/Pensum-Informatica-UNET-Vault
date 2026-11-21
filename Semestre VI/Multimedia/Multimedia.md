---
tags: [materia, semestre-VI]
semestre: VI
---
# Multimedia

**Semestre:** [[Semestre VI]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Base de Datos I]]

## Desbloquea
- _Ninguna_

## Apuntes

### Descripción general y objetivos
Multimedia estudia la integración de texto, imagen, audio, video y animación en sistemas informáticos: representación digital de cada medio, compresión, almacenamiento y recuperación, autoría, y distribución por la web. Está prelada por [[Base de Datos I]] porque aborda el almacenamiento y la gestión de datos multimedia. No hay Material del estudiante; el contenido se basa en el programa típico (verificar con el programa oficial).

### Contenido programático
1. **Introducción**: concepto, tipos de medios, aplicaciones, evolución.
2. **Texto y tipografía**: codificación, fuentes, hipertexto y marcado (HTML).
3. **Imagen digital**: mapa de bits y vectorial, resolución, profundidad de color, modelos RGB/CMYK/HSV, formatos (JPEG, PNG, GIF, SVG).
4. **Audio digital**: muestreo, cuantificación, formatos (WAV, MP3, OGG), MIDI.
5. **Video y animación**: fotogramas, frecuencia, códecs (H.264, VP9), contenedores (MP4, MKV), animación 2D/3D.
6. **Compresión**: sin pérdida (Huffman, LZW, RLE) y con pérdida (DCT en JPEG, modelos psicoacústicos en MP3).
7. **Bases de datos y recuperación multimedia**: almacenamiento de objetos grandes (BLOB), metadatos, búsqueda por contenido.
8. **Diseño de aplicaciones multimedia**: guion, interactividad, usabilidad, publicación y streaming.

### Conceptos clave
- **Muestreo y cuantificación**: discretizar tiempo y amplitud (Nyquist: fs ≥ 2 fmax).
- **Tasa de bits**: bits por segundo de un medio comprimido.
- **Compresión con pérdida**: descarta información poco perceptible.
- **Códec**: algoritmo que comprime y descomprime; **contenedor** empaqueta pistas.

### Fórmulas y ejemplos
```
Tamaño de imagen sin comprimir = ancho * alto * bits_por_pixel / 8   (bytes)
Audio sin comprimir (bps)      = fs * bits * canales
Video sin comprimir (bps)      = ancho * alto * bits_por_pixel * fps
Razón de compresión            = tamaño_original / tamaño_comprimido
```
- Imagen 1920x1080 a 24 bits: 1920·1080·3 = 6.22 MB.
- Audio CD: 44100·16·2 = 1.41 Mbps.
- Código de Huffman: símbolos más frecuentes reciben códigos más cortos; para A(0.5), B(0.25), C(0.25): A=0, B=10, C=11 (1.5 bits promedio).

### Relación con otras materias
Usa [[Base de Datos I]] y se enlaza con [[Desarrollo de Aplicaciones Web]], [[Comunicaciones I]] (señales y muestreo), [[Estructura de Datos]] (árboles de Huffman) y [[Interfaces Digitales Biomédicas]] (señales).

### Evaluación y consejos
- Probable evaluación con parciales y un proyecto multimedia final; verificar con el programa oficial.
- Calcula siempre tamaños con unidades; practica con herramientas (GIMP, Audacity, ffmpeg).
- Documenta formatos elegidos y su justificación.

### Bibliografía recomendada
- Vaughan, T. *Multimedia: Making it Work*. McGraw-Hill.
- Fluckiger, F. *Understanding Networked Multimedia*.
- Li, Z. y Drew, M. *Fundamentals of Multimedia*. Pearson.

### Recursos del Material/
No hay carpeta `Material/` en esta materia.
