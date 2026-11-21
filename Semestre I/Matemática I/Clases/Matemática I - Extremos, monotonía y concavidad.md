---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf (secciones VI, VII y IX)
---
# Matemática I - Extremos, monotonía y concavidad

Materia: [[Matemática I]]
Anterior: [[Matemática I - Razón de cambio y razones relacionadas]]
Siguiente: [[Matemática I - Optimización y trazado de gráficas]]

## Contexto y objetivo
Secciones de la guía: VI números críticos y extremos absolutos (88-97) y monotonía (98-107); VII extremos relativos con 1.ª y 2.ª derivada (108-126); IX concavidad y puntos de inflexión (143-151). Objetivo: usar $f'$ y $f''$ para describir el comportamiento de una función.

## 1. Definiciones
- **Número crítico:** $c$ en el dominio con $f'(c)=0$ o $f'(c)$ inexistente.
- **Extremo absoluto:** mayor/menor valor en un intervalo. **Teorema del valor extremo:** una $f$ continua en $[a,b]$ tiene máximo y mínimo absolutos.
- **Extremo relativo (local):** mayor/menor valor en un entorno.
- **Creciente** si $f'>0$ en un intervalo; **decreciente** si $f'<0$ (consecuencia de Lagrange).
- **Cóncava hacia arriba** si $f''>0$; **hacia abajo** si $f''<0$. **Punto de inflexión:** donde cambia la concavidad (con $f''=0$ o inexistente).

## 2. Método para extremos absolutos en $[a,b]$
1. Hallar números críticos en $(a,b)$.
2. Evaluar $f$ en ellos y en $a,b$.
3. Mayor = máximo; menor = mínimo.
**Ejemplo #89.** $f(x)=x^3-3x+2$ en $[-2,1]$: $f'=3x^2-3=0\Rightarrow x=\pm1$ (ambos en el intervalo, $-1$ interior y $1$ extremo). $f(-2)=0$, $f(-1)=4$, $f(1)=0$. Máximo absoluto $f(-1)=4$; mínimo absoluto $0$ (en $-2$ y $1$). ✓
**Ejemplo #88.** $f=-3x^2(x^2-2)=-3x^4+6x^2$ en $[-3,0]$: $f'=-12x^3+12x=-12x(x^2-1)$; críticos $0,-1$. $f(-3)=-189$, $f(-1)=3$, $f(0)=0$. Mín $-189$, máx $3$ ✓.

## 3. Monotonía
Resolver $f'(x)=0$ y signo de $f'$ en cada subintervalo.
**#102** $f=e^{x^2-2x}$: $f'=(2x-2)e^{x^2-2x}$; decrece en $(-\infty,1)$, crece en $(1,\infty)$ ✓.
**#101** $f=\sqrt{1-x^2}$: $f'=-x/\sqrt{1-x^2}$; crece en $(-1,0)$, decrece en $(0,1)$ ✓.
**#98** $f=3-e^{-3x}$: $f'=3e^{-3x}>0$, crece en $\mathbb R$.
**#103** $f=1+|x-2|$: decrece hasta 2, crece después.

## 4. Criterios para extremos relativos
- **1.ª derivada:** en un crítico $c$, si $f'$ pasa de $+$ a $-$: máximo; de $-$ a $+$: mínimo; sin cambio: ninguno.
- **2.ª derivada:** si $f'(c)=0$: $f''(c)>0$ mínimo; $f''(c)<0$ máximo; $f''(c)=0$ no concluye (usar la 1.ª).
**#108** $f=2x^2(x+3)=2x^3+6x^2$: $f'=6x(x+2)$; críticos $-2,0$. $f''=12x+12$: $f''(-2)=-12<0\Rightarrow$ máximo local $f(-2)=8$; $f''(0)=12>0\Rightarrow$ mínimo local $f(0)=0$ ✓.
**#114** $f=\frac{x}{x^2-2x+9}$... según la guía: máximo local $f(3)=\frac14$ y mínimo local $f(-3)=-\frac18$. (Verificación: $f'=\frac{9-x^2}{(\cdot)^2}$ con denominador $x^2+9$ sería la forma que da estos valores; el texto extraído del denominador podría estar alterado, verificar en el PDF.)
**#120** $s=x^2e^x$: $s'=e^x(x^2+2x)$; críticos $0,-2$; $s''=e^x(x^2+4x+2)$: $s''(0)=2>0$ mínimo en $0$; $s''(-2)=-2e^{-2}<0$ máximo en $-2$ ✓.
**#111** $f=3(x+2)^3(2x^2-7x+8)$: sin extremos locales (el factor cúbico no cambia de signo de modo útil; discriminante de la cuadrática negativo).
**#161 de trazado** relacionado: $\ln x/x$ tiene máximo en $x=e$.

## 5. Concavidad e inflexión
Resolver $f''=0$ o inexistente; estudiar el signo de $f''$.
**#143** $g=x^3+3x^2-2x+4$: $g''=6x+6$; cóncava hacia abajo en $(-\infty,-1)$, hacia arriba en $(-1,\infty)$; inflexión en $x=-1$ ✓.
**#147** $s=xe^{-x}$: $s''=(x-2)e^{-x}$; abajo en $(-\infty,2)$, arriba en $(2,\infty)$, inflexión $x=2$.
**#148** $t=\frac1{x+5}$: $t''=\frac{2}{(x+5)^3}$; cambia de signo en $-5$ pero $-5$ no está en el dominio: **sin inflexión**.
**#151** $m=\frac{x^2}{x^2+4}$: inflexiones en $x=\pm\frac{2\sqrt3}3$ ✓.
**#150** $j=\frac{x}{x^2-1}$: inflexión en $x=0$ (las asíntotas $\pm1$ cambian concavidad pero no son inflexiones).

## Errores comunes
- Olvidar evaluar los extremos del intervalo.
- Decir que $f''(c)=0$ implica inflexión (ej. $x^4$ en 0: mínimo, sin inflexión).
- Considerar inflexión un punto fuera del dominio.
- Confundir creciente con cóncava hacia arriba.

## Ejercicios propuestos
1. Extremos absolutos de $x^3-3x+2$ en $[0,2]$. (R: mín $0$ en $x=1$; máx $4$ en $x=-1$ no está; máx $f(2)=4$.)
2. Monotonía de $x e^{-x}$. (R: crece en $(-\infty,1)$, decrece en $(1,\infty)$.)
3. Concavidad de $x^4-6x^2$. (R: inflexiones en $x=\pm1$.)
4. Clasifica los críticos de $x^3-3x$. (R: máx en $-1$, mín en $1$.)

## Conexiones
Son la base del trazado y la optimización ([[Matemática I - Optimización y trazado de gráficas]]). Se apoya en [[Matemática I - Derivación: reglas, Rolle, Lagrange y tangentes]]. En [[Investigación de Operaciones I]] se generaliza a varias variables.

## Fuente
`Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf` (secciones VI, VII, IX).
