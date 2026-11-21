---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/TEMA 3-INTERPOLACION Y APROXIMACION POLINOMIAL/MINIMOS CUADRADOS.pdf; Scripts Tema 3/ (polinomio_lagrange.m, otro.m, minimos_cuadrados.m); Scripts Tema 2 (metodo_Newthon.m)
---
# Análisis Numérico - Mínimos cuadrados e interpolación

Materia: [[Análisis Numérico]]
Anterior: [[Análisis Numérico - Práctica 2 Ecuaciones no lineales]]
Siguiente: [[Análisis Numérico - Gauss con pivoteo y factorización LU]]

## Contexto y objetivo
El Tema 3 trata dos formas de construir una función a partir de datos $(x_i,y_i)$: **interpolar** (pasar exactamente por los puntos: Lagrange, diferencias divididas de Newton) y **aproximar** (pasar "cerca": mínimos cuadrados). El único PDF del tema es la presentación "Aproximación de mínimos cuadrados" (Prof. Jenny Pérez); los scripts `polinomio_lagrange.m`, `otro.m`, `metodo_Newthon.m` y `minimos_cuadrados.m` ilustran la interpolación y la regresión. Se añade teoría general de interpolación porque es parte del temario y se evalúa en [[Análisis Numérico - Parcial 1 cuestionario resuelto]].

## A. Mínimos cuadrados (regresión lineal)
**Planteamiento.** Un experimento produce $(x_1,y_1),\dots,(x_n,y_n)$ con abscisas distintas. Se busca $f(x)=ax+b$ (la presentación usa $y=b+mx$). Cada dato cumple $y_i=f(x_i)+e_i$, donde $e_i$ es el error de medición. Las normas posibles de los residuos $r_i=y_i-f(x_i)$ son $\ell_1$, $\ell_2$ y $\ell_\infty$; mínimos cuadrados usa $\ell_2$ al cuadrado (diferenciable y con solución en forma cerrada).

**Deducción.** Se minimiza $E(a,b)=\sum_{i=1}^n(y_i-ax_i-b)^2$. Las condiciones $\partial E/\partial a=0$, $\partial E/\partial b=0$ dan las **ecuaciones normales**:
$$a\sum x_i^2+b\sum x_i=\sum x_iy_i,\qquad a\sum x_i+nb=\sum y_i.$$
Con solución $a=\dfrac{n\sum x_iy_i-\sum x_i\sum y_i}{n\sum x_i^2-(\sum x_i)^2}$, $b=\dfrac{\sum y_i-a\sum x_i}{n}$. El determinante es positivo si las abscisas no son todas iguales.

**Algoritmo (de la presentación).** (1) Tabular $x_i,y_i,x_iy_i,x_i^2$ y sumas; (2) sustituir en las fórmulas; (3) escribir la recta; (4) calcular el error con una tabla $x_i,y_i,f(x_i),(y_i-f(x_i))^2$ y su suma; (5) fin.

**Ejemplo con el script `minimos_cuadrados.m`.** Datos $x=(1,3,5,7,10,12,13,16,18,20)$, $y=(4,5,6,5,8,7,6,9,12,11)$, $n=10$. Sumas: $\sum x=105$, $\sum y=73$, $\sum xy=906$, $\sum x^2=1477$.
$a=\dfrac{10\cdot906-105\cdot73}{10\cdot1477-105^2}=\dfrac{9060-7665}{14770-11025}=\dfrac{1395}{3745}=0.3725$; $b=(73-0.3725\cdot105)/10=3.3888$. El script resuelve el sistema $A\,B=C$ con $A=\begin{pmatrix}n&\sum x\\ \sum x&\sum x^2\end{pmatrix}$, $C=(\sum y,\sum xy)^T$ (`B = inv(A)*C`; es preferible `A\C`) e imprime `a0 = 3.4 y a1 = 0.4` (formato `%.1f`). Suma de cuadrados del error $=12.137$; coeficiente de determinación $R^2=0.811$.
```matlab
A = [n sx; sx sx2];  C = [sy; sxy];
B = A\C;  yp = B(1) + B(2)*x;
plot(x,y,'*'); hold on; plot(x,yp);
```

**Linealización de modelos no lineales.** Si el modelo no es lineal en los parámetros se transforma: $y=ae^{bx}\Rightarrow\ln y=\ln a+bx$; $y=ax^b\Rightarrow\ln y=\ln a+b\ln x$; $k=\dfrac{k_{max}c^2}{c_s+c^2}\Rightarrow\dfrac1k=\dfrac1{k_{max}}+\dfrac{c_s}{k_{max}}\dfrac1{c^2}$ (caso de [[Análisis Numérico - Asignación 1 NACA y ajuste de datos]]). Caso del parcial: $y=K\sin(t+\varphi)=a\cos t+b\sin t$ con $a=K\sin\varphi$, $b=K\cos\varphi$ es **lineal en $(a,b)$**: se resuelve $A^TA\,c=A^Ty$ (ver [[Análisis Numérico - Parcial 1 cuestionario resuelto]]). Para ajuste polinomial de grado $m$: matriz de Vandermonde $V$ y ecuaciones normales $V^TVc=V^Ty$.

