---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 08 - Estadística aplicada a la investigación

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 07 - Instrumentos, validez y confiabilidad]]
Siguiente: [[MI 09 - Redacción académica, citas y referencias]]

## Contexto y objetivo
Tras recolectar datos hay que describirlos, contrastar hipótesis y presentar resultados con honestidad. Esta clase es una guía de decisión: qué prueba usar según escala y diseño, con ejemplos calculados a mano y en Python. Presupone [[Estadística I]] y [[Estadística II]].

## Estadística descriptiva
- **Tendencia central**: media $\bar{x}=\frac{1}{n}\sum x_i$, mediana, moda.
- **Dispersión**: varianza $s^2 = \frac{\sum (x_i-\bar{x})^2}{n-1}$, desviación estándar $s$, rango, coeficiente de variación $CV = s/\bar{x}$, cuartiles y IQR.
- **Forma**: asimetría, curtosis.
- **Presentación**: tablas de frecuencia, histogramas, diagramas de caja, barras; gráficos sin truncar ejes de manera engañosa; etiquetar unidades y *n*.
- **Intervalo de confianza** para la media: $\bar{x} \pm t_{\alpha/2,\,n-1}\,\dfrac{s}{\sqrt{n}}$.

## Elección de la prueba de hipótesis
| Objetivo | Datos (razón/intervalo, normales) | No paramétrica / ordinal |
|---|---|---|
| Comparar 2 grupos independientes | t de Student (Welch si varianzas distintas) | Mann-Whitney U |
| Comparar 2 mediciones del mismo grupo (pre/post) | t pareada | Wilcoxon de rangos con signo |
| Comparar 3 o más grupos | ANOVA de un factor (+ post hoc Tukey) | Kruskal-Wallis |
| Relación entre dos variables | Pearson $r$ | Spearman $\rho$ |
| Asociación entre categóricas | $\chi^2$ de independencia (Fisher si frecuencias esperadas menores de 5) | |
| Proporciones | Prueba z de proporciones | |
| Predicción | Regresión lineal/logística | |
Verificar supuestos: normalidad (Shapiro-Wilk, gráfico Q-Q), homogeneidad de varianzas (Levene), independencia de observaciones.

## Prueba t pareada: ejemplo resuelto
Tiempos (min) de préstamo de 6 solicitudes **antes** y **después** del sistema (mismos tipos de solicitud):
| i | Antes | Después | d = antes - después |
|---|---|---|---|
| 1 | 12 | 8 | 4 |
| 2 | 10 | 7 | 3 |
| 3 | 15 | 9 | 6 |
| 4 | 9 | 8 | 1 |
| 5 | 14 | 9 | 5 |
| 6 | 11 | 7 | 4 |
1. $H_0: \mu_d = 0$; $H_a: \mu_d > 0$; $\alpha = 0.05$.
2. $\bar{d} = 23/6 = 3.833$. Desviaciones: .167, -.833, 2.167, -2.833, 1.167, .167 → cuadrados: .028+.694+4.694+8.028+1.361+.028 = 14.833; $s_d^2 = 14.833/5 = 2.967$; $s_d = 1.722$.
3. $t = \bar{d}/(s_d/\sqrt{n}) = 3.833/(1.722/2.449) = 3.833/0.703 = 5.45$, gl = 5.
4. $t_{crit}(0.05,5)$ unilateral = 2.015. Como 5.45 > 2.015 → **se rechaza H0**; p aproximado 0.0014.
5. Conclusión: hay evidencia de que el tiempo disminuyó. Reporta además el tamaño del efecto: $d_{Cohen} = \bar{d}/s_d = 2.2$ (grande).
```python
import numpy as np
from scipy import stats
antes  = np.array([12,10,15,9,14,11])
despues= np.array([8,7,9,8,9,7])
t, p = stats.ttest_rel(antes, despues, alternative="greater")
print(round(t,2), round(p,4))               # 5.45  0.0014
d = antes - despues
print(round(d.mean()/d.std(ddof=1), 2))     # tamaño de efecto 2.23
print(stats.shapiro(d))                     # normalidad de diferencias
```
Nota: con n=6 los supuestos son difíciles de verificar; úsalo como demostración.

