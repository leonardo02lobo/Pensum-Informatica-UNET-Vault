---
tags: [clase, semestre-VI]
materia: Multimedia
---
# Multimedia - Introducción a los Sistemas Multimedia, Texto e Hipertexto

Materia: [[Multimedia]]
Anterior: _Ninguna_
Siguiente: [[Multimedia - Imagen Digital, Modelos de Color y Formatos Gráficos]]

## Contexto y objetivo
Un sistema informático moderno raramente procesa solo texto plano o tablas numéricas: integra imágenes, audio, video y animaciones de forma sincronizada e interactiva. La asignatura [[Multimedia]] estudia cómo se representan digitalmente estos medios, cómo se comprimen, almacenan, recuperan y distribuyen a través de redes y aplicaciones web.

Al finalizar esta clase, el estudiante comprenderá la definición y clasificación de los sistemas multimedia, la diferencia entre medios estáticos y continuos, y los fundamentos de la codificación de texto, tipografía, hipertexto e hipermedia.

## 1. Concepto y taxonomía de los sistemas multimedia
**Multimedia** es cualquier combinación de **texto, arte gráfico, sonido, animación y video** presentada al usuario por medios digitales. Cuando el usuario tiene control sobre qué elementos se muestran y cuándo, se habla de **multimedia interactiva**; cuando se provee una estructura de elementos enlazados por los que el usuario puede navegar, se denomina **hipermedia**.

Desde el punto de vista temporal, los medios se clasifican en:
- **Medios discretos o estáticos (independientes del tiempo)**: texto, gráficos vectoriales, imágenes de mapa de bits. Su validez no depende de una velocidad de reproducción constante.
- **Medios continuos o dinámicos (dependientes del tiempo)**: audio, video y animación. Exigen sincronización temporal estricta (flujo continuo de muestras o fotogramas por segundo) y mayor ancho de banda.

## 2. Texto y codificación de caracteres
El texto sigue siendo el medio más compacto y preciso para transmitir información y metadatos. Su representación digital asigna un código binario único a cada carácter:
- **ASCII (7 bits)**: 128 caracteres (inglés básico, dígitos y control).
- **ISO-8859-1 (Latin-1, 8 bits)**: extiende ASCII a 256 caracteres para incluir acentos y la `ñ`.
- **Unicode / UTF-8**: estándar universal actual que soporta más de 149 000 caracteres de todos los idiomas y emojis. **UTF-8** es de longitud variable (1 a 4 bytes por carácter) y mantiene compatibilidad hacia atrás con ASCII.

## 3. Tipografía digital: mapa de bits vs. vectorial
Para renderizar texto en pantalla o impresora existen dos enfoques:
- **Fuentes de mapa de bits (Raster)**: almacenan una matriz fija de píxeles para cada glifo y tamaño. Son rápidas de dibujar, pero se pixelan ("dientes de sierra") al escalarlas.
- **Fuentes vectoriales o de contorno (Outline)**: describen cada letra mediante curvas matemáticas (curvas de Bézier cuadráticas en **TrueType `.ttf`** o cúbicas en **PostScript / OpenType `.otf`**). Pueden escalarse a cualquier resolución sin perder nitidez.
- **Webfonts (WOFF / WOFF2)**: formatos comprimidos optimizados para descarga rápida en [[Desarrollo de Aplicaciones Web]].

## 4. Hipertexto, Hipermedia y Lenguajes de Marcado
El **hipertexto** (término acuñado por Ted Nelson) organiza la información de manera **no lineal** mediante nodos y enlaces (*links*). Cuando los nodos contienen además imágenes, audio y video, el sistema pasa a ser **hipermedia**.

En la web, esta estructura se implementa mediante lenguajes de marcado como **HTML5** (estructura semántica y etiquetas nativas `<audio>`, `<video>`, `<canvas>`, `<svg>`) y **CSS3** (presentación tipográfica y diseño adaptable).

```html
<article>
  <h1>Recurso Hipermedia</h1>
  <p>Consulta el <a href="#audio-guia">audio explicativo</a>.</p>
  <audio id="audio-guia" controls src="explicacion.mp3"></audio>
</article>
```

## Errores comunes
- **Usar codificaciones heredadas (Windows-1252 o Latin-1) en sistemas nuevos**: genera caracteres corruptos (`Ã¡`, `Ã±`) al interactuar con APIs modernas que esperan UTF-8.
- **Incrustar texto importante dentro de imágenes**: impide la indexación por buscadores, rompe la accesibilidad (lectores de pantalla) y degrada la legibilidad al hacer zoom.

## Ejercicios propuestos
1. Clasifica los siguientes elementos como medio discreto o continuo: (a) un diagrama SVG, (b) una pista MP3, (c) un párrafo en UTF-8, (d) un video MP4.
   - *Respuesta esperada:* Discretos: (a) diagrama SVG y (c) párrafo en UTF-8. Continuos: (b) pista MP3 y (d) video MP4.
2. ¿Cuántos bytes ocupa la palabra `"UNET"` en UTF-8 y cuántos ocuparía `"Táchira"` en UTF-8 (considerando que `á` usa 2 bytes en UTF-8)?
   - *Respuesta esperada:* `"UNET"` tiene 4 caracteres ASCII $\rightarrow 4\text{ bytes}$. `"Táchira"` tiene 6 caracteres ASCII (6 bytes) + `á` (2 bytes) = **8 bytes**.

## Conexiones
- Materia principal: [[Multimedia]]
- Siguiente: [[Multimedia - Imagen Digital, Modelos de Color y Formatos Gráficos]]
- Relación con desarrollo web: [[Desarrollo de Aplicaciones Web]]

## Fuente
Basado en el programa típico de la asignatura y en Vaughan (*Multimedia: Making it Work*) y Li & Drew (*Fundamentals of Multimedia*).
