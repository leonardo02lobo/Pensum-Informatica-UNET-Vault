---
tags: [electiva]
---
# Introducción a la Inteligencia Artificial

Opción de [[Electivas]].

## Descripción
Panorama de la inteligencia artificial clásica: agentes, búsqueda, representación del conocimiento, razonamiento y aprendizaje. Objetivo: comprender los paradigmas y programar soluciones básicas.

## Temario típico (verificar con el programa oficial)
1. Historia, agentes racionales y entornos.
2. Búsqueda no informada (BFS, DFS) e informada (A*, voraz), búsqueda local, algoritmos genéticos.
3. Juegos: minimax y poda alfa-beta.
4. Lógica proposicional y de primer orden, sistemas basados en reglas y Prolog.
5. Razonamiento con incertidumbre: probabilidad, redes bayesianas.
6. Introducción al aprendizaje automático, procesamiento de lenguaje natural y visión.
7. Ética e impacto de la IA.

## Algoritmo y código
A* usa `f(n) = g(n) + h(n)`; es óptimo si `h` es admisible.

```python
import heapq
def a_estrella(grafo, ini, meta, h):
    abierta = [(h(ini), 0, ini, [ini])]; visto = set()
    while abierta:
        f, g, n, ruta = heapq.heappop(abierta)
        if n == meta: return ruta
        if n in visto: continue
        visto.add(n)
        for v, c in grafo[n]:
            heapq.heappush(abierta, (g+c+h(v), g+c, v, ruta+[v]))
```

## Relación con el pensum
[[Estructura de Datos]] (grafos, colas de prioridad), [[Matemática Discreta]] (lógica), [[Estadística I]], [[Programación II]]. Siguientes: [[Aprendizaje Automático]], [[Redes Neuronales y Lógica Difusa]].

## Recursos y bibliografía
- Russell y Norvig. *Inteligencia Artificial: un enfoque moderno*.
- Poole y Mackworth. *Artificial Intelligence: Foundations of Computational Agents* (gratuito).
- Curso CS50 AI de Harvard; SWI-Prolog.
