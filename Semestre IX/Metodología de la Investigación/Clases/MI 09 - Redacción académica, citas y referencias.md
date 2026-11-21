---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 09 - Redacción académica, citas y referencias

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 08 - Estadística aplicada a la investigación]]

## Contexto y objetivo
Una buena investigación mal comunicada pierde valor. Esta clase trata la escritura científico-técnica, el manejo de citas y referencias (APA 7 como estándar de referencia; verificar si la UNET exige APA, IEEE o la norma UPEL), y la integridad académica. Cierra el ciclo con la estructura del documento ([[Estructura del anteproyecto de investigación]], [[Estructura del informe de trabajo de grado]]).

## Principios de la escritura académica
1. **Claridad**: una idea por párrafo; oraciones de 15-25 palabras; voz activa o impersonal consistente ("se desarrolló", "se aplicó").
2. **Precisión**: términos técnicos definidos; cifras con unidades.
3. **Objetividad**: evitar adjetivos valorativos sin evidencia ("excelente", "muy bueno").
4. **Coherencia y cohesión**: conectores lógicos (además, sin embargo, por consiguiente, en consecuencia).
5. **Concisión**: eliminar redundancias ("subir para arriba").
6. **Estructura del párrafo**: oración temática + desarrollo (evidencia/cita) + cierre o transición.
7. **Registro formal**: sin coloquialismos ni primera persona excesiva (según la norma de la institución).

Proceso: planificar (esquema), escribir un borrador sin autocensura, revisar el contenido (argumento), luego estilo y por último ortografía; pedir lectura a un compañero; la ortografía y la gramática son parte de la evaluación ([[Lenguaje y Comunicación]]).

## Estructura IMRyD (artículos y buena parte de informes)
**I**ntroducción (problema, brecha, objetivo), **M**étodos (replicable), **R**esultados (sin interpretar), **D**iscusión (interpretar, comparar con la literatura, limitaciones), más conclusiones y referencias. Resumen (abstract) de 150-250 palabras con: contexto, objetivo, método, resultados clave y conclusión; palabras clave.

## Citas
Una **cita** da crédito a la fuente de ideas o textos ajenos. Dos formas:
- **Parafraseada** (preferible): reformulas con tus palabras y citas igual.
- **Textual (directa)**: entre comillas; si tiene menos de 40 palabras va en el párrafo; si tiene 40 o más, en bloque sangrado sin comillas (APA 7). Incluye página.

### Formato APA 7 en el texto
- Un autor: (Sommerville, 2011) o Sommerville (2011) afirma...
- Dos autores: (Gamma y Helm, 1994) [en español "y"; en inglés "&" dentro del paréntesis].
- Tres o más autores: (Hernández et al., 2014).
- Cita textual: (Pressman, 2010, p. 45).
- Fuente secundaria: (Piaget, 1970, citado en Pérez, 2015). Evítala si puedes acceder a la original.
- Sin fecha: (García, s. f.). Organización: (Organización de las Naciones Unidas [ONU], 2020).

### Lista de referencias (APA 7)
Orden alfabético por apellido, sangría francesa, DOI como URL cuando exista.
- **Libro**: Sommerville, I. (2011). *Ingeniería de software* (9.ª ed.). Pearson Educación.
- **Artículo de revista**: Hevner, A. R., March, S. T., Park, J., y Ram, S. (2004). Design science in information systems research. *MIS Quarterly, 28*(1), 75-105.
- **Capítulo**: Autor, A. (año). Título del capítulo. En E. Editor (Ed.), *Título del libro* (pp. xx-xx). Editorial.
- **Página web**: Organización. (2023, 5 de mayo). *Título de la página*. URL
- **Trabajo de grado**: Apellido, N. (2022). *Título* [Trabajo de grado, Universidad]. Repositorio. URL
- **Software/repositorio**: Autor/Organización. (año). *Nombre* (versión) [Software]. URL
Regla: toda cita en el texto debe estar en las referencias, y viceversa.

### Estilo IEEE (numérico) para informática
Cita por número entre corchetes en orden de aparición: "como se describe en [3]". Referencia: [3] E. Gamma, R. Helm, R. Johnson y J. Vlissides, *Design Patterns*. Boston, MA, USA: Addison-Wesley, 1994. Ampliamente usado en revistas de ingeniería; confirma cuál aplica a tu trabajo.

