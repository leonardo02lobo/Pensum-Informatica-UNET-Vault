---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 02 - Enfoques y tipos de investigación

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 01 - Conocimiento científico y método científico]]
Siguiente: [[MI 03 - Planteamiento del problema y objetivos]]

## Contexto y objetivo
Al iniciar un trabajo debes declarar **enfoque**, **nivel** (alcance), **diseño** y **modalidad**. Cada uno condiciona instrumentos, análisis y conclusiones. Objetivo: clasificar correctamente tu investigación y justificar la clasificación, incluyendo la modalidad "proyecto factible" muy común en Ingeniería (verificar qué modalidad y terminología exige la normativa vigente de la UNET).

## Enfoques

### Cuantitativo
Mide variables con números y prueba hipótesis con estadística. Secuencia lineal: problema, hipótesis, medición, análisis, conclusión. Busca generalización y replicabilidad. Ejemplos: comparar tiempos de respuesta de dos algoritmos; encuesta de satisfacción con escala Likert.

### Cualitativo
Explora significados, experiencias y contextos con datos textuales, observación, entrevistas en profundidad, grupos focales. Proceso inductivo y flexible; la muestra es intencional y se busca **saturación**. Diseños: fenomenología, etnografía, teoría fundamentada, estudio de caso, investigación-acción.

### Mixto
Integra ambos (diseños explicativo secuencial, exploratorio secuencial, convergente). Útil cuando se requiere medir y comprender (p.ej., medir la adopción de un sistema y entrevistar usuarios sobre las barreras). Exige justificar la integración (triangulación).

| Aspecto | Cuantitativo | Cualitativo |
|---|---|---|
| Pregunta | ¿Cuánto? ¿Qué relación? | ¿Cómo? ¿Por qué? |
| Datos | Numéricos | Textos, imágenes |
| Muestra | Grande, probabilística | Pequeña, intencional |
| Análisis | Estadístico | Codificación temática |
| Rigor | Validez y confiabilidad | Credibilidad, transferibilidad |

## Tipos según el nivel o alcance
1. **Exploratoria**: tema poco estudiado; familiarizarse; genera hipótesis. 
2. **Descriptiva**: especifica propiedades y características de un fenómeno (diagnóstico, estado actual). No manipula variables.
3. **Correlacional**: mide el grado de asociación entre variables (sin afirmar causa). Coeficiente $r$ de Pearson (ver [[MI 08 - Estadística aplicada a la investigación]]).
4. **Explicativa (causal)**: responde por qué ocurre y bajo qué condiciones; suele requerir experimento.
5. **Evaluativa**: juzga el valor o efecto de un programa o sistema.
Un trabajo puede combinar niveles (descriptivo en el diagnóstico, explicativo en la evaluación).

## Tipos según el diseño
- **Experimental**: manipula deliberadamente una variable independiente y controla variables extrañas. *Puro* (grupo de control y asignación aleatoria), *cuasiexperimental* (sin aleatorización), *preexperimental* (pre-post sin control).
- **No experimental**: observa sin manipular. *Transversal* (un momento) o *longitudinal* (varios momentos: tendencia, evolución, panel).
- **De campo**: datos tomados directamente en el entorno real. **Documental/bibliográfica**: análisis de fuentes secundarias. **De laboratorio**: condiciones controladas.

## Modalidades usuales en ingeniería
### Proyecto factible (o proyecto tecnológico)
Elaboración y desarrollo de una propuesta de modelo operativo viable para resolver un problema o necesidad de una organización o grupo. Fases típicas (Arias; UPEL): 
1. **Diagnóstico** de la situación actual (necesidades, procesos).
2. **Estudio de factibilidad**: técnica, operativa, económica (y legal).
3. **Diseño de la propuesta**.
4. **Desarrollo/implementación** (en algunos trabajos, solo hasta prototipo).
5. **Evaluación**.
En software se mapea al ciclo de vida: diagnóstico = requisitos; propuesta = diseño; implementación = construcción y pruebas ([[Ingeniería de Software]]).

### Investigación aplicada con prototipo / desarrollo experimental
Se construye un artefacto y se evalúa con métricas (rendimiento, exactitud, usabilidad con SUS).

### Estudio de caso, investigación-acción, revisión sistemática de la literatura (SLR, protocolo PRISMA o Kitchenham).

## Cómo clasificar tu investigación: procedimiento
1. ¿Qué pregunto? (qué, cuánto, por qué, cómo mejorar) lo que da el enfoque.
2. ¿Hasta dónde quiero llegar? (describir, relacionar, explicar, evaluar) lo que da el nivel.
3. ¿Manipulo variables? lo que da el diseño.
4. ¿De dónde vienen los datos? (campo, documental, laboratorio).
5. ¿Qué produzco? (conocimiento o artefacto) lo que da la modalidad.

**Ejemplo resuelto.** Título: "Sistema web para el control de préstamos de equipos del Laboratorio X".
- Enfoque: mixto con predominio cuantitativo (tiempos y satisfacción).
- Nivel: descriptivo (diagnóstico) y evaluativo (efecto del sistema).
- Diseño: de campo, cuasiexperimental pre-post sin grupo control (preprueba/posprueba) y transversal en el diagnóstico.
- Modalidad: proyecto factible/desarrollo tecnológico.
- Justificación: se mide la situación antes y después; no hay aleatorización posible porque el laboratorio es uno solo.

## Ejemplo contrastante
Título: "Percepción de los docentes sobre IA generativa en la evaluación". Enfoque cualitativo; nivel exploratorio; diseño fenomenológico; entrevistas semiestructuradas a 10-15 docentes hasta saturación.

## Errores comunes
- Declarar "experimental" sin manipular variable ni controlar nada.
- Decir "mixto" por haber usado una encuesta y una entrevista sin integración.
- Poner "descriptivo" cuando los objetivos dicen "determinar el efecto de..." (eso es explicativo/evaluativo).
- Copiar la clasificación de otra tesis sin verificar que aplica.

## Ejercicios propuestos
1. Estudiar si hay relación entre horas de estudio y nota. *Resp.: cuantitativo, correlacional, no experimental.*
2. Comparar dos métodos de enseñanza con grupos asignados al azar. *Resp.: cuantitativo, explicativo, experimental puro.*
3. Clasificar "Propuesta de red WiFi para la facultad". *Resp.: proyecto factible; diagnóstico descriptivo; de campo.*

## Conexiones
[[Estadística I]], [[Estadística II]], [[Seminario]], [[Estructura del anteproyecto de investigación]], [[IS 01 - Ciclo de vida y modelos de proceso]].

## Fuente
Conocimiento general. Hernández Sampieri et al.; Arias, *El Proyecto de Investigación*; UPEL, *Manual de Trabajos de Grado* (verificar normativa vigente).
