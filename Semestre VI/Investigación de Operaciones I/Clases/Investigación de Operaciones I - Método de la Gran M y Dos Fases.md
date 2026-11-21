---
tags: [clase, semestre-VI]
materia: Investigación de Operaciones I
---
# Investigación de Operaciones I - Método de la Gran M y Dos Fases

Materia: [[Investigación de Operaciones I]]  
Anterior: [[Investigación de Operaciones I - Método Símplex]]  
Siguiente: [[Investigación de Operaciones I - Dualidad y Análisis de Sensibilidad]]

## Contexto y objetivo

Extender el algoritmo símplex a modelos con restricciones de igualdad ($=$) o mayor o igual ($\ge$), donde el origen $(0, \dots, 0)$ no es factible, mediante **variables de exceso**, **variables artificiales**, el **método de la Gran M** y el **método de las Dos Fases**.

## 1. Variables de exceso y artificiales

Cuando una restricción tiene signo $\ge$ o $=$ (con $b_i \ge 0$):
- **Restricción $\ge$**: se resta una **variable de exceso** $e_i \ge 0$ y se suma una **variable artificial** $A_i \ge 0$ para obtener una columna identidad inicial:
  $$x_1 + x_2 \ge 10 \implies x_1 + x_2 - e_1 + A_1 = 10$$
- **Restricción $=$**: se suma directamente una **variable artificial** $A_i \ge 0$:
  $$2x_1 + x_2 = 8 \implies 2x_1 + x_2 + A_2 = 8$$

Las variables artificiales **no tienen significado físico**; son un artificio matemático para arrancar el símplex y deben valer $0$ en la solución óptima final.

## 2. Método de la Gran M (Penalización)

Se asigna una penalización muy grande $M > 0$ a cada variable artificial en la función objetivo para forzar su salida de la base:
- En **Maximización**: $Z_{\text{M}} = \sum c_j x_j - M \sum A_i$
- En **Minimización**: $Z_{\text{M}} = \sum c_j x_j + M \sum A_i$

**Paso crítico antes de iterar:** como las variables artificiales $A_i$ forman la base inicial, sus coeficientes en la fila $Z$ deben hacerse **cero** sumando o restando múltiplos de las filas de las restricciones correspondientes a la fila $Z$.

### Ejemplo breve (Minimización)
$$\text{Min } Z = 4x_1 + x_2 \quad \text{s.a.} \quad 3x_1 + x_2 = 3, \quad 4x_1 + 3x_2 \ge 6, \quad x_1, x_2 \ge 0$$
Forma aumentada:
$$3x_1 + x_2 + A_1 = 3$$
$$4x_1 + 3x_2 - e_2 + A_2 = 6$$
$$\text{Min } Z = 4x_1 + x_2 + M A_1 + M A_2 \implies Z - 4x_1 - x_2 - M A_1 - M A_2 = 0$$
Eliminando $A_1$ y $A_2$ de la fila $Z$ (sumando $M \cdot F_1 + M \cdot F_2$):
$$Z + (7M - 4)x_1 + (4M - 1)x_2 - M e_2 = 9M$$
En minimización entra la variable con coeficiente más positivo en la fila $Z$ ($7M - 4$, es decir $x_1$). Al iterar, $A_1$ y $A_2$ salen de la base y se obtiene el óptimo real: $x_1 = 3/5, x_2 = 6/5, Z^* = 18/5 = 3.6$.

## 3. Método de las Dos Fases

Evita problemas numéricos de elegir un valor concreto para $M$ (muy útil en implementaciones computacionales):

- **Fase I**: se ignora la función objetivo original y se resuelve:
  $$\text{Min } W = \sum A_i$$
  sujeto a las restricciones aumentadas.
  - Si $W^* > 0$ (alguna $A_i > 0$ en la base), el problema original es **infactible** y se detiene.
  - Si $W^* = 0$, todas las $A_i$ valen cero: se eliminan las columnas artificiales y se pasa a la Fase II.
- **Fase II**: se restaura la función objetivo original $Z$ (eliminando de la fila $Z$ las variables básicas actuales) y se aplica el símplex estándar desde la SBF factible hallada en la Fase I.

## Errores comunes

- Olvidar **despejar las variables artificiales de la fila $Z$** antes de elegir la primera variable de entrada.
- Usar el criterio de entrada de maximización en un problema de minimización (en minimización con fila $Z - c_j x_j = 0$, entra la variable con coeficiente más **positivo**; o bien se convierte $\text{Min } Z$ en $\text{Max } (-Z)$ y se aplica siempre la misma regla).
- No detectar **infactibilidad** cuando la tabla es óptima pero persiste alguna variable artificial básica con valor $> 0$.

## Ejercicios propuestos

1. Escribe la Fase I (restricciones aumentadas y función $W$) para: $\text{Min } Z = 2x_1 + 3x_2$ s.a. $x_1 + 2x_2 \ge 4$, $x_1 + x_2 = 3$, $x_1, x_2 \ge 0$.
   - *Respuesta:* $x_1 + 2x_2 - e_1 + A_1 = 4$, $x_1 + x_2 + A_2 = 3$; $\text{Min } W = A_1 + A_2$. Al eliminar $A_1, A_2$ de la fila $W$: $W - 2x_1 - 3x_2 + e_1 = -7$ (si se expresa $W - \sum c_j x_j = 0$, o $W + 2x_1 + 3x_2 - e_1 = 7$).

## Conexiones

- Anterior: [[Investigación de Operaciones I - Método Símplex]]
- Siguiente: [[Investigación de Operaciones I - Dualidad y Análisis de Sensibilidad]]
- Materia: [[Investigación de Operaciones I]]
- Materias relacionadas: [[Análisis Numérico]], [[Matemática IV]]

## Fuente

- Programa de [[Investigación de Operaciones I]] (Taha, Cap. 3.4; Hillier & Lieberman, Cap. 4.6).
