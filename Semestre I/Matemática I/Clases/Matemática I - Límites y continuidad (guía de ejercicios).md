---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/Ejercicios de Límites.pdf
---
# Matemática I - Límites y continuidad (guía de ejercicios)

Materia: [[Matemática I]]
Anterior: [[Matemática I - Funciones y sus gráficas]]
Siguiente: [[Matemática I - Derivación: reglas, Rolle, Lagrange y tangentes]]

## Contexto y objetivo
La guía "Ejercicios de Límites y Continuidad" (Unidad 2, UNET, lapso 2016-1) reúne unos 220 ejercicios tomados de Demidovich, Larson, Pita y Purcell. Su estructura es: (1-3) estimación numérica y gráfica; (4-8) existencia de límites y proposiciones verdadero/falso; (9-13) pruebas formales $\varepsilon$-$\delta$; (14-28) propiedades de límites con justificación; (29-185) cálculo de límites (factorización, racionalización, límites al infinito, trigonométricos, exponenciales, etc.); (187-188) teorema del encaje; (189-208) continuidad en un punto y parámetros; (209-216) continuidad en intervalos; (217-220) teorema del valor intermedio. Algunos símbolos del PDF se perdieron en la extracción (funciones definidas por partes), por lo que aquí se explican los métodos con ejemplos propios y los resultados legibles de la guía.

## 1. Idea de límite y límites laterales
$\lim_{x\to a}f(x)=L$ significa que $f(x)$ se acerca a $L$ cuando $x$ se acerca a $a$ (sin importar $f(a)$). Existe si y solo si los **límites laterales** coinciden: $\lim_{x\to a^-}f=\lim_{x\to a^+}f=L$.
La guía enfatiza (ejercicios 6-8): decir que el límite es $L$ **no** significa $f(a)=L$; que el límite no exista no implica que $f(a)$ no exista; y si $f(a)$ no existe el límite puede existir. Contraejemplo: $f(x)=\frac{x^2-9}{x-3}$ en $a=3$: $f(3)$ no existe pero el límite es $6$.

## 2. Definición formal
$\lim_{x\to a}f(x)=L$ si para todo $\varepsilon>0$ existe $\delta>0$ tal que $0<|x-a|<\delta\Rightarrow|f(x)-L|<\varepsilon$.
**Ejemplo (tipo ejercicio 12/13):** probar $\lim_{x\to2}(9x+2)=20$. Se tiene $|9x+2-20|=9|x-2|<\varepsilon$ cuando $|x-2|<\varepsilon/9$. Tomando $\delta=\varepsilon/9$ se cumple. En general, para $kx+d$ (ejercicio 13), $\delta=\varepsilon/|k|$.

## 3. Propiedades
Suma, producto, cociente (denominador del límite $\ne0$), potencia y raíz de límites. Para polinomios y racionales con denominador no nulo basta **sustituir**.
Ejemplo (tipo 18): $\lim_{x\to2}(3x^2+2x-2)=12+4-2=14$.

## 4. Indeterminación $0/0$
- **Factorizar:** $\lim_{x\to3}\frac{x^2-9}{x-3}=\lim(x+3)=6$ (ejercicio 29, R: 6).
- **Cociente de potencias:** $\lim_{x\to1}\frac{x^m-1}{x^n-1}=\frac mn$ (ejercicio 58), por $x^m-1=(x-1)(x^{m-1}+\dots+1)$.
- **Racionalizar** (raíces): $\lim_{x\to0}\frac{\sqrt{x+4}-2}{x}$: multiplicar por el conjugado, $=\lim\frac{1}{\sqrt{x+4}+2}=\frac14$.
- **Productos notables:** $\lim_{x\to0}\frac{(1+x)(1+2x)(1+3x)-1}{x}=\lim\frac{6x+11x^2+6x^3}{x}=6$ (ejercicio 50, R: 6).
- $\lim_{x\to0}\frac{(1+x)^5-(1+5x)}{x^2+x^5}$: el numerador es $10x^2+10x^3+5x^4+x^5$; dividiendo entre $x^2$ resulta $10$ (ejercicio 51, R: 10).
- Con cambio de variable $x=t^n$ para raíces de distinto índice.

