---
tags: [clase, semestre-2]
materia: Matemática II
fuente: conocimiento general
---
# Matemática II - Integrales trigonométricas y sustitución trigonométrica

Materia: [[Matemática II]]
Anterior: [[Matemática II - Sustitución e integración por partes]]
Siguiente: [[Matemática II - Fracciones parciales]]

## Contexto y objetivo
Integrar potencias de funciones trigonométricas y expresiones con $\sqrt{a^2\pm x^2}$, $\sqrt{x^2-a^2}$. Requiere las identidades: $\sin^2+\cos^2=1$, $1+\tan^2=\sec^2$, $\sin^2x=\frac{1-\cos2x}2$, $\cos^2x=\frac{1+\cos2x}2$, $\sin A\cos B=\frac12[\sin(A+B)+\sin(A-B)]$.

## 1. $\int\sin^m x\cos^nx\,dx$
- **$m$ impar:** separar un $\sin x$, convertir el resto con $\sin^2=1-\cos^2$, $u=\cos x$.
 Ej. $\int\sin^3x\cos^2x\,dx=\int(1-\cos^2x)\cos^2x\sin x\,dx=-\frac{\cos^3x}3+\frac{\cos^5x}5+C$.
- **$n$ impar:** análogo con $u=\sin x$.
- **Ambos pares:** fórmulas del ángulo medio. $\int\sin^2x\,dx=\frac x2-\frac{\sin2x}4+C$. $\int\sin^2x\cos^2x\,dx=\int\frac{\sin^22x}4=\frac x8-\frac{\sin4x}{32}+C$.

## 2. $\int\tan^m x\sec^nx\,dx$
- $n$ par: separar $\sec^2x$, $u=\tan x$. $\int\tan^2x\sec^4x\,dx=\frac{\tan^3x}3+\frac{\tan^5x}5+C$.
- $m$ impar: separar $\sec x\tan x$, $u=\sec x$. $\int\tan^3x\sec x\,dx=\frac{\sec^3x}3-\sec x+C$.
- $\int\sec x\,dx=\ln|\sec x+\tan x|+C$ (multiplicar y dividir por $\sec x+\tan x$).
- $\int\sec^3x\,dx=\frac12(\sec x\tan x+\ln|\sec x+\tan x|)+C$ (partes).

## 3. Sustitución trigonométrica
| Radical | Sustitución | Identidad |
|---|---|---|
| $\sqrt{a^2-x^2}$ | $x=a\sin\theta$ | $a\cos\theta$ |
| $\sqrt{a^2+x^2}$ | $x=a\tan\theta$ | $a\sec\theta$ |
| $\sqrt{x^2-a^2}$ | $x=a\sec\theta$ | $a\tan\theta$ |
Usar un triángulo rectángulo de referencia para volver a $x$.

**Ejemplo 1.** $\int\frac{dx}{x^2\sqrt{4-x^2}}$: $x=2\sin\theta$, $dx=2\cos\theta d\theta$; $=\int\frac{2\cos\theta}{4\sin^2\theta\cdot2\cos\theta}d\theta=\frac14\int\csc^2\theta=-\frac14\cot\theta+C$. Con $\sin\theta=\frac x2$: $\cot\theta=\frac{\sqrt{4-x^2}}{x}$. Resultado: $-\frac{\sqrt{4-x^2}}{4x}+C$.

**Ejemplo 2.** Área del círculo: $\int_{-r}^r2\sqrt{r^2-x^2}dx$; $x=r\sin\theta$: $2r^2\int_{-\pi/2}^{\pi/2}\cos^2\theta d\theta=2r^2\cdot\frac\pi2=\pi r^2$.

**Ejemplo 3.** $\int\frac{dx}{\sqrt{x^2+9}}$: $x=3\tan\theta$: $\int\sec\theta d\theta=\ln|\sec\theta+\tan\theta|=\ln\left|\frac{\sqrt{x^2+9}+x}3\right|+C$.

**Ejemplo 4 (completar cuadrados).** $\int\frac{dx}{\sqrt{x^2+2x+5}}=\int\frac{dx}{\sqrt{(x+1)^2+4}}$, $x+1=2\tan\theta$: $\ln|\sqrt{x^2+2x+5}+x+1|+C$.

## Errores comunes
- No volver a la variable original.
- Olvidar $dx$ en la sustitución.
- Usar $\sqrt{\sin^2}=\sin$ sin cuidar el signo (restringir $\theta$).
- Confundir las tres sustituciones.

## Ejercicios propuestos
1. $\int\cos^3x\,dx$. (R: $\sin x-\frac{\sin^3x}3+C$.)
2. $\int\tan x\sec^2x\,dx$. (R: $\frac{\tan^2x}2+C$.)
3. $\int\sqrt{1-x^2}\,dx$. (R: $\frac12(\arcsin x+x\sqrt{1-x^2})+C$.)
4. $\int\frac{dx}{(x^2+1)^{3/2}}$. (R: $\frac{x}{\sqrt{x^2+1}}+C$.)

## Conexiones
Se usan en longitud de arco ([[Matemática II - Aplicaciones de la integral: longitud, trabajo y valor medio]]) y coordenadas polares/esféricas de [[Matemática III]].

## Fuente
Conocimiento general (sin Material).
