---
tags: [clase, semestre-III]
materia: Estructura de Datos
---
# Estructura de Datos - Grafos, Recorridos y Ruta Mínima

Materia: [[Estructura de Datos]]
Anterior: [[Estructura de Datos - Árboles Binarios de Búsqueda y AVL]]
Siguiente: —

## Contexto y objetivo

Los **grafos** generalizan a los árboles permitiendo ciclos y múltiples caminos entre nodos, lo que los convierte en el modelo natural para redes de transporte, topologías de red y dependencias. En el Tema 5 de [[Estructura de Datos]] (ver Grafos y representaciones), se aplican grafos ponderados al proyecto SpeedCar para calcular rutas mínimas entre sectores de San Cristóbal.

## 1. Definiciones y representaciones

Un grafo $G = (V, E)$ consta de un conjunto de vértices $V$ y aristas $E$:
- **Dirigido (digrafo)** vs. **no dirigido**.
- **Ponderado**: cada arista $(u, v)$ tiene un peso $w(u, v)$ (distancia, costo o tiempo).

| Representación | Memoria | Consultar si existe $(u, v)$ | Recorrer vecinos de $u$ | Cuándo usar |
|---|---|---|---|---|
| **Matriz de adyacencia** | $O(\|V\|^2)$ | $O(1)$ | $O(\|V\|)$ | Grafos densos ($\|E\| \approx \|V\|^2$) |
| **Lista de adyacencia** | $O(\|V\| + \|E\|)$ | $O(\text{grado}(u))$ | $O(\text{grado}(u))$ | Grafos dispersos ($\|E\| \ll \|V\|^2$) |

## 2. Recorridos: BFS y DFS

- **BFS (Búsqueda en Anchura)**: explora por niveles usando una **cola**. Encuentra el camino con menor número de aristas en grafos no ponderados. Complejidad: $O(|V| + |E|)$ con lista de adyacencia, $O(|V|^2)$ con matriz.
- **DFS (Búsqueda en Profundidad)**: avanza lo más profundo posible antes de retroceder, usando **recursión** o una **pila**. Útil para detectar ciclos y componentes conexas.

```cpp
void dfs(int u, bool vis[], int M[][N], int n) {
    vis[u] = true;
    cout << u << " ";
    for (int v = 0; v < n; v++) {
        if (M[u][v] > 0 && !vis[v]) {
            dfs(v, vis, M, n);
        }
    }
}
```

## 3. Ruta mínima: Algoritmo de Dijkstra

Dado un vértice origen $s$ y pesos **no negativos** ($w \ge 0$), Dijkstra calcula la distancia mínima hacia todos los demás vértices:

1. Inicializar `dist[s] = 0` y `dist[v] = INF` para $v \ne s$; marcar todos como no visitados.
2. Repetir $|V|$ veces:
   - Seleccionar el vértice no visitado $u$ con menor `dist[u]`.
   - Marcar $u$ como visitado.
   - Para cada vecino $v$ de $u$, **relajar** la arista:
     $$\text{si } \text{dist}[u] + w(u, v) < \text{dist}[v] \implies \text{dist}[v] = \text{dist}[u] + w(u, v), \; \text{padre}[v] = u$$

Complejidad: $O(|V|^2)$ con matriz/búsqueda lineal, y $O((|V| + |E|) \log |V|)$ usando cola de prioridad (`priority_queue`).

## Ejemplo resuelto

Grafo no dirigido con aristas `A-B(4)`, `A-C(2)`, `C-B(1)`, `B-D(5)`, `C-D(8)`. Desde `A`:
- Inicio: `dist = {A:0, B:∞, C:∞, D:∞}`.
- Visita `A`: `dist(B)=4`, `dist(C)=2`.
- Menor no visitado es `C(2)`: relaja `B` a $\min(4, 2+1)=3$ y `D` a $2+8=10$.
- Menor no visitado es `B(3)`: relaja `D` a $\min(10, 3+5)=8$.
- Ruta mínima `A -> D`: `A - C - B - D` con costo total **8**.

## Errores comunes

- Aplicar Dijkstra en grafos con **pesos negativos** (el algoritmo asume que al marcar un nodo como visitado su distancia ya es definitiva; con pesos negativos debe usarse Bellman-Ford).
- Olvidar el arreglo `vis[]` en BFS/DFS cuando el grafo tiene ciclos, cayendo en bucle infinito.
- Al eliminar un vértice en matriz de adyacencia, no reindexar correctamente los vértices o las referencias en los archivos.

## Ejercicios propuestos

1. ¿Qué estructura auxiliar utiliza BFS y qué estructura utiliza DFS?
2. En el ejemplo resuelto, si agregamos la arista `C-D(4)`, ¿cuál sería la nueva distancia mínima de `A` a `D`?

**Respuestas:**
1. BFS usa una **cola** (FIFO); DFS usa una **pila** (LIFO) o la pila de llamadas recursivas.
2. `dist(C) + 4 = 2 + 4 = 6`, mejor que `8`. La ruta sería `A - C - D`.

## Conexiones

- Amplía Grafos y representaciones.
- Cierra la secuencia de [[Estructura de Datos]] y enlaza con [[Programación II]], [[Matemática Discreta]] e [[Investigación de Operaciones I]].

## Fuente

Basado en `Material/Tema 5-Grafos/Presentacion Grafos.ppsx` y `Primer Proyecto Parcial 3/Grafo.h`.
