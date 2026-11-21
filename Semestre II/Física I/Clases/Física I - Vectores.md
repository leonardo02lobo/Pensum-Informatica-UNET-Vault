---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/CT1(00)1-2021-2 Vectores.pdf
---
# Física I - Vectores

Materia: [[Física I]]
Anterior: [[Física I - Conceptos previos y magnitudes físicas]]
Siguiente: [[Física I - Tema 1 Movimiento en una dimensión]]

## Contexto y objetivo
El capítulo 3 "Vectores" del material 2021-2 (Dpto. de Matemática y Física, profesoras Yazmira Porras y Mary L. Roa, 19 páginas) presenta el cálculo vectorial elemental necesario para toda la mecánica. Históricamente la noción surge de la composición de fuerzas y velocidades (siglo XVII); Grassmann (1844) formalizó suma, producto escalar y vectorial, Hamilton introdujo los términos *escalar* y *vector*, y Gibbs popularizó la notación del punto ($\cdot$) y la cruz ($\times$). El capítulo se limita a las definiciones y operaciones básicas, en forma geométrica y analítica.

## 1. Escalares y vectores
Tiempo, distancia, masa, densidad y volumen quedan definidos con un número y su unidad (escalares): 1 kg de azúcar + 2 kg de harina = 3 kg; 6 L − 2 L = 4 L. No tiene sentido "3 kg hacia el sur". En cambio, la velocidad de un avión se da con rapidez y dirección ("920 km/h a 45° al noroeste"). Desplazamiento, velocidad, aceleración, fuerza y cantidad de movimiento son vectores.

Un vector se dibuja como flecha a escala; se simboliza $\vec A$ y su módulo $|\vec A|=A$.

## 2. Representación analítica
En el plano: $\vec A = A_x\hat i + A_y\hat j$, con
$$A=\sqrt{A_x^2+A_y^2},\qquad A_x = A\cos\theta,\quad A_y = A\sin\theta,\quad \tan\theta=\frac{A_y}{A_x}$$
($\theta$ medido desde $+X$ antihorario). En el espacio se añade $A_z\hat k$ y $A=\sqrt{A_x^2+A_y^2+A_z^2}$. Un vector unitario en la dirección de $\vec A$ es $\hat u_A=\vec A/A$.

**Ojo con el cuadrante**: $\arctan$ de la calculadora da valores entre −90° y 90°. Si $A_x<0$ hay que sumar 180°. Ejemplo: $\vec A=-3\hat i+4\hat j$: $\arctan(4/-3)=-53{,}1°$, pero el vector está en el segundo cuadrante: $\theta=126{,}9°$.

## 3. Suma y resta
**Gráfica**: método del triángulo/polígono (cola de uno con punta del otro) o del paralelogramo (colas juntas). **Analítica**: componente a componente:
$$\vec A\pm\vec B=(A_x\pm B_x)\hat i+(A_y\pm B_y)\hat j+(A_z\pm B_z)\hat k$$
Propiedades: conmutativa y asociativa en la suma; $\vec B-\vec A=-(\vec A-\vec B)$.

**Ejemplo 1** (excursionista): 4 km al sur y 6 km al este. Con $\hat i$ = este, $\hat j$ = norte: $\vec C=6\hat i-4\hat j$ km, $|\vec C|=\sqrt{36+16}=7{,}21$ km, a $\arctan(4/6)=33{,}7°$ al sur del este.

**Ejemplo 2** (distancia entre excursionista y auto): si $\vec r_E$ y $\vec r_A$ son las posiciones respecto al campamento, el vector que va de uno al otro es $\vec r_A-\vec r_E$; con componentes 10 km y 8 km su módulo es $\sqrt{10^2+8^2}=12{,}81$ km.

## 4. Producto por un escalar
$n\vec A=nA_x\hat i+nA_y\hat j+nA_z\hat k$. Si $n>0$ conserva el sentido y escala el módulo; si $n<0$ invierte el sentido. Ejemplo: $\vec A=6\hat i-4\hat j$, $n=0{,}5$: $n\vec A=3\hat i-2\hat j$.

