---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/TEMA 4-Sistemas de Ecuaciones Lineales y No Lineales/GAUSS CON PIVOTE y LU.pdf; Script-Tema4/Gauss.m, FactorizacionUL.m, croult.m
---
# Análisis Numérico - Gauss con pivoteo y factorización LU

Materia: [[Análisis Numérico]]
Anterior: [[Análisis Numérico - Mínimos cuadrados e interpolación]]
Siguiente: [[Análisis Numérico - Gauss-Seidel]]

## Contexto y objetivo
Primer documento del Tema 4: métodos **directos** para $Ax=b$, con $A\in\mathbb R^{n\times n}$. La presentación (que se apoya en los textos de Burden/Chapra) repasa conceptos (vector, matriz diagonal, triangular superior e inferior, identidad, permutación, inversa, dominante, definida positiva, aumentada $[A\,|\,b]$), la eliminación gaussiana con pivoteo parcial y la factorización $LU$ (Doolittle y Crout). Objetivo: resolver sistemas controlando la estabilidad numérica y reutilizar la factorización para varios lados derechos.

## Eliminación de Gauss con pivoteo parcial
**Operaciones elementales** (las tres de la presentación): $\lambda E_j\to E_j$ ($\lambda\ne0$); $E_j+\lambda E_i\to E_j$; $E_i\leftrightarrow E_j$. Reducir a forma triangular es la eliminación; añadir la sustitución regresiva da la solución.

**Pivoteo parcial (columna máxima).** En el paso $i$ se busca el $p\ge i$ con $|a_{pi}|=\max_{j\ge i}|a_{ji}|$ y se intercambian las filas $E_p\leftrightarrow E_i$. Así los multiplicadores $m_{ji}=a_{ji}/a_{ii}$ cumplen $|m_{ji}|\le1$ y el crecimiento de errores se controla (sin pivoteo un pivote pequeño amplifica el error de redondeo).

**Algoritmo (pasos de la presentación).**
1. $i=1$. 2. Hallar $p$ con $|a_{pi}|$ máximo en la columna. 3. Si $a_{pi}=0$: no hay solución única; si no, intercambiar $E_p\leftrightarrow E_i$. 4. Para $j=i+1,\dots,n$: $m_{ji}=a_{ji}/a_{ii}$ y $E_j-m_{ji}E_i\to E_j$. 5-6. $i=i+1$; repetir mientras $i<n$. 7. Si $a_{nn}=0$: sin solución única. 8. $x_n=a_{n,n+1}/a_{nn}$. 9. $x_i=\dfrac{a_{i,n+1}-\sum_{j=i+1}^na_{ij}x_j}{a_{ii}}$ para $i=n-1,\dots,1$.
Costo: $\tfrac23n^3$ operaciones en la eliminación y $n^2$ en la sustitución.

**Ejemplo paso a paso.** $\begin{cases}3.03x-12.1y+14z=-119\\6.11x-14.2y+31z=-139\\-3.03x+12.1y-7z=120\end{cases}$ (tomado del parcial; ver [[Análisis Numérico - Parcial 2 cuestionario resuelto]]). La primera columna es $(3.03,\,6.11,\,-3.03)$: el mayor valor absoluto es $6.11$ (fila 2), luego el primer pivote exige **intercambiar la fila 1 con la fila 2**. Multiplicadores: $m_{21}=3.03/6.11=0.4959$, $m_{31}=-3.03/6.11=-0.4959$.

## Script Gauss.m del material
Resuelve el sistema $4\times4$ con matriz aumentada
$\begin{pmatrix}1.19&2.11&-100&1&|&1.12\\14.2&-0.122&12.2&-1&|&3.44\\0&100&-99.9&1&|&2.15\\15.3&0.11&-13.1&-1&|&4.16\end{pmatrix}$
con un bucle `while` de eliminación y otro de sustitución regresiva. Solución (verificada con aritmética de doble precisión): $x\approx(0.176825,\;0.012693,\;-0.020654,\;-1.182609)$. Observación importante: el script solo permuta filas si el pivote es **exactamente 0** (`if A(i,i)==0`) y busca el mayor *con signo* (`A(h,i)>mayor`), por lo que no implementa un verdadero pivoteo parcial por valor absoluto; para este sistema, con pivote inicial $1.19$ y elementos $14.2$ y $15.3$ debajo, el resultado coincide, pero con $x_{11}$ pequeño habría pérdida de precisión. Una versión correcta usaría `[~,p]=max(abs(A(i:n,i)))`.

