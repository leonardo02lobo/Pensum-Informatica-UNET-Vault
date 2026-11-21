---
tags: [clase, semestre-2]
materia: Matemática II
fuente: conocimiento general
---
# Matemática II - Sustitución e integración por partes

Materia: [[Matemática II]]
Anterior: [[Matemática II - Integral definida y Teorema Fundamental del Cálculo]]
Siguiente: [[Matemática II - Integrales trigonométricas y sustitución trigonométrica]]

## Contexto y objetivo
Primeras técnicas de integración. Objetivo: reconocer cuándo usar cambio de variable y cuándo integración por partes.

## 1. Sustitución (cambio de variable)
Si el integrando tiene la forma $f(g(x))g'(x)$: sea $u=g(x)$, $du=g'(x)dx$ y $\int f(g)g'dx=\int f(u)du$. Es la regla de la cadena al revés.
**Ejemplos.**
1. $\int2x\cos(x^2)dx$: $u=x^2$, $du=2xdx$: $\sin(x^2)+C$.
2. $\int\frac{x}{x^2+1}dx$: $u=x^2+1$, $du=2xdx$: $\frac12\ln(x^2+1)+C$.
3. $\int\tan x\,dx=\int\frac{\sin x}{\cos x}dx$, $u=\cos x$: $-\ln|\cos x|+C=\ln|\sec x|+C$.
4. $\int x\sqrt{x-1}\,dx$: $u=x-1$, $x=u+1$: $\int(u+1)u^{1/2}du=\frac25u^{5/2}+\frac23u^{3/2}+C$.
5. Definida: $\int_0^{\pi/2}\sin^3x\cos x\,dx$, $u=\sin x$: $\int_0^1u^3du=\frac14$.
6. $\int\frac{e^x}{1+e^{2x}}dx$, $u=e^x$: $\arctan(e^x)+C$.

## 2. Integración por partes
De $(uv)'=u'v+uv'$: $$\int u\,dv=uv-\int v\,du.$$ En definidas: $\int_a^bu\,dv=[uv]_a^b-\int_a^bv\,du$.
**Elección de $u$ (regla LIATE):** Logarítmicas, Inversas trigonométricas, Algebraicas, Trigonométricas, Exponenciales; $u$ es la primera que aparezca en la lista.

**Ejemplos.**
1. $\int xe^x dx$: $u=x$, $dv=e^xdx$; $=xe^x-\int e^xdx=e^x(x-1)+C$.
2. $\int\ln x\,dx$: $u=\ln x$, $dv=dx$, $du=\frac{dx}x$, $v=x$: $x\ln x-x+C$.
3. $\int x^2\sin x\,dx$ (dos veces): $u=x^2$: $-x^2\cos x+2\int x\cos x\,dx$; luego $u=x$: $\int x\cos x=x\sin x+\cos x$. Total: $-x^2\cos x+2x\sin x+2\cos x+C$.
4. $\int e^x\sin x\,dx$ (cíclica): $I=e^x\sin x-\int e^x\cos x=e^x\sin x-e^x\cos x-I\Rightarrow I=\frac{e^x}2(\sin x-\cos x)+C$.
5. $\int\arctan x\,dx=x\arctan x-\frac12\ln(1+x^2)+C$.
6. $\int_1^e\ln x\,dx=[x\ln x-x]_1^e=(e-e)-(0-1)=1$.

## 3. Combinar técnicas
$\int x^3e^{x^2}dx$: sustitución $w=x^2$ ($x^2\cdot xdx=w\,dw/2$) y luego partes: $\frac12\int we^wdw=\frac12e^w(w-1)=\frac12e^{x^2}(x^2-1)+C$.

## Errores comunes
- No convertir todo el integrando a $u$ (queda $x$ mezclada).
- Olvidar cambiar límites o volver a $x$.
- Escoger mal $u$ y complicar (p. ej. $u=e^x$, $dv=x\,dx$ en $\int xe^x$).
- Signos en partes repetidas.

## Ejercicios propuestos
1. $\int x\cos x\,dx$. (R: $x\sin x+\cos x+C$.)
2. $\int\frac{\ln x}{x}dx$. (R: $\frac12\ln^2x+C$.)
3. $\int_0^1xe^{-x}dx$. (R: $1-2/e$.)
4. $\int x\ln x\,dx$. (R: $\frac{x^2}2\ln x-\frac{x^2}4+C$.)

## Conexiones
Preparan las integrales trigonométricas y fracciones parciales; se usan en [[Matemática II - Series de potencias, Taylor y Maclaurin]] y en transformadas de [[Matemática IV]].

## Fuente
Conocimiento general (sin Material).
