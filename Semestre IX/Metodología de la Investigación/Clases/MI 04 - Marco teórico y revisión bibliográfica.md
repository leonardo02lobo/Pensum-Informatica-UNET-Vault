---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 04 - Marco teórico y revisión bibliográfica

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 03 - Planteamiento del problema y objetivos]]
Siguiente: [[MI 05 - Hipótesis, variables y operacionalización]]

## Contexto y objetivo
El marco teórico (o referencial) sitúa el problema dentro del conocimiento existente: qué se ha hecho, con qué conceptos y teorías se explica, y qué falta. No es un resumen de enciclopedia sino un argumento que sostiene tu investigación. Objetivo: realizar una búsqueda sistemática, organizar el estado del arte, y redactar antecedentes, bases teóricas, bases legales y definición de términos.

## Funciones del marco teórico
1. Evitar duplicar trabajos y detectar la **brecha** (gap).
2. Delimitar conceptos y variables con definiciones aceptadas.
3. Proveer teorías/modelos que guíen el diseño y la interpretación.
4. Justificar decisiones metodológicas (por qué esa técnica o algoritmo).

## Componentes (formato habitual; verificar el manual vigente)
- **Antecedentes de la investigación**: estudios previos relacionados (3 a 8 más relevantes), cada uno con autor, año, objetivo, metodología, resultados y **relación con tu trabajo**. Ordénalos de lo internacional a lo local o por cercanía temática.
- **Bases teóricas**: conceptos y teorías organizados de lo general a lo particular (p.ej. sistemas de información, gestión de inventarios, aplicaciones web, base de datos relacional).
- **Bases legales**: leyes, normas y reglamentos aplicables (en Venezuela, por ejemplo, la Ley de Infogobierno, Ley de Mensajes de Datos y Firmas Electrónicas, Ley Especial contra los Delitos Informáticos; verificar vigencia y pertinencia).
- **Definición de términos básicos**: glosario de términos clave.
- **Sistema de variables** (en trabajos cuantitativos): ver [[MI 05 - Hipótesis, variables y operacionalización]].
- **Marco conceptual** vs **referencial**: el conceptual define términos; el referencial integra teorías, antecedentes y contexto institucional.

## Estrategia de búsqueda bibliográfica
1. **Pregunta y conceptos clave**: extrae 3-5 conceptos de tu pregunta.
2. **Sinónimos y traducciones**: en inglés suelen estar la mayoría de los artículos (p.ej. "inventory management system", "web-based", "equipment loan").
3. **Operadores booleanos**: `AND`, `OR`, `NOT`, comillas para frases, comodín `*`.
   Ejemplo: `("inventory management" OR "stock control") AND ("web application" OR "web-based") AND university`.
4. **Bases de datos**: Google Académico, IEEE Xplore, ACM Digital Library, ScienceDirect, Scopus, Web of Science, SciELO y Redalyc (iberoamericanas), arXiv (preprints), repositorios institucionales (verificar acceso desde la UNET).
5. **Filtros**: años recientes (en tecnología, preferiblemente últimos 5 años salvo trabajos fundacionales), tipo (artículo revisado por pares, revisión, tesis).
6. **Bola de nieve**: revisa las referencias de un artículo clave (hacia atrás) y quién lo cita (hacia adelante).
7. **Registro**: gestor de referencias (Zotero, Mendeley, JabRef) con etiquetas y notas.

### Evaluación de fuentes
Autoridad (autor, institución), revisión por pares, actualidad, pertinencia, evidencia (metodología explícita), citas recibidas. Cuidado con revistas depredadoras, blogs sin referencias y contenido generado sin verificación.

## Lectura eficiente de un artículo
Orden sugerido: título, resumen, conclusiones, figuras, introducción, métodos, resultados. Registra en una **matriz de síntesis**:
| Ref. | Problema | Método/datos | Resultado | Limitaciones | Relevancia |
|---|---|---|---|---|---|
| Pérez (2022) | Control de inventario | Estudio de caso | -30% tiempo | Una sola sede | Alta |
Con la matriz identificas patrones y la brecha ("ningún estudio evalúa X en laboratorios universitarios venezolanos", afirmar solo si lo comprobaste).

## Estado del arte y revisión sistemática
- **Estado del arte**: panorama de lo más reciente en el tema; agrupa por enfoques (taxonomía) y concluye con comparaciones y brechas.
- **Revisión sistemática (SLR)** (Kitchenham): protocolo previo con preguntas de revisión, cadenas de búsqueda, criterios de inclusión y exclusión, extracción de datos, evaluación de calidad; PRISMA para el diagrama de flujo. Puede ser tu metodología principal si el trabajo es documental.

## Redacción del marco teórico
- **Parafrasea** y sintetiza, no pegues; **cita** siempre ([[MI 09 - Redacción académica, citas y referencias]]).
- Estructura por **temas**, no por autor ("Autor A dice..., Autor B dice..."): agrupa ideas, compara, contrasta.
- Usa conectores: "en contraste", "de manera similar", "sin embargo".
- Cierra cada sección vinculando con tu estudio.

## Ejemplo resuelto: antecedente bien redactado
"Gómez y Rivas (2021) desarrollaron un sistema web de control de inventario para laboratorios de ingeniería utilizando Django y PostgreSQL bajo la metodología Scrum; evaluaron la usabilidad con la escala SUS (n = 25) y obtuvieron 82 puntos. Su trabajo evidencia la viabilidad de soluciones web de bajo costo, pero no incorpora alertas de vencimiento, funcionalidad que sí aborda la presente investigación." 
Observa: qué se hizo, con qué, cómo se midió, resultado y **aporte diferencial**. (Cifras ilustrativas; en tu trabajo deben ser de fuentes reales.)

## Ejemplo: esquema de bases teóricas para un sistema de préstamos
1. Sistemas de información (definición, componentes) 2. Gestión de inventarios 3. Aplicaciones web y arquitectura cliente-servidor 4. Bases de datos relacionales 5. Metodología de desarrollo (Scrum) 6. Usabilidad (ISO 9241, SUS). Cada tema 1-2 páginas con citas.

## Errores comunes
- Copiar definiciones sin citar (plagio) o con parafraseo mínimo.
- Antecedentes sin relación con el problema ("relleno").
- Citar solo Wikipedia o tesis antiguas.
- Marco teórico como compilación de capítulos de libro sin vínculo con las variables.
- No registrar las referencias al leer (luego no se encuentran).

## Ejercicios propuestos
1. Escribe una cadena de búsqueda booleana para "detección de fraude con aprendizaje automático en tarjetas". *Resp.: ("fraud detection" AND "machine learning") AND ("credit card" OR "payment").*
2. ¿Diferencia entre antecedentes y bases teóricas? *Resp.: antecedentes = estudios previos; bases teóricas = conceptos y teorías.*
3. ¿Cuándo es válido afirmar una "brecha"? *Resp.: tras una búsqueda documentada y sistemática que no encontró estudios.*

## Conexiones
[[Seminario]] (estado del arte), [[Lenguaje y Comunicación]], [[Ingeniería de Software]] (fundamentos del dominio), [[Estructura del anteproyecto de investigación]].

## Fuente
Conocimiento general. Hernández Sampieri; Kitchenham y Charters (2007), guidelines para SLR; Page et al. (2021), PRISMA.
