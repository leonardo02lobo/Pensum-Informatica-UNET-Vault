---
tags: [clase, semestre-2]
materia: Matemática II
fuente: conocimiento general
---
# Matemática II - Integral definida y Teorema Fundamental del Cálculo

Materia: [[Matemática II]]
Anterior: [[Matemática II - Antiderivadas e integral indefinida]]
Siguiente: [[Matemática II - Sustitución e integración por partes]]

## Contexto y objetivo
Unidad 2 del temario típico (verificar con el programa oficial): definir el área bajo una curva mediante sumas de Riemann y conectarla con la antiderivada con el Teorema Fundamental del Cálculo (TFC).

## 1. Sumas de Riemann
Partir $[a,b]$ en $n$ subintervalos de ancho $\Delta x=\frac{b-a}n$; elegir $x_i^*$ en cada uno:
$$\int_a^bf(x)\,dx=\lim_{n\to\infty}\sum_{i=1}^nf(x_i^*)\Delta x.$$
Existe si $f$ es continua (o acotada con finitas discontinuidades). Si $f\ge0$ es el área bajo la curva; en general es el **área neta** (sobre el eje $x$ positiva, bajo el eje negativa).

**Ejemplo 1 (por definición).** $\int_0^2x^2dx$: $\Delta x=\frac2n$, $x_i=\frac{2i}n$ (extremo derecho): $\sum\frac{4i^2}{n^2}\cdot\frac2n=\frac8{n^3}\cdot\frac{n(n+1)(2n+1)}6\to\frac{8\cdot2}{6}=\frac83$.

## 2. Propiedades
$\int_a^a f=0$; $\int_b^af=-\int_a^bf$; aditividad $\int_a^b=\int_a^c+\int_c^b$; linealidad; si $f\ge g$ entonces $\int f\ge\int g$; $\left|\int f\right|\le\int|f|$. Simetría: $f$ impar $\Rightarrow\int_{-a}^af=0$; $f$ par $\Rightarrow2\int_0^af$.

## 3. Teorema Fundamental del Cálculo
**Parte 1.** Si $f$ es continua en $[a,b]$ y $g(x)=\int_a^xf(t)dt$, entonces $g'(x)=f(x)$.
Con límite variable y regla de la cadena: $\frac{d}{dx}\int_a^{u(x)}f(t)dt=f(u(x))u'(x)$.
**Parte 2.** Si $F'=f$: $\displaystyle\int_a^bf(x)dx=F(b)-F(a)=\big[F(x)\big]_a^b$.
Idea de la demostración de la parte 2: por la parte 1, $g(x)=\int_a^xf$ es una antiderivada; $F-g$ es constante; $F(b)-F(a)=g(b)-g(a)=\int_a^bf$.

## 4. Ejemplos resueltos
**2.** $\int_1^3(x^2+1)dx=\left[\frac{x^3}3+x\right]_1^3=(9+3)-(\tfrac13+1)=\frac{32}{3}$.
**3.** $\int_0^\pi\sin x\,dx=[-\cos x]_0^\pi=1+1=2$.
**4.** $\int_{-1}^1x^3dx=0$ (impar). Pero $\int_{-1}^1\frac{dx}{x^2}$ **no** se calcula así: el integrando no es acotado en 0 (véase [[Matemática II - Integrales impropias]]).
**5.** $\frac{d}{dx}\int_1^{x^2}\sqrt{1+t^3}\,dt=\sqrt{1+x^6}\cdot2x$.
**6.** Área neta vs área total: $\int_0^{2\pi}\sin x\,dx=0$, pero el área total es $\int_0^{2\pi}|\sin x|dx=4$.
**7. Valor medio.** $f_{prom}=\frac1{b-a}\int_a^bf$. Para $f=x^2$ en $[0,3]$: $\frac13\cdot9=3$.
**8. Teorema del valor medio para integrales:** si $f$ continua, existe $c$ con $f(c)=f_{prom}$; en el ejemplo $c=\sqrt3$.

## 5. Cambio de variable en integral definida
Si $u=g(x)$, $\int_a^bf(g(x))g'(x)dx=\int_{g(a)}^{g(b)}f(u)du$. Ejemplo: $\int_0^1 2x\,e^{x^2}dx$, $u=x^2$: $\int_0^1e^udu=e-1$.

## Errores comunes
- Olvidar cambiar los límites al sustituir.
- Confundir área neta con área total.
- Aplicar el TFC con integrando discontinuo en el intervalo.
- Escribir $F(a)-F(b)$.

## Ejercicios propuestos
1. $\int_0^4\sqrt x\,dx$. (R: $16/3$.)
2. $\frac{d}{dx}\int_0^{\sin x}e^{t^2}dt$. (R: $e^{\sin^2x}\cos x$.)
3. Valor promedio de $\sin x$ en $[0,\pi]$. (R: $2/\pi$.)
4. $\int_0^2|x-1|dx$. (R: 1.)

## Conexiones
El TFC une [[Matemática I]] (derivada) con la integral; se aplica en [[Matemática II - Aplicaciones de la integral: áreas y volúmenes]] y en [[Física I]] (trabajo, desplazamiento).

## Fuente
Conocimiento general (sin Material).