## B. Interpolación de Lagrange
Dados $n+1$ nodos distintos, existe un único polinomio de grado $\le n$ con $p(x_i)=y_i$:
$$p(x)=\sum_{i=0}^ny_iL_i(x),\quad L_i(x)=\prod_{j\ne i}\frac{x-x_j}{x_i-x_j},\quad L_i(x_k)=\delta_{ik}.$$
**Error:** $f(x)-p(x)=\dfrac{f^{(n+1)}(\xi)}{(n+1)!}\prod_{i=0}^n(x-x_i)$.
**Ejemplo (Asignación 1, problema 3):** datos $(1.6,2),(2,8),(2.5,14),(3.2,15),(4,8),(4.5,2)$, estimar $f(2.8)$. Orden 1 con $(2.5,14),(3.2,15)$: $14+\frac{0.3}{0.7}=14.4286$. Orden 2 con $(2,8),(2.5,14),(3.2,15)$: $15.4857$. Orden 3 con $(2,8),(2.5,14),(3.2,15),(4,8)$: $15.3886$. Orden 4 con los cinco primeros: $15.6014$. Criterio: elegir los nodos más cercanos al punto evaluado y rodearlo.

`polinomio_lagrange.m` construye simbólicamente $p(x)$ para $\cos x$ en los nodos $x_k=k\pi/2$, $k=0..4$, con `syms x`, un doble bucle para $L_i$, `expand` y `coeffs`. Resultado: coeficientes en orden decreciente $(-0.0274,\;0.3440,\;-1.1483,\;0.4244,\;1.0)$, es decir $p(x)\approx-0.0274x^4+0.3440x^3-1.1483x^2+0.4244x+1$.

## C. Diferencias divididas de Newton
$f[x_i]=f(x_i)$, $f[x_i,\dots,x_{i+k}]=\dfrac{f[x_{i+1},\dots,x_{i+k}]-f[x_i,\dots,x_{i+k-1}]}{x_{i+k}-x_i}$ y
$p(x)=f[x_0]+f[x_0,x_1](x-x_0)+f[x_0,x_1,x_2](x-x_0)(x-x_1)+\cdots$. Mismo polinomio que Lagrange, pero agregar un nodo no obliga a recalcular.
`metodo_Newthon.m`: $x=(60,80,100,120)$, $y=(81,104,137,162)$: columnas $1.15,1.65,1.25$; luego $0.0125,-0.01$; la tercera diferencia es $-0.000375$ (el script imprime `-0.000375`; indexa `dd_table(4,4)`).
`otro.m`: tabla para $\cos$ en $0,\pi/2,\dots,2\pi$; las diferencias en la diagonal son $1,\,-0.6366,\,0,\,0.0860,\,-0.0274$ (orden 0 a 4); `diag(tabla)` las extrae solo si la tabla se llena por filas como en el script.
Ejemplo de parcial: interpolar $1/(1+x^2)$ en $[-5,5]$ con 5 nodos equiespaciados y evaluar en $x=1$ da $p(1)=0.8342$ (función par: $p=1-0.17109x^2+0.005305x^4$, mientras que el valor real es $0.5$). Es el **fenómeno de Runge**: nodos equiespaciados con grado alto oscilan en los extremos; remedio: nodos de Chebyshev o splines.

## Errores comunes
Usar la tabla de diferencias con nodos repetidos; confundir "pasa por los puntos" con "mejor ajuste"; extrapolar con polinomios de grado alto; calcular $R^2$ sobre datos linealizados y presentarlo como si fuera del modelo original; `inv(A)` en vez de `A\b`.

## Ejercicios propuestos
1. Recta de mínimos cuadrados para $(0,1),(1,3),(2,4),(3,8)$. (Resp.: $y=0.7+2.2x$.)
2. Polinomio que interpola $(0,1),(1,2),(2,5)$. (Resp.: $x^2+1$.)
3. Cota del error de interpolar $\cos$ con los nodos $0,\pi/2,\pi$ en $x=\pi/4$. (Resp.: $\le\frac16\cdot\frac{\pi}{4}\cdot\frac{\pi}{4}\cdot\frac{3\pi}{4}\approx0.242$, pues $|\cos'''|\le1$.)

## Conexiones
Mismo sistema lineal de [[Análisis Numérico - Gauss con pivoteo y factorización LU]] (ecuaciones normales). La integración de Newton-Cotes ([[Análisis Numérico - Integración numérica Newton-Cotes]]) integra el polinomio interpolante.

## Fuente
`MINIMOS CUADRADOS.pdf` (presentación; las fórmulas estaban en imágenes y se reconstruyeron), y los scripts indicados en `Material/TEMA 3.../Scripts Tema 3/`.
