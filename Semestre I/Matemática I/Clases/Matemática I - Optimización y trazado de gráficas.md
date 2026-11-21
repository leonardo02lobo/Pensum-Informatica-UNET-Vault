---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf (secciones VIII y X)
---
# Matemática I - Optimización y trazado de gráficas

Materia: [[Matemática I]]
Anterior: [[Matemática I - Extremos, monotonía y concavidad]]

## Contexto y objetivo
Secciones VIII (problemas de optimización 127-142) y X (trazado de gráficas 152-174+) de la guía de aplicaciones de derivadas. Objetivo: modelar problemas de máximos/mínimos con una variable y realizar el análisis completo de una función para esbozar su gráfica.

## 1. Método de optimización
1. Dibujar y definir variables. 2. Escribir la **función objetivo**. 3. Usar la restricción para dejar **una sola variable**. 4. Determinar el dominio. 5. Hallar críticos, comparar con los extremos del dominio. 6. Verificar (2.ª derivada) y responder con unidades.

## 2. Problemas resueltos de la guía
**#136 (caja sin tapa de cartón de 12 cm).** Se cortan cuadrados de lado $x$: $V=x(12-2x)^2$, $0<x<6$. $V'=(12-2x)(12-6x)=0\Rightarrow x=2$ (o 6, descartado). $V''(2)<0$: máximo; $V=2\cdot64=128$ cm³. Respuesta: $x=2$ cm ✓.

**#134 (caja de base cuadrada, 1200 cm² de material, sin tapa).** Base $x$, altura $h$: $x^2+4xh=1200\Rightarrow h=\frac{1200-x^2}{4x}$; $V=x^2h=\frac{1200x-x^3}4$; $V'=\frac{1200-3x^2}{4}=0\Rightarrow x=20$, $h=10$, $V=4000$ cm³ ✓ (coincide con la respuesta de la guía, lo que indica que la caja es abierta).

**#140 (barca y caminata).** Remar a un punto a distancia $x$ del punto más cercano de la costa: tiempo $T(x)=\frac{\sqrt{4+x^2}}{3}+\frac{6-x}{5}$. $T'=\frac{x}{3\sqrt{4+x^2}}-\frac15=0\Rightarrow5x=3\sqrt{4+x^2}\Rightarrow16x^2=36\Rightarrow x=1{,}5$. $T=\frac{2{,}5}{3}+\frac{4{,}5}{5}=1{,}733$ h $=1$ h 44 min ✓.

**#142 (torres de 150 m y 100 m, separadas 200 m).** Punto a distancia $x$ de la torre alta: $L=\sqrt{150^2+x^2}+\sqrt{100^2+(200-x)^2}$; $L'=0\Rightarrow\frac{x}{\sqrt{150^2+x^2}}=\frac{200-x}{\sqrt{100^2+(200-x)^2}}$ (iguales ángulos, triángulos semejantes) $\Rightarrow\frac x{150}=\frac{200-x}{100}\Rightarrow x=120$ m y $80$ m ✓.

**#127.** Diferencia 20, producto mínimo: $P=x(x-20)$, $P'=2x-20=0\Rightarrow x=10$; números $10$ y $-10$ (producto $-100$) ✓.

**#128.** Perímetro $P$, área máxima: lados $x$ y $\frac P2-x$; $A'=0\Rightarrow x=\frac P4$ (cuadrado), $A=\frac{P^2}{16}$ ✓.

**#132 (cilindro en esfera de radio $\sqrt3$... guía "3 cm").** $V=\pi r^2h$, $r^2=R^2-\frac{h^2}4$; $V=\pi(R^2h-\frac{h^3}4)$; $V'=0\Rightarrow h=\frac{2R}{\sqrt3}$. Con $R=3$: $h=2\sqrt3$ cm ✓.

**#138.** Triángulo rectángulo de hipotenusa 20: $A=\frac12c_1\sqrt{400-c_1^2}$, máximo cuando $c_1^2=200$: $c_1=c_2=\sqrt{200}=10\sqrt2$ ✓.

