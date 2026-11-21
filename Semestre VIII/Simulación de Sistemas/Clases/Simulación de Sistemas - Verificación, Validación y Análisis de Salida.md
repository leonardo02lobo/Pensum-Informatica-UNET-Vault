---
tags: [clase, semestre-VIII]
materia: Simulación de Sistemas
---
# Simulación de Sistemas - Verificación, Validación y Análisis de Salida

Materia: [[Simulación de Sistemas]]
Anterior: [[Simulación de Sistemas - Simulación Montecarlo y Modelado Formal]]
Siguiente: — (última clase)

## Contexto y objetivo
Garantizar la credibilidad de un modelo mediante **verificación** y **validación**, diseñar experimentos estadísticamente válidos (réplicas independientes, período de calentamiento) y construir **intervalos de confianza**, **comparación de alternativas** y **análisis de sensibilidad**.

## 1. Verificación vs. Validación
Aunque suelen confundirse, responden a preguntas distintas:
- **Verificación** (*¿construimos el modelo correctamente?*): comprueba que el programa implementa fielmente el modelo conceptual y formal. Técnicas:
  - Pruebas unitarias de eventos y casos de borde (fronteras: cola vacía, tesoro en cero, `clamp`).
  - Depuración paso a paso comparando contra una **traza dorada** (*golden trace*) calculada a mano.
  - Conservación de flujos/entidades (entraron $N$ clientes = atendidos + en sistema).
- **Validación** (*¿construimos el modelo correcto?*): comprueba que el modelo representa adecuadamente al sistema real para los objetivos del estudio. Técnicas:
  - Validación por expertos (validez aparente).
  - Comparación con soluciones analíticas en casos simplificados ($M/M/1$, cadenas de Markov).
  - Pruebas históricas: alimentar el modelo con datos pasados reales y contrastar sus salidas con la realidad observada.

## 2. Simulaciones terminales vs. no terminales (estado estable)
- **Simulación terminal**: tiene un evento o tiempo natural de inicio y fin (p. ej., jornada bancaria de 8:00 a 16:00, o una partida de *Age of Conquest* hasta conquistar el mapa). Cada corrida completa con una semilla distinta es una **réplica independiente**.
- **Simulación no terminal (estado estable)**: estudia el comportamiento a largo plazo de un sistema continuo. Como suele iniciar vacío e inactivo, las primeras observaciones están sesgadas (**sesgo de condición inicial**). Se define un **período de calentamiento** (*warm-up*) $T_0$ cuyas estadísticas se descartan antes de comenzar a medir.

## 3. Análisis de salida e intervalos de confianza
Una sola corrida de simulación estocástica produce una única realización aleatoria, nunca una respuesta definitiva. Se deben ejecutar $n$ **réplicas independientes** (distintas semillas) obteniendo observaciones $X_1, X_2, \dots, X_n$:
$$\bar{X} = \frac{1}{n}\sum_{i=1}^{n} X_i, \qquad s^2 = \frac{1}{n-1}\sum_{i=1}^{n} (X_i - \bar{X})^2$$
El **intervalo de confianza** al nivel $1 - \alpha$ es:
$$\bar{X} \pm t_{n-1,\,\alpha/2}\,\frac{s}{\sqrt{n}}$$

### Ejemplo resuelto
En $n = 10$ réplicas de una cola se mide el tiempo medio de espera en minutos, obteniendo $\bar{X} = 14{,}2\text{ min}$ y $s = 2{,}4\text{ min}$. Para $95\,\%$ de confianza ($t_{9,\,0{,}025} = 2{,}262$):
$$\text{IC}_{95\,\%} = 14{,}2 \pm 2{,}262 \cdot \frac{2{,}4}{\sqrt{10}} = 14{,}2 \pm 1{,}72 \implies [12{,}48;\; 15{,}92]\text{ min}$$

## 4. Comparación de alternativas y análisis de sensibilidad
- **Comparación de escenarios (A vs. B)**: usar **Números Aleatorios Comunes (CRN)** —las mismas semillas para ambos escenarios— para reducir la varianza de la diferencia $\bar{X}_A - \bar{X}_B$ y evaluar con una prueba $t$ pareada si la mejora es estadísticamente significativa.
- **Análisis de sensibilidad**: variar sistemáticamente parámetros críticos ($\pm 10\,\%, \pm 20\,\%$, p. ej., tasa impositiva o tasa de llegada $\lambda$) y medir cuánto cambian las métricas de salida. Permite detectar qué parámetros requieren estimación más precisa.

## Errores comunes
- Reportar los resultados de **una sola corrida** sin réplicas ni intervalo de confianza.
- Tratar muestras correlacionadas dentro de una misma corrida (tiempos de espera de clientes consecutivos) como si fueran independientes para calcular $s/\sqrt{n}$.
- Usar la misma semilla para dos réplicas que se pretenden independientes.

## Ejercicios propuestos
1. Si con $n = 10$ réplicas el semi-ancho del intervalo de confianza es $\pm 4{,}0$ y se desea reducirlo aproximadamente a $\pm 1{,}0$, ¿cuántas réplicas se necesitan aproximadamente?
   - *Respuesta*: para reducir el semi-ancho a $1/4$, se requiere multiplicar $n$ por $4^2 = 16$, es decir, $n \approx 160$ réplicas.
2. Explique la diferencia entre `test_traza_dorada.py` y comparar la simulación contra las fórmulas de $M/M/1$.
   - *Respuesta*: la traza dorada es **verificación** (comprueba que el código ejecuta exactamente las ecuaciones y eventos diseñados); comparar contra $M/M/1$ o datos reales es **validación** (comprueba que el modelo reproduce el comportamiento teórico/real esperado).

## Conexiones
- Inferencia estadística e intervalos $t$ de Student en [[Estadística II]].
- Pruebas automatizadas y análisis de sensibilidad en [[Age of Conquest Simulación de Eventos Discretos]].
- Toma de decisiones bajo incertidumbre en [[Gerencia de Proyectos]].

## Fuente
Basado en [[Simulación de Sistemas]] (Law & Kelton, *Simulation Modeling and Analysis*; Banks et al., *Discrete-Event System Simulation*) y pruebas del proyecto `Age of Conquest - Clon/`.
