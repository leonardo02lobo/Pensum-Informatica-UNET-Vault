---
tags: [clase, semestre-I]
materia: Matemática Discreta
---
# Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton

Materia: [[Matemática Discreta]]  
Anterior: [[Matemática Discreta - Propiedades de relaciones, equivalencia y orden parcial]] · Siguiente: [[Matemática Discreta - Árboles, árboles binarios y recorridos]]

## Contexto y objetivo
Los **grafos** modelan redes de computadores, rutas de transporte, dependencias de tareas y estructuras de datos. En esta clase (correspondiente al III parcial) se estudian las definiciones de grafos y dígrafos, grados de vértices, representaciones matriciales (**adyacencia e incidencia**) y los criterios clásicos de **caminos y circuitos de Euler y Hamilton**.

## 1. Definiciones fundamentales
Un **grafo** $G = (V, E)$ consta de un conjunto finito no vacío de **vértices** $V$ y un conjunto de **aristas** $E$ que conectan pares de vértices:
- **Grafo no dirigido vs. dígrafo**: en el primero las aristas no tienen orientación $\{u,v\}$; en el dígrafo son pares ordenados $(u,v)$.
- **Grafo simple**: no tiene **lazos** (arista de un vértice a sí mismo) ni **aristas paralelas** (múltiples aristas entre el mismo par de vértices).
- **Grafo completo $K_n$**: grafo simple donde todo par de vértices distintos está conectado; tiene $\frac{n(n-1)}{2}$ aristas.
- **Grafo conexo**: existe al menos un camino entre cualquier par de vértices.

### Grado de un vértice
El **grado** $\text{gr}(v)$ es el número de aristas incidentes en $v$ (cada lazo aporta $2$ al grado). En dígrafos se distingue entre **grado de entrada** $\text{gr}^-(v)$ y **grado de salida** $\text{gr}^+(v)$.

> [!important] Teorema del apretón de manos
> En todo grafo no dirigido, la suma de los grados de todos los vértices es el doble del número de aristas:
> $$\sum_{v \in V} \text{gr}(v) = 2|E|$$
> Corolario: el número de vértices con **grado impar** siempre es **par**.

## 2. Matrices de representación
- **Matriz de adyacencia $A$ ($|V| \times |V|$)**: $A[i][j]$ indica el número de aristas entre $v_i$ y $v_j$ ($1$ o $0$ en grafos simples). Para grafos no dirigidos, $A$ es simétrica.
- **Matriz de incidencia $M$ ($|V| \times |E|$)**: filas = vértices, columnas = aristas. En grafos no dirigidos, $M[i][k] = 1$ si $v_i$ es extremo de la arista $e_k$ (y $2$ si es un lazo).

### Ejemplo de matriz de adyacencia para $K_3$
Para el triángulo con vértices $\{1, 2, 3\}$ y aristas $\{1\text{-}2, 2\text{-}3, 1\text{-}3\}$:
$$A = \begin{pmatrix} 0 & 1 & 1 \\ 1 & 0 & 1 \\ 1 & 1 & 0 \end{pmatrix}$$

## 3. Caminos y circuitos de Euler y Hamilton
- **Euleriano** (recorre **todas las aristas** exactamente una vez):
  - Un grafo conexo tiene **circuito euleriano** (empieza y termina en el mismo vértice) $\iff$ **todos** sus vértices tienen grado par.
  - Tiene **camino euleriano** (no cerrado) $\iff$ tiene **exactamente 2** vértices de grado impar (el camino empieza en uno y termina en el otro).
- **Hamiltoniano** (visita **todos los vértices** exactamente una vez, sin repetir salvo el cierre):
  - No existe una condición necesaria y suficiente simple.
  - **Teorema de Dirac** (condición suficiente): si $G$ es simple con $n \ge 3$ vértices y $\text{gr}(v) \ge n/2$ para todo $v$, entonces $G$ tiene un ciclo hamiltoniano.

## Errores comunes
- Confundir Euler (pasar por todas las **aristas** una vez) con Hamilton (pasar por todos los **vértices** una vez).
- Contar un lazo como grado $1$ en lugar de grado $2$ al verificar $\sum \text{gr}(v) = 2|E|$.
- Olvidar verificar que el grafo sea **conexo** (salvo vértices aislados) antes de aplicar el criterio de Euler.

## Ejercicios propuestos
1. ¿Cuántas aristas tiene un grafo regular de $6$ vértices donde cada vértice tiene grado $3$?  
   *Respuesta:* $\sum \text{gr}(v) = 6 \cdot 3 = 18 = 2|E| \implies |E| = 9$ aristas.
2. Un grafo conexo tiene grados $2, 2, 3, 3, 4$. ¿Tiene circuito euleriano o camino euleriano?  
   *Respuesta:* Tiene **camino euleriano** (exactamente dos vértices de grado impar: los de grado $3$), pero no circuito euleriano.

## Conexiones
- Materia principal: [[Matemática Discreta]]
- Nota resumen: Grafos y árboles (Matemática Discreta)
- Anterior: [[Matemática Discreta - Propiedades de relaciones, equivalencia y orden parcial]]
- Siguiente: [[Matemática Discreta - Árboles, árboles binarios y recorridos]]
- Aplicación: [[Estructura de Datos]] (implementación en código), [[Investigación de Operaciones I]] (redes y ruta más corta).

## Fuente
Material de [[Matemática Discreta]] en `Material/Teorema de grafos /` (`1  Mate_Discreta(IIIparcial).pdf`, `2  mapa conceptual Digrafo bcarvajal.pdf`, `Ejemplo de matriz de adyacencia e incidencia en un grafo no dirigido y dirigido..pdf`).
