---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 07 - Instrumentos, validez y confiabilidad

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 06 - Diseño metodológico, población y muestra]]
Siguiente: [[MI 08 - Estadística aplicada a la investigación]]

## Contexto y objetivo
Los datos son tan buenos como el instrumento que los produce. Esta clase presenta las técnicas de recolección (encuesta, entrevista, observación, análisis documental, pruebas técnicas), cómo construir un cuestionario y cómo demostrar que mide lo que debe (**validez**) y con consistencia (**confiabilidad**), incluyendo el alfa de Cronbach con cálculo resuelto y código.

## Técnica vs instrumento
- **Técnica**: procedimiento general (encuesta, entrevista, observación).
- **Instrumento**: medio concreto (cuestionario, guía de entrevista, lista de cotejo, ficha de registro, prueba de rendimiento, *logs* del sistema).

## Principales técnicas
| Técnica | Instrumento | Ventaja | Limitación |
|---|---|---|---|
| Encuesta | Cuestionario (papel, Google Forms, LimeSurvey) | Muchos datos, bajo costo | Respuesta superficial, sesgo de deseabilidad |
| Entrevista | Guía estructurada/semiestructurada | Profundidad | Tiempo, sesgo del entrevistador |
| Observación | Lista de cotejo, bitácora | Conducta real | Efecto del observador |
| Análisis documental | Matriz de análisis | Evidencia objetiva | Disponibilidad |
| Medición técnica | Scripts, herramientas de *benchmark*, métricas | Objetividad | Requiere control del entorno |
| Grupo focal | Guía de moderación | Dinámica de grupo | Dominio de voces |

## Construcción de un cuestionario
1. Parte de la **tabla de operacionalización** ([[MI 05 - Hipótesis, variables y operacionalización]]): al menos 2-3 ítems por indicador.
2. Redacta ítems cortos, claros, de una sola idea (evita doble pregunta: "¿el sistema es rápido y fácil?").
3. Evita preguntas tendenciosas, negaciones dobles y jerga.
4. Elige el formato: cerrada dicotómica, opción múltiple, **escala Likert** (1-5: totalmente en desacuerdo ... totalmente de acuerdo), diferencial semántico, abiertas (pocas).
5. Ordena: de lo fácil a lo sensible; agrupa por dimensión; datos demográficos al final.
6. Incluye instrucciones, consentimiento informado y tiempo estimado.
7. **Prueba piloto** con 10-30 personas para ajustar comprensión y calcular confiabilidad.

Escalas estandarizadas útiles en informática: **SUS** (System Usability Scale, 10 ítems, puntaje 0-100; mayor de 68 se considera sobre el promedio), **UEQ**, **NASA-TLX** (carga de trabajo), **TAM** (aceptación de tecnología).

**Cálculo del SUS.** Para ítems impares (1,3,5,7,9): puntaje - 1; para pares (2,4,6,8,10): 5 - puntaje; suma x 2.5.
Ejemplo: respuestas (4,2,5,1,4,2,4,2,5,1): impares: 3+4+3+3+4 = 17; pares: 3+4+3+3+4 = 17; suma 34; SUS = 85.

## Validez
**Validez**: grado en que el instrumento mide lo que pretende medir.
- **De contenido**: juicio de expertos (3-5) que evalúan pertinencia, claridad y coherencia de cada ítem; se calcula el **coeficiente de validez de contenido (CVC)** o la **V de Aiken**: $V = \dfrac{\bar{x} - l}{k}$ donde $\bar{x}$ es el promedio de las calificaciones de los jueces, $l$ la calificación mínima y $k$ el rango (máx - mín). Ítem aceptable típicamente cuando $V \ge 0.70$-$0.80$.
- **De constructo**: el instrumento refleja el concepto teórico (análisis factorial exploratorio/confirmatorio, correlaciones con otros instrumentos).
- **De criterio**: correlación con un criterio externo (concurrente o predictiva).
- **Validez aparente (de cara)**: parece medir lo correcto a los usuarios.

**Ejemplo (Aiken).** 4 jueces califican un ítem de 1 a 4: (4,4,3,4): $\bar{x}=3.75$; $l=1$; $k=3$. $V = (3.75-1)/3 = 0.917$ → ítem válido.

