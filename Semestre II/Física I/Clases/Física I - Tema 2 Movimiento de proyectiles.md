---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/CT12-1_imprimir.pdf (y CT12-1.pps)
---
# Física I - Tema 2 Movimiento de proyectiles

Materia: [[Física I]]
Anterior: [[Física I - Tema 1 Problemas de movimiento en una dimensión]]
Siguiente: [[Física I - Tema 2 Problemas de proyectiles]]

## Contexto y objetivo
El Tema 2 (octubre 2009) estudia el **movimiento parabólico**: movimiento bidimensional donde la partícula se mueve a la vez en $x$ y en $y$ y describe una parábola. Objetivo: descomponer el movimiento en dos movimientos rectilíneos independientes (MRU en $x$, MRUV en $y$) y calcular posición, velocidad, tiempo de vuelo, altura máxima y alcance.

## 1. Hipótesis
- Sin resistencia del aire.
- Aceleración constante $\vec a=-g\hat j$, con $g=9{,}8$ m/s² (el material escribe $\vec g=-9{,}8\hat j$).
- Alcances pequeños: la Tierra es plana y $g$ constante.

## 2. Principio de independencia de los movimientos
La aceleración horizontal es cero y la vertical es $-g$; por tanto los movimientos en $x$ e $y$ se analizan por separado y se vinculan **solo por el tiempo**.

Velocidad inicial: $\vec v_0=v_{0x}\hat i+v_{0y}\hat j$, con $v_{0x}=v_0\cos\theta_0$, $v_{0y}=v_0\sin\theta_0$.

| Eje x (MRU) | Eje y (MRUV) |
|---|---|
| $x=x_0+v_{0x}t$ | $y=y_0+v_{0y}t-\tfrac12gt^2$ |
| $v_x=v_{0x}$ | $v_y=v_{0y}-gt$ |
| $a_x=0$ | $a_y=-g$ |

Rapidez: $v=\sqrt{v_x^2+v_y^2}$; ángulo de la velocidad: $\tan\theta=v_y/v_x$ (tangente a la trayectoria).

## 3. Magnitudes características
- **Tiempo de subida (tiempo máximo)**: $v_y=0\Rightarrow t_{max}=v_{0y}/g$.
- **Altura máxima**: $y_{max}=y_0+v_{0y}t_{max}-\tfrac12gt_{max}^2=y_0+\dfrac{v_{0y}^2}{2g}$.
- **Tiempo de vuelo** $t_v$: solución positiva de $y_f=y_0+v_{0y}t_v-\tfrac12gt_v^2$. Si $y_f=y_0$: $t_v=2v_{0y}/g$.
- **Alcance**: $R=v_{0x}t_v$. Para $y_f=y_0$: $R=\dfrac{v_0^2\sin2\theta_0}{g}$ (máximo a 45°; ángulos complementarios dan igual alcance).

**Deducción de la ecuación de la trayectoria**: de $t=x/v_{0x}$ sustituido en $y$: $y=y_0+x\tan\theta_0-\dfrac{g}{2v_0^2\cos^2\theta_0}x^2$, una parábola.

**Aclaración conceptual**: en el punto más alto $v_y=0$ pero $v_x\ne0$ (no se anula la velocidad total) y la aceleración sigue siendo $-g\hat j$.

## 4. Casos particulares
- **Lanzamiento horizontal** desde altura $h$: $\theta_0=0$; $t_v=\sqrt{2h/g}$, $R=v_0t_v$; el tiempo de caída es el mismo que dejar caer el objeto.
- **Lanzamiento vertical** ($\theta_0=90°$): MRUV en $y$.
- **Proyectil que cae a un nivel distinto**: se resuelve la cuadrática para $t_v$.

## 5. Ejemplos resueltos
**A. Balón de fútbol (de la guía resuelta, ver también [[Física I - Tema 2 Problemas de proyectiles]]).** Un jugador patea desde 1 m de altura con $\vec v_0=14{,}14\hat i+14{,}14\hat j$ m/s hacia una pared a 20 m y de 23 m de altura.
- Ángulo: $\tan\theta=14{,}14/14{,}14=1\Rightarrow\theta=45°$.
- Posición a los 0,52 s: $x=14{,}14(0{,}52)=7{,}35$ m; $y=1+14{,}14(0{,}52)-4{,}9(0{,}52)^2=7{,}03$ m.
- Tiempo hasta la pared: $t=20/14{,}14=1{,}41$ s; altura del impacto $y=1+14{,}14(1{,}41)-4{,}9(1{,}41)^2=11{,}2$ m.
- Velocidad de impacto: $v_x=14{,}14$; $v_y=14{,}14-9{,}8(1{,}41)=0{,}32$ m/s: $\vec v=14{,}14\hat i+0{,}32\hat j$ m/s.

**B. Lanzamiento horizontal.** Moneda que sale de una mesa de 1,25 m con 3 m/s: $t=\sqrt{2(1{,}25)/9{,}8}=0{,}505$ s; $R=1{,}52$ m; $v_y=-9{,}8(0{,}505)=-4{,}95$ m/s; rapidez $5{,}79$ m/s.

**C. Alcance máximo.** $v_0=20$ m/s a 30°: $R=\frac{400\sin60°}{9{,}8}=35{,}3$ m; $y_{max}=\frac{(10)^2}{19{,}6}=5{,}1$ m; $t_v=\frac{2\cdot10}{9{,}8}=2{,}04$ s.

## Errores comunes
1. Usar $v_0$ en lugar de sus componentes en las ecuaciones de $x$ e $y$.
2. Poner $a_x=-g$ o suponer $v_x$ variable.
3. Calcular el tiempo de vuelo con $y_f=y_0$ cuando el blanco está a otra altura.
4. Dejar la calculadora en radianes al evaluar $\sin\theta$.
5. Creer que la rapidez es mínima y nula en el punto más alto.

## Ejercicios propuestos
1. $v_0=25$ m/s, $\theta=37°$, $y_0=0$. Hallar $t_v$, $R$, $y_{max}$. *Resp.: 3,07 s; 61,3 m; 11,5 m.*
2. Se lanza horizontalmente a 15 m/s desde un acantilado de 50 m. ¿Dónde cae? *Resp.: t=3,19 s; 47,9 m.*
3. ¿Con qué ángulo debe lanzarse para $R=R_{max}$? *Resp.: 45°.*
4. Calcular la velocidad (módulo y ángulo) a $t=1$ s para $\vec v_0=10\hat i+15\hat j$. *Resp.: 11,6 m/s; 27,5°.*

## Conexiones
Aplica [[Física I - Tema 1 Movimiento en una dimensión]] a dos ejes y los vectores de [[Física I - Vectores]]. Prepara el análisis de aceleración centrípeta en [[Física I - Tema 3 Movimiento circular]].

## Fuente
Material/Parcial 1/CT12-1_imprimir.pdf y CT12-1.pps; fórmulas según el [[Física I - Formulario I parcial]].
