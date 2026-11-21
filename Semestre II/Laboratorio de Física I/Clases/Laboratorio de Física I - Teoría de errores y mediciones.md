---
tags: [clase, semestre-II]
materia: Laboratorio de Física I
fuente: conocimiento general
---
# Laboratorio de Física I - Teoría de errores y mediciones

Materia: [[Laboratorio de Física I]]
Siguiente: [[Laboratorio de Física I - Informe de inercia]]

## Contexto y objetivo
Toda práctica de laboratorio (inercia, choques, proyectos) produce números obtenidos con instrumentos imperfectos. Esta nota explica cómo expresar una medida, cuantificar su incertidumbre, propagarla a magnitudes calculadas y ajustar modelos lineales, semilogarítmicos y bilogarítmicos, que son las tres formas de gráfica que aparecen en el cuestionario del informe de inercia. Es el marco teórico común de todos los informes. Complementa a [[Física I]] y usa herramientas de [[Matemática I]] (pendientes, logaritmos) y [[Estadística I]] (dispersión y ajuste).

## 1. Medir y comparar con un patrón
Medir es comparar una magnitud con un patrón. En el Sistema Internacional: longitud (m), masa (kg), tiempo (s). Una medida se escribe $x = (\bar{x} \pm \Delta x)\ \text{unidad}$. Un resultado sin unidad o sin incertidumbre es incompleto.

Instrumentos típicos del laboratorio:
- Regla: apreciación 1 mm (0,1 cm).
- Cronómetro manual: apreciación 0,01 s, pero el tiempo de reacción humano (~0,2 s) domina el error real.
- Balanza: apreciación según modelo (0,1 g, 1 g).
- Vernier (calibrador): 0,05 mm o 0,02 mm.
- Timbre registrador de chispas: frecuencia fija (en el informe de choques, 30 chispas por segundo).

## 2. Tipos de error
- **Sistemáticos**: desvían siempre en el mismo sentido (cero mal ajustado, regla dilatada, mesa no nivelada, fricción no considerada). No se reducen repitiendo la medida; se corrigen calibrando o mejorando el modelo.
- **Aleatorios** (accidentales): fluctúan en ambos sentidos (tiempo de reacción, lectura de escala). Se reducen promediando muchas medidas.
- **Groseros**: equivocaciones (anotar 11 en vez de 1; en el informe de choques aparece "1+11+1.5+1.1" cuando el dato era 1). Se detectan revisando.

## 3. Cifras significativas y redondeo
Las cifras significativas son los dígitos confiables más el primero dudoso. Reglas:
1. Los ceros a la izquierda no cuentan (0,0045 tiene 2 cifras).
2. En multiplicación y división el resultado lleva tantas cifras como el factor con menos cifras.
3. En suma y resta se conserva el menor número de decimales.
4. La incertidumbre se redondea a 1 cifra significativa (a 2 si empieza en 1) y la medida se redondea al mismo decimal: $9{,}8 \pm 0{,}1$, no $9{,}8137 \pm 0{,}1$.

## 4. Incertidumbre de una medida repetida
Dadas $n$ mediciones $x_i$:
- Media: $\bar{x} = \frac{1}{n}\sum x_i$.
- Desviación estándar muestral: $s = \sqrt{\frac{\sum (x_i-\bar{x})^2}{n-1}}$.
- Incertidumbre de la media: $\Delta \bar{x} = \frac{s}{\sqrt{n}}$.
- Error absoluto: $\Delta x$ (mismas unidades). Error relativo: $\Delta x/\bar{x}$. Error porcentual: $\varepsilon\% = \frac{|x_{teo} - x_{exp}|}{x_{teo}}\cdot 100$.

### Ejemplo resuelto
Cinco mediciones del tiempo de caída: 2,39; 2,41; 2,35; 2,44; 2,36 s.
1. $\bar t = (2{,}39+2{,}41+2{,}35+2{,}44+2{,}36)/5 = 2{,}39$ s.
2. Desviaciones: 0; 0,02; -0,04; 0,05; -0,03. Cuadrados: 0; 0,0004; 0,0016; 0,0025; 0,0009; suma 0,0054.
3. $s=\sqrt{0{,}0054/4}=0{,}037$ s. $\Delta\bar t = 0{,}037/\sqrt5 = 0{,}017$ s.
4. Resultado: $t = (2{,}39 \pm 0{,}02)$ s.