**#141 (barcos).** Distancia$^2$ $D=(65-10t)^2+(15t)^2$; $D'=-20(65-10t)+450t=0\Rightarrow650t=1300\Rightarrow t=2$ h; $d=\sqrt{45^2+30^2}=\sqrt{2925}=15\sqrt{13}$ km ✓.

**#139.** Rectángulo bajo $y=x+8$ y $y=-2x+5$ sobre el eje $x$ (según la guía): $b=3{,}5$, $h=5{,}25$, $A=18{,}375$.

## 3. Trazado de gráficas: lista de verificación
1. Dominio. 2. Intersecciones ($f(0)$ y $f=0$). 3. Simetrías (par/impar). 4. Asíntotas: verticales (ceros del denominador), horizontales ($\lim_{\pm\infty}$), oblicuas $y=mx+b$ con $m=\lim f/x$, $b=\lim(f-mx)$. 5. $f'$: crecimiento y extremos. 6. $f''$: concavidad e inflexiones. 7. Tabla y esbozo.

**Ejemplo #161: $f=\frac{\ln x}{x}$.** Dominio $(0,\infty)$; corte $(1,0)$. $f'=\frac{1-\ln x}{x^2}$: crece en $(0,e)$, decrece en $(e,\infty)$, máximo $f(e)=1/e$. $f''=\frac{2\ln x-3}{x^3}$: cóncava abajo en $(0,e^{3/2})$, arriba después; inflexión en $x=e^{3/2}$. Asíntotas: $x=0$ (con $f\to-\infty$) y $y=0$ ($f\to0^+$) ✓.

**Ejemplo #169: $f=\frac{1+x^2}{x}=x+\frac1x$.** Impar; asíntota vertical $x=0$, oblicua $y=x$; $f'=1-\frac1{x^2}$: crece si $|x|>1$; máximo local $f(-1)=-2$, mínimo local $f(1)=2$; $f''=\frac{2}{x^3}$: cóncava arriba para $x>0$, abajo para $x<0$ ✓.

**Ejemplo #152: $f=x^4-12x^3+48x^2-64x=x(x-4)^3$.** Cortes $(0,0),(4,0)$; $f'=4(x-4)^2(x-1)$... mínimo absoluto en $x=1$ con $f(1)=-27$; $f''=12(x-4)(x-2)$: inflexiones en $x=2$ ($f=-16$) y $x=4$ ✓.

**#157: $xe^{-x}$**: máximo en $x=1$ con $1/e$; inflexión en $x=2$; asíntota $y=0$ ($x\to\infty$).
**#168: $\frac{2x}{x^2-1}$**: impar, asíntotas $x=\pm1$, $y=0$, decreciente en todo su dominio, inflexión en el origen.
**#167: $\frac{7-3x}{x-2}$**: cortes $(0,-\tfrac72)$ y $(\tfrac73,0)$; asíntotas $x=2$, $y=-3$.

## Errores comunes
- No justificar que el crítico es máximo/mínimo (comparar con bordes).
- Olvidar la restricción de dominio ($0<x<6$).
- Dar una respuesta sin unidades ni responder lo preguntado (p. ej. el valor y no la variable).
- En trazado, ignorar puntos donde $f'$ no existe (picos, tangentes verticales como $x^{2/3}$).

## Ejercicios propuestos
1. Rectángulo de área máxima con perímetro 40. (R: $10\times10$, $A=100$.)
2. Cilindro de volumen fijo $V$ y área total mínima. (R: $h=2r$.)
3. Punto de $y=\sqrt x$ más cercano a $(4,0)$. (R: $x=3{,}5$.)
4. Traza $f=x^3-3x$. (R: máx $(-1,2)$, mín $(1,-2)$, inflexión $(0,0)$.)

## Conexiones
Resume la Unidad 4 del cronograma ([[Matemática I - Cronograma y temario 2023-1]]). Se generaliza en [[Matemática III]] (extremos de varias variables y multiplicadores de Lagrange) y [[Investigación de Operaciones I]].

## Fuente
`Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf` (secciones VIII y X; respuestas de la guía verificadas con cálculo propio).
