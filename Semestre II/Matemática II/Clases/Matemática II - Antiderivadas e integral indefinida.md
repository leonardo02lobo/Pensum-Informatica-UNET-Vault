---
tags: [clase, semestre-2]
materia: Matemática II
fuente: conocimiento general
---
# Matemática II - Antiderivadas e integral indefinida

Materia: [[Matemática II]]
Siguiente: [[Matemática II - Integral definida y Teorema Fundamental del Cálculo]]

## Contexto y objetivo
No hay Material para Matemática II; esta nota cubre la Unidad 1 del temario típico (verificar con el programa oficial). Objetivo: entender la integración como operación inversa de la derivación y dominar las integrales inmediatas.

## 1. Definición
$F$ es una **antiderivada** de $f$ en un intervalo si $F'(x)=f(x)$. Si $F$ lo es, todas las demás son $F+C$ (consecuencia del teorema de Lagrange de [[Matemática I - Derivación: reglas, Rolle, Lagrange y tangentes]]: dos funciones con igual derivada difieren en una constante). La familia se escribe
$$\int f(x)\,dx=F(x)+C.$$
$\int$ es el signo de integral, $f$ el integrando, $dx$ indica la variable, $C$ la constante de integración. Verificación universal: **derivar el resultado**.

## 2. Propiedades
- Linealidad: $\int[af+bg]=a\int f+b\int g$.
- No hay regla del producto ni del cociente: $\int fg\ne\int f\int g$.

## 3. Tabla de integrales inmediatas
| Integrando | Antiderivada |
|---|---|
| $x^n\ (n\ne-1)$ | $\frac{x^{n+1}}{n+1}$ |
| $1/x$ | $\ln|x|$ |
| $e^x$ | $e^x$ |
| $a^x$ | $\frac{a^x}{\ln a}$ |
| $\sin x$ | $-\cos x$ |
| $\cos x$ | $\sin x$ |
| $\sec^2x$ | $\tan x$ |
| $\csc^2x$ | $-\cot x$ |
| $\sec x\tan x$ | $\sec x$ |
| $\frac1{1+x^2}$ | $\arctan x$ |
| $\frac1{\sqrt{1-x^2}}$ | $\arcsin x$ |

## 4. Ejemplos resueltos
**1.** $\int(3x^2-4x+5)\,dx=x^3-2x^2+5x+C$.
**2.** $\int\left(\sqrt x+\frac1{x^2}\right)dx=\int(x^{1/2}+x^{-2})dx=\frac23x^{3/2}-\frac1x+C$.
**3.** $\int\frac{x^2+1}{x}dx=\int(x+\frac1x)dx=\frac{x^2}{2}+\ln|x|+C$.
**4.** $\int\tan^2x\,dx=\int(\sec^2x-1)dx=\tan x-x+C$.
**5. Problema de valor inicial.** Hallar $f$ con $f'(x)=6x^2-2$, $f(1)=3$: $f=2x^3-2x+C$; $f(1)=0+C=3\Rightarrow C=3$. $f(x)=2x^3-2x+3$.
**6. Movimiento.** $a(t)=-9{,}8$, $v(0)=20$, $s(0)=0$: $v=-9{,}8t+20$, $s=-4{,}9t^2+20t$. Se retoma en [[Física I]].

## 5. Constantes y valor absoluto
$\int\frac1x dx=\ln|x|+C$ vale en $x<0$ y $x>0$ (con constantes posiblemente distintas en cada rama). $\int\frac{dx}{x^2+4}=\frac12\arctan\frac x2+C$ (ajustar el argumento).

## Errores comunes
- Olvidar $+C$.
- Aplicar $\frac{x^{n+1}}{n+1}$ con $n=-1$.
- $\int\frac{1}{3x+1}dx=\ln|3x+1|$ sin dividir entre 3 (correcto: $\frac13\ln|3x+1|$).
- Integrar $\sin(2x)$ como $-\cos(2x)$ (falta el $\frac12$).

## Ejercicios propuestos
1. $\int(e^x+2\cos x)dx$. (R: $e^x+2\sin x+C$.)
2. $\int\frac{dx}{\sqrt{1-x^2}}$. (R: $\arcsin x+C$.)
3. $f''=12x$, $f'(0)=1$, $f(0)=2$. (R: $2x^3+x+2$.)
4. $\int\sec x(\sec x+\tan x)dx$. (R: $\tan x+\sec x+C$.)

## Conexiones
Operación inversa de la derivada ([[Matemática I]]); continúa con integración por sustitución ([[Matemática II - Sustitución e integración por partes]]).

## Fuente
Conocimiento general (sin Material en la carpeta).
