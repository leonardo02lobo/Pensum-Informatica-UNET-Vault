---
tags: [clase, semestre-VI]
materia: Investigación de Operaciones I
---
# Investigación de Operaciones I - Método Gráfico y Casos Especiales

Materia: [[Investigación de Operaciones I]]  
Anterior: [[Investigación de Operaciones I - Formulación de Programación Lineal]]  
Siguiente: [[Investigación de Operaciones I - Método Símplex]]

## Contexto y objetivo

Resolver problemas de Programación Lineal de dos variables mediante el **método gráfico**, comprender el teorema fundamental de la PL (el óptimo en un vértice de la región factible) e identificar los **casos especiales** (óptimos alternativos, infactibilidad, solución no acotada y restricciones redundantes).

## 1. Fundamento geométrico y región factible

Cada restricción lineal $a_{i1}x_1 + a_{i2}x_2 \le b_i$ define un **semiplano cerrado** en $\mathbb{R}^2$. La intersección de todos los semiplanos (incluyendo $x_1 \ge 0, x_2 \ge 0$) forma la **región factible**, que es un conjunto convexo (polígono o poliedro convexo).

> **Teorema fundamental de la PL:** Si existe una solución óptima finita, al menos un **vértice (punto extremo)** de la región factible es óptimo.

## 2. Procedimiento paso a paso

1. Graficar la recta frontera de cada restricción (hallando sus interceptos con los ejes).
2. Determinar el semiplano válido (probando el punto $(0,0)$ si la recta no pasa por el origen).
3. Sombrear la **región factible** común a todas las restricciones.
4. Hallar las coordenadas de todos los **vértices** resolviendo los sistemas $2\times 2$ correspondientes.
5. Evaluar $Z$ en cada vértice (o trazar rectas de isoutilidad/isocosto) y seleccionar el mejor valor.

### Ejemplo resuelto (mesas y sillas)
$$\text{Max } Z = 50x_1 + 30x_2 \quad \text{s.a.} \quad 4x_1 + 3x_2 \le 240, \quad 2x_1 + x_2 \le 100, \quad x_1, x_2 \ge 0$$

| Vértice | Cómo se obtiene | Valor de $Z = 50x_1 + 30x_2$ |
|---|---|---|
| $(0, 0)$ | Origen | $0$ |
| $(50, 0)$ | Intercepto de $2x_1 + x_2 = 100$ con $x_2 = 0$ | $2500$ |
| $(0, 80)$ | Intercepto de $4x_1 + 3x_2 = 240$ con $x_1 = 0$ | $2400$ |
| $(30, 40)$ | Intersección de $4x_1 + 3x_2 = 240$ y $2x_1 + x_2 = 100$ | **$2700$ (Óptimo)** |

## 3. Casos especiales en Programación Lineal

1. **Soluciones óptimas alternativas (múltiples)**: la recta de la función objetivo es paralela a una restricción activa en el borde óptimo. Todos los puntos del segmento entre dos vértices óptimos $(x^A, x^B)$ dan el mismo $Z^*$:
   $$x(\lambda) = \lambda x^A + (1-\lambda) x^B, \quad \lambda \in [0, 1]$$
2. **Problema infactible**: las restricciones son contradictorias y la región factible es vacía ($\emptyset$). Ejemplo: $x_1 + x_2 \le 4$ y $x_1 + x_2 \ge 6$.
3. **Solución no acotada**: la región factible es abierta en la dirección de mejora de $Z$, por lo que $Z \to +\infty$ (en Max) o $Z \to -\infty$ (en Min). Suele indicar que falta una restricción real en el modelo.
4. **Restricción redundante**: una restricción que, al eliminarse, no modifica la región factible.

## Errores comunes

- Elegir el intercepto más lejano en lugar del más cercano al origen en restricciones $\le$, saliendo de la región factible.
- Concluir que un problema con región factible no acotada es automáticamente "no acotado": un problema de **minimización** con $x_1, x_2 \ge 0$ sobre una región abierta hacia arriba suele tener óptimo finito.

## Ejercicios propuestos

1. Resuelve gráficamente: $\text{Max } Z = 6x_1 + 4x_2$ s.a. $3x_1 + 2x_2 \le 18$, $x_1 \le 4$, $x_1, x_2 \ge 0$. ¿Qué caso especial ocurre?
   - *Respuesta:* Vértices $(0,0)\to 0$, $(4,0)\to 24$, $(4,3)\to 36$, $(0,9)\to 36$. Existen **óptimos alternativos** a lo largo del segmento entre $(4,3)$ y $(0,9)$, todos con $Z^* = 36$.

## Conexiones

- Anterior: [[Investigación de Operaciones I - Formulación de Programación Lineal]]
- Siguiente: [[Investigación de Operaciones I - Método Símplex]]
- Materia: [[Investigación de Operaciones I]]
- Materias relacionadas: [[Matemática I]], [[Matemática IV]]

## Fuente

- Programa de [[Investigación de Operaciones I]] (Taha, Cap. 2; Hillier & Lieberman, Cap. 3).
