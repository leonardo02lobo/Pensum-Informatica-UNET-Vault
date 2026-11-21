---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/PR11-1_imprimir.pdf; PR11-0.pps; PP11-1.pdf
---
# Física I - Tema 1 Problemas de movimiento en una dimensión

Materia: [[Física I]]
Anterior: [[Física I - Tema 1 Movimiento en una dimensión]]
Siguiente: [[Física I - Tema 2 Movimiento de proyectiles]]

## Contexto y objetivo
Reúne el **problema resuelto** del tema (PR11-0 / PR11-1, Neyra Tellez, marzo 2009) y la guía de **problemas propuestos** (PP11-1, 11 páginas del Dpto. de Matemática y Física). Muestra la metodología UNET: identificar leyes y conceptos, extraer información de figura y gráfica, construir funciones por tramos y responder cada pregunta.

## 1. Problema resuelto: las atletas María (A) y Ana (B)
**Enunciado.** Dos atletas parten de $x_A=+45$ m y $x_B=-45$ m respecto de la meta ($x=0$). Gana quien llegue primero a la meta. Su movimiento se describe con un gráfico $v(t)$ (poligonal, una curva por atleta). Se piden: (1) posición de B a los 3 s; (2) aceleración media de A; (3) aceleración de A en $t=9{,}5$ s; (4) velocidad de B en $t=6{,}75$ s; (5) velocidad media de B; (6) posición de B a los 6 s; (7) instante en que se encuentran por primera vez.

**Método general.** Los datos de la figura dan $x_0$; la gráfica $v(t)$ da velocidades, aceleraciones (pendientes) y desplazamientos (áreas).

**(1) Posición de B a los 3 s.** En $0\le t\le3$ s la recta $v(t)$ va de 0 a 10 m/s: MRUV con $a=\frac{10-0}{3-0}=3{,}33$ m/s². Dos vías equivalentes:
- Área: $\Delta x=\frac12(3)(10)=15$ m, entonces $x_3=-45+15=-30$ m.
- Función: $x=-45+\tfrac12(3{,}33)t^2$; en $t=3$: $-45+15=-30$ m (la guía escribe $3{,}33t^2$ con redondeo de la mitad; el resultado de 15 m de desplazamiento es el correcto).

**(2) Aceleración media de A.** $\langle a\rangle=\frac{v_f-v_i}{\Delta t}$. La guía usa $v_0=0$ y $v_{10}=12$ m/s: $\langle a\rangle=1{,}2$ m/s² (el enunciado dice 12 s pero la solución evalúa 10 s: se advierte la inconsistencia, **verificar con el original**).

**(3) Aceleración instantánea de A en 9,5 s.** Está en el tramo recto $7{,}5\le t\le10$ donde $v$ va de 0 a 12 m/s: $a=\frac{12-0}{10-7{,}5}=4{,}8$ m/s² (la pendiente de la recta; es constante en todo el tramo, así que la de 9,5 s coincide). Nota: en el texto extraído de la guía aparece "0,8", probablemente un dígito perdido en la conversión; el cálculo directo da 4,8.

**(4) Velocidad de B en 6,75 s.** En $6\le t\le7$ la velocidad cae de $10$ m/s con $a=-10$ m/s²: $v=10-10(t-6)$; en 6,75 s: $v=10-7{,}5=2{,}5$ m/s. *Lección*: dentro de un tramo se resta el instante inicial.

**(5) Velocidad media de B en $0\le t\le10$ s.** $\Delta x=A_1+A_2+A_3$ con trapecio $A_1=\frac{(6+3)\,10}{2}=45$ m, triángulo $A_2=5$ m y triángulo negativo $A_3=-15$ m: $\Delta x=35$ m y $\langle v\rangle=35/10=3{,}5$ m/s.

**(6) Posición de B a los 6 s**: $x_6=-45+\text{área}(0\text{–}6)=-45+\left[\tfrac12(3)(10)+(3)(10)\right]=-45+45=0$ m: B está exactamente en la meta (según los números de la guía).

**(7) Encuentro.** Se escriben $x_A(t)$ y $x_B(t)$ en el tramo donde coinciden y se resuelve $x_A=x_B$; se descartan raíces fuera del tramo.

## 2. Problemas propuestos (PP11-1): tipos
La guía está organizada en secciones:
1. **Comprensión** (verdadero/falso): "la distancia recorrida siempre es igual al desplazamiento" (F: solo si no hay retroceso en línea recta), "la velocidad media es siempre positiva" (F), "si $\langle v\rangle=0$ la partícula estuvo en reposo" (F: pudo volver al punto de partida), "$v=0$ equivale a reposo" (F: puede ser un instante), "$\langle a\rangle=0$ implica $v$ constante" (F: solo implica $v_f=v_i$).
2. **Selección** con gráficas $v(t)$: leer áreas, pendientes y signos; por ejemplo el automovilista que viaja 30 min a 80 km/h hacia el norte, se detiene 30 min y regresa (gráfica $v(t)$ del retorno con velocidad negativa; velocidad media total en km/h).
3. **Desarrollo** con gráficos: pilotos de fórmula 1 (velocidad de Montoya a $t=6{,}5$ s y velocidad media en $[0;5]$ s), dos jugadores (aceleración media de uno en $0\le t\le3$ s, distancia entre ambos a $t=2$ s, velocidad media del otro), etc.

### Ejemplo trabajado en el espíritu de la guía
Automovilista: 30 min (0,5 h) a 80 km/h al norte, parada de 0,5 h y regreso a casa a 40 km/h.
- Ida: $0{,}5\cdot80=40$ km. Parada: 0. Regreso: $40/40=1$ h.
- Tiempo total 2 h, desplazamiento neto 0, entonces velocidad media 0; rapidez media $=80\text{ km}/2\text{ h}=40$ km/h.

## Errores comunes
- Leer el valor de una gráfica en una cuadrícula equivocada (verifica la escala de cada eje).
- Calcular la aceleración como $v/t$ cuando $v_0\ne0$.
- Olvidar que el área bajo el eje del tiempo resta.
- Usar en el tramo 2 el instante absoluto $t$ en lugar de $t-t_i$.

## Ejercicios propuestos
1. Gráfica $v(t)$: sube de 0 a 6 m/s en 3 s, constante 4 s, baja a 0 en 2 s. Desplazamiento total. *Resp.: 9+24+6=39 m.*
2. Con los datos de 1, aceleración en cada tramo. *Resp.: +2, 0, −3 m/s².*
3. $x_A=-40+8t$, $x_B=60-12t$. Encuentro. *Resp.: t=5 s, x=0.*
4. Una moto frena de 30 a 0 m/s en 6 s: ¿distancia? *Resp.: 90 m.*

## Conexiones
Teoría en [[Física I - Tema 1 Movimiento en una dimensión]]; el [[Física I - Examen diferido I parcial]] repite este tipo de ejercicio (autos A y B con cambio de movimiento).

## Fuente
Material/Parcial 1/PR11-1_imprimir.pdf y PR11-0.pps (problema resuelto), PP11-1.pdf (propuestos). Los valores de la gráfica se leyeron de la figura y del texto de la guía; donde hay incoherencias se indica.
