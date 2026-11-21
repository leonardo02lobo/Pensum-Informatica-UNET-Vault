---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/CT11-1_imprimir.pdf (y CT11-1.pps)
---
# Física I - Tema 1 Movimiento en una dimensión

Materia: [[Física I]]
Anterior: [[Física I - Vectores]]
Siguiente: [[Física I - Tema 1 Problemas de movimiento en una dimensión]]

## Contexto y objetivo
El Tema 1 (Ing. Neyra Tellez, marzo 2009, Rev. 1) introduce la **cinemática de la partícula**: describir el movimiento sin preguntar por sus causas. Se estudia el movimiento rectilíneo, primero el uniforme (MRU) y luego el uniformemente variado (MRUV, que incluye la caída libre). Objetivo: construir las funciones posición y velocidad a partir de datos, gráficas o enunciados, y leer información de gráficas $x(t)$ y $v(t)$.

## 1. Magnitudes cinemáticas (vectoriales)
- **Vector posición** $\vec r$: va del origen del sistema de referencia hasta la partícula; $\vec r=x\hat i+y\hat j$. Depende del sistema de referencia elegido.
- **Desplazamiento** $\Delta\vec r=\vec r_2-\vec r_1$: variación de posición (no es la distancia recorrida, que es un escalar y puede ser mayor).
- **Velocidad media**: $\langle\vec v\rangle=\dfrac{\Delta\vec r}{\Delta t}=\dfrac{\vec r_2-\vec r_1}{t_2-t_1}$, paralela al desplazamiento (m/s).
- **Velocidad instantánea**: $\vec v=\lim_{\Delta t\to0}\dfrac{\Delta\vec r}{\Delta t}=\dfrac{d\vec r}{dt}$; geométricamente, pendiente de la recta tangente en la gráfica de posición. Su módulo es la **rapidez**.
- **Aceleración media**: $\langle\vec a\rangle=\Delta\vec v/\Delta t$; **instantánea**: $\vec a=d\vec v/dt$ (m/s²).

En una dimensión el movimiento ocurre sobre un eje ($x$, $y$ o $z$) y los vectores se reducen a un componente con signo: $\Delta x=x_2-x_1$. El signo indica el sentido respecto al eje elegido.

## 2. Movimiento rectilíneo uniforme (MRU)
Velocidad constante, aceleración nula. **Función posición (itinerario)**:
$$x(t)=x_0+v\,t$$
con $x_0$ la posición inicial y $v$ la velocidad (ambas con signo).
- En la gráfica $x(t)$ es una recta: el corte con el eje vertical es $x_0$ y la pendiente es $v$.
- En $v(t)$ es una recta horizontal; el **área** bajo ella es el desplazamiento.

**Ejemplos de la clase**
1. $x=15+10t$: el atleta parte 15 m a la derecha del origen y se mueve a +10 m/s.
2. Ciclista a 120 m de la meta con rapidez 11 m/s acercándose: si el origen se fija en la meta, $x_0=-120$ m y $v=+11$ m/s, luego $x=-120+11t$. Llega a la meta cuando $x=0$: $t=120/11=10{,}9$ s. (Si se escogiera el origen en el ciclista y el eje al revés, cambiarían los signos: el resultado físico es el mismo.)
3. Desde una gráfica: recta que pasa por $x_0=80$ m y por $(10\text{ s},20\text{ m})$: $v=\dfrac{20-80}{10-0}=-6$ m/s, entonces $x=80-6t$ (se mueve hacia la izquierda).

## 3. Movimiento rectilíneo uniformemente variado (MRUV)
Aceleración constante. Funciones:
$$v(t)=v_0+a\,t,\qquad x(t)=x_0+v_0t+\tfrac12at^2,\qquad v^2=v_0^2+2a\,\Delta x$$
**Deducción**: de $a=dv/dt=\text{cte}$, integrando $v=v_0+at$; integrando otra vez $x=x_0+v_0t+\tfrac12at^2$; eliminando $t$ entre ambas se obtiene la tercera. También $\Delta x=\tfrac12(v_0+v)t$ (velocidad media = promedio de $v_0$ y $v$, válida solo con $a$ constante).

