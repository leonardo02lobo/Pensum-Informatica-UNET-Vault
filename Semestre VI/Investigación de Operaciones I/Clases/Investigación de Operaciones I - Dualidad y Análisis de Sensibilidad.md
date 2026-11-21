---
tags: [clase, semestre-VI]
materia: Investigación de Operaciones I
---
# Investigación de Operaciones I - Dualidad y Análisis de Sensibilidad

Materia: [[Investigación de Operaciones I]]  
Anterior: [[Investigación de Operaciones I - Método de la Gran M y Dos Fases]]  
Siguiente: [[Investigación de Operaciones I - Modelos de Transporte, Asignación y Transbordo]]

## Contexto y objetivo

Formular el **problema dual** asociado a cualquier modelo primal de PL, interpretar económicamente las variables duales como **precios sombra** y realizar **análisis de sensibilidad** (rangos de optimalidad para $c_j$ y rangos de factibilidad para $b_i$) sobre la tabla símplex óptima.

## 1. Formulación del modelo Dual

Todo problema de PL (**Primal**) tiene un problema espejo llamado **Dual**. Para el par simétrico estándar:

| Primal (Max) | Dual (Min) |
|---|---|
| $\text{Max } Z = \mathbf{c}^T \mathbf{x}$ | $\text{Min } W = \mathbf{b}^T \mathbf{y}$ |
| $\mathbf{A}\mathbf{x} \le \mathbf{b}$ | $\mathbf{A}^T \mathbf{y} \ge \mathbf{c}$ |
| $\mathbf{x} \ge \mathbf{0}$ | $\mathbf{y} \ge \mathbf{0}$ |

**Reglas generales de conversión (Primal Max $\to$ Dual Min):**
- Cada **restricción** $i$ del primal genera una **variable dual** $y_i$:
  - Restricción $\le \implies y_i \ge 0$
  - Restricción $= \implies y_i$ irrestricta (libre de signo)
  - Restricción $\ge \implies y_i \le 0$
- Cada **variable** $x_j$ del primal genera una **restricción** $j$ del dual:
  - $x_j \ge 0 \implies$ restricción $\ge c_j$
  - $x_j$ irrestricta $\implies$ restricción $= c_j$

## 2. Teoremas fundamentales de la Dualidad

1. **Dualidad débil**: para cualquier $\mathbf{x}$ factible primal y $\mathbf{y}$ factible dual, $\mathbf{c}^T\mathbf{x} \le \mathbf{b}^T\mathbf{y}$.
2. **Dualidad fuerte**: si el primal tiene óptimo finito $\mathbf{x}^*$, el dual también lo tiene ($\mathbf{y}^*$) y $Z^* = W^*$.
3. **Holgura complementaria**: en el óptimo, $y_i^* \cdot s_i^* = 0$ (si un recurso tiene holgura $s_i^* > 0$, su precio sombra es $y_i^* = 0$).

## 3. Precios sombra y lectura en la tabla óptima

El **precio sombra ($y_i^*$)** de la restricción $i$ indica cuánto cambia el valor óptimo $Z^*$ por cada unidad adicional del recurso $b_i$, manteniendo los demás parámetros constantes.

En la tabla símplex óptima del ejemplo de mesas y sillas ($Z^* = 2700$), la fila $Z$ mostró:
$$Z + 0x_1 + 0x_2 + 5s_1 + 15s_2 = 2700$$
- Precio sombra de la madera ($s_1$): **$y_1^* = 5$** (\$/m² adicional).
- Precio sombra de las horas ($s_2$): **$y_2^* = 15$** (\$/hora adicional).
- Comprobación dual: $W^* = 240(5) + 100(15) = 1200 + 1500 = 2700 = Z^*$.

## 4. Análisis de sensibilidad

Permite saber en qué rango puede variar un parámetro sin que cambie la **base óptima** (sin necesidad de re-resolver desde cero):

1. **Variación en el lado derecho ($b_i \to b_i + \Delta b_i$, rango de factibilidad)**:
   La nueva columna LD es $\mathbf{B}^{-1}(\mathbf{b} + \Delta \mathbf{b}) = \bar{\mathbf{b}} + \Delta b_i \cdot (\text{columna de } s_i) \ge \mathbf{0}$.
   En nuestro ejemplo, la columna de $s_1$ en la tabla óptima es $(1, -1/2)^T$:
   $$40 + 1\Delta b_1 \ge 0 \implies \Delta b_1 \ge -40$$
   $$30 - \frac{1}{2}\Delta b_1 \ge 0 \implies \Delta b_1 \le 60$$
   Rango válido para la madera: $b_1 \in [200, 300]$ m². Dentro de ese rango, cada m² adicional aumenta $Z^*$ exactamente en \$5.

2. **Variación en un coeficiente objetivo ($c_j \to c_j + \Delta c_j$, rango de optimalidad)**:
   Se verifica que todos los costos reducidos en la fila $Z$ sigan siendo $\ge 0$ tras actualizar la fila $Z$.

## Errores comunes

- Aplicar el precio sombra fuera del **rango de factibilidad** de $b_i$ (cuando cambia la base óptima, el precio sombra también cambia).
- Confundir el precio sombra con el costo de compra del recurso: si el precio sombra de la madera es \$5/m² y un proveedor ofrece madera extra a \$4/m², conviene comprarla porque genera una ganancia neta de \$1/m²; si la ofrece a \$7/m², no conviene.

## Ejercicios propuestos

1. Escribe el dual de: $\text{Max } Z = 3x_1 + 5x_2$ s.a. $x_1 \le 4$, $2x_2 \le 12$, $3x_1 + 2x_2 = 18$, $x_1, x_2 \ge 0$.
   - *Respuesta:* $\text{Min } W = 4y_1 + 12y_2 + 18y_3$ s.a. $y_1 + 3y_3 \ge 3$, $2y_2 + 2y_3 \ge 5$, con $y_1, y_2 \ge 0$ e $y_3$ irrestricta.

## Conexiones

- Anterior: [[Investigación de Operaciones I - Método de la Gran M y Dos Fases]]
- Siguiente: [[Investigación de Operaciones I - Modelos de Transporte, Asignación y Transbordo]]
- Materia: [[Investigación de Operaciones I]]
- Materias relacionadas: [[Economía]], [[Ingeniería Económica]], [[Matemática IV]]

## Fuente

- Programa de [[Investigación de Operaciones I]] (Taha, Cap. 4; Hillier & Lieberman, Cap. 6).
