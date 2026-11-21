---
tags: [clase, semestre-VII]
materia: Investigación de Operaciones II
---
# Investigación de Operaciones II - Teoría de Juegos y Solución por PL

Materia: [[Investigación de Operaciones II]]  
Anterior: [[Investigación de Operaciones II - Teoría de Inventarios EOQ y Modelos Probabilísticos]]  
Siguiente: —

## Contexto y objetivo

Abordar la **Unidad IV (Teoría de Juegos)**: modelar conflictos estratégicos de suma cero entre dos jugadores, determinar **estrategias puras (punto de silla)**, aplicar **reducción por dominancia**, resolver **estrategias mixtas** (método analítico $2\times 2$, método gráfico $2\times n$ o $m\times 2$, y **Programación Lineal** para $m\times n$) e introducir el **equilibrio de Nash** en juegos no cooperativos.

## 1. Juegos de suma cero para dos personas

El Jugador A (filas) elige entre $m$ estrategias y el Jugador B (columnas) entre $n$ estrategias. La matriz de pagos $\mathbf{A} = [a_{ij}]$ representa la ganancia de A (y pérdida de B, pues $\text{pago}_A + \text{pago}_B = 0$).

### Criterio Minimax / Maximin y Punto de Silla
- **Maximin (A)**: $\underline{v} = \max_i \left(\min_j a_{ij}\right)$ (mejor garantía mínima para A).
- **Minimax (B)**: $\overline{v} = \min_j \left(\max_i a_{ij}\right)$ (menor pérdida máxima para B).
- Si $\underline{v} = \overline{v} = v$, existe un **punto de silla** y la solución es en **estrategias puras** con valor del juego $v$.

## 2. Reducción por dominancia

Antes de resolver un juego sin punto de silla, se eliminan estrategias inferiores:
- **Para A (filas)**: una fila $r$ es dominada por otra fila $k$ si $a_{rj} \le a_{kj}$ para todo $j$ (se elimina la fila $r$).
- **Para B (columnas)**: una columna $s$ es dominada por otra columna $k$ si $a_{is} \ge a_{ik}$ para todo $i$ (se elimina la columna $s$, pues B busca minimizar el pago).

## 3. Estrategias mixtas: caso $2\times 2$ y método gráfico

Cuando $\underline{v} < \overline{v}$, los jugadores aleatorizan sus decisiones: A elige sus filas con probabilidades $\mathbf{p} = (p_1, \dots, p_m)$ ($\sum p_i = 1$) y B sus columnas con $\mathbf{q} = (q_1, \dots, q_n)$ ($\sum q_j = 1$).

### Fórmulas cerradas para juegos $2 \times 2$ sin punto de silla
Para $\mathbf{A} = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}$:
$$p_1 = \frac{a_{22} - a_{21}}{a_{11} + a_{22} - a_{12} - a_{21}}, \qquad p_2 = 1 - p_1$$
$$q_1 = \frac{a_{22} - a_{12}}{a_{11} + a_{22} - a_{12} - a_{21}}, \qquad q_2 = 1 - q_1$$
$$v = \frac{a_{11}a_{22} - a_{12}a_{21}}{a_{11} + a_{22} - a_{12} - a_{21}}$$

**Ejemplo del programa:** $\mathbf{A} = \begin{pmatrix} 3 & 1 \\ 2 & 4 \end{pmatrix}$.
$\text{Maximin} = \max(1, 2) = 2$; $\text{Minimax} = \min(3, 4) = 3 \implies$ no hay punto de silla.
$$p_1 = \frac{4 - 2}{3 + 4 - 1 - 2} = \frac{2}{4} = 0.5, \quad v = \frac{12 - 2}{4} = 2.5$$

## 4. Solución general por Programación Lineal ($m \times n$)

Asegurando que $v > 0$ (sumando una constante $K$ a toda la matriz si hay valores negativos), el problema del Jugador A se transforma en un modelo de PL definiendo $x_i = p_i / v$:

$$\text{Min } Z = \sum_{i=1}^{m} x_i \quad \left(= \frac{1}{v}\right)$$
$$\text{s.a.} \quad \sum_{i=1}^{m} a_{ij} x_i \ge 1, \quad j = 1, \dots, n$$
$$x_i \ge 0$$

El problema dual corresponde exactamente al Jugador B ($\text{Max } W = \sum y_j$ s.a. $\sum a_{ij} y_j \le 1$).

## 5. Equilibrio de Nash (juegos de suma no nula)

En juegos generales (ej. *Dilema del Prisionero*), un perfil de estrategias $(s_A^*, s_B^*)$ es un **equilibrio de Nash** si ningún jugador puede mejorar su propio pago cambiando unilateralmente su estrategia.

## Errores comunes

- Invertir la regla de dominancia para columnas (recuerda: la matriz muestra pagos para **A**, por lo que **B** prefiere los valores *más pequeños*).
- Aplicar las fórmulas $2\times 2$ de estrategias mixtas sin verificar antes si ya existe un punto de silla (si hay punto de silla, las fórmulas pueden dar probabilidades fuera de $[0,1]$).

## Ejercicios propuestos

1. Verifica si el juego $\begin{pmatrix} 4 & 2 & 5 \\ 1 & 3 & 0 \\ 3 & 4 & 2 \end{pmatrix}$ tiene punto de silla o reduce por dominancia.
   - *Respuesta:* Mínimos por fila: $2, 0, 2 \implies \text{Maximin} = 2$. Máximos por columna: $4, 4, 5 \implies \text{Minimax} = 4$. No hay punto de silla. La fila 2 está dominada por la fila 3 ($1\le 3, 3\le 4, 0\le 2$); se elimina fila 2. Luego columna 3 está dominada por columna 1 en las filas restantes ($5\ge 4, 2\ge 3$? No, $2 < 3$, no domina). Se resuelve el $2\times 3$ restante gráficamente o por PL.

## Conexiones

- Anterior: [[Investigación de Operaciones II - Teoría de Inventarios EOQ y Modelos Probabilísticos]]
- Materia: [[Investigación de Operaciones II]]
- Materias relacionadas: [[Investigación de Operaciones I]], [[Economía]], [[Simulación de Sistemas]]

## Fuente

- `Material/ProgramaInvOperacionesII.doc` (Unidad IV) y Taha (Cap. 15); Binmore, K. *Teoría de Juegos*.