Interpretación gráfica:
- $v(t)$: recta, la **pendiente** es $a$; el **área** bajo la curva (trapecios y triángulos) es $\Delta x$ (con signo: área bajo el eje es desplazamiento negativo).
- $x(t)$: parábola; la concavidad hacia arriba significa $a>0$.
- Si $v$ y $a$ tienen el mismo signo, el cuerpo **acelera**; con signos opuestos, **frena**.

**Caída libre**: MRUV vertical con $a=-g=-9{,}8\ \text{m/s}^2$ (eje $y$ hacia arriba), sin resistencia del aire. En el punto más alto $v=0$ pero $a=-g$ (error común pensar que la aceleración es cero ahí).

## 4. Movimiento por tramos
Cuando la gráfica $v(t)$ es una poligonal, el movimiento se divide en intervalos; en cada uno se construye $x$ y $v$ con las condiciones iniciales **tomadas al final del tramo anterior** (posición y velocidad continuas). Al evaluar dentro de un tramo se resta el instante inicial del mismo: $v=v_0+a(t-t_i)$.

## 5. Ejemplos resueltos
**A. Frenado.** Un auto va a 72 km/h (20 m/s) y frena con $a=-4$ m/s² hasta detenerse. Tiempo: $t=\frac{0-20}{-4}=5$ s. Distancia: $\Delta x=\frac{0-20^2}{2(-4)}=50$ m.

**B. Lanzamiento vertical.** Pelota a $v_0=19{,}6$ m/s hacia arriba. Altura máxima: $h=\frac{v_0^2}{2g}=19{,}6$ m; tiempo de subida $t=v_0/g=2$ s; vuelve al punto de partida a los 4 s con rapidez 19,6 m/s.

**C. Encuentro.** Dos móviles: A en $x_A=-300+70t$ y B en $x_B=150-20t$ (unidades SI). Se encuentran si $-300+70t=150-20t\Rightarrow t=5$ s, en $x=50$ m.

## Errores comunes
1. Confundir distancia con desplazamiento y rapidez media con velocidad media.
2. Usar las fórmulas MRUV cuando la aceleración **no** es constante (tramos distintos).
3. Mezclar signos: elegir un eje y respetarlo para $x_0$, $v_0$ y $a$.
4. Decir que $v=0$ implica reposo permanente (el lanzamiento vertical tiene $v=0$ en el máximo).
5. Pensar que pendiente de $x(t)$ es la aceleración (es la velocidad).

## Ejercicios propuestos
1. Un tren pasa de 10 a 30 m/s en 8 s. Hallar $a$ y distancia. *Resp.: 2,5 m/s²; 160 m.*
2. Se suelta una piedra desde 45 m. Tiempo y velocidad al llegar. *Resp.: 3,03 s; −29,7 m/s.*
3. $x=4-2t+3t^2$. Hallar $v(t)$ y $a$. *Resp.: $v=-2+6t$; $a=6$ m/s².*
4. Área bajo $v(t)$: triángulo de base 4 s y altura 8 m/s. *Resp.: 16 m.*
5. Dos ciclistas separados 600 m se acercan a 8 y 12 m/s. ¿Cuándo se cruzan? *Resp.: 30 s.*

## Conexiones
Base de [[Física I - Tema 2 Movimiento de proyectiles]] (dos MRUV/MRU independientes) y de [[Física I - Tema 3 Movimiento circular]] (analogía angular). Las derivadas e integrales provienen de [[Matemática I]] y [[Matemática II]]. Se verifica en [[Laboratorio de Física I]].

## Fuente
Material/Parcial 1/CT11-1_imprimir.pdf y CT11-1.pps (diapositivas "Tema 1: Movimiento en una dimensión"); fórmulas contrastadas con el [[Física I - Formulario I parcial]].
