---
tags: [clase, semestre-VI]
materia: Investigación de Operaciones I
---
# Investigación de Operaciones I - Método Símplex

Materia: [[Investigación de Operaciones I]]  
Anterior: [[Investigación de Operaciones I - Método Gráfico y Casos Especiales]]  
Siguiente: [[Investigación de Operaciones I - Método de la Gran M y Dos Fases]]

## Contexto y objetivo

Comprender y ejecutar el **algoritmo Símplex** para resolver modelos de Programación Lineal de cualquier número de variables: conversión a **forma estándar**, variables de holgura, concepto de **solución básica factible (SBF)**, criterio de optimalidad, criterio de factibilidad (cociente mínimo) y pivoteo de Gauss-Jordan.

## 1. Forma estándar y variables de holgura

Para aplicar el método símplex, todas las restricciones funcionales deben ser igualdades con lado derecho $b_i \ge 0$ y todas las variables no negativas.
- En una restricción $\le$: se suma una **variable de holgura** $s_i \ge 0$ que representa recurso no utilizado.
  $$4x_1 + 3x_2 \le 240 \implies 4x_1 + 3x_2 + s_1 = 240$$
- La función objetivo se escribe como ecuación igualada a cero:
  $$Z - 50x_1 - 30x_2 = 0$$

Con $m$ restricciones y $n$ variables totales ($n > m$), una **solución básica** se obtiene fijando $n - m$ variables en cero (**no básicas**) y resolviendo el sistema $m \times m$ para las $m$ **variables básicas**. Si todas las básicas son $\ge 0$, es una **Solución Básica Factible (SBF)**, equivalente algebraico a un vértice.

## 2. Algoritmo Símplex (Maximización)

1. **Inicialización**: partir de la SBF inicial donde las holguras son básicas ($x_1 = x_2 = 0, s_1 = 240, s_2 = 100, Z = 0$).
2. **Prueba de optimalidad (variable de entrada)**: en la fila $Z$, si todos los coeficientes de las variables no básicas son $\ge 0$, la solución actual es óptima. Si hay negativos, entra la variable con el coeficiente **más negativo** (mayor tasa de mejora por unidad).
3. **Prueba de factibilidad / razón mínima (variable de salida)**: para la columna pivote $k$ con $a_{ik} > 0$, calcular $\theta_i = b_i / a_{ik}$. Sale de la base la fila con el **menor cociente $\theta_i \ge 0$** (si ningún $a_{ik} > 0$, el problema es **no acotado**).
4. **Pivoteo (Gauss-Jordan)**: normalizar la fila pivote dividiendo por el elemento pivote y hacer ceros en el resto de la columna pivote (incluyendo la fila $Z$). Repetir desde el paso 2.

## 3. Ejemplo trabajado paso a paso

Modelo: $\text{Max } Z = 50x_1 + 30x_2$ s.a. $4x_1 + 3x_2 + s_1 = 240$, $2x_1 + x_2 + s_2 = 100$.

**Tabla inicial:**

| Básica | $Z$ | $x_1$ | $x_2$ | $s_1$ | $s_2$ | LD | Razón $\theta$ |
|---|---|---|---|---|---|---|---|
| $Z$ | $1$ | $-50$ | $-30$ | $0$ | $0$ | $0$ | — |
| $s_1$ | $0$ | $4$ | $3$ | $1$ | $0$ | $240$ | $240/4 = 60$ |
| $s_2$ | $0$ | $2$ | $1$ | $0$ | $1$ | $100$ | $100/2 = 50$ (sale $s_2$) |

Entra $x_1$ (coef. $-50$), sale $s_2$ ($\theta = 50$). Pivote: $2$.

**Iteración 1** ($F_2' = F_2/2$; $F_1' = F_1 - 4F_2'$; $F_Z' = F_Z + 50F_2'$):

| Básica | $Z$ | $x_1$ | $x_2$ | $s_1$ | $s_2$ | LD | Razón $\theta$ |
|---|---|---|---|---|---|---|---|
| $Z$ | $1$ | $0$ | $-5$ | $0$ | $25$ | $2500$ | — |
| $s_1$ | $0$ | $0$ | $1$ | $1$ | $-2$ | $40$ | $40/1 = 40$ (sale $s_1$) |
| $x_1$ | $0$ | $1$ | $1/2$ | $0$ | $1/2$ | $50$ | $50/(1/2) = 100$ |

Entra $x_2$ (coef. $-5$), sale $s_1$ ($\theta = 40$). Pivote: $1$.

**Iteración 2 (Tabla óptima):**

| Básica | $Z$ | $x_1$ | $x_2$ | $s_1$ | $s_2$ | LD |
|---|---|---|---|---|---|---|
| $Z$ | $1$ | $0$ | $0$ | $5$ | $15$ | $2700$ |
| $x_2$ | $0$ | $0$ | $1$ | $1$ | $-2$ | $40$ |
| $x_1$ | $0$ | $1$ | $0$ | $-1/2$ | $3/2$ | $30$ |

Todos los coeficientes de la fila $Z$ son $\ge 0$: **óptimo alcanzado** en $(x_1^*, x_2^*) = (30, 40)$ con $Z^* = 2700$.

## 4. Degeneración y casos especiales en la tabla

- **Degeneración**: ocurre cuando hay empate en la razón mínima o una variable básica vale $0$; puede producir iteraciones sin mejora en $Z$.
- **Óptimos alternativos**: en la tabla óptima, una variable *no básica* tiene coeficiente $0$ en la fila $Z$.

## Errores comunes

- Dividir por un elemento pivote negativo o cero en la prueba de razón mínima ($\theta$ solo se calcula para $a_{ik} > 0$).
- Olvidar actualizar la fila $Z$ durante el pivoteo.

## Ejercicios propuestos

1. Aplica el método símplex a $\text{Max } Z = 3x_1 + 2x_2$ s.a. $x_1 + x_2 \le 4$, $2x_1 + x_2 \le 6$, $x_1, x_2 \ge 0$.
   - *Respuesta:* Iteración 1: entra $x_1$, sale $s_2$ ($x_1=3, Z=9$). Iteración 2: entra $x_2$, sale $s_1$. Óptimo: $x_1^* = 2, x_2^* = 2, Z^* = 10$.

## Conexiones

- Anterior: [[Investigación de Operaciones I - Método Gráfico y Casos Especiales]]
- Siguiente: [[Investigación de Operaciones I - Método de la Gran M y Dos Fases]]
- Materia: [[Investigación de Operaciones I]]
- Materias relacionadas: [[Matemática IV]], [[Análisis Numérico]]

## Fuente

- Programa de [[Investigación de Operaciones I]] (Taha, Cap. 3; Hillier & Lieberman, Cap. 4).
