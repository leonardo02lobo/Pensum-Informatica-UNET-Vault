---
tags: [clase, semestre-I]
materia: Matemática Discreta
---
# Matemática Discreta - Teoría de conjuntos y operaciones básicas

Materia: [[Matemática Discreta]]  
Anterior: [[Matemática Discreta - Lógica proposicional y cuantificadores]] · Siguiente: [[Matemática Discreta - Leyes del álgebra de conjuntos y cardinalidad]]

## Contexto y objetivo
La **teoría de conjuntos** constituye el bloque del I parcial de Matemática Discreta y es el lenguaje base sobre el que se definen relaciones, funciones, grafos y bases de datos relacionales. En esta clase se estudian la notación de conjuntos, las relaciones de pertenencia e inclusión, los conjuntos especiales y todas las operaciones conjuntistas con su representación en **diagramas de Venn**.

## 1. Definición, notación y subconjuntos
Un **conjunto** es una colección bien definida de objetos distintos llamados *elementos*. Puede expresarse:
- **Por extensión**: enumerando sus elementos, $A = \{1, 2, 3, 4\}$.
- **Por comprensión**: indicando la propiedad que cumplen, $A = \{x \in \mathbb{N} \mid 1 \le x \le 4\}$.

### Pertenencia ($\in$) vs. Inclusión ($\subseteq$)
- $a \in A$: el elemento $a$ pertenece al conjunto $A$.
- $A \subseteq B$: $A$ es **subconjunto** de $B$ si $\forall x,\, (x \in A \rightarrow x \in B)$.
- **Subconjunto propio ($A \subset B$)**: $A \subseteq B$ y $A \neq B$.
- **Igualdad**: $A = B \iff A \subseteq B \text{ y } B \subseteq A$.

### Conjuntos especiales
- **Conjunto vacío ($\emptyset$ o $\{\}$)**: no tiene elementos; es subconjunto de todo conjunto ($\emptyset \subseteq A$).
- **Conjunto universal ($U$)**: contiene todos los elementos del contexto bajo estudio.
- **Conjunto potencia $\mathcal{P}(A)$**: conjunto de todos los subconjuntos de $A$. Si $|A| = n$, entonces $|\mathcal{P}(A)| = 2^n$.

## 2. Operaciones entre conjuntos
Sean $A, B \subseteq U$:
- **Unión ($A \cup B$)**: $\{x \in U \mid x \in A \lor x \in B\}$.
- **Intersección ($A \cap B$)**: $\{x \in U \mid x \in A \land x \in B\}$. Si $A \cap B = \emptyset$, se dicen *disjuntos*.
- **Diferencia ($A - B$ o $A \setminus B$)**: $\{x \in U \mid x \in A \land x \notin B\}$.
- **Complemento ($A'$ o $\overline{A}$ o $A^c$)**: $\{x \in U \mid x \notin A\} = U - A$.
- **Diferencia simétrica ($A \triangle B$)**: elementos que están en $A$ o en $B$, pero no en ambos:
  $$A \triangle B = (A - B) \cup (B - A) = (A \cup B) - (A \cap B)$$

## 3. Producto cartesiano
El **producto cartesiano** de $A$ y $B$ es el conjunto de todos los pares ordenados $(a, b)$:
$$A \times B = \{(a, b) \mid a \in A \land b \in B\}$$
En general, $A \times B \neq B \times A$ (el orden importa). Su cardinalidad es $|A \times B| = |A| \cdot |B|$.

## 4. Ejemplo resuelto
Sea $U = \{1, 2, 3, 4, 5, 6\}$, $A = \{1, 2, 3\}$ y $B = \{3, 4, 5\}$:
- $A \cup B = \{1, 2, 3, 4, 5\}$
- $A \cap B = \{3\}$
- $A - B = \{1, 2\}$
- $A' = \{4, 5, 6\}$
- $A \triangle B = \{1, 2, 4, 5\}$
- $\mathcal{P}(A)$ tiene $2^3 = 8$ subconjuntos: $\{\emptyset, \{1\}, \{2\}, \{3\}, \{1,2\}, \{1,3\}, \{2,3\}, \{1,2,3\}\}$.

## Errores comunes
- Confundir $\in$ (elemento–conjunto) con $\subseteq$ (conjunto–conjunto): escribir $\{1\} \in \{1, 2\}$ es falso; lo correcto es $\{1\} \subseteq \{1, 2\}$ o $1 \in \{1, 2\}$.
- Olvidar que $\emptyset$ y el propio $A$ siempre forman parte de $\mathcal{P}(A)$.
- Asumir que $A - B = B - A$ (la diferencia no es conmutativa).

## Ejercicios propuestos
1. Si $A = \{a, b\}$ y $B = \{1, 2, 3\}$, halla $A \times B$ y $|A \times B|$.  
   *Respuesta:* $\{(a,1),(a,2),(a,3),(b,1),(b,2),(b,3)\}$, con cardinalidad $2 \cdot 3 = 6$.
2. Sombrea en un diagrama de Venn la región $(A \cup B) - C$ y verifica qué elementos de $U=\{1..6\}$ pertenecen si $A=\{1,2\}$, $B=\{2,3,4\}$, $C=\{4,5\}$.  
   *Respuesta:* $\{1, 2, 3\}$.

## Conexiones
- Materia principal: [[Matemática Discreta]]
- Nota resumen: Teoría de conjuntos y leyes (Matemática Discreta)
- Anterior: [[Matemática Discreta - Lógica proposicional y cuantificadores]]
- Siguiente: [[Matemática Discreta - Leyes del álgebra de conjuntos y cardinalidad]]
- Aplicación: [[Base de Datos I]] (álgebra relacional y operaciones de conjuntos en SQL).

## Fuente
Material de [[Matemática Discreta]] en `Material/PARCIAL 1/` (`01. Teoría de Conjuntos.pdf`, `1 IntroduccTeoriaConjuntos-Operac Murillo Tsijli.pdf`).
