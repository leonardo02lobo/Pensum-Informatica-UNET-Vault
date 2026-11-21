---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 05 - Hipótesis, variables y operacionalización

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 04 - Marco teórico y revisión bibliográfica]]
Siguiente: [[MI 06 - Diseño metodológico, población y muestra]]

## Contexto y objetivo
Para que una investigación cuantitativa sea contrastable, sus conceptos deben convertirse en **variables medibles** y sus suposiciones en **hipótesis** con forma lógica precisa. Objetivo: formular hipótesis nula y alterna, identificar tipos de variables y escalas de medición, y construir una tabla de operacionalización.

## Hipótesis

### Definición y condiciones
Una **hipótesis** es una afirmación tentativa sobre la relación entre dos o más variables (o sobre un parámetro) que puede contrastarse con datos. Debe ser: clara, referirse a una situación real, relacionar variables medibles, ser **falsable** y estar fundamentada en el marco teórico.

### Tipos
- **De investigación (H1/Hi)**: descriptivas de un valor ("el tiempo medio será menor de 5 min"), correlacionales ("a más horas de estudio, mayor nota"), de diferencia de grupos, causales.
- **Nula (H0)**: niega relación o diferencia ("no hay diferencia"). Es la que se somete a prueba estadística.
- **Alterna (Ha)**: afirma la relación o diferencia (direccional: unilateral; no direccional: bilateral).
- Hipótesis **estadísticas**: expresadas en parámetros ($\mu$, $\rho$, $p$).

**Ejemplo.** Investigación: efecto del sistema sobre el tiempo de atención.
- $H_0: \mu_{antes} = \mu_{despu\acute{e}s}$ (no hay diferencia).
- $H_a: \mu_{antes} > \mu_{despu\acute{e}s}$ (el tiempo disminuye; prueba unilateral).

No todos los estudios necesitan hipótesis: las exploratorias y muchas descriptivas y de proyecto factible usan **preguntas y objetivos** en su lugar. Verifica qué exige tu tutor.

### Lógica del contraste
1. Fija el nivel de significancia $\alpha$ (típico 0.05).
2. Calcula el estadístico y el **valor p** (probabilidad de observar datos tan extremos si H0 es cierta).
3. Si $p < \alpha$ se **rechaza H0**; si no, **no se rechaza** (no equivale a "demostrar H0").
Errores: **Tipo I** ($\alpha$): rechazar H0 verdadera. **Tipo II** ($\beta$): no rechazar H0 falsa. Potencia $= 1-\beta$. Ver [[Estadística II]] y [[MI 08 - Estadística aplicada a la investigación]].

## Variables

### Definición y clasificación
**Variable**: propiedad que puede variar y cuya variación es medible u observable.
- Según su función: **independiente** (causa o factor manipulado), **dependiente** (efecto medido), **interviniente/moderadora/de control** (influyen o se mantienen constantes), **extrañas** (no controladas; amenazan la validez).
- Según su naturaleza: **cualitativas** (nominales: sexo, carrera; ordinales: nivel de satisfacción) y **cuantitativas** (discretas: número de fallos; continuas: tiempo).

### Escalas de medición (Stevens)
| Escala | Propiedades | Ejemplos | Estadísticos válidos |
|---|---|---|---|
| Nominal | Categorías sin orden | Carrera, sistema operativo | Moda, frecuencias, $\chi^2$ |
| Ordinal | Orden, sin distancia fija | Likert, ranking | Mediana, Spearman, no paramétricas |
| Intervalo | Distancias iguales, sin cero absoluto | Temperatura en °C | Media, desviación, Pearson |
| Razón | Cero absoluto | Tiempo, peso, número de errores | Todas, incluida razón |
La escala determina las pruebas estadísticas permitidas.

## Operacionalización
Proceso de pasar de lo abstracto a lo medible: **variable (definición conceptual) a dimensiones, indicadores, ítems/instrumento**.
- **Definición conceptual**: qué significa en la teoría.
- **Definición operacional**: cómo se medirá concretamente.
- **Dimensión**: faceta de la variable. **Indicador**: señal observable. **Ítem**: pregunta o medición específica.

### Ejemplo de tabla de operacionalización
Variable dependiente: **Eficiencia del proceso de préstamo**.
| Dimensión | Indicador | Instrumento | Escala/unidad |
|---|---|---|---|
| Tiempo | Minutos por préstamo | Cronometraje / registro de logs | Razón (min) |
| Exactitud | Errores de registro por 100 préstamos | Lista de cotejo | Razón (%) |
| Satisfacción | Percepción del servicio | Cuestionario Likert de 5 puntos | Ordinal |

Variable independiente: **Uso del sistema web** (con/sin sistema; nominal dicotómica).

Para productos de software, indicadores comunes: tiempo de respuesta, tasa de error, exactitud/precisión/recall (modelos), usabilidad (SUS, escala 0-100), disponibilidad, cobertura de pruebas ([[IS 09 - Calidad y métricas de software]]).

## Ejemplo resuelto completo
Problema: ¿El uso de un chatbot reduce el tiempo de resolución de consultas del soporte?
1. Variables: V.I. = uso del chatbot (sí/no). V.D. = tiempo de resolución (minutos). Control: tipo de consulta, hora del día.
2. Hipótesis: $H_0: \mu_{sin} = \mu_{con}$; $H_a: \mu_{sin} > \mu_{con}$.
3. Escala de la V.D.: razón, lo que permite prueba t (si hay normalidad) o Mann-Whitney (si no).
4. Operacionalización: tiempo = diferencia entre sello de apertura y de cierre del ticket en el sistema.
5. Riesgos para validez: consultas más sencillas llegan al chatbot (sesgo de selección): asignar aleatoriamente.

## Errores comunes
- Hipótesis con "mejor", "más eficiente" sin indicador.
- Hipótesis como "aceptar H0".
- Confundir variable con valor ("hombre" no es variable; "sexo" sí).
- Indicadores que no miden la dimensión (validez de contenido).
- Aplicar media a escala ordinal sin justificar.
- Más de una variable dependiente sin tratamiento estadístico adecuado.

## Ejercicios propuestos
1. Formula H0 y Ha: "El algoritmo B tiene mayor exactitud que A". *Resp.: H0: exactitud A = B; Ha: exactitud B mayor que A.*
2. Clasifica la escala: nivel de satisfacción (muy bajo...muy alto). *Resp.: ordinal.*
3. Operacionaliza "usabilidad de un sitio". *Resp.: dimensiones: facilidad de aprendizaje, eficiencia, satisfacción; indicadores: tiempo en completar tarea, tasa de errores, puntaje SUS.*

## Conexiones
[[Estadística I]], [[Estadística II]], [[MI 07 - Instrumentos, validez y confiabilidad]], [[IS 08 - Pruebas de software]].

## Fuente
Conocimiento general. Hernández Sampieri; Stevens (1946), escalas de medición; Montgomery, *Diseño y análisis de experimentos*.