## 5. Producto punto (escalar)
$$\vec A\cdot\vec B = A_xB_x+A_yB_y+A_zB_z = AB\cos\theta,\qquad 0°\le\theta\le180°$$
Se deduce de $\hat i\cdot\hat i=\hat j\cdot\hat j=\hat k\cdot\hat k=1$ y $\hat i\cdot\hat j=0$, etc. (los términos cruzados se anulan por perpendicularidad). Resultado: un escalar. Usos: ángulo entre vectores, proyección de uno sobre otro, **trabajo** $W=\vec F\cdot\Delta\vec r$.

**Ejemplo (trabajo)**: $\vec F=90\hat i-10\hat j$ N y $\Delta\vec r=5\hat i$ m: $\vec F\cdot\Delta\vec r=90\cdot5=450$ J.

**Ejemplo (ángulo)**: $\vec r=4\hat i+2\hat j$, $\vec p=-6\hat i$. $\vec r\cdot\vec p=-24$; $|\vec r|=4{,}47$; $|\vec p|=6$; $\cos\theta=-24/(4{,}47\cdot6)=-0{,}894$, $\theta=153{,}4°$.

Criterios: $\vec A\cdot\vec B=0\iff$ perpendiculares (con $A,B\ne0$); $>0$ ángulo agudo; $<0$ obtuso.

## 6. Producto cruz (vectorial)
$$\vec A\times\vec B=\begin{vmatrix}\hat i&\hat j&\hat k\\A_x&A_y&A_z\\B_x&B_y&B_z\end{vmatrix}=(A_yB_z-A_zB_y)\hat i+(A_zB_x-A_xB_z)\hat j+(A_xB_y-A_yB_x)\hat k$$
Módulo $|\vec A\times\vec B|=AB\sin\theta$ (área del paralelogramo). Dirección: perpendicular al plano de $\vec A$ y $\vec B$; sentido por la **regla de la mano derecha** (girar $\vec A$ hacia $\vec B$ por el ángulo menor; el pulgar da el sentido). Regla de los unitarios: $\hat i\times\hat j=\hat k$, $\hat j\times\hat k=\hat i$, $\hat k\times\hat i=\hat j$ (cíclico, +); en orden inverso, signo −; $\hat i\times\hat i=0$.

**Ejemplo**: $\vec r=9\hat i+10\hat j$, $\vec p=-10\hat i+8\hat j$:
$\vec r\times\vec p=9\cdot8\,\hat k+10\cdot(-10)(\hat j\times\hat i)=72\hat k+100\hat k=172\hat k$. Es perpendicular al plano $XY$, como debe ser.

Propiedades: **anticonmutativo** $\vec A\times\vec B=-\vec B\times\vec A$; $\vec A\times\vec A=0$; distributivo. Usos: torque $\vec\tau=\vec r\times\vec F$, momento angular $\vec L=\vec r\times\vec p$ (ver [[Física I - Tema 10 Dinámica rotacional]]).

## Errores comunes
- Aplicar $\vec A\cdot\vec B$ y esperar un vector (es un escalar) o $\vec A\times\vec B$ y esperar un número.
- Sumar módulos en lugar de componentes.
- Olvidar el signo de los términos con $\hat j$ al expandir el determinante.
- Usar ángulos en grados con la calculadora en radianes.

## Ejercicios propuestos
1. $\vec A=2\hat i+3\hat j$, $\vec B=-\hat i+4\hat j$. Calcula $\vec A+\vec B$, $|\vec A-\vec B|$. *Resp.: $\hat i+7\hat j$; $\sqrt{10}=3{,}16$.*
2. Ángulo entre $\vec A=\hat i+\hat j$ y $\vec B=\hat i-\hat j$. *Resp.: 90°.*
3. $\vec A\times\vec B$ con $\vec A=2\hat i$, $\vec B=3\hat j$. *Resp.: $6\hat k$.*
4. Componentes de un vector de 20 N a 150°. *Resp.: $-17{,}3\hat i+10\hat j$.*
5. Demuestra que $\vec A\times\vec B$ es perpendicular a $\vec A$ calculando $\vec A\cdot(\vec A\times\vec B)$. *Resp.: se anula término a término.*

## Conexiones
Cinemática vectorial ([[Física I - Tema 1 Movimiento en una dimensión]], [[Física I - Tema 2 Movimiento de proyectiles]]); álgebra de vectores en [[Matemática I]] y cálculo vectorial posterior en [[Física II]].

## Fuente
Material/Parcial 1/CT1(00)1-2021-2 Vectores.pdf (existe una copia idéntica "(1)"); complementado con las diapositivas de Conceptos básicos.