### Gestores de referencias
**Zotero** (libre; extensión del navegador, plugin para LibreOffice/Word), Mendeley, JabRef con BibTeX (para LaTeX: `\cite{key}`). Ventajas: formato automático y cambio de estilo con un clic.
```bibtex
@book{sommerville2011,
  author    = {Sommerville, Ian},
  title     = {Ingenier{\'i}a de software},
  edition   = {9},
  publisher = {Pearson Educaci{\'o}n},
  year      = {2011}
}
```

## Elementos de presentación
- **Figuras y tablas**: numeradas, título descriptivo, fuente ("Elaboración propia" o cita), referenciadas en el texto; tablas con pocas líneas; gráficos legibles en impresión en blanco y negro.
- **Ecuaciones**: numeradas, variables definidas.
- **Código**: en apéndices o bloques breves con tipografía monoespaciada; repositorio con licencia.
- **Índices** automáticos (contenido, tablas, figuras), paginación, márgenes y tipografía según el manual (verificar medidas con la normativa de la UNET).
- **Resumen y abstract** al inicio; **anexos** para instrumentos, manuales y datos extensos.

## Integridad académica y ética
- **Plagio**: textual, de ideas, mosaico (copiar frases cambiando palabras), autoplagio, uso no declarado de contenido generado por IA. Consecuencias: reprobación, sanciones disciplinarias. Detectores de similitud (Turnitin y similares) se usan en muchas instituciones.
- **Uso de IA generativa**: declararlo si la institución lo permite, nunca citar fuentes no verificadas (las IA pueden inventar referencias), tú eres responsable de cada afirmación.
- **Autoría**: criterios de contribución sustancial; agradecimientos para quienes no cumplen.
- **Datos personales y confidencialidad**: anonimizar, consentimiento, permiso de la empresa para publicar (relevante en [[TAP Pasantía]]).
- **Licencias**: software libre (MIT, GPL, Apache), contenido (Creative Commons); respeta licencias de imágenes y datasets.

## Ejemplo resuelto: de una fuente a una cita bien hecha
Fuente leída: Sommerville (2011, p. 25) explica que en el modelo en cascada cada fase debe terminar antes de comenzar la siguiente.
1. Mala: copiar la oración literal sin comillas.
2. Aceptable (parafraseo con cita): "En el modelo en cascada las etapas se ejecutan de forma secuencial y una no inicia hasta que la anterior concluye (Sommerville, 2011)."
3. Referencia en la lista: Sommerville, I. (2011). *Ingeniería de software* (9.ª ed.). Pearson Educación.
4. Verificación: ¿aparece en la lista? ¿coinciden año y autor? ¿está en orden alfabético? Sí.
(Número de página y edición ilustrativos: verifica con tu ejemplar.)

## Lista de verificación final antes de entregar
- Título coherente con objetivos. 
- Objetivos respondidos en conclusiones, una conclusión por objetivo.
- Todas las citas con referencia y viceversa.
- Tablas/figuras numeradas y mencionadas.
- Ortografía y formato revisados; PDF generado y revisado.
- Tutor aprobó la versión.

## Errores comunes
- Citar sin referencia o referenciar sin citar.
- Parafrasear cambiando solo sinónimos.
- Conclusiones que introducen datos nuevos.
- Resultados mezclados con discusión.
- Usar "etc." y expresiones vagas ("muchos estudios dicen").
- Referencias incompletas (sin año, sin editorial, enlaces rotos).

## Ejercicios propuestos
1. Escribe en APA la cita de tres autores (Pressman, Maxim y otro) en el texto. *Resp.: (Pressman et al., 2020).*
2. ¿Cuándo se usa cita en bloque? *Resp.: cuando la cita textual tiene 40 o más palabras (APA 7).*
3. Reescribe: "La verdad es que el sistema fue súper bueno". *Resp.: "El sistema obtuvo un puntaje SUS de 85, superior al promedio de referencia (68)."*

## Conexiones
[[Lenguaje y Comunicación]], [[Seminario]], [[TAP Tesis]], [[TAP Pasantía]], [[Legislación, Valores y Proyecto de País]].

## Fuente
Conocimiento general. American Psychological Association, *Manual de Publicaciones de la APA* (7.ª ed.); IEEE Editorial Style Manual; UPEL, *Manual de Trabajos de Grado* (verificar normativa vigente).
