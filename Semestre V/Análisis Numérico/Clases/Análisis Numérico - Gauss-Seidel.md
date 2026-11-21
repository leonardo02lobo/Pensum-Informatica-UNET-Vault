---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/TEMA 4-Sistemas de Ecuaciones Lineales y No Lineales/Gauss-Seidel.pdf; Script-Tema4/GaussSeidel.m
---
# Análisis Numérico - Gauss-Seidel

Materia: [[Análisis Numérico]]
Anterior: [[Análisis Numérico - Gauss con pivoteo y factorización LU]]
Siguiente: [[Análisis Numérico - SOR y Jacobi]]

## Contexto y objetivo
Presentación "Método iterativo de Gauss-Seidel" (Prof. Jenny Pérez, UNET). Se resuelve $Ax=b$, $A$ de orden $n\times n$, generando una sucesión $x^{(k)}$ a partir de una aproximación inicial $x^{(0)}$ y una tolerancia $\xi$. Los métodos iterativos son preferibles a los directos en sistemas grandes y **ralos** (por ejemplo, 46 de 64 entradas nulas en la armadura de [[Análisis Numérico - Asignación 2 Sistemas lineales]]).

## Teoría
Descomponiendo $A=D-L-U$ ($D$ diagonal, $-L$ y $-U$ las partes estrictamente inferior y superior), Gauss-Seidel usa los valores ya actualizados en el mismo barrido:
$$x_i^{(k+1)}=\frac1{a_{ii}}\Big(b_i-\sum_{j<i}a_{ij}x_j^{(k+1)}-\sum_{j>i}a_{ij}x_j^{(k)}\Big).$$
En forma matricial $(D-L)x^{(k+1)}=Ux^{(k)}+b$, es decir $x^{(k+1)}=T_{GS}x^{(k)}+c$ con $T_{GS}=(D-L)^{-1}U$. **Convergencia:** para toda $x^{(0)}$ si $\rho(T_{GS})<1$; condiciones suficientes: $A$ **estrictamente diagonal dominante** por filas ($|a_{ii}|>\sum_{j\ne i}|a_{ij}|$) o $A$ simétrica definida positiva. Suele converger el doble de rápido que Jacobi cuando ambos convergen. Criterio de parada: $\|x^{(k+1)}-x^{(k)}\|_\infty<\xi$, con $\|v\|_\infty=\max_i|v_i|$.

## Algoritmo
1. $k=0$. 2. Para $i=1..n$ calcular $x_i^{(k+1)}$. 3. Si $\|x^{(k+1)}-x^{(k)}\|_\infty<\xi$, ir al paso 5. 4. $k=k+1$ y volver al paso 2. 5. Fin.

## Ejemplo resuelto (de la presentación)
$\begin{cases}10x_1-x_2=9\\-x_1+10x_2-2x_3=7\\-2x_2+10x_3=6\end{cases}$, $x^{(0)}=(0,0,0)^T$, $\xi=0.001$. La matriz es diagonal dominante.
- $k=1$: $x_1=0.9$; $x_2=(7+0.9)/10=0.79$; $x_3=(6+2\cdot0.79)/10=0.758$. Error $\|x^{(1)}-x^{(0)}\|_\infty=0.9$.
- $k=2$: $x_1=(9+0.79)/10=0.979$; $x_2=(7+0.979+2\cdot0.758)/10=0.9495$; $x_3=(6+2\cdot0.9495)/10=0.7899$. Error $0.1595$.
- $k=3$: $(0.99495,\;0.957475,\;0.791495)$, error $0.01595$.
- $k=4$: $(0.995748,\;0.957874,\;0.791575)$, error $0.000798<0.001$. **Parada.** Coincide con el material ($0.0008<0.001$).
Solución exacta: $x=(0.995789,\,0.957895,\,0.791579)^T$ (verificada). Con Jacobi el mismo sistema necesita 6 iteraciones (ver [[Análisis Numérico - SOR y Jacobi]]).

## Script GaussSeidel.m del material
Lee interactivamente $A$, $b$, $x^{(0)}$, tolerancia y máximo de iteraciones (`input(...,'s')` + `str2num`), y aplica el algoritmo con `norm(y-x,inf)<tol`:
```matlab
dim = size(A);  y = zeros(dim(2),1);  k = 1;  band = 0;
while k<=n & ~band
  for i = 1:dim(2)
    sum1 = 0; for j = 1:i-1,      sum1 = sum1 + A(i,j)*y(j); end
    sum2 = 0; for j = i+1:dim(2), sum2 = sum2 + A(i,j)*x(j); end
    y(i) = (b(i) - sum1 - sum2)/A(i,i);
  end
  if norm(y-x,inf) < tol, band = 1; end
  k = k+1;  x = y;
end
```
Detalle técnico: usa dos vectores (`y` nuevo, `x` anterior), por lo que `sum1` toma valores ya actualizados de `y` y `sum2` valores viejos de `x`: es Gauss-Seidel genuino. Con el sistema anterior debería imprimir el vector solución y `Total iteraciones realizadas: 4`. (En la versión del PDF, la rama `else` usa `fprint` en lugar de `fprintf`: error tipográfico del PDF; el script del zip está correcto.)

## Errores comunes
- No comprobar diagonal dominancia y esperar convergencia (ver los tres conjuntos de la [[Análisis Numérico - Práctica 4 Sistemas lineales]]).
- Mezclar valores nuevos y viejos en Jacobi (ahí se usan todos los viejos).
- Orden de ecuaciones inadecuado: permutar filas para hacer dominante la diagonal.
- Parar por el residuo y no por la diferencia (o viceversa) sin informarlo.

## Ejercicios propuestos
1. Dos iteraciones para $4x+y=9$, $x+3y=7$, $x^{(0)}=0$. (Resp.: $(2.25,1.5833)$; $(1.8542,1.7153)$.)
2. ¿Converge $x+2y=3$, $3x+y=4$? (Resp.: no con ese orden; permute las filas.)

## Conexiones
Caso particular $\omega=1$ de [[Análisis Numérico - SOR y Jacobi]]; normas en [[Análisis Numérico - Práctica 4 Sistemas lineales]].

## Fuente
`Gauss-Seidel.pdf` y `Script-Tema4/GaussSeidel.m`.
