---
tags: [clase, semestre-VI]
materia: Multimedia
---
# Multimedia - Bases de Datos Multimedia, Streaming y Diseño de Aplicaciones

Materia: [[Multimedia]]
Anterior: [[Multimedia - Compresión de Datos Multimedia sin Pérdida y con Pérdida]]
Siguiente: _Ninguna_

## Contexto y objetivo
La asignatura [[Multimedia]] está prelada por [[Base de Datos I]] porque, además de codificar y comprimir medios, un ingeniero en informática debe saber cómo **almacenar, indexar, consultar y distribuir** grandes volúmenes de objetos multimedia en aplicaciones reales y plataformas web.

Al finalizar esta clase, el estudiante comprenderá las estrategias de almacenamiento multimedia en bases de datos, los métodos de búsqueda por metadatos y por contenido (CBIR), los protocolos de *streaming* adaptativo y las etapas de diseño de una aplicación multimedia.

## 1. Almacenamiento en Bases de Datos Multimedia (MMDBMS)
Al diseñar un sistema con imágenes, audios o videos en [[Base de Datos I]], existen dos arquitecturas principales:
1. **Almacenamiento interno (BLOB - *Binary Large Object*)**: el archivo binario se guarda directamente dentro de una columna de la tabla.
   - *Ventaja:* integridad transaccional (ACID) y respaldos unificados.
   - *Desventaja:* infla rápidamente el tamaño de la BD y degrada el rendimiento de lectura.
2. **Almacenamiento externo por referencia (Recomendado en web)**: los archivos residen en el sistema de archivos o en almacenamiento de objetos (S3, MinIO, CDN) y la base de datos guarda únicamente la **ruta/URL** junto con sus **metadatos** (tipo MIME, tamaño, duración, resolución, hash).

## 2. Recuperación de Información Multimedia: Metadatos vs. CBIR
- **Búsqueda basada en metadatos/etiquetas**: consulta SQL tradicional sobre campos estructurados (título, autor, fecha, etiquetas EXIF/ID3). Es rápida y exacta, pero depende de que alguien haya etiquetado manualmente el recurso.
- **CBIR (*Content-Based Image Retrieval* / Búsqueda por contenido)**: extrae automáticamente **vectores de características** visuales o acústicas (histogramas de color, descriptores de textura, forma, huellas digitales de audio) y busca objetos similares midiendo distancias vectoriales (euclidiana o coseno) en el espacio de características.

## 3. Distribución en Red y *Streaming* Adaptativo
Distribuir audio y video por internet requiere equilibrar latencia y estabilidad:
- **Descarga progresiva**: el navegador descarga el archivo MP4 por HTTP desde el inicio y empieza a reproducir mientras descarga. No se adapta si cae el ancho de banda.
- **Streaming adaptativo (HLS - *HTTP Live Streaming*, MPEG-DASH)**: divide el video en pequeños segmentos de pocos segundos (p. ej. 2–6 s) codificados en múltiples calidades (360p, 720p, 1080p). El reproductor mide continuamente la velocidad de red del cliente y cambia de calidad dinámicamente sin detener la reproducción.
- **Streaming en tiempo real de baja latencia (WebRTC, RTP/RTSP)**: usado en videoconferencias y transmisiones interactivas donde el retardo debe ser mínimo ($< 300\text{ ms}$).

## 4. Ciclo de Diseño de una Aplicación Multimedia
El desarrollo de un producto multimedia (educativo, informativo o web) sigue fases estructuradas:
1. **Análisis y concepto**: definir público objetivo, requisitos técnicos y plataformas de destino.
2. **Diseño y guionización (*Storyboarding*)**: elaborar el **guion literario** (contenido), **guion técnico** (medios por pantalla) y **mapa de navegación** (estructura interactiva).
3. **Producción de activos**: captura/edición de gráficos, audio y video en formatos optimizados.
4. **Autoría e integración**: ensamblaje en la herramienta o framework web ([[Desarrollo de Aplicaciones Web]]).
5. **Pruebas de usabilidad, accesibilidad y publicación**: verificar contraste, subtítulos para personas con discapacidad auditiva, textos alternativos (`alt`) y tiempos de carga.

## Errores comunes
- **Guardar videos de cientos de megabytes como BLOB dentro de una BD relacional**: bloquea conexiones y dificulta la entrega mediante CDN.
- **Publicar un único archivo MP4 de 4K para usuarios móviles**: sin *streaming* adaptativo ni versiones reducidas, los usuarios con conexiones lentas sufren cortes constantes (*buffering*).

## Ejercicios propuestos
1. Estás diseñando una plataforma educativa en la UNET con 500 videoclases. ¿Almacenarías los videos como BLOB en PostgreSQL o por referencia en almacenamiento de objetos? Justifica tu respuesta.
   - *Respuesta esperada:* Por referencia en almacenamiento de objetos/CDN (guardando en PostgreSQL solo URLs, duración, tema y metadatos), ya que evita saturar la BD, permite servir los videos mediante HLS/DASH y facilita el escalado.
2. ¿Qué ventaja ofrece HLS o MPEG-DASH frente a la descarga progresiva de un archivo MP4?
   - *Respuesta esperada:* Permite cambiar dinámicamente la resolución/bitrate según el ancho de banda disponible del usuario en tiempo real, evitando interrupciones de reproducción.

## Conexiones
- Materia principal: [[Multimedia]]
- Anterior: [[Multimedia - Compresión de Datos Multimedia sin Pérdida y con Pérdida]]
- Prelación de bases de datos: [[Base de Datos I]]
- Integración web y redes: [[Desarrollo de Aplicaciones Web]], [[Comunicaciones I]]

## Fuente
Basado en el programa típico de la asignatura, Vaughan (*Multimedia: Making it Work*) y Fluckiger (*Understanding Networked Multimedia*).
