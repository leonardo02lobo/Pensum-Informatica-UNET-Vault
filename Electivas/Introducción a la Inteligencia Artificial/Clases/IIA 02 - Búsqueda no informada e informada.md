---
tags: [clase, electiva]
materia: Introducción a la Inteligencia Artificial
fuente: "conocimiento general"
---
# IIA 02 - Búsqueda no informada e informada

Materia: [[Introducción a la Inteligencia Artificial]]
Anterior: [[IIA 01 - Agentes racionales y entornos]]
Siguiente: [[IIA 03 - Búsqueda local y algoritmos genéticos]]

## Contexto y objetivo
Un agente basado en objetivos resuelve problemas buscando una secuencia de acciones que lleve del estado inicial a una meta. Objetivo: formular problemas, comparar BFS, DFS, costo uniforme y A* en completitud, optimalidad y complejidad, y diseñar heurísticas.

## Formulación de un problema de búsqueda
Cinco componentes: estado inicial, acciones aplicables, modelo de transición (resultado de una acción), prueba de meta y costo de camino (suma de costos de paso $c(s,a,s')\ge0$). Una solución es un camino del inicial a una meta; es óptima si tiene costo mínimo. El espacio de estados es un grafo; la búsqueda construye un árbol de nodos con: estado, padre, acción y costo $g$.

Medidas: completitud, optimalidad, complejidad temporal y espacial en términos de $b$ (factor de ramificación), $d$ (profundidad de la meta menos profunda) y $m$ (profundidad máxima).

## Búsqueda no informada
| Algoritmo | Frontera | Completo | Óptimo | Tiempo | Espacio |
|---|---|---|---|---|---|
| BFS (anchura) | cola FIFO | sí ($b$ finito) | sí si costos iguales | $O(b^d)$ | $O(b^d)$ |
| Costo uniforme | cola de prioridad por $g$ | sí (costos $\ge\epsilon>0$) | sí | $O(b^{1+\lfloor C^*/\epsilon\rfloor})$ | igual |
| DFS (profundidad) | pila LIFO | no (ciclos o profundidad infinita) | no | $O(b^m)$ | $O(bm)$ |
| Profundidad limitada | DFS con límite $l$ | no si $l<d$ | no | $O(b^l)$ | $O(bl)$ |
| Profundización iterativa | DFS con $l=0,1,2,\dots$ | sí | sí (costos iguales) | $O(b^d)$ | $O(bd)$ |

Con grafos hay que recordar los nodos ya explorados (conjunto "explorados") para no ciclar.

## Búsqueda informada
Usa una **heurística** $h(n)$: estimación del costo desde $n$ a la meta.
- **Voraz (primero el mejor):** ordena por $h(n)$. Rápida, ni completa ni óptima.
- **A\*:** ordena por $f(n)=g(n)+h(n)$.

**Condiciones de optimalidad de A\*:** $h$ **admisible** ($h(n)\le h^*(n)$, nunca sobreestima) garantiza optimalidad en búsqueda en árbol; $h$ **consistente** ($h(n)\le c(n,a,n')+h(n')$) la garantiza en grafos y hace $f$ no decreciente a lo largo de un camino. Consistente implica admisible.

**Diseño de heurísticas:** resolver una versión relajada del problema. Para el 8-puzzle: $h_1$ = fichas fuera de lugar; $h_2$ = suma de distancias Manhattan. Ambas admisibles; $h_2$ domina a $h_1$ ($h_2\ge h_1$) y expande menos nodos. Combinar: $\max(h_1,h_2)$ sigue siendo admisible. Otras: bases de datos de patrones.

## Ejemplo resuelto: A* en un grafo
Aristas: S-A (1), S-B (4), A-B (2), A-G (5), B-G (1). Heurística: $h(S)=4$, $h(A)=3$, $h(B)=1$, $h(G)=0$ (admisible: costo real óptimo S-A-B-G = 4).

1. Frontera: S ($f=0+4=4$). Se expande S.
2. Genera A ($g=1$, $f=4$) y B ($g=4$, $f=5$).
3. Se expande A ($f=4$). Genera B por A: $g=3$, $f=4$ (mejor que el anterior, que se reemplaza); G por A: $g=6$, $f=6$.
4. Frontera: B ($f=4$), G ($f=6$). Se expande B: G por B: $g=4$, $f=4$ (reemplaza a G con $f=6$).
5. Se expande G con $f=4$: meta. Camino S-A-B-G, costo 4, óptimo.

## Código
```python
import heapq
from collections import deque

grafo = {"S": [("A", 1), ("B", 4)], "A": [("B", 2), ("G", 5)],
         "B": [("G", 1)], "G": []}
h = {"S": 4, "A": 3, "B": 1, "G": 0}

def bfs(grafo, ini, meta):
    cola, vistos = deque([[ini]]), {ini}
    while cola:
        ruta = cola.popleft()
        if ruta[-1] == meta:
            return ruta
        for v, _ in grafo[ruta[-1]]:
            if v not in vistos:
                vistos.add(v)
                cola.append(ruta + [v])

def a_estrella(grafo, ini, meta, h):
    # frontera ordenada por f = g + h
    abierta = [(h[ini], 0, ini, [ini])]
    mejor_g = {}
    while abierta:
        f, g, n, ruta = heapq.heappop(abierta)
        if n == meta:
            return ruta, g
        if n in mejor_g and mejor_g[n] <= g:   # ya llegamos mejor
            continue
        mejor_g[n] = g
        for v, c in grafo[n]:
            heapq.heappush(abierta, (g + c + h[v], g + c, v, ruta + [v]))
    return None

print(bfs(grafo, "S", "G"))            # menos aristas, no menor costo
print(a_estrella(grafo, "S", "G", h))  # (['S','A','B','G'], 4)

# 8-puzzle: heurística Manhattan
def manhattan(estado, meta):
    pos = {v: (i // 3, i % 3) for i, v in enumerate(meta)}
    return sum(abs(i // 3 - pos[v][0]) + abs(i % 3 - pos[v][1])
               for i, v in enumerate(estado) if v != 0)
```

## Errores comunes
- No marcar nodos explorados (bucles infinitos en grafos).
- Detener A* al generar la meta en vez de al expandirla (pierde optimalidad).
- Usar una heurística no admisible y esperar el óptimo.
- Aplicar BFS con costos distintos y esperar camino de costo mínimo (da menos pasos).
- Ignorar la memoria: BFS y A* son limitados por espacio.

## Ejercicios propuestos
1. ¿Cuántos nodos puede generar BFS con $b=10$ hasta $d=5$ (aproximadamente)? *Respuesta: del orden de $10^5$ a $10^6$ ($\sum_{i\le5}10^i\approx111\,111$ más la última capa generada).*
2. Si $h\equiv0$, ¿en qué se convierte A*? *Respuesta: en búsqueda de costo uniforme.*
3. ¿Por qué Manhattan es admisible en el 8-puzzle? *Respuesta: cada ficha necesita al menos esa cantidad de movimientos, que es la solución del problema relajado.*

## Conexiones
- Grafos, colas de prioridad y montículos: [[Estructura de Datos]].
- Teoría de grafos y complejidad: [[Matemática Discreta]].
- Caminos mínimos como optimización: [[Investigación de Operaciones I]].

## Fuente
Conocimiento general (Russell y Norvig, caps. 3-4; Poole y Mackworth). Código base ampliado de la nota principal [[Introducción a la Inteligencia Artificial]]. Verificar el temario con el programa oficial.
