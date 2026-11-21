---
tags: [clase, semestre-I]
materia: Matemática Discreta
---
# Matemática Discreta - Relaciones binarias y representaciones

Materia: [[Matemática Discreta]]  
Anterior: [[Matemática Discreta - Leyes del álgebra de conjuntos y cardinalidad]] · Siguiente: [[Matemática Discreta - Propiedades de relaciones, equivalencia y orden parcial]]

## Contexto y objetivo
Las **relaciones binarias** formalizan cómo se vinculan los elementos de dos conjuntos (o de un conjunto consigo mismo): desde la relación *"es menor o igual que"* hasta las tablas de una base de datos relacional. En esta clase se definen las relaciones, su dominio y rango, la relación inversa, la composición y sus tres formas de representación: **pares ordenados, matriz booleana y dígrafo**.

## 1. Definición de relación binaria, dominio y rango
Dados dos conjuntos $A$ y $B$, una **relación binaria $R$ de $A$ en $B$** es cualquier subconjunto del producto cartesiano:
$$R \subseteq A \times B$$
Si $(a, b) \in R$, también se escribe $a\, R\, b$. Cuando $B = A$, se dice que $R$ es una **relación en $A$** ($R \subseteq A \times A$).
- **Dominio ($\text{Dom}(R)$)**: $\{a \in A \mid \exists b \in B,\, (a, b) \in R\}$ (primeras componentes).
- **Rango o imagen ($\text{Ran}(R)$)**: $\{b \in B \mid \exists a \in A,\, (a, b) \in R\}$ (segundas componentes).

## 2. Operaciones: inversa y composición
- **Relación inversa ($R^{-1}$)**: se invierte el orden de cada par:
  $$R^{-1} = \{(b, a) \in B \times A \mid (a, b) \in R\}$$
- **Composición ($S \circ R$)**: si $R \subseteq A \times B$ y $S \subseteq B \times C$, entonces:
  $$S \circ R = \{(a, c) \in A \times C \mid \exists b \in B,\, (a, b) \in R \land (b, c) \in S\}$$

## 3. Representación de una relación en $A$
Sea $A = \{a_1, a_2, \dots, a_n\}$ y $R \subseteq A \times A$:

1. **Matriz booleana $M_R$ ($n \times n$)**:
   $$M_R[i][j] = \begin{cases} 1 & \text{si } (a_i, a_j) \in R \\ 0 & \text{si } (a_i, a_j) \notin R \end{cases}$$
   La matriz de $R^{-1}$ es la **transpuesta** $M_R^T$. La matriz de $R \circ R$ se obtiene mediante el **producto booleano** $M_R \odot M_R$ (donde la suma se reemplaza por $\lor$ y el producto por $\land$).
2. **Grafo dirigido (dígrafo)**: cada elemento de $A$ es un vértice, y cada par $(a_i, a_j) \in R$ es una flecha (arista dirigida) de $a_i$ hacia $a_j$. Un par $(a_i, a_i)$ se dibuja como un **lazo**.

## 4. Ejemplo resuelto
Sea $A = \{1, 2, 3\}$ y la relación $R = \{(1, 1), (1, 2), (2, 3), (3, 1)\}$:
- $\text{Dom}(R) = \{1, 2, 3\}$, $\text{Ran}(R) = \{1, 2, 3\}$.
- $R^{-1} = \{(1, 1), (2, 1), (3, 2), (1, 3)\}$.
- Matriz booleana:
  $$M_R = \begin{pmatrix} 1 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{pmatrix}$$
- En el dígrafo hay un lazo en $1$, y flechas $1 \to 2$, $2 \to 3$ y $3 \to 1$.

## Errores comunes
- Invertir filas y columnas al construir $M_R$: la fila $i$ corresponde al primer elemento del par $(a_i, a_j)$ y la columna $j$ al segundo.
- Confundir el orden en la composición $S \circ R$: primero se aplica $R$ (de $A$ a $B$) y luego $S$ (de $B$ a $C$).
- Usar suma aritmética ordinaria en vez de suma booleana ($1 + 1 = 1$) al calcular el producto matricial de composición.

## Ejercicios propuestos
1. Dado $A = \{1, 2, 3, 4\}$ y $R = \{(a, b) \mid a \text{ divide a } b\}$, escribe los pares de $R$ y su matriz booleana.  
   *Respuesta:* $R = \{(1,1),(1,2),(1,3),(1,4),(2,2),(2,4),(3,3),(4,4)\}$; $M_R$ tiene $1$ en la diagonal, toda la fila $1$, y la entrada $(2,4)$.
2. Si $M_R$ es $3 \times 3$, ¿cuántas relaciones binarias distintas pueden definirse sobre un conjunto de $3$ elementos?  
   *Respuesta:* $2^{3 \times 3} = 2^9 = 512$ relaciones.

## Conexiones
- Materia principal: [[Matemática Discreta]]
- Nota resumen: Relaciones binarias (Matemática Discreta)
- Anterior: [[Matemática Discreta - Leyes del álgebra de conjuntos y cardinalidad]]
- Siguiente: [[Matemática Discreta - Propiedades de relaciones, equivalencia y orden parcial]]
- Aplicación: [[Base de Datos I]] (modelo relacional), [[Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton]].

## Fuente
Material de [[Matemática Discreta]] en `Material/Relaciones/` (`1 Relacionesparte1bcarvajal.pdf`, `2 Relación binaria AxAparte2bcarvajal.pdf`).
