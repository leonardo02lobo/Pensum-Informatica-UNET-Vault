---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf (sección IV, ejercicios 36-67)
---
# Matemática I - Regla de L'Hôpital

Materia: [[Matemática I]]
Anterior: [[Matemática I - Derivación: reglas, Rolle, Lagrange y tangentes]]
Siguiente: [[Matemática I - Razón de cambio y razones relacionadas]]

## Contexto y objetivo
La sección IV de la guía propone 32 límites (ejercicios 36-67) para resolver con la regla de L'Hôpital. Objetivo: reconocer las siete formas indeterminadas, transformarlas a $0/0$ o $\infty/\infty$ y aplicar la regla correctamente.

## 1. Enunciado
Si $\lim_{x\to a}\frac{f}{g}$ es de la forma $\frac00$ o $\frac{\pm\infty}{\pm\infty}$, $f,g$ derivables cerca de $a$ ($g'\ne0$) y existe $\lim\frac{f'}{g'}$ (finito o infinito), entonces $\lim\frac fg=\lim\frac{f'}{g'}$. Vale también para $x\to\pm\infty$ y límites laterales. Se deduce del teorema de Cauchy (generalización de Lagrange). **Se deriva numerador y denominador por separado; no es la derivada del cociente.**

## 2. Otras formas
- $0\cdot\infty$: escribir $f\cdot g=\frac{f}{1/g}$.
- $\infty-\infty$: común denominador o racionalizar.
- $0^0,\ 1^\infty,\ \infty^0$: tomar logaritmo: $\lim f^g=e^{\lim g\ln f}$.

## 3. Ejemplos de la guía, resueltos
**#36** $\lim_{x\to2}\frac{2x^3-9x^2+12x-4}{2x^3-3x^2-12x+20}$. En 2: $16-36+24-4=0$ y $16-12-24+20=0$ ($0/0$). Primera derivada: $\frac{6x^2-18x+12}{6x^2-6x-12}\to\frac00$ otra vez. Segunda: $\frac{12x-18}{12x-6}=\frac{6}{18}=\frac13$. R: $1/3$ ✓.

**#37** $\lim_{x\to\infty}\frac{x^{10}}{10^x}$: $\infty/\infty$; derivando 10 veces: $\frac{10!}{(\ln10)^{10}10^x}\to0$. Idea: la exponencial domina a cualquier potencia.

**#44** $\lim_{x\to\infty}xe^{-x}=\lim\frac{x}{e^x}=\lim\frac1{e^x}=0$ ($0\cdot\infty$).

**#38** $\lim_{x\to1}\left(\frac{2}{x^2-1}-\frac1{x-1}\right)$ ($\infty-\infty$): $=\lim\frac{2-(x+1)}{x^2-1}=\lim\frac{1-x}{x^2-1}=\lim\frac{-1}{x+1}=-\frac12$ ✓.

**#39** $\lim_{x\to0^+}[\ln(1+x)]^x$ ($0^0$): $\ln L=\lim x\ln\ln(1+x)=\lim\frac{\ln\ln(1+x)}{1/x}$; derivando: $\frac{\frac{1}{(1+x)\ln(1+x)}}{-1/x^2}=-\frac{x^2}{(1+x)\ln(1+x)}\to0$ (pues $\ln(1+x)\sim x$). $L=e^0=1$ ✓.

**#47** $\lim_{x\to0^+}(1/x)^{\tan x}$ ($\infty^0$): $\ln L=\lim(-\tan x\ln x)=\lim\frac{-\ln x}{\cot x}=\lim\frac{-1/x}{-\csc^2x}=\lim\frac{\sin^2x}{x}=0$. $L=1$ ✓.

**#51** $\lim_{x\to\infty}(1+e^{-x})^x$ ($1^\infty$): $\ln L=\lim x\ln(1+e^{-x})=\lim\frac{\ln(1+e^{-x})}{1/x}$; derivando: $\frac{-e^{-x}/(1+e^{-x})}{-1/x^2}=\frac{x^2e^{-x}}{1+e^{-x}}\to0$. $L=1$ ✓.

**#53** $\lim_{x\to0^+}\frac{e^x-e^{-x}}{\sin x}$: aquí es $0/0$; $\to\frac{e^x+e^{-x}}{\cos x}=2$ ✓.

**#59** $\lim_{x\to0}\frac{1-\cos^3x}{\sin^2x}$: $\frac{3\cos^2x\sin x}{2\sin x\cos x}=\frac32\cos x\to\frac32$ ✓.

**#60** $\lim_{x\to\infty}x\tan\frac1x=\lim\frac{\tan(1/x)}{1/x}=1$ ✓.

**#42** $\lim_{x\to a}\frac{x-a}{x^n-a^n}=\frac1{na^{n-1}}$ (es la derivada de $x^n$).

**#48** $\lim_{x\to\infty}\frac{2e^{3x}+\ln x}{e^{3x}+x^2}=2$ (domina $e^{3x}$).

Resultados de la guía: #40 $\frac12$, #41 $\frac5{12}$, #43 $\infty$, #45 $-\infty$, #46 $0$, #49 $0$, #50 $\frac12$, #52 $1$, #54 $-\frac12$, #55 $1$, #57 $2$, #61 $1$, #62 $1$, #63 $\frac13$, #64 $0$, #65 $-\frac16$, #66 $2$.

## 4. Cuándo NO usar L'Hôpital
- Si no es indeterminado: $\lim_{x\to0}\frac{x+1}{x+2}=\frac12$; derivar daría $1$, mal.
- Si el límite de $f'/g'$ no existe, la regla no concluye (p. ej. $\lim\frac{x+\sin x}{x}=1$ vía otro método; $\frac{1+\cos x}{1}$ oscila).
- Atajos: equivalencias $\sin x\sim x$, $\ln(1+x)\sim x$, $e^x-1\sim x$ cerca de 0; o factorizar.

## Errores comunes
- Derivar el cociente completo.
- Aplicarla con $\frac{1}{0}$ o $\frac{0}{1}$.
- Olvidar volver de $\ln L$ a $L$ en $1^\infty,0^0,\infty^0$.
- Escribir "$0\cdot\infty=0$".

## Ejercicios propuestos
1. $\lim_{x\to0}\frac{e^x-1-x}{x^2}$. (R: 1/2.)
2. $\lim_{x\to0^+}x\ln x$. (R: 0.)
3. $\lim_{x\to\infty}\left(1+\frac2x\right)^x$. (R: $e^2$.)
4. $\lim_{x\to0}\left(\frac1x-\frac1{\sin x}\right)$. (R: 0.)
5. $\lim_{x\to0^+}x^x$. (R: 1.)

## Conexiones
Complementa [[Matemática I - Límites y continuidad (guía de ejercicios)]]; imprescindible para integrales impropias y series en [[Matemática II]].

## Fuente
`Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf`, sección IV (respuestas de la guía; desarrollos verificados).
