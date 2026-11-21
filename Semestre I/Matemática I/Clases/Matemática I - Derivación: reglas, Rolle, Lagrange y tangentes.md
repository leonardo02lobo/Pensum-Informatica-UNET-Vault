---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf (secciones I-III)
---
# Matemática I - Derivación: reglas, Rolle, Lagrange y tangentes

Materia: [[Matemática I]]
Anterior: [[Matemática I - Límites y continuidad (guía de ejercicios)]]
Siguiente: [[Matemática I - Regla de L'Hôpital]]

## Contexto y objetivo
La "Guía de aplicaciones de derivadas" (Unidad V, UNET 2016-1, 174+ ejercicios con respuestas) se divide en: I Teorema de Rolle (1-10), II Teorema del valor medio (11-25), III Rectas tangentes y normales (26-35), IV L'Hôpital (36-67), V Razón de cambio (68-87), VI Números críticos (88-107), VII Extremos relativos (108-126), VIII Optimización (127-142), IX Concavidad (143-151), X Trazado (152 en adelante). Esta nota cubre derivación y las secciones I-III; las demás en notas posteriores.

## 1. Definición y reglas
$$f'(x)=\lim_{h\to0}\frac{f(x+h)-f(x)}{h}$$
Geométricamente es la pendiente de la recta tangente; físicamente, la razón de cambio instantánea. Derivable en $a$ implica continua en $a$ (no al revés: $|x|$ en 0).

Reglas: $(c)'=0$; $(x^n)'=nx^{n-1}$; $(fg)'=f'g+fg'$; $(f/g)'=\frac{f'g-fg'}{g^2}$; cadena $(f\circ g)'=f'(g)g'$.
Tabla: $(e^x)'=e^x$, $(a^x)'=a^x\ln a$, $(\ln x)'=1/x$, $(\sin)'=\cos$, $(\cos)'=-\sin$, $(\tan)'=\sec^2$, $(\arcsin)'=\frac1{\sqrt{1-x^2}}$, $(\arctan)'=\frac{1}{1+x^2}$.
- **Implícita:** derivar ambos lados tratando $y=y(x)$. $x^2+y^2=25\Rightarrow y'=-x/y$.
- **Logarítmica:** para $y=x^x$: $\ln y=x\ln x\Rightarrow y'=x^x(\ln x+1)$.

## 2. Teorema de Rolle
Si $f$ es continua en $[a,b]$, derivable en $(a,b)$ y $f(a)=f(b)$, existe $c\in(a,b)$ con $f'(c)=0$.
**Ejemplo (guía #4):** $f(x)=x^2-4x+3$ en $[1,3]$: $f(1)=f(3)=0$; $f'(x)=2x-4=0\Rightarrow c=2$. R: $c=2$.
**Ejemplo (#5):** $f(x)=\sin x\cos x=\tfrac12\sin2x$ en $[0,\pi]$: $f(0)=f(\pi)=0$, $f'=\cos2x=0\Rightarrow c=\pi/4,\,3\pi/4$.
**No aplica (#2):** $f(x)=1-x^{2/3}$ en $[-1,1]$: $f(\pm1)=0$ pero $f'(x)=-\frac23x^{-1/3}$ no existe en $0$. **(#8):** $1/x^2$ no es continua en $0$.
Otros resultados de la guía: #1 $c=\pm\sqrt{2/3}$; #7 $c=0$; #9 $c=0$; #10 $c=0$.

## 3. Teorema del valor medio (Lagrange)
Si $f$ es continua en $[a,b]$ y derivable en $(a,b)$, existe $c$ con $f'(c)=\dfrac{f(b)-f(a)}{b-a}$ (tangente paralela a la secante). Rolle es el caso $f(a)=f(b)$.
**Ejemplo (#12):** $f(x)=1/x$ en $[\tfrac12,2]$: pendiente secante $\frac{1/2-2}{3/2}=-1$; $-1/c^2=-1\Rightarrow c=1$.
**(#14):** $\sin x$ en $[0,\pi]$: pendiente $0$, $\cos c=0$, $c=\pi/2$.
**(#15):** $\ln x$ en $[1,e^2]$: $\frac{2}{e^2-1}=\frac1c\Rightarrow c=\frac{e^2-1}2\approx3{,}19$.
**(#13):** $\cos x$ en $[0,\pi]$: pendiente $-2/\pi$; $\sin c=2/\pi$, $c=\arcsin(2/\pi)\approx0{,}69$.
No aplican: #18 ($1/(x^2-1)$ no continua en $[0,2]$), #21 ($x^{2/3}$ no derivable en 0).
Afirmaciones: Rolle $\Rightarrow$ Lagrange es **verdadero**; Lagrange $\Rightarrow$ Rolle es **falso** (#22-23); que no se cumplan las hipótesis no prohíbe que exista $c$ (#24).
**Demostración del #25:** $p$ polinomio con $p(0)=0$; en $[0,1]$ Lagrange da $c$ con $p'(c)=\frac{p(1)-p(0)}{1}=p(1)$.

## 4. Recta tangente y normal
En $(a,f(a))$: tangente $y-f(a)=f'(a)(x-a)$; normal (perpendicular) $y-f(a)=-\frac1{f'(a)}(x-a)$.
**Ejemplo (#26):** tangente a $y=2x^2+4x-2$ paralela a $2x-y+5=0$ ($m=2$): $y'=4x+4=2\Rightarrow x=-\tfrac12$, $y=\tfrac12-2-2=-\tfrac72$. $y+\tfrac72=2(x+\tfrac12)\Rightarrow y=2x-\tfrac52$. ✓
**(#33):** $f=x^x$ en $(1,1)$: $f'(1)=1$; tangente $y=x$, normal $y=-x+2$.
**(#34):** tangentes a $y=-x^2$ por $(0,1)$ (punto externo a la curva): tangente en $x=a$: $y=-a^2-2a(x-a)$; en $x=0$ da $a^2=1$, $a=\pm1$: $y=-2x+1$ y $y=2x+1$.
**(#32):** $f=\frac13x^3-4x^2+7x+5$, tangente horizontal: $f'=x^2-8x+7=0\Rightarrow x=1,7$; puntos $(1,\tfrac{25}3)$, $(7,-\tfrac{83}3)$.
**(#30):** tangentes a $y=x^3$ paralelas a $y=x$: $3x^2=1$, $x=\pm\frac{1}{\sqrt3}$; $y=x\pm\frac{2\sqrt3}{9}$.

## Errores comunes
- Aplicar Rolle sin comprobar $f(a)=f(b)$.
- Olvidar la regla de la cadena ($(e^{-2x^2})'=-4xe^{-2x^2}$).
- Usar la pendiente de la tangente como pendiente de la normal.
- En tangentes "por un punto" suponer que el punto está en la curva.

## Ejercicios propuestos
1. Verifica Rolle para $f=x^3-3x$ en $[-\sqrt3,\sqrt3]$. (R: $c=\pm1$.)
2. Lagrange para $\sqrt x$ en $[1,4]$. (R: $c=9/4$.)
3. Tangente a $y=\ln x$ en $x=e$. (R: $y=x/e$.)
4. Normal a $y=x^2$ en $(1,1)$. (R: $y=-\tfrac12x+\tfrac32$.)
5. Derivar $y=x^{\sin x}$. (R: $y=x^{\sin x}(\cos x\ln x+\frac{\sin x}{x})$.)

## Conexiones
Rolle y Lagrange fundamentan el criterio de monotonía ([[Matemática I - Extremos, monotonía y concavidad]]) y el TFC en [[Matemática II]]. En [[Física I]] la derivada da velocidad y aceleración.

## Fuente
`Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf` (UNET 2016-1; respuestas oficiales de la guía contrastadas con cálculo propio).