## 5. Propagación de incertidumbres
Para $z = f(x,y)$ con errores independientes:
$$\Delta z = \sqrt{\left(\frac{\partial f}{\partial x}\Delta x\right)^2 + \left(\frac{\partial f}{\partial y}\Delta y\right)^2}$$
Casos prácticos:
- Suma/resta: $\Delta z = \sqrt{\Delta x^2 + \Delta y^2}$.
- Producto/cociente $z = x^a y^b$: $\frac{\Delta z}{z} = \sqrt{(a\frac{\Delta x}{x})^2 + (b\frac{\Delta y}{y})^2}$.

### Ejemplo: aceleración en la práctica de inercia
$a = 2H/t^2$ con $H = 0{,}95 \pm 0{,}01$ m y $t = 2{,}39 \pm 0{,}02$ s.
- $a = 1{,}90/5{,}712 = 0{,}333$ m/s².
- $\Delta a/a = \sqrt{(0{,}01/0{,}95)^2 + (2\cdot 0{,}02/2{,}39)^2} = \sqrt{1{,}1\times10^{-4}+2{,}8\times10^{-4}} = 0{,}0198$.
- $\Delta a = 0{,}0066$ m/s². Resultado $a = (0{,}333 \pm 0{,}007)$ m/s². Notar que el tiempo, elevado al cuadrado, domina.

## 6. Gráficas y ajuste de modelos
El informe de inercia plantea tres modelos; se elige el que linealiza los datos.
1. **Lineal**: $y = mx + b$, con $m = \frac{y_2-y_1}{x_2-x_1}$. Se verifica con papel milimetrado (puntos alineados).
2. **Semilogarítmica**: $y = b\,e^{mx}$ (en el informe escrita $b e^{2{,}3 m x}$ con $m=\frac{\log y_2 - \log y_1}{x_2-x_1}$, usando $\ln 10 \approx 2{,}3$). Es una recta en papel semilogarítmico; típica de decaimientos.
3. **Bilogarítmica** (log-log): $y = b x^m$, con $m = \frac{\log y_2-\log y_1}{\log x_2-\log x_1}$ y $b = y/x^m$. Recta en papel log-log; la pendiente es el exponente. Si $m \approx 2$ la ley es cuadrática, como $H = \tfrac12 a t^2$.

Significado físico: la pendiente tiene unidades $[y]/[x]$; el corte con el eje $y$ es el valor de $y$ cuando $x=0$ (por ejemplo torque residual por fricción en el eje). Para elegir una escala: usa al menos 2/3 de la hoja, rotula ejes con unidades, no unir los puntos con línea quebrada; traza la recta de mejor ajuste (mínimos cuadrados) y toma dos puntos de la recta, no de los datos, para la pendiente.

### Mínimos cuadrados (ajuste lineal)
$m = \frac{n\sum xy - \sum x \sum y}{n\sum x^2 - (\sum x)^2}$, $b = \bar{y} - m\bar{x}$.

## Errores comunes
- Dar 8 decimales de una calculadora cuando el instrumento tiene 2 cifras.
- Cambiar de unidades a mitad del cálculo (cm y m).
- Cronometrar una sola vez.
- Calcular la pendiente con puntos experimentales dispersos en lugar de puntos de la recta.
- Confundir exactitud (cercanía al valor verdadero) con precisión (dispersión pequeña).

## Ejercicios propuestos
1. Una regla de 1 mm mide 24,3 cm y 5,2 cm. Suma e incertidumbre. (Resp. 29,5 cm; $\pm 0{,}14$ cm si se propaga cuadráticamente.)
2. Calcula $g$ con un péndulo $T=2\pi\sqrt{L/g}$, $L=1{,}00\pm0{,}01$ m, $T=2{,}01\pm0{,}02$ s. (Resp. $g\approx 9{,}77 \pm 0{,}2$ m/s².)
3. Datos $(x,y)$: (1;2,1), (2;4,0), (3;6,1), (4;7,9). Pendiente por mínimos cuadrados. (Resp. $m\approx 1{,}95$, $b\approx 0{,}15$.)
4. Si $y=b x^m$ y al duplicar $x$ se triplica $y$, ¿cuánto vale $m$? (Resp. $\log 3/\log 2 \approx 1{,}58$.)

## Conexiones
- Aplicación directa en [[Laboratorio de Física I - Informe de inercia]] (gráficas e interpretación de pendiente) y [[Laboratorio de Física I - Informe de choques]] (porcentaje de pérdida de energía).
- Se profundiza en [[Estadística I]].

## Fuente
Conocimiento general; los tres modelos de gráfica provienen del cuestionario de `Material/informe de inercia.docx`.
