---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/GRÁFICAS.pdf
---
# Matemática I - Funciones y sus gráficas

Materia: [[Matemática I]]
Anterior: [[Matemática I - Conjuntos numéricos, plano cartesiano y recta]]
Siguiente: [[Matemática I - Límites y continuidad (guía de ejercicios)]]

## Contexto y objetivo
`GRÁFICAS.pdf` es una hoja de una página (escaneada; leída como imagen) titulada "Gráficas - Funciones" con las nueve **funciones básicas**: identidad $f(x)=x$, cuadrada $x^2$, cúbica $x^3$, raíz cuadrada $\sqrt x$, recíproca $1/x$, raíz cúbica $\sqrt[3]x$, valor absoluto $|x|$, exponencial $e^x$ y logaritmo natural $\ln x$, con puntos de referencia marcados. El cronograma ([[Matemática I - Cronograma y temario 2023-1]]) pide dominarlas junto con transformaciones, operaciones y funciones inversas. Esta nota desarrolla ese bloque de la Unidad 1.

## 1. Definiciones
Una **función** $f:A\to B$ asigna a cada $x$ del dominio exactamente un $y$. **Dominio**: valores de $x$ admisibles; **rango**: valores que toma $y$. **Criterio de la recta vertical:** una curva es gráfica de función si toda recta vertical la corta a lo sumo una vez.

## 2. Catálogo de gráficas básicas
| Función | Dominio | Rango | Rasgos / puntos |
|---|---|---|---|
| $x$ | $\mathbb R$ | $\mathbb R$ | recta por (0,0), (1,1), (-1,-1) |
| $x^2$ | $\mathbb R$ | $[0,\infty)$ | parábola, par, vértice (0,0); (±1,1), (±2,4) |
| $x^3$ | $\mathbb R$ | $\mathbb R$ | impar, creciente |
| $\sqrt x$ | $[0,\infty)$ | $[0,\infty)$ | (0,0), (1,1), (4,2) |
| $1/x$ | $x\ne0$ | $y\ne0$ | hipérbola, impar; asíntotas $x=0$, $y=0$ |
| $\sqrt[3]x$ | $\mathbb R$ | $\mathbb R$ | impar; (−1,−1), (1,1), (8,2) |
| $|x|$ | $\mathbb R$ | $[0,\infty)$ | forma de V, par; (±2,2) |
| $e^x$ | $\mathbb R$ | $(0,\infty)$ | pasa por (0,1) y (1,e); asíntota $y=0$ |
| $\ln x$ | $(0,\infty)$ | $\mathbb R$ | pasa por (1,0) y (e,1); asíntota $x=0$ |

Simetrías: **par** si $f(-x)=f(x)$ (simétrica respecto al eje $y$); **impar** si $f(-x)=-f(x)$ (simétrica respecto al origen).

## 3. Transformaciones
Dada $y=f(x)$ y $c>0$:
- $f(x)+c$ sube $c$; $f(x)-c$ baja $c$ (traslación vertical).
- $f(x-c)$ mueve a la derecha $c$; $f(x+c)$ a la izquierda (traslación horizontal).
- $-f(x)$ refleja respecto al eje $x$; $f(-x)$ respecto al eje $y$.
- $cf(x)$ con $c>1$ estira verticalmente, $0<c<1$ comprime; $f(cx)$ comprime horizontalmente si $c>1$.

**Ejemplo 1.** Graficar $g(x)=-(x-2)^2+3$. Parte de $x^2$: trasladar 2 a la derecha, reflejar en $x$, subir 3. Vértice $(2,3)$, abre hacia abajo, cortes: $-(x-2)^2+3=0\Rightarrow x=2\pm\sqrt3$.

**Ejemplo 2.** $h(x)=\sqrt{x+1}-2$: dominio $[-1,\infty)$, punto inicial $(-1,-2)$; corta el eje $x$ cuando $\sqrt{x+1}=2$, $x=3$.

## 4. Otras funciones del temario
- **Lineal** $mx+b$, **cuadrática** $ax^2+bx+c$ (vértice en $x=-b/2a$), **potencias, radicales, racionales**.
- **Parte entera** $\lfloor x\rfloor$: función escalón, discontinua en cada entero.
- **Definidas por partes**, p. ej. $f(x)=\begin{cases}x+1&x<0\\x^2&x\ge0\end{cases}$.
- **Trigonométricas** $\sin x,\cos x,\tan x$ (periodo $2\pi$, $2\pi$, $\pi$) y sus inversas $\arcsin,\arccos,\arctan$ (dominios restringidos: $[-1,1]$ para arcsen y arccos, $\mathbb R$ para arctan con rango $(-\pi/2,\pi/2)$).

## 5. Dominio analítico
Reglas: denominador $\ne0$; radicando de raíz par $\ge0$; argumento del logaritmo $>0$.
**Ejemplo 3.** $f(x)=\dfrac{\sqrt{x-1}}{x^2-9}$: $x\ge1$ y $x\ne\pm3$, dominio $[1,3)\cup(3,\infty)$.

## 6. Operaciones y composición
$(f\pm g)(x)$, $(fg)(x)$, $(f/g)(x)$ (con $g\ne0$), $(f\circ g)(x)=f(g(x))$.
**Ejemplo 4.** $f=x^2$, $g=x+1$: $f\circ g=(x+1)^2$, $g\circ f=x^2+1$. No conmutan.

## 7. Inyectividad e inversa
$f$ es **inyectiva** si $f(a)=f(b)\Rightarrow a=b$ (criterio de la recta horizontal). Entonces existe $f^{-1}$ con $f^{-1}(f(x))=x$; su gráfica es reflexión de la de $f$ respecto a $y=x$.
**Ejemplo 5.** $f(x)=2x-3$: $y=2x-3\Rightarrow x=\frac{y+3}2$, $f^{-1}(x)=\frac{x+3}{2}$. $e^x$ y $\ln x$ son inversas entre sí. $x^2$ no es inyectiva en $\mathbb R$ pero sí en $[0,\infty)$ (inversa $\sqrt x$).

## Errores comunes
- Mover en sentido contrario en traslaciones horizontales ($f(x-2)$ va a la derecha).
- Olvidar restringir el dominio para definir una inversa.
- Confundir $f^{-1}(x)$ con $1/f(x)$.
- Dominio de $\ln$ con argumento $\le0$.

## Ejercicios propuestos
1. Dominio de $\ln(4-x^2)$. (R: $(-2,2)$.)
2. Inversa de $f(x)=\sqrt{x-1}$. (R: $x^2+1$, $x\ge0$.)
3. ¿Es par o impar $x^3-x$? (R: impar.)
4. Describe $y=|x-1|+2$. (R: V con vértice (1,2).)
5. Calcula $f\circ g$ si $f=\sqrt x$, $g=x^2+1$. (R: $\sqrt{x^2+1}$.)

## Conexiones
Los límites ([[Matemática I - Límites y continuidad (guía de ejercicios)]]) y el trazado de curvas ([[Matemática I - Optimización y trazado de gráficas]]) parten de estas gráficas. La exponencial y el logaritmo reaparecen en [[Matemática II]].

## Fuente
`Material/GUIAS/GRÁFICAS.pdf` (2 páginas; la primera, con las nueve gráficas, leída como imagen; la segunda no se revisó en detalle). El resto es conocimiento general del temario.
