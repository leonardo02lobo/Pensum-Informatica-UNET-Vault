---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 01 - Conocimiento científico y método científico

Materia: [[Metodología de la Investigación]]
Siguiente: [[MI 02 - Enfoques y tipos de investigación]]

## Contexto y objetivo
Antes de planificar un trabajo de grado ([[TAP Tesis]]) conviene entender qué distingue a la investigación científica de la opinión o la experiencia cotidiana. Objetivo: diferenciar tipos de conocimiento, comprender el método científico y los paradigmas, y situar la investigación en ingeniería (donde conviven la ciencia y el diseño).

## Tipos de conocimiento
- **Empírico (vulgar)**: surge de la experiencia, es asistemático, superficial, no verificado.
- **Filosófico**: reflexión crítica sobre fundamentos (lógica, ética, epistemología).
- **Científico**: sistemático, metódico, verificable, objetivo, general, falible y acumulativo. Busca explicar y predecir fenómenos mediante leyes y teorías.
- **Técnico/tecnológico**: aplicación del conocimiento para crear artefactos y procesos; se evalúa por eficacia y eficiencia.

Características del conocimiento científico (Bunge): fáctico, trasciende los hechos, analítico, claro y preciso, comunicable, verificable, sistemático, general, legal (busca leyes), explicativo, predictivo, abierto, útil.

## Niveles de la actividad científica
- **Hecho/dato**, **concepto**, **proposición**, **ley** (relación constante entre variables), **teoría** (conjunto sistemático de leyes que explica un dominio), **modelo** (representación simplificada).
- **Investigación básica (pura)**: amplía el conocimiento sin aplicación inmediata. **Aplicada**: resuelve problemas prácticos. **Desarrollo tecnológico**: crea productos/prototipos. En Ingeniería Informática predominan la aplicada y el desarrollo, con rigor científico en la evaluación.

## El método científico
No es una receta única; es un conjunto de pasos lógicos iterativos:
1. **Observación** de un fenómeno y revisión de lo ya conocido.
2. **Problema**: pregunta concreta y delimitada.
3. **Hipótesis**: respuesta tentativa, contrastable.
4. **Predicciones**: consecuencias observables si la hipótesis es cierta.
5. **Experimento / recolección de datos** controlados.
6. **Análisis** (estadístico o cualitativo).
7. **Conclusión**: se acepta, se rechaza o se refina la hipótesis.
8. **Comunicación** y replicación por otros.

**Razonamiento**: *deductivo* (de lo general a lo particular: si las premisas son verdaderas, la conclusión necesariamente lo es), *inductivo* (de casos particulares a generalización: probabilística), *hipotético-deductivo* (Popper: se formula hipótesis y se intenta **falsarla**; una teoría es científica si es refutable). *Abductivo*: inferir la mejor explicación.

**Criterios de demarcación**: falsabilidad (Popper); paradigmas y revoluciones científicas (Kuhn); programas de investigación (Lakatos). 

## Paradigmas de investigación
| Paradigma | Realidad | Método | Meta |
|---|---|---|---|
| Positivista | Objetiva, medible | Cuantitativo, experimental | Explicar, predecir, generalizar |
| Interpretativo (constructivista) | Construida socialmente | Cualitativo | Comprender significados |
| Sociocrítico | Transformable | Investigación-acción | Cambiar situaciones |
| Pragmático | Lo que funciona | Mixto | Resolver problemas |

## Ciencia, tecnología e ingeniería
- Diseño científico: se busca verdad. Diseño en ingeniería: se busca **solución que satisfaga restricciones** (Simon, *Ciencias de lo artificial*).
- **Design Science Research (DSR)** (Hevner, Peffers): metodología muy usada en sistemas de información: 1) identificar problema y motivación, 2) definir objetivos de la solución, 3) diseñar y desarrollar el artefacto, 4) demostrar, 5) evaluar, 6) comunicar. Es compatible con el proyecto factible.
- En computación se mezclan experimentos controlados (comparar algoritmos con métricas y pruebas estadísticas), estudios de caso, encuestas y desarrollo de prototipos.

## Ética de la investigación (introducción)
Honestidad, consentimiento informado, confidencialidad, no fabricación (invención de datos) ni falsificación, **plagio** (apropiarse de ideas o texto ajeno sin citar), autoría justa, conflictos de interés, reproducibilidad (compartir código y datos cuando sea posible, licencias). Ver [[MI 09 - Redacción académica, citas y referencias]] y [[Legislación, Valores y Proyecto de País]].

## Ejemplo resuelto: del fenómeno al problema
Observación: "Los estudiantes del laboratorio tardan mucho en conseguir equipos."
1. Revisión: ¿hay estudios sobre gestión de inventarios en laboratorios universitarios?
2. Problema delimitado: "¿Cuánto tiempo promedio demora el préstamo de equipos en el Laboratorio X y qué factores lo causan?"
3. Hipótesis (si el enfoque es cuantitativo): "El tiempo medio de préstamo con registro manual es mayor que con un sistema automatizado".
4. Predicción: tras implantar el prototipo, el tiempo medio bajará al menos 30% (valor a justificar).
5. Contraste: medir tiempos antes y después con n tomas y aplicar una prueba t pareada (ver [[MI 08 - Estadística aplicada a la investigación]]).
6. Conclusión: aceptar o rechazar con un nivel de significancia $\alpha$ prefijado.

## Errores comunes
- Confundir **opinión** con evidencia; "me parece" no es resultado.
- Formular hipótesis no contrastables ("el sistema será mejor") sin indicadores.
- Generalizar a partir de muestras pequeñas o sesgadas.
- Confundir **correlación** con **causalidad**.
- Elegir las conclusiones antes de analizar los datos (sesgo de confirmación).

## Ejercicios propuestos
1. Clasifica: "Todos los metales se dilatan con el calor; el cobre es metal; luego se dilata." *Resp.: razonamiento deductivo.*
2. ¿Una afirmación como "algún día el sistema fallará" es falsable? *Resp.: no con un criterio temporal abierto; no puede refutarse.*
3. ¿Qué tipo de investigación es construir un sistema de inventario? *Resp.: aplicada / desarrollo tecnológico (proyecto factible).*

## Conexiones
[[Seminario]] (elección del tema), [[Estadística I]] y [[Estadística II]], [[Lenguaje y Comunicación]], [[Ingeniería de Software]].

## Fuente
Conocimiento general. Bunge, *La ciencia, su método y su filosofía*; Popper, *La lógica de la investigación científica*; Hernández Sampieri, *Metodología de la Investigación*; Hevner et al. (2004) sobre Design Science.
