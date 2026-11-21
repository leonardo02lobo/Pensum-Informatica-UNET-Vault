---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/TEMA 2-SOLUCION DE ECUACIONES DE UNA VARIABLE/Teoria/practica_2.pdf
---
# Análisis Numérico - Práctica 2 Ecuaciones no lineales

Materia: [[Análisis Numérico]]
Anterior: [[Análisis Numérico - Newton-Raphson y Secante]]
Siguiente: [[Análisis Numérico - Mínimos cuadrados e interpolación]]

## Contexto y objetivo
Práctica 2 (Prof. Blanca L. Guillén V.): resolver ecuaciones no lineales de una variable con bisección, Newton-Raphson y secante, a mano y con MATLAB/Scilab. Dos secciones: diseño de algoritmos (programar las funciones) y solución de problemas. El enfoque pide identificar: (i) existencia de la raíz, (ii) intervalo, (iii) función objetivo $f$. Programar los métodos enseña a evitar ciclos infinitos y sirve de preparación para el cuestionario.

## 1. Diseño de algoritmos (firmas obligatorias)
- `[r,iter]=biseccion(f,a,b,tol,itmax)`
- `[r,iter]=newtonra(f,df,x0,tol,itmax)`
- `[r,iter]=secante(f,x0,x1,tol,itmax)`
Con salidas: raíz aproximada y número de iteraciones. El código de referencia está en [[Análisis Numérico - Bisección]] y [[Análisis Numérico - Newton-Raphson y Secante]].

## 2. Problemas y su resolución
**a) Raíces con exactitud $10^{-6}$.**
(i) $e^x+2^{-x}+2\cos x-6=0$, $1\le x\le2$. $f(1)=2.718+0.5+1.081-6=-1.70<0$, $f(2)=7.389+0.25-0.832-6=0.807>0$: hay cambio de signo. Raíz $x\approx1.829384$.
(ii) $\ln(x-1)+\cos(x-1)=0$, $1.3\le x\le2$. $f(1.3)=\ln0.3+\cos0.3=-1.204+0.955<0$, $f(2)=0+\cos1=0.540>0$. Raíz $x\approx1.397748$. Nótese que $f'(x)=1/(x-1)-\sin(x-1)$ es positiva en el intervalo: raíz única.

**b) Aproximar $\sqrt[3]{25}$ por bisección.** $f(x)=x^3-25$, $[2,3]$: $f(2)=-17$, $f(3)=2$. $n\ge\log_2(1/10^{-6})\approx20$ iteraciones. Resultado $2.924018$.

**c) Newton para $f(x)=0.5x^3-4x^2+6x-2$ con $x_0=4.2$ y $x_0=4.43$.** $f'(x)=1.5x^2-8x+6$, que se anula en $x=(8\pm\sqrt{28})/3=4.43$ y $0.90$. Con $x_0=4.43$ la tangente es casi horizontal ($f'(4.43)\approx 0.0$): el primer paso salta a $x_1\approx-3939$ y luego se acerca lentamente a la raíz real. Con $x_0=4.2$ el primer paso va a $-4.849$ y la sucesión $-2.574,-1.138,-0.273,0.203,0.415,\dots$ converge a la raíz real $x\approx0.4746$ (valores verificados numéricamente hasta $0.4154$ en seis iteraciones). Lección: la pendiente casi nula provoca saltos lejanos; el análisis gráfico (cerca de $x=4.43$ está el mínimo local de $f$) y analítico ($f'=0$) explica las "peculiaridades".

**d) Abrevadero semicircular.** $V=L[0.5\pi r^2-r^2\arcsin(h/r)-h\sqrt{r^2-h^2}]$ con $L=10$, $r=1$, $V=12.4$. Función objetivo $f(h)=10[0.5\pi-\arcsin h-h\sqrt{1-h^2}]-12.4$, $0\le h\le1$. $f(0)=15.708-12.4=3.31>0$, $f(1)=-12.4<0$. Raíz $h\approx0.1662$ pies, con exactitud 0.01 se obtiene $0.17$ (bisección: $\log_2(1/0.01)\approx7$ pasos; Newton y secante, 3-4). Comparación esperada: Newton y secante alcanzan la tolerancia en menos iteraciones; bisección siempre converge.

## Plan de trabajo para una asignación tipo
1. Graficar $f$ y acotar la raíz.
2. Comprobar $f(a)f(b)<0$ y continuidad.
3. Elegir método, tolerancia, `itmax`.
4. Ejecutar, tabular iteraciones y errores.
5. Verificar sustituyendo en la ecuación original.

## Errores comunes
Intervalo con raíz de multiplicidad par; derivada mal escrita; olvidar el punto `.` en operaciones con vectores (`x.^2`); no definir `df`; usar `iter` fuera del `for`.

## Ejercicios propuestos
1. Halle la raíz de $x=\cos x$ con los tres métodos. (Resp.: 0.739085.)
2. ¿Qué ocurre con Newton en $f(x)=x^{1/3}$, $x_0=1$? (Resp.: $x_{n+1}=-2x_n$: diverge; $f'$ infinita en la raíz.)

## Conexiones
Los mismos métodos con datos reales en [[Análisis Numérico - Asignación 1 NACA y ajuste de datos]].

## Fuente
`Material/TEMA 2-.../Teoria/practica_2.pdf`. Los valores numéricos de las raíces fueron calculados para esta nota.