`croult.m` (a pesar de su nombre, que sugiere Crout) contiene una eliminación gaussiana **sin pivoteo** para $A=\begin{pmatrix}2&-1&0\\-1&3&2\\0&-1&1\end{pmatrix}$, $b=(1,2,0)^T$, con matriz aumentada `[A b]`, bucle `for k=1:n-1`, factor `A(i,k)/A(k,k)` y sustitución regresiva. Solución exacta: $x=(7/9,\;5/9,\;5/9)\approx(0.7778,0.5556,0.5556)$. La factorización de Crout real está en [[Análisis Numérico - Práctica 4 Sistemas lineales]].

## Factorización LU
Si $A$ es no singular y las submatrices principales también (o se permutan filas: $PA=LU$), $A=LU$ con $L$ triangular inferior y $U$ triangular superior. Resolver $Ax=b$:
1. $Ly=b$ (sustitución progresiva), 2. $Ux=y$ (regresiva).
La condición necesaria y suficiente enunciada en la presentación es $\det A\ne0$ (con la salvedad de pivotes nulos: se necesita permutación). Conviene cuando hay varios $b$ distintos: la factorización cuesta $O(n^3)$ y cada resolución $O(n^2)$.

**Doolittle:** $l_{ii}=1$. $u_{ij}=a_{ij}-\sum_{k<i}l_{ik}u_{kj}$ ($j\ge i$); $l_{ji}=\dfrac{a_{ji}-\sum_{k<i}l_{jk}u_{ki}}{u_{ii}}$ ($j>i$).
**Crout:** $u_{ii}=1$. $l_{ji}=a_{ji}-\sum_{k<i}l_{jk}u_{ki}$ ($j\ge i$); $u_{ij}=\dfrac{a_{ij}-\sum_{k<i}l_{ik}u_{kj}}{l_{ii}}$ ($j>i$).

**Ejemplo con `FactorizacionUL.m`:** $A=\begin{pmatrix}1&7&-4\\4&-4&9\\12&-1&3\end{pmatrix}$. Fila 1 de $U$: $(1,7,-4)$. Columna 1 de $L$: $l_{21}=4$, $l_{31}=12$. $u_{22}=-4-4\cdot7=-32$; $u_{23}=9-4(-4)=25$; $l_{32}=(-1-12\cdot7)/(-32)=85/32$; $u_{33}=3-12(-4)-\tfrac{85}{32}\cdot25=51-66.4063=-15.4063=-493/32$. Así
$L=\begin{pmatrix}1&0&0\\4&1&0\\12&2.65625&1\end{pmatrix}$, $U=\begin{pmatrix}1&7&-4\\0&-32&25\\0&0&-15.40625\end{pmatrix}$ (el script recorre por columnas y calcula `U(i,j)` y `L(i,j)` con las fórmulas anteriores). Comprobación: $LU$ fila 3, col 3 $=12(-4)+2.65625\cdot25-15.40625=-48+66.40625-15.40625=3$. Determinante: $1\cdot(-32)(-15.40625)=493$.

## Errores comunes
- Pivotear solo cuando el pivote es cero (no es pivoteo parcial).
- Olvidar permutar también el vector $b$.
- No guardar los multiplicadores (se pierde $L$).
- Aplicar LU sin pivoteo a matrices con pivotes pequeños.
- Confundir Doolittle (diagonal de $L$ unitaria) con Crout (diagonal de $U$ unitaria).

## Ejercicios propuestos
1. Factorice con Doolittle $\begin{pmatrix}2&1\\4&5\end{pmatrix}$. (Resp.: $L=\begin{pmatrix}1&0\\2&1\end{pmatrix}$, $U=\begin{pmatrix}2&1\\0&3\end{pmatrix}$.)
2. Resuelva $x+y=2$, $x-y=0$ por LU. (Resp.: $(1,1)$.)
3. Calcule $\det$ de la matriz del ejemplo. (Resp.: 493.)

## Conexiones
Sirve de base de [[Análisis Numérico - Práctica 4 Sistemas lineales]] y de la solución de [[Análisis Numérico - Asignación 2 Sistemas lineales]]. Los métodos iterativos alternativos: [[Análisis Numérico - Gauss-Seidel]]. Álgebra previa: [[Matemática IV]].

## Fuente
`GAUSS CON PIVOTE y LU.pdf` (en la presentación faltan los pasos 1-9 y 11-13 de LU, que eran imágenes; se reconstruyeron con la teoría estándar) y los scripts del `Script-Tema4.zip` (carpeta `Script-Tema4/`).
