---
tags: [clase, electiva]
materia: Introducción a la Inteligencia Artificial
fuente: "conocimiento general"
---
# IIA 04 - Juegos, minimax y poda alfa-beta

Materia: [[Introducción a la Inteligencia Artificial]]
Anterior: [[IIA 03 - Búsqueda local y algoritmos genéticos]]
Siguiente: [[IIA 05 - Lógica proposicional, primer orden y Prolog]]

## Contexto y objetivo
En entornos multiagente competitivos, la mejor acción depende de la respuesta del adversario. Los juegos de dos jugadores, por turnos, deterministas, de suma cero e información perfecta (ajedrez, damas, tres en raya) se resuelven con búsqueda adversaria. Objetivo: aplicar minimax y poda alfa-beta, y entender funciones de evaluación y límites de profundidad.

## Formulación
Un juego se define por: estado inicial, jugador a mover, acciones, modelo de transición, prueba de terminal y **utilidad** (valor final, p. ej. +1 gana MAX, 0 empate, -1 gana MIN). MAX intenta maximizar la utilidad; MIN, minimizarla.

## Minimax
Valor de un nodo bajo juego óptimo de ambos:

$$\text{MINIMAX}(s)=\begin{cases}\text{UTILIDAD}(s)&s\text{ terminal}\\\max_a\text{MINIMAX}(\text{RESULT}(s,a))&\text{turno de MAX}\\\min_a\text{MINIMAX}(\text{RESULT}(s,a))&\text{turno de MIN}\end{cases}$$

Es una búsqueda en profundidad: completa en árboles finitos, óptima contra un adversario óptimo, tiempo $O(b^m)$, espacio $O(bm)$. Para el ajedrez ($b\approx35$, $m\approx80$) es inviable completo.

## Poda alfa-beta
Mantiene $\alpha$ (mejor valor garantizado para MAX en el camino) y $\beta$ (mejor para MIN). Se poda una rama cuando $\alpha\ge\beta$, porque el adversario no permitirá llegar a ella. No cambia el resultado del minimax. Con ordenamiento ideal de movimientos el costo baja a $O(b^{m/2})$, duplicando la profundidad alcanzable; en promedio, $O(b^{3m/4})$.

## Límites prácticos
- **Profundidad limitada** y función de evaluación heurística $\text{EVAL}(s)$ en el límite (p. ej. material en ajedrez: peón 1, caballo/alfil 3, torre 5, dama 9, más posición). Típicamente combinación lineal $\sum w_if_i(s)$.
- **Profundización iterativa** con límite de tiempo y ordenamiento por la iteración previa.
- **Tablas de transposición** (memorizar posiciones repetidas), libros de aperturas, poda hacia adelante.
- Juegos con azar: nodos de expectativa (expectiminimax). Juegos complejos (Go): búsqueda en árbol de Monte Carlo (MCTS), combinada con redes neuronales (AlphaGo).

## Ejemplo resuelto
Árbol de dos niveles: la raíz es MAX con tres hijos (MIN) cuyas hojas son: A: (3, 12, 8); B: (2, 4, 6); C: (14, 5, 2).

Minimax:
1. A (MIN): $\min(3,12,8)=3$.
2. B: $\min(2,4,6)=2$.
3. C: $\min(14,5,2)=2$.
4. Raíz: $\max(3,2,2)=3$. MAX elige A.

Con alfa-beta (inicio $\alpha=-\infty,\beta=+\infty$):
1. A: tras ver 3, 12, 8 el valor es 3; en la raíz $\alpha=3$.
2. B: se ve la primera hoja 2. MIN ya garantiza $\le2<\alpha=3$, así que se **podan** las hojas 4 y 6.
3. C: hoja 14 ($\beta$ pasa a 14, sin poda), luego 5, luego 2: valor 2 $<3$. Sin poda adicional aquí.
4. Resultado idéntico (3), con 2 hojas menos evaluadas.

## Código
```python
import math

def minimax(estado, profundidad, es_max, hijos, eval_fn, alfa=-math.inf, beta=math.inf):
    """Minimax con poda alfa-beta. 'hijos(estado)' lista sucesores."""
    sucesores = hijos(estado)
    if profundidad == 0 or not sucesores:
        return eval_fn(estado), None
    mejor_mov = None
    if es_max:
        valor = -math.inf
        for s in sucesores:
            v, _ = minimax(s, profundidad - 1, False, hijos, eval_fn, alfa, beta)
            if v > valor:
                valor, mejor_mov = v, s
            alfa = max(alfa, valor)
            if alfa >= beta:           # poda beta
                break
    else:
        valor = math.inf
        for s in sucesores:
            v, _ = minimax(s, profundidad - 1, True, hijos, eval_fn, alfa, beta)
            if v < valor:
                valor, mejor_mov = v, s
            beta = min(beta, valor)
            if alfa >= beta:           # poda alfa
                break
    return valor, mejor_mov

# Tres en raya: tablero como tupla de 9 elementos 'X', 'O' o ' '
LINEAS = [(0,1,2),(3,4,5),(6,7,8),(0,3,6),(1,4,7),(2,5,8),(0,4,8),(2,4,6)]
def ganador(t):
    for a, b, c in LINEAS:
        if t[a] != ' ' and t[a] == t[b] == t[c]:
            return t[a]

def jugar(t, turno):
    return [t[:i] + (turno,) + t[i+1:] for i in range(9) if t[i] == ' ']

# MAX = 'X'. Estado = (tablero, turno)
def hijos(e):
    t, turno = e
    if ganador(t):
        return []
    return [(h, 'O' if turno == 'X' else 'X') for h in jugar(t, turno)]

def evaluar(e):
    g = ganador(e[0])
    return 1 if g == 'X' else -1 if g == 'O' else 0

ini = ((' ',) * 9, 'X')
print(minimax(ini, 9, True, hijos, evaluar)[0])    # 0: empate con juego óptimo
```

## Errores comunes
- Olvidar alternar MAX y MIN o los signos de la evaluación.
- Actualizar $\alpha$ o $\beta$ en el nivel equivocado.
- Esperar que alfa-beta cambie el resultado (solo ahorra cálculo).
- Función de evaluación no monótona respecto a la utilidad real, o evaluar en posiciones inestables (efecto horizonte).
- Suponer que minimax es óptimo contra jugadores no óptimos (solo garantiza lo peor).

## Ejercicios propuestos
1. Con $b=10$, $m=6$ y ordenamiento perfecto, ¿aproximadamente cuántas hojas evalúa alfa-beta? *Respuesta: del orden de $10^{3}$ (en lugar de $10^{6}$).*
2. Valor minimax de MAX con hijos MIN de hojas $(4,6)$ y $(5,9)$. *Respuesta: $\max(4,5)=5$.*
3. ¿Qué es el efecto horizonte? *Respuesta: retrasar una pérdida inevitable más allá del límite de profundidad, evaluando mal posiciones inestables.*

## Conexiones
- Recursión y árboles: [[Estructura de Datos]] y [[Matemática Discreta]].
- Teoría de decisión y utilidad esperada: [[Estadística I]].
- Aprendizaje de funciones de evaluación: [[AA 01 - Fundamentos del aprendizaje automático]].

## Fuente
Conocimiento general (Russell y Norvig, cap. 5; Knuth y Moore 1975). Verificar el temario con el programa oficial.
