---
tags: [clase, semestre-VIII]
materia: Simulación de Sistemas
---
# Simulación de Sistemas - Generación de Números Pseudoaleatorios y Pruebas Estadísticas

Materia: [[Simulación de Sistemas]]
Anterior: [[Simulación de Sistemas - Introducción, Conceptos de Modelo y Metodología]]
Siguiente: [[Simulación de Sistemas - Generación de Variables Aleatorias]]

## Contexto y objetivo
Comprender cómo se generan secuencias de números **pseudoaleatorios** uniformes $U(0,1)$ mediante algoritmos deterministas reproducibles (generadores congruenciales lineales) y cómo verificar estadísticamente su **uniformidad** e **independencia**.

## 1. Números pseudoaleatorios y semilla
En simulación estocástica no usamos azar físico puro, sino algoritmos deterministas que producen secuencias con apariencia de aleatoriedad en $[0, 1)$. La **semilla** ($X_0$) fija el punto de partida y garantiza la **reproducibilidad** de los experimentos (fundamental para depurar y comparar escenarios bajo las mismas condiciones).

Propiedades deseables: uniformidad en $(0,1)$, independencia entre valores sucesivos, período largo antes de repetirse, rapidez de cálculo y reproducibilidad.

## 2. Generador Congruencial Lineal (GCL)
Propuesto por Lehmer (1951), es la base clásica de los generadores:
$$X_{n+1} = (a\,X_n + c) \bmod m, \qquad U_n = \frac{X_n}{m}$$
donde:
- $m > 0$: módulo (determina el período máximo $m$).
- $a$: multiplicador ($0 < a < m$).
- $c$: incremento ($0 \le c < m$; si $c = 0$ es *multiplicativo*, si $c > 0$ es *mixto*).
- $X_0$: semilla ($0 \le X_0 < m$).

**Teorema de Hull-Dobell**: un GCL mixto alcanza período completo $m$ si y solo si:
1. $\text{mcd}(c, m) = 1$ ($c$ y $m$ son coprimos).
2. $a - 1$ es divisible por todos los factores primos de $m$.
3. Si $m$ es divisible por $4$, entonces $a - 1$ también debe ser divisible por $4$.

### Ejemplo resuelto
Sea $a = 5$, $c = 3$, $m = 16$ y semilla $X_0 = 7$:
- $X_1 = (5 \cdot 7 + 3) \bmod 16 = 38 \bmod 16 = 6 \implies U_1 = 6/16 = 0{,}3750$
- $X_2 = (5 \cdot 6 + 3) \bmod 16 = 33 \bmod 16 = 1 \implies U_2 = 1/16 = 0{,}0625$
- $X_3 = (5 \cdot 1 + 3) \bmod 16 = 8 \bmod 16 = 8 \implies U_3 = 8/16 = 0{,}5000$

Verificación de Hull-Dobell: $\text{mcd}(3, 16) = 1$; el único primo de $16$ es $2$ y $a-1=4$ es divisible por $2$ y por $4$. Por tanto, el período es completo ($16$).

## 3. Pruebas estadísticas de uniformidad e independencia
Antes de usar un generador (o para validar una muestra), se aplican pruebas de hipótesis con nivel de significancia $\alpha$ (típicamente $0{,}05$):

### A. Prueba de uniformidad Chi-Cuadrado ($\chi^2$)
Se divide $[0,1)$ en $k$ subintervalos iguales. La frecuencia esperada en cada uno es $E_i = N/k$. Se calcula:
$$\chi_0^2 = \sum_{i=1}^{k} \frac{(O_i - E_i)^2}{E_i}$$
Si $\chi_0^2 \le \chi^2_{\alpha,\, k-1}$, no se rechaza la hipótesis nula de uniformidad.

### B. Prueba de Kolmogorov-Smirnov (K-S)
Compara la función de distribución acumulada empírica $F_N(x)$ con la teórica $F(x) = x$ (útil incluso con muestras pequeñas $N < 30$):
$$D = \max_{1 \le i \le N} \left\{ \left|\frac{i}{N} - U_{(i)}\right|, \; \left|U_{(i)} - \frac{i-1}{N}\right| \right\}$$
donde $U_{(i)}$ son los valores ordenados. Se acepta uniformidad si $D \le D_{\alpha, N}$.

### C. Prueba de independencia: corridas arriba y abajo de la media
Cuenta cuántas secuencias consecutivas (**corridas**) se mantienen por encima o por debajo de $0{,}5$ (o crecientes/decrecientes). Un número excesivamente bajo de corridas indica tendencia/autocorrelación positiva; uno excesivamente alto indica alternancia artificial.

## 4. Generadores modernos
Para simulaciones modernas se usan generadores de período inmenso como **Mersenne Twister** (`random` de Python, período $2^{19937}-1$) o **PCG64** (por defecto en `numpy.random.default_rng`), nunca GCLs pequeños en producción.

## Errores comunes
- Dividir entre $m-1$ cuando el GCL solo alcanza hasta $m-1$ puede producir $U_n = 1{,}0$, lo que rompe fórmulas como $\ln(1 - U)$.
- Usar un GCL con parámetros arbitrarios que colapsan en ciclos muy cortos (p. ej., $a=4, c=2, m=16$).
- No fijar la semilla durante las pruebas de depuración, haciendo imposible reproducir un fallo.

## Ejercicios propuestos
1. Genere los primeros 4 valores de un GCL con $a = 9$, $c = 5$, $m = 16$, $X_0 = 2$. ¿Tiene período completo?
   - *Respuesta*: $X_1 = 7$, $X_2 = 4$, $X_3 = 9$, $X_4 = 6$ ($U = 0{,}4375; 0{,}25; 0{,}5625; 0{,}375$). Cumple Hull-Dobell ($\text{mcd}(5,16)=1$, $9-1=8$ divisible por $2$ y $4$), por lo que tiene período $16$.
2. En una prueba $\chi^2$ con $N = 100$ números y $k = 5$ intervalos se observan frecuencias $O = [18, 22, 19, 21, 20]$. Calcule $\chi_0^2$.
   - *Respuesta*: $E_i = 20$; $\chi_0^2 = \frac{(-2)^2 + 2^2 + (-1)^2 + 1^2 + 0^2}{20} = \frac{10}{20} = 0{,}50$ (muy por debajo de $\chi^2_{0{,}05, 4} = 9{,}49$, pasa uniformidad).

## Conexiones
- Pruebas de bondad de ajuste e hipótesis en [[Estadística II]].
- Aritmética modular en [[Estructuras Discretas]].
- Uso de $U(0,1)$ para generar distribuciones en [[Simulación de Sistemas - Generación de Variables Aleatorias]].

## Fuente
Basado en [[Simulación de Sistemas]] (Banks et al., *Discrete-Event System Simulation*; Law & Kelton, *Simulation Modeling and Analysis*).