## 5. Límites infinitos y al infinito
- $\lim_{x\to a}f(x)=\pm\infty$: **asíntota vertical** $x=a$.
- $\lim_{x\to\pm\infty}f(x)=L$: **asíntota horizontal** $y=L$.
- Racionales: dividir numerador y denominador por la mayor potencia de $x$. $\lim_{x\to\infty}\frac{3x^2+1}{x^2-5}=3$. Si el grado del numerador es menor el límite es $0$; si es mayor, es $\pm\infty$ (y si excede en 1, hay asíntota oblicua).
- $\infty-\infty$: racionalizar. $\lim_{x\to\infty}(\sqrt{x^2+x}-x)=\lim\frac{x}{\sqrt{x^2+x}+x}=\frac12$.
- $1^\infty$: $\lim(1+\frac1x)^x=e$; en general $\lim(1+f)^{g}=e^{\lim fg}$ si $f\to0,g\to\infty$.

## 6. Trigonométricos y teorema del encaje
$\lim_{x\to0}\frac{\sin x}{x}=1$, $\lim_{x\to0}\frac{1-\cos x}{x^2}=\frac12$. Ejemplo: $\lim_{x\to0}\frac{\sin 3x}{5x}=\frac35$.
**Encaje (sándwich):** si $g\le f\le h$ cerca de $a$ y $\lim g=\lim h=L$, entonces $\lim f=L$. Ejemplo: $\lim_{x\to0}x^2\sin(1/x)=0$ porque $-x^2\le x^2\sin(1/x)\le x^2$ (ejercicios 187-188 son de este tipo).

## 7. Continuidad
$f$ es continua en $a$ si (i) $f(a)$ existe, (ii) $\lim_{x\to a}f(x)$ existe, (iii) son iguales. Tipos de discontinuidad: **removible** (el límite existe pero no coincide o no hay $f(a)$), **de salto** (laterales finitos distintos), **esencial/infinita** (límite infinito u oscilante). Respuestas de la guía: #193 discontinuidad esencial infinita; #194 y #195 removible; #196 continua.
**Parámetros (203-208):** se imponen igualdad de límites laterales y valor. Ejemplo propio: $f(x)=\begin{cases}x^2&x<2\\Ax-2&x\ge2\end{cases}$ continua en $2$: $4=2A-2\Rightarrow A=3$.
**En intervalos (209-216):** continua en $(a,b)$ si lo es en cada punto; en $[a,b]$ además continuidad lateral en los extremos. Ej. $f=1/x$ es discontinua en $[-2,5]$ (contiene $0$) pero continua en $[2,5]$.

## 8. Teorema del valor intermedio (TVI)
Si $f$ es continua en $[a,b]$ y $k$ está entre $f(a)$ y $f(b)$, existe $c\in[a,b]$ con $f(c)=k$.
**Ejemplo (ejercicio 217):** $f(x)=x^2+x-1$ en $[0,5]$, $k=11$: $f(0)=-1$, $f(5)=29$. $x^2+x-12=0\Rightarrow x=3$ (o $-4$, fuera). $c=3$.
**Ejemplo (218):** $f(x)=x^2-6x+8$ en $[0,3]$, $k=0$: $f(0)=8$, $f(3)=-1$; $(x-2)(x-4)=0\Rightarrow c=2$.
Uso típico: probar que una ecuación tiene raíz. $x^3+x-1=0$: $f(0)=-1<0$, $f(1)=1>0$, hay raíz en $(0,1)$.

## Errores comunes
- Sustituir directamente cuando resulta $0/0$ y concluir "no existe".
- Cancelar términos en vez de factores.
- Usar L'Hôpital sin verificar la forma indeterminada (véase [[Matemática I - Regla de L'Hôpital]]).
- Olvidar que $\lim_{x\to\infty}$ de $\sqrt{x^2}$ es $|x|$, signo distinto en $-\infty$.

## Ejercicios propuestos
1. $\lim_{x\to1}\frac{x^3-1}{x-1}$. (R: 3.)
2. $\lim_{x\to\infty}\frac{2x^3-x}{5x^3+4}$. (R: 2/5.)
3. $\lim_{x\to0}\frac{\tan x}{x}$. (R: 1.)
4. Probar con $\varepsilon$-$\delta$ que $\lim_{x\to3}(2x+1)=7$. (R: $\delta=\varepsilon/2$.)
5. Hallar $A$ para que $f(x)=\begin{cases}x+1&x<1\\A&x=1\\3-x&x>1\end{cases}$ sea continua en 1. (R: 2.)

## Conexiones
Límites definen la derivada ([[Matemática I - Derivación: reglas, Rolle, Lagrange y tangentes]]); continuidad es hipótesis de Rolle/Lagrange. Resumen previo: [[Matemática I - Optimización y trazado de gráficas]]. Se amplía en [[Matemática II]] (integrales impropias) y [[Matemática III]].

## Fuente
`Material/GUIAS/Ejercicios de Límites.pdf` (guía UNET 2016-1; texto extraído, con símbolos de piecewise parcialmente perdidos).
