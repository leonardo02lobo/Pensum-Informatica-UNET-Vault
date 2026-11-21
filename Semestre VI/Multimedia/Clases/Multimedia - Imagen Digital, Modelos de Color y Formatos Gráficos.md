---
tags: [clase, semestre-VI]
materia: Multimedia
---
# Multimedia - Imagen Digital, Modelos de Color y Formatos Gráficos

Materia: [[Multimedia]]
Anterior: [[Multimedia - Introducción a los Sistemas Multimedia, Texto e Hipertexto]]
Siguiente: [[Multimedia - Audio Digital, Muestreo, Cuantificación y MIDI]]

## Contexto y objetivo
La imagen es el componente visual central de casi toda aplicación multimedia. Elegir incorrectamente entre gráficos vectoriales o mapas de bits, o seleccionar un modelo de color o formato inadecuado, produce archivos innecesariamente pesados, colores alterados al imprimir o logotipos borrosos.

Al finalizar esta clase, el estudiante distinguirá entre imágenes raster y vectoriales, calculará tamaños de imagen sin comprimir, comprenderá los modelos de color RGB, CMYK y HSV, y sabrá seleccionar el formato gráfico óptimo (JPEG, PNG, GIF, WebP, SVG).

## 1. Mapa de bits (Raster) vs. Gráficos Vectoriales
- **Mapa de bits (Bitmap / Raster)**: la imagen se representa como una matriz bidimensional de $W \times H$ elementos llamados **píxeles** (*picture elements*). Es ideal para fotografías y escenas complejas con gradientes continuos, pero depende de la resolución (al ampliar demasiado aparece pixelación).
- **Gráfico vectorial**: la imagen se define mediante primitivas geométricas (líneas, polígonos, curvas de Bézier) expresadas como ecuaciones matemáticas. Es independiente de la resolución, ocupa muy poco espacio para logotipos, iconos y diagramas, y se edita fácilmente.

## 2. Resolución y Profundidad de Color
- **Resolución espacial**: dimensiones en píxeles ($W \times H$, p. ej. $1920 \times 1080$). Para impresión se expresa en **PPP / DPI** (*píxeles/puntos por pulgada*; estándar de imprenta: $300\text{ DPI}$, pantalla: $72\text{–}96\text{ DPI}$ o superior en pantallas HiDPI).
- **Profundidad de color ($b$)**: número de bits asignados a cada píxel. Con $b$ bits se pueden representar $2^b$ colores distintos:
  - $b = 1$: binario / blanco y negro ($2^1 = 2$ colores).
  - $b = 8$: escala de grises o color indexado ($2^8 = 256$ niveles/colores).
  - $b = 24$: **Color verdadero (True Color)**, 8 bits por canal R, G y B ($2^{24} \approx 16.7$ millones de colores).
  - $b = 32$: True Color + canal Alfa de transparencia (RGBA, 8 bits por canal).

### Cálculo de tamaño sin comprimir
$$\text{Tamaño (bytes)} = \frac{W \times H \times b}{8}$$

**Ejemplo resuelto:** Una imagen Full HD de $1920 \times 1080$ píxeles a $24\text{ bits}$ de profundidad:
$$\text{Tamaño} = \frac{1920 \times 1080 \times 24}{8} = 6\,220\,800\text{ bytes} \approx 6.22\text{ MB (o } 5.93\text{ MiB)}$$

## 3. Modelos de Color: RGB, CMYK y HSV
- **RGB (Red, Green, Blue)**: modelo **aditivo** basado en luz emitida (monitores, televisores, cámaras). La suma máxima $(255, 255, 255)$ produce blanco; $(0, 0, 0)$ produce negro.
- **CMYK (Cyan, Magenta, Yellow, Key/Black)**: modelo **sustractivo** basado en tintas que absorben luz sobre papel (impresión). Se añade negro ($K$) porque la mezcla física de C+M+Y genera un marrón oscuro impuro y consume mucha tinta.
- **HSV / HSB (Hue, Saturation, Value/Brightness)**: modelo perceptual más cercano a cómo los humanos describen el color: **Matiz** ($0^\circ\text{–}360^\circ$), **Saturación** ($0\text{–}100\%$) y **Valor/Brillo** ($0\text{–}100\%$). Muy usado en selectores de color y visión por computador.

## 4. Comparativa de formatos gráficos
| Formato | Tipo | Compresión | Transparencia | Uso recomendado |
| :--- | :--- | :--- | :---: | :--- |
| **JPEG (.jpg)** | Raster | Con pérdida (DCT) | No | Fotografías y escenas naturales |
| **PNG (.png)** | Raster | Sin pérdida (DEFLATE) | Sí (Alfa 8-bit) | Capturas de UI, gráficos con texto, transparencias |
| **GIF (.gif)** | Raster | Sin pérdida (LZW), máx. 256 colores | Sí (1-bit) | Animaciones simples heredadas |
| **WebP (.webp)** | Raster | Con o sin pérdida | Sí | Web moderna (menor peso que JPEG/PNG) |
| **SVG (.svg)** | Vectorial | Texto XML / gzip | Sí | Logotipos, iconos, diagramas escalables |

## Errores comunes
- **Guardar capturas de texto o logotipos en JPEG**: la compresión con pérdida genera artefactos ("manchas") alrededor de bordes nítidos y letras.
- **Enviar archivos RGB sin perfil de conversión a imprenta**: ciertos tonos neón de pantalla no existen en la gama CMYK y se ven apagados al imprimir.
- **Usar imágenes de 4000×3000 px en una tarjeta web de 300×200 px**: desperdicia ancho de banda y ralentiza la carga de la página.

## Ejercicios propuestos
1. Calcula el tamaño sin comprimir (en MiB y MB) de una imagen RGBA (32 bits) de $1280 \times 720$ píxeles.
   - *Respuesta esperada:* $\frac{1280 \times 720 \times 32}{8} = 3\,686\,400\text{ bytes} = 3.69\text{ MB} \approx 3.52\text{ MiB}$.
2. ¿Qué formato elegirías para: (a) el logotipo de una empresa en una página web, y (b) una fotografía de paisaje en una galería?
   - *Respuesta esperada:* (a) **SVG** (vectorial, nítido en cualquier pantalla y liviano); (b) **JPEG** o **WebP con pérdida** (alta compresión para tonos continuos).

## Conexiones
- Materia principal: [[Multimedia]]
- Anterior: [[Multimedia - Introducción a los Sistemas Multimedia, Texto e Hipertexto]]
- Siguiente: [[Multimedia - Audio Digital, Muestreo, Cuantificación y MIDI]]
- Profundización en compresión: [[Multimedia - Compresión de Datos Multimedia sin Pérdida y con Pérdida]]

## Fuente
Basado en el programa típico de la asignatura y en Li & Drew (*Fundamentals of Multimedia*).