## Confiabilidad
**Confiabilidad**: consistencia o estabilidad de las medidas.
- **Test-retest**: correlación entre dos aplicaciones.
- **Formas paralelas**.
- **Mitades partidas** (Spearman-Brown: $r_{SB} = 2r/(1+r)$).
- **Consistencia interna: alfa de Cronbach**:
$$\alpha = \frac{k}{k-1}\left(1 - \frac{\sum_{i=1}^{k}\sigma_i^2}{\sigma_T^2}\right)$$
$k$ = número de ítems; $\sigma_i^2$ varianza del ítem $i$; $\sigma_T^2$ varianza de la puntuación total.
Interpretación orientativa: $\ge 0.9$ excelente; $0.8$-$0.9$ buena; $0.7$-$0.8$ aceptable; $<0.6$ pobre. Un $\alpha$ muy alto (mayor de 0.95) puede indicar redundancia. KR-20 es el caso para ítems dicotómicos.
- **Entre evaluadores**: kappa de Cohen, ICC.

### Ejemplo resuelto de alfa de Cronbach
5 encuestados, 3 ítems (escala 1-5):
| Sujeto | I1 | I2 | I3 | Total |
|---|---|---|---|---|
| 1 | 4 | 5 | 4 | 13 |
| 2 | 3 | 3 | 4 | 10 |
| 3 | 5 | 5 | 5 | 15 |
| 4 | 2 | 3 | 2 | 7 |
| 5 | 4 | 4 | 5 | 13 |
Varianzas muestrales (n-1): I1: media 3.6; desviaciones: .4, -.6, 1.4, -1.6, .4 → cuadrados .16+.36+1.96+2.56+.16 = 5.2; var = 1.3. I2: media 4.0; (1,-1,1,-1,0) → 4; var = 1.0. I3: media 4.0; (0,0,1,-2,1) → 6; var = 1.5. Suma = 3.8. Total: media 11.6; desviaciones 1.4, -1.6, 3.4, -4.6, 1.4 → 1.96+2.56+11.56+21.16+1.96 = 39.2; var = 9.8.
$\alpha = \frac{3}{2}(1 - 3.8/9.8) = 1.5 \times 0.612 = 0.918$ → consistencia excelente (muestra muy pequeña: solo ilustrativa).

```python
import numpy as np
def cronbach(datos):                       # filas: sujetos, columnas: ítems
    x = np.asarray(datos, dtype=float)
    k = x.shape[1]
    var_items = x.var(axis=0, ddof=1).sum()   # suma de varianzas de ítems
    var_total = x.sum(axis=1).var(ddof=1)     # varianza de totales
    return k / (k - 1) * (1 - var_items / var_total)

d = [(4,5,4),(3,3,4),(5,5,5),(2,3,2),(4,4,5)]
print(round(cronbach(d), 3))   # 0.918
```

## Relación entre validez y confiabilidad
Un instrumento puede ser confiable sin ser válido (una balanza que siempre marca 2 kg de más es consistente pero errónea); no puede ser válido si no es confiable. Analogía del tiro al blanco.

## Instrumentos en proyectos de ingeniería
Además de cuestionarios: **listas de verificación** de requisitos, **pruebas funcionales** (casos de prueba), *benchmarks* con repeticiones (reportar media, desviación e IC), **matriz de evaluación** comparativa de tecnologías con ponderaciones, **entrevistas** de levantamiento. Para algoritmos: conjuntos de datos de referencia, validación cruzada y métricas estándar ([[Aprendizaje Automático]]).

## Errores comunes
- Aplicar el cuestionario sin piloto ni validación.
- Calcular alfa con ítems invertidos sin recodificar.
- Interpretar alfa como "validez".
- Preguntas obligatorias que fuerzan respuestas falsas.
- Olvidar el consentimiento informado y el anonimato.

## Ejercicios propuestos
1. Calcula el SUS para (5,1,5,1,5,1,5,1,5,1). *Resp.: impares 4x5=20, pares 4x5=20; 40 x 2.5 = 100.*
2. V de Aiken con jueces (3,4,4) en escala 1-4. *Resp.: media 3.67; V = 2.67/3 = 0.89.*
3. ¿Qué tipo de confiabilidad evalúa alfa? *Resp.: consistencia interna.*

## Conexiones
[[Estadística I]], [[Estadística II]], [[IS 02 - Ingeniería de requisitos]] (entrevistas/cuestionarios), [[Aprendizaje Automático]] (validación de modelos).

## Fuente
Conocimiento general. Cronbach (1951); Aiken (1985); Brooke (1996), SUS; Hernández Sampieri.
