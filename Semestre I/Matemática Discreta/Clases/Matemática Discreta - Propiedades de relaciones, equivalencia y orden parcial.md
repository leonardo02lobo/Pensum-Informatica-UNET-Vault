---
tags: [clase, semestre-I]
materia: Matemática Discreta
---
# Matemática Discreta - Propiedades de relaciones, equivalencia y orden parcial

Materia: [[Matemática Discreta]]  
Anterior: [[Matemática Discreta - Relaciones binarias y representaciones]] · Siguiente: [[Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton]]

## Contexto y objetivo
Las relaciones binarias sobre un conjunto $A$ se clasifican según propiedades estructurales muy concretas. Dos combinaciones de estas propiedades dan lugar a estructuras fundamentales en matemáticas e informática: las **relaciones de equivalencia** (que particionan un conjunto en clases) y las **relaciones de orden parcial** (que jerarquizan elementos mediante diagramas de Hasse).

## 1. Propiedades de una relación $R$ en $A$

| Propiedad | Definición formal | En matriz $M_R$ | En dígrafo |
|---|---|---|---|
| **Reflexiva** | $\forall a \in A,\; (a,a) \in R$ | Toda la diagonal principal es $1$. | Cada vértice tiene un lazo. |
| **Irreflexiva** | $\forall a \in A,\; (a,a) \notin R$ | Toda la diagonal principal es $0$. | Ningún vértice tiene lazo. |
| **Simétrica** | $(a,b) \in R \rightarrow (b,a) \in R$ | $M_R = M_R^T$ (simétrica). | Toda flecha $a \to b$ tiene su vuelta $b \to a$. |
| **Antisimétrica** | $(a,b) \in R \land (b,a) \in R \rightarrow a = b$ | Si $i \neq j$ y $M[i][j]=1$, entonces $M[j][i]=0$. | No hay flechas bidireccionales entre vértices distintos. |
| **Transitiva** | $(a,b) \in R \land (b,c) \in R \rightarrow (a,c) \in R$ | $M_R^2 \le M_R$ (donde $M_R^2$ tiene $1$, $M_R$ tiene $1$). | Si hay camino $a \to b \to c$, hay atajo $a \to c$. |

> [!warning] Simétrica vs. Antisimétrica
> No son opuestas: una relación puede no ser ninguna de las dos, o puede ser **ambas a la vez** (por ejemplo, la relación identidad $R = \{(1,1),(2,2)\}$).

## 2. Relaciones de equivalencia y particiones
Una relación $R$ en $A$ es de **equivalencia** si es **reflexiva, simétrica y transitiva**.
- La **clase de equivalencia** de $a \in A$ es $[a] = \{x \in A \mid (a, x) \in R\}$.
- Las clases de equivalencia distintas son disjuntas entre sí y su unión es todo $A$: forman una **partición** de $A$.

### Ejemplo
En $A = \{1, 2, 3, 4\}$, sea $R = \{(1,1),(2,2),(3,3),(4,4),(1,2),(2,1),(3,4),(4,3)\}$.
- Es reflexiva (están los 4 pares $(i,i)$), simétrica y transitiva.
- Clases de equivalencia: $[1] = [2] = \{1, 2\}$ y $[3] = [4] = \{3, 4\}$.

## 3. Relaciones de orden parcial y diagrama de Hasse
Una relación $R$ en $A$ es un **orden parcial** (y $(A, R)$ es un conjunto parcialmente ordenado o *poset*) si es **reflexiva, antisimétrica y transitiva**. Ejemplo clásico: la divisibilidad ($a \mid b$) o la inclusión de conjuntos ($\subseteq$).

El **diagrama de Hasse** simplifica el dígrafo de un orden parcial finito:
1. Se omiten todos los lazos (se asume reflexividad).
2. Se omiten las aristas implicadas por transitividad (ej. si $1 \mid 2$ y $2 \mid 4$, no se dibuja $1 \to 4$).
3. Se orientan las conexiones hacia arriba y se quitan las puntas de flecha.

## Errores comunes
- Creer que una relación es reflexiva solo porque tiene *algunos* pares $(a,a)$: debe tener $(a,a)$ para **todos** los elementos de $A$.
- Verificar transitividad solo en pares evidentes y pasar por alto un caso $(a,b),(b,c)$ donde $(a,c)$ falta.
- Confundir antisimétrica con asimétrica (la antisimétrica sí permite lazos $(a,a)$).

## Ejercicios propuestos
1. En $A = \{1, 2, 3\}$, determina qué propiedades cumple $R = \{(1,1), (2,2), (3,3), (1,2), (2,3)\}$.  
   *Respuesta:* Reflexiva y antisimétrica; **no** es simétrica (falta $(2,1)$) ni transitiva (están $(1,2)$ y $(2,3)$ pero falta $(1,3)$).
2. Dibuja mentalmente o en papel el diagrama de Hasse para los divisores de $6$: $D_6 = \{1, 2, 3, 6\}$ con la relación $a \mid b$.  
   *Respuesta:* $1$ abajo conectado hacia arriba con $2$ y $3$, y ambos conectados hacia arriba con $6$ (sin arista directa $1$–$6$).

## Conexiones
- Materia principal: [[Matemática Discreta]]
- Nota resumen: [[Matemática Discreta - Relaciones binarias y representaciones]]
- Anterior: [[Matemática Discreta - Relaciones binarias y representaciones]]
- Siguiente: [[Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton]]

## Fuente
Material de [[Matemática Discreta]] en `Material/Relaciones/` (`1 Relacionesparte1bcarvajal.pdf`, `2 Relación binaria AxAparte2bcarvajal.pdf`).