## Correlación
**Pearson**: $r = \dfrac{\sum (x_i-\bar{x})(y_i-\bar{y})}{\sqrt{\sum (x_i-\bar{x})^2 \sum (y_i-\bar{y})^2}}$, con $-1\le r\le 1$. Interpretación orientativa (Cohen): 0.1 pequeño, 0.3 mediano, 0.5 grande. **Determinación** $r^2$. **Correlación no implica causalidad** (variables confusoras, causalidad inversa, azar).
```python
from scipy.stats import pearsonr, spearmanr
horas = [2,4,5,7,8,10]; nota = [8,10,11,14,15,18]
print(pearsonr(horas, nota))     # r cercano a 1
```

## Chi-cuadrado de independencia
$\chi^2 = \sum \dfrac{(O-E)^2}{E}$, con $E = \frac{\text{total fila}\times \text{total col}}{n}$, gl = (filas-1)(columnas-1).
Ejemplo: tabla 2x2 (usa el sistema: sí/no) x (satisfecho: sí/no) con O = (40, 10; 20, 30), n = 100. E = (30, 20; 30, 20)... totales de fila 50 y 50; de columna 60 y 40. $E_{11} = 50\times 60/100 = 30$; $E_{12}=20$; $E_{21}=30$; $E_{22}=20$. $\chi^2 = 100/30 + 100/20 + 100/30 + 100/20 = 3.33+5+3.33+5 = 16.67$; gl = 1; crítico (0.05) = 3.84 → hay asociación.

## Regresión lineal simple
$\hat{y} = b_0 + b_1 x$, $b_1 = \dfrac{\sum (x-\bar{x})(y-\bar{y})}{\sum (x-\bar{x})^2}$, $b_0 = \bar{y} - b_1\bar{x}$. Reporta coeficientes con IC, $R^2$, residuos. Supuestos: linealidad, independencia, homocedasticidad, normalidad de residuos.

## Evaluación de modelos y software (comparaciones)
- Comparar algoritmos: **validación cruzada k-fold** y prueba t pareada sobre los folds (o Wilcoxon), reporta media $\pm$ desviación. Ver [[Aprendizaje Automático]].
- Benchmarks: repeticiones (mínimo 10-30), eliminar el calentamiento, reportar mediana e IC; usar pruebas no paramétricas si hay colas largas.
- Usabilidad: SUS por usuario, contrastar con 68.

## Reporte de resultados
Estructura por objetivo: tabla/figura + interpretación breve + vínculo con hipótesis. Reporta: estadístico, gl, valor p exacto, tamaño del efecto, IC; **no** solo "p < 0.05". Evita *p-hacking* (probar muchas pruebas hasta hallar significancia) y corrige comparaciones múltiples (Bonferroni: $\alpha/m$). Distingue **significancia estadística** de **relevancia práctica**.

## Análisis cualitativo (breve)
Transcribir, **codificar** (abierta, axial, selectiva), agrupar en categorías/temas, verificar con triangulación y revisión por pares, presentar citas textuales anonimizadas; software: Atlas.ti, NVivo, Taguette (libre).

## Herramientas
Excel/LibreOffice Calc (descriptiva básica), **Python** (pandas, scipy, statsmodels, matplotlib/seaborn), **R**, JASP/jamovi (gráficas e interfaz amigable), SPSS (licenciado).

## Errores comunes
- Usar t con datos ordinales o muy asimétricos sin justificar.
- Concluir "se aceptó H0".
- Comparar grupos de distinto tamaño con una prueba para muestras pareadas, o viceversa.
- Ignorar valores atípicos sin documentarlo.
- Reportar solo medias, sin dispersión.
- Muestras diminutas con conclusiones categóricas.

## Ejercicios propuestos
1. n=25, $\bar{x}=50$, $s=10$; IC 95% de la media ($t_{24}=2.064$). *Resp.: 50 $\pm$ 2.064(10/5) = (45.87; 54.13).*
2. ¿Prueba para comparar tres algoritmos con exactitud en 10 folds cada uno? *Resp.: ANOVA de medidas repetidas o Friedman (no paramétrica).*
3. Si $p = 0.03$ y $\alpha=0.01$, ¿decisión? *Resp.: no se rechaza H0.*

## Conexiones
[[Estadística I]], [[Estadística II]], [[Análisis y Procesamiento de Datos]], [[Aprendizaje Automático]], [[MI 06 - Diseño metodológico, población y muestra]].

## Fuente
Conocimiento general. Montgomery y Runger, *Probabilidad y estadística aplicadas a la ingeniería*; Field, *Discovering Statistics*; documentación de SciPy.
