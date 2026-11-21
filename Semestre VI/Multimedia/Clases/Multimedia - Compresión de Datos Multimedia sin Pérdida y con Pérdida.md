---
tags: [clase, semestre-VI]
materia: Multimedia
---
# Multimedia - Compresión de Datos Multimedia sin Pérdida y con Pérdida

Materia: [[Multimedia]]
Anterior: [[Multimedia - Video Digital, Animación, Códecs y Contenedores]]
Siguiente: [[Multimedia - Bases de Datos Multimedia, Streaming y Diseño de Aplicaciones]]

## Contexto y objetivo
La compresión de datos es el corazón técnico de los sistemas multimedia: permite almacenar miles de canciones o transmitir video en tiempo real reduciendo redundancias estadísticas y perceptuales. Además, conecta directamente con las estructuras de árboles binarios vistas en [[Estructura de Datos]].

Al finalizar esta clase, el estudiante calculará razones de compresión, aplicará algoritmos sin pérdida (RLE, Huffman, LZW) y comprenderá los principios de la compresión con pérdida en imagen (DCT en JPEG), audio (psicoacústica) y video (predicción temporal).

## 1. Métricas de compresión y tipos de redundancia
$$\text{Razón de compresión } (C_R) = \frac{\text{Tamaño original}}{\text{Tamaño comprimido}}, \qquad \text{Ahorro (\%)} = \left(1 - \frac{1}{C_R}\right) \times 100\%$$

La compresión explota tres tipos de redundancia:
1. **Redundancia estadística / de codificación**: algunos símbolos aparecen con mucha más frecuencia que otros.
2. **Redundancia espacial / inter-píxel**: píxeles vecinos en una imagen suelen tener colores muy similares.
3. **Redundancia psico-visual o psicoacústica (irrelevancia)**: información que el ojo o el oído humano no perciben (base de la compresión **con pérdida**).

## 2. Compresión sin pérdida (*Lossless*)
Permite reconstruir el archivo original **exactamente bit a bit**.
- **RLE (Run-Length Encoding)**: reemplaza secuencias repetidas por un contador y el símbolo.
  - *Ejemplo:* `AAAAABBBCC` $\rightarrow$ `5A3B2C` (10 caracteres $\rightarrow$ 6 caracteres). Muy útil en imágenes simples con grandes áreas planas, ineficiente en ruido o fotos.
- **Codificación de Huffman**: asigna códigos binarios de longitud variable más cortos a los símbolos más frecuentes, garantizando códigos **prefijo** (ningún código es prefijo de otro) mediante un árbol binario construido en [[Estructura de Datos]].
  - *Ejemplo resuelto:* Símbolos con probabilidades $P(A)=0.5$, $P(B)=0.25$, $P(C)=0.25$.
    Se asigna $A = \texttt{0}$ (1 bit), $B = \texttt{10}$ (2 bits), $C = \texttt{11}$ (2 bits).
    Longitud promedio por símbolo:
    $$L = 0.5(1) + 0.25(2) + 0.25(2) = 1.5\text{ bits/símbolo}$$
    (Frente a $2\text{ bits/símbolo}$ en codificación fija, $C_R = 2 / 1.5 = 1.33$).
- **LZW (Lempel-Ziv-Welch)**: construye dinámicamente un diccionario de secuencias repetidas conforme lee los datos (usado en GIF, TIFF y variantes en ZIP/PNG).

## 3. Compresión con pérdida (*Lossy*)
Descarta información poco perceptible para lograr razones de compresión mucho mayores ($10:1$ a $50:1$):
- **Imagen (JPEG)**:
  1. Convierte RGB a $YC_bC_r$ y aplica submuestreo `4:2:0`.
  2. Divide la imagen en bloques de $8 \times 8$ píxeles.
  3. Aplica la **DCT (Transformada Discreta del Coseno)**, pasando del dominio espacial al dominio de frecuencias (energía concentrada en bajas frecuencias).
  4. **Cuantificación** (paso con pérdida): divide por una matriz de cuantificación y redondea, anulando muchas frecuencias altas casi imperceptibles.
  5. Recorrido en zig-zag + RLE + Huffman.
- **Audio (MP3 / AAC)**: usa bancos de filtros y un **modelo psicoacústico** que elimina sonidos débiles ocultos por otros más fuertes en frecuencias cercanas (**enmascaramiento frecuencial**) o justo antes/después de un sonido intenso (**enmascaramiento temporal**).
- **Video (H.264 / H.265)**: combina compresión espacial (intra-cuadro) con **predicción temporal (inter-cuadro)** mediante **estimación y compensación de movimiento** entre tres tipos de cuadros:
  - **Cuadros I (*Intra*)**: imagen completa comprimida independientemente (como un JPEG).
  - **Cuadros P (*Predicted*)**: almacenan solo diferencias y vectores de movimiento respecto a un cuadro anterior.
  - **Cuadros B (*Bi-predictive*)**: predicen usando tanto cuadros anteriores como futuros (máxima compresión).

## Errores comunes
- **Aplicar RLE a texto natural o fotografías ruidosas**: puede terminar generando un archivo **más grande** que el original.
- **Editar y re-guardar un JPEG repetidamente**: cada guardado aplica nuevamente cuantificación DCT y degrada progresivamente la imagen (*generation loss*).

## Ejercicios propuestos
1. Un archivo de audio WAV de $30\text{ MB}$ se comprime a MP3 quedando en $3\text{ MB}$. Calcula la razón de compresión y el porcentaje de ahorro.
   - *Respuesta esperada:* $C_R = \frac{30}{3} = 10$ (razón $10:1$). Ahorro: $\left(1 - \frac{1}{10}\right) \times 100\% = 90\%$.
2. Construye códigos de Huffman válidos para los símbolos $X(0.4), Y(0.3), Z(0.2), W(0.1)$ y calcula la longitud promedio $L$.
   - *Respuesta esperada:* Agrupando $Z$ y $W$ ($0.3$), luego $(Z,W)$ con $Y$ ($0.6$), se obtiene por ejemplo: $X=\texttt{0}$ (1 bit), $Y=\texttt{10}$ (2 bits), $Z=\texttt{110}$ (3 bits), $W=\texttt{111}$ (3 bits). $L = 0.4(1) + 0.3(2) + 0.2(3) + 0.1(3) = 1.9\text{ bits/símbolo}$.

## Conexiones
- Materia principal: [[Multimedia]]
- Anterior: [[Multimedia - Video Digital, Animación, Códecs y Contenedores]]
- Siguiente: [[Multimedia - Bases de Datos Multimedia, Streaming y Diseño de Aplicaciones]]
- Estructuras de soporte: [[Estructura de Datos]] (árboles de Huffman)

## Fuente
Basado en el programa típico de la asignatura y en Li & Drew (*Fundamentals of Multimedia*).
