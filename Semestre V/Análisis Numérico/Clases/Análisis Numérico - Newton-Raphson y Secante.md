---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/TEMA 2-SOLUCION DE ECUACIONES DE UNA VARIABLE/Teoria/MétNewton Raphson y Secante.pdf
---
# Análisis Numérico - Newton-Raphson y Secante

Materia: [[Análisis Numérico]]
Anterior: [[Análisis Numérico - Bisección]]
Siguiente: [[Análisis Numérico - Práctica 2 Ecuaciones no lineales]]

## Contexto y objetivo
Presentación "Raíces de ecuaciones no lineales" sobre los dos métodos **abiertos** de la unidad. A diferencia de bisección, no exigen cambio de signo, pero sí buenas aproximaciones iniciales y pueden divergir. Objetivo: entender la deducción, el algoritmo, los criterios de error y las situaciones donde fallan.

## Newton-Raphson ("método de las tangentes sucesivas")
Requiere una aproximación inicial $x_0$ y $f$ continua y derivable (al menos dos veces para el análisis de convergencia).

**Deducción.** La tangente en $(x_{i},f(x_i))$ es $y=f(x_i)+f'(x_i)(x-x_i)$. Su intersección con el eje $x$ ($y=0$) da la siguiente aproximación:
$$x_{i+1}=x_i-\frac{f(x_i)}{f'(x_i)}.$$
Equivalentemente, es la iteración de punto fijo con $g(x)=x-f(x)/f'(x)$; como $g'(x)=f(x)f''(x)/f'(x)^2$ se anula en una raíz simple, la convergencia es **cuadrática**: $|e_{i+1}|\approx\frac{|f''(r)|}{2|f'(r)|}e_i^2$ (las cifras correctas se duplican por iteración).

**Algoritmo.** (1) $i=1$. (2) Calcular $x_i$. (3) Si el error es menor que $\varepsilon$ terminar; si no, $i=i+1$ y repetir. Criterios de error propuestos: (a) residuo $|f(x_i)|<\varepsilon$; (b) error absoluto $|x_i-x_{i-1}|<\varepsilon$; (c) error relativo $|x_i-x_{i-1}|/|x_i|<\varepsilon$ con $x_i\neq0$.

**Ejemplo numérico.** $f(x)=\cos x-x$, $f'(x)=-\sin x-1$, $x_0=0.5$: $x_1=0.5-\frac{0.377583}{-1.479426}=0.755222$; $x_2=0.739142$; $x_3=0.739085$. Raíz $0.739085$ (error cuadrático: $0.2552\to0.0161\to0.00006$).

**Desventajas (de la presentación).** Raíces múltiples (convergencia lineal); aun con raíces simples, $f(x)=x^{10}-1$ desde $x_0$ pequeño converge lentamente: los iterados son $x_1=51.65$ (si $x_0=0.5$), luego $46.5,\;41.8,\dots$ (decrece un 10% por paso) hasta llegar cerca de 1. Otros casos: punto de inflexión cerca de la raíz ($f''=0$); oscilación alrededor de un máximo o mínimo local; salto a otra raíz lejana por pendientes cercanas a cero; $f'(x)=0$ produce división por cero (la tangente es horizontal y nunca corta el eje).

## Método de la secante
Motivación: la derivada puede ser difícil de calcular, o Newton no converge. Se sustituye por la diferencia dividida hacia atrás $f'(x_i)\approx\frac{f(x_i)-f(x_{i-1})}{x_i-x_{i-1}}$:
$$x_{i+1}=x_i-\frac{f(x_i)(x_{i-1}-x_i)}{f(x_{i-1})-f(x_i)}=x_i-\frac{f(x_i)(x_i-x_{i-1})}{f(x_i)-f(x_{i-1})}.$$
Necesita **dos** aproximaciones iniciales y no exige cambio de signo. Orden de convergencia $(1+\sqrt5)/2\approx1.618$ (superlineal), con una sola evaluación nueva de $f$ por paso (Newton usa $f$ y $f'$).

**Ejemplo paso a paso (de la presentación).** $f(x)=e^x-3x^2$, $x_0=1.5$, $x_1=2$, $\varepsilon=10^{-5}$, error absoluto. $f(1.5)=4.481689-6.75=-2.268311$; $f(2)=7.389056-12=-4.610944$.
$x_2=2-\frac{(-4.610944)(1.5-2)}{-2.268311-(-4.610944)}=2-\frac{2.305472}{2.342633}=1.015863$ (coincide con el material). Error $|x_2-x_1|=0.984137>\varepsilon$ (la presentación imprime 0.0974137: parece un error de transcripción; el valor correcto es 0.984137, verificar). Iteraciones siguientes (verificadas): $x_3=0.938962$, $x_4=0.911633$, $x_5=0.910035$, $x_6=0.910008$, $x_7=0.910008$. Raíz $0.910008$ en la iteración 7, como indica el material.

## Scripts del material
`metodo_secante.m` implementa exactamente ese ejemplo: `format long`, $f=@(x)\exp(x)-3x^2$, `x0=1.5; x1=2; tol=1e-5; max_iter=1000`, bucle `for` que calcula `x2 = x1 - fx1*(x1-x0)/(fx1-fx0)`, corta si `abs(x2-x1)<tol` y actualiza `x0=x1; x1=x2`; imprime `La raíz es 0.910008`. Una versión genérica:
```matlab
function [r,iter] = newtonra(f,df,x0,tol,itmax)
  for iter = 1:itmax
    x1 = x0 - f(x0)/df(x0);
    if abs(x1-x0) < tol, r = x1; return; end
    x0 = x1;
  end
  r = x0;
end
```
Ver el uso de derivada por diferencia finita en [[Análisis Numérico - Asignación 1 NACA y ajuste de datos]].

## Comparación
| | Bisección | Newton | Secante |
|---|---|---|---|
| Orden | 1 | 2 | 1.618 |
| Requiere | cambio de signo | $f'$ y buen $x_0$ | 2 puntos |
| Garantía | sí | no | no |

## Errores comunes
Dividir por $f'(x_i)\approx0$; usar la secante con $f(x_i)=f(x_{i-1})$; confundir tolerancia sobre $x$ con tolerancia sobre $f$; no limitar iteraciones.

## Ejercicios propuestos
1. Newton para $\sqrt2$ con $f=x^2-2$, $x_0=1$: (Resp.: 1.5, 1.41667, 1.414216.)
2. Secante para $x^2-2$ con $x_0=1$, $x_1=2$: $x_2=1.3333$, $x_3=1.4$, $x_4=1.41463$.

## Conexiones
Aplicados en [[Análisis Numérico - Práctica 2 Ecuaciones no lineales]]; la extensión a varias variables está en [[Análisis Numérico - Sistemas no lineales y Práctica 5]]; Newton también resuelve el disparo no lineal ([[Análisis Numérico - Práctica 7 EDO y problemas de frontera]]).

## Fuente
`Material/TEMA 2-.../Teoria/MétNewton Raphson y Secante.pdf` y `Scripts Tema 2/Scripts Tema 2/metodo_secante.m`.
