---
tags: [clase, semestre-III]
materia: Laboratorio de Física II
---
# Laboratorio de Física II - Campo Magnético e Inducción Electromagnética

Materia: [[Laboratorio de Física II]]
Anterior: [[Laboratorio de Física II - Carga y Descarga de Capacitores (Circuito RC)]]
Siguiente: —

## Contexto y objetivo

La última práctica de [[Laboratorio de Física II]] explora la interacción entre electricidad y magnetismo: la visualización de líneas de campo magnético en imanes y solenoides, la fuerza magnética sobre conductores con corriente y la verificación cualitativa y cuantitativa de las **leyes de Faraday y Lenz** sobre inducción electromagnética.

## 1. Campo magnético de imanes y solenoides

- Las líneas de campo magnético $\vec{B}$ son siempre **cerradas**: salen del polo norte (N) y entran al polo sur (S) en el exterior del imán.
- En el interior de un **solenoide largo** de longitud $L$ con $N$ espiras y corriente $I$, el campo magnético es prácticamente uniforme y paralelo al eje:
  $$B = \mu_0 \frac{N}{L} I = \mu_0\, n\, I \qquad (\mu_0 = 4\pi \times 10^{-7}\,\text{T}\cdot\text{m/A})$$
- Su sentido se determina con la **regla de la mano derecha** (curvando los dedos en el sentido de $I$, el pulgar apunta al polo norte del solenoide).

## 2. Fuerza magnética sobre un conductor con corriente

Un segmento recto de longitud $\vec{L}$ que transporta corriente $I$ dentro de un campo magnético uniforme $\vec{B}$ experimenta una fuerza:
$$\vec{F} = I (\vec{L} \times \vec{B}) \implies |\vec{F}| = I\,L\,B \sin\theta$$
En el laboratorio se verifica con una balanza de corriente o un riel conductor observando cómo la fuerza invierte su sentido al invertir la corriente o los polos del imán.

## 3. Inducción electromagnética: Ley de Faraday y Ley de Lenz

El **flujo magnético** a través de una espira de área $A$ es $\Phi_B = \int \vec{B} \cdot d\vec{A} = B A \cos\theta$.

Según la **Ley de Faraday-Lenz**, una variación temporal del flujo magnético induce una fuerza electromotriz (fem) $\mathcal{E}$ en una bobina de $N$ espiras:
$$\mathcal{E} = -N \frac{d\Phi_B}{dt}$$

- **Ley de Faraday**: la magnitud de $\mathcal{E}$ es proporcional a la **rapidez** con que cambia el flujo magnético (por ejemplo, al mover un imán más rápido dentro de una bobina, mayor pico de voltaje o deflexión en el galvanómetro).
- **Ley de Lenz** (el signo negativo): la corriente inducida genera un campo magnético propio que **se opone al cambio** de flujo que la produjo.
  - Si acercamos el polo Norte de un imán a una bobina, la cara de la bobina frente al imán desarrolla un polo Norte para repelerlo.
  - Si alejamos el polo Norte, desarrolla un polo Sur para atraerlo.

## Ejemplo resuelto

Una bobina de $N = 200$ espiras y área $A = 4{,}0 \times 10^{-3}\,\text{m}^2$ se encuentra perpendicular a un campo magnético uniforme que cambia linealmente de $0{,}10\,\text{T}$ a $0{,}50\,\text{T}$ en $\Delta t = 0{,}20\,\text{s}$. La fem inducida promedio es:
$$|\mathcal{E}| = N \frac{\Delta \Phi_B}{\Delta t} = N A \frac{\Delta B}{\Delta t} = 200 \times (4{,}0 \times 10^{-3}) \times \frac{0{,}50 - 0{,}10}{0{,}20} = 1{,}6\,\text{V}$$

## Errores comunes

- Creer que un campo magnético intenso pero **estático** ($\Delta \Phi_B / \Delta t = 0$) induce corriente en una bobina inmóvil.
- No invertir la escala del galvanómetro o multímetro al cambiar el sentido del movimiento del imán (en corriente inducida la señal cambia de signo).
- Dejar corriente elevada circulando por un solenoide durante mucho tiempo, sobrecalentando el bobinado.

## Ejercicios propuestos

1. ¿Qué ocurre con la fem inducida si se duplica la velocidad con la que se introduce el imán en la bobina?
2. Calcula el campo magnético en el centro de un solenoide de $0{,}25\,\text{m}$ de longitud, $500$ espiras y corriente $I = 2{,}0\,\text{A}$.

**Respuestas:**
1. Se duplica, porque $\Delta t$ se reduce a la mitad y $|\mathcal{E}| \propto 1/\Delta t$.
2. $B = (4\pi \times 10^{-7}) \cdot \frac{500}{0{,}25} \cdot 2{,}0 \approx 5{,}03 \times 10^{-3}\,\text{T} = 5{,}03\,\text{mT}$.

## Conexiones

- Cierra la secuencia de [[Laboratorio de Física II]] iniciada en [[Laboratorio de Física II - Instrumentos de Medición y Análisis de Errores]].
- Verifica experimentalmente el magnetismo e inducción de [[Física II]].

## Fuente

Elaborado siguiendo el programa referencial de [[Laboratorio de Física II]] (Prácticas 6 y 7: Campo magnético e inducción electromagnética).
