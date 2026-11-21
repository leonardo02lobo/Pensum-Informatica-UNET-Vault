---
tags: [clase, semestre-VIII]
materia: Finanzas para Ingenieros
---
# Finanzas para Ingenieros - Rendimiento, Riesgo y Teoría de Portafolios de Markowitz

Materia: [[Finanzas para Ingenieros]]
Anterior: [[Finanzas para Ingenieros - Fundamentos Económicos, Mercancía y Sistema Financiero]]
Siguiente: [[Finanzas para Ingenieros - Algoritmos Genéticos y Optimización de Portafolios]]

## Contexto y objetivo
Cuantificar el **rendimiento esperado** y el **riesgo** de activos financieros individuales y portafolios, demostrar el efecto matemático de la **diversificación** mediante covarianzas y formular el modelo de media-varianza de **Harry Markowitz (1952)** y el **Ratio de Sharpe**.

## 1. Rendimiento y riesgo de un activo individual
A partir de una serie de precios $P_t$, el rendimiento por período se calcula como:
- **Rendimiento simple**: $R_t = \dfrac{P_t - P_{t-1}}{P_{t-1}}$
- **Rendimiento logarítmico** (aditivo en el tiempo): $r_t = \ln\left(\dfrac{P_t}{P_{t-1}}\right)$

Para un activo con escenarios probabilísticos (o serie histórica):
- **Rendimiento esperado**: $\mu = E(R) = \sum_{i} p_i R_i$
- **Varianza y volatilidad (riesgo)**:
  $$\sigma^2 = \text{Var}(R) = \sum_{i} p_i \big(R_i - E(R)\big)^2, \qquad \sigma = \sqrt{\sigma^2}$$
Para anualizar datos semanales (52 semanas/año): $\mu_{\text{anual}} = 52\,\mu_{\text{sem}}$ y $\sigma_{\text{anual}} = \sqrt{52}\,\sigma_{\text{sem}}$.

## 2. Rendimiento y riesgo de un portafolio (diversificación)
Sea un portafolio con pesos $x = (x_1, \dots, x_n)^T$ tales que $\sum_{i=1}^n x_i = 1$ y $x_i \ge 0$ (sin ventas en corto):
$$E(R_p) = \sum_{i=1}^{n} x_i E(R_i) = x^T \mu$$
$$\sigma_p^2 = \sum_{i=1}^{n}\sum_{j=1}^{n} x_i x_j \sigma_{ij} = x^T \Sigma x$$
donde $\sigma_{ij} = \text{Cov}(R_i, R_j) = \rho_{ij}\sigma_i\sigma_j$ y $\Sigma$ es la matriz de covarianzas.

Para **dos activos**, la varianza del portafolio es:
$$\sigma_p^2 = x_1^2\sigma_1^2 + x_2^2\sigma_2^2 + 2 x_1 x_2 \rho_{12}\sigma_1\sigma_2$$
Siempre que la correlación $\rho_{12} < 1$, el riesgo del portafolio $\sigma_p$ es **estrictamente menor** que el promedio ponderado de los riesgos individuales $x_1\sigma_1 + x_2\sigma_2$: ese es el beneficio de la **diversificación** (reduce el *riesgo no sistemático*).

### Ejemplo resuelto
Activo A ($\mu_A = 10\,\%, \sigma_A = 20\,\%$) y Activo B ($\mu_B = 14\,\%, \sigma_B = 30\,\%$), con $\rho = 0{,}20$, invertidos $50\,\%$ y $50\,\%$:
- $E(R_p) = 0{,}5(10\,\%) + 0{,}5(14\,\%) = 12\,\%$
- $\sigma_p^2 = 0{,}5^2(0{,}20)^2 + 0{,}5^2(0{,}30)^2 + 2(0{,}5)(0{,}5)(0{,}20)(0{,}20)(0{,}30) = 0{,}01 + 0{,}0225 + 0{,}006 = 0{,}0385$
- $\sigma_p = \sqrt{0{,}0385} \approx 19{,}62\,\%$ (menor que el riesgo de A, ¡con mayor rendimiento!).

## 3. Modelo de Markowitz, frontera eficiente y Ratio de Sharpe
El problema de optimización paramétrica de Markowitz busca carteras eficientes:
$$\min_{x} \; x^T \Sigma x \quad \text{sujeto a} \quad x^T \mu = R^*, \quad \sum_{i=1}^n x_i = 1, \quad x_i \ge 0$$
Variando el rendimiento objetivo $R^*$ se traza la **frontera eficiente**: el conjunto de portafolios que ofrecen el máximo rendimiento posible para cada nivel de riesgo (o mínimo riesgo para cada rendimiento).

Al introducir un activo libre de riesgo con tasa $R_f$, la mejor cartera riesgosa es la que maximiza el **Ratio de Sharpe** (rendimiento excedente por unidad de riesgo total):
$$\text{Sharpe} = \frac{E(R_p) - R_f}{\sigma_p}$$

En el **CAPM** (Modelo de Valoración de Activos de Capital), el riesgo sistemático de un activo se mide mediante su coeficiente $\beta_i = \frac{\text{Cov}(R_i, R_m)}{\text{Var}(R_m)}$ y su rendimiento esperado en equilibrio es $E(R_i) = R_f + \beta_i\big(E(R_m) - R_f\big)$.

## Errores comunes
- Promediar desviaciones estándar linealmente ($\sigma_p = \sum x_i \sigma_i$), olvidando el término de covarianza/correlación.
- Anualizar la desviación estándar multiplicando por 52 en lugar de $\sqrt{52}$.
- Olvidar normalizar los pesos para que $\sum x_i = 1$.

## Ejercicios propuestos
1. Dos activos incorrelacionados ($\rho = 0$) tienen $\sigma_1 = \sigma_2 = 20\,\%$. ¿Qué volatilidad tiene un portafolio equiponderado ($50\,\% / 50\,\%$)?
   - *Respuesta*: $\sigma_p = \sqrt{0{,}25(0{,}04) + 0{,}25(0{,}04)} = \sqrt{0{,}02} \approx 14{,}14\,\%$.
2. Si un portafolio tiene $E(R_p) = 16\,\%$, $\sigma_p = 24\,\%$ y $R_f = 4\,\%$, calcule su Ratio de Sharpe.
   - *Respuesta*: $(0{,}16 - 0{,}04) / 0{,}24 = 0{,}50$.

## Conexiones
- Estadística descriptiva, varianza y covarianza en [[Estadística I]] y [[Estadística II]].
- Álgebra lineal y matrices cuadráticas en [[Matemática IV]].
- Implementación evolutiva en [[Finanzas para Ingenieros - Algoritmos Genéticos y Optimización de Portafolios]] y [[Modelo de Markowitz y Algoritmo Genético]].

## Fuente
Basado en [[Finanzas para Ingenieros]] y `Material/Tema 2/TeoriadePortafolios-0408.pdf` y `La rentabilidad y el riesgo en las inversiones financieras.pdf`.
