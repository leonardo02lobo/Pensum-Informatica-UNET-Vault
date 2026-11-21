---
tags: [clase, electiva]
materia: Introducción a la Inteligencia Artificial
fuente: "conocimiento general"
---
# IIA 03 - Búsqueda local y algoritmos genéticos

Materia: [[Introducción a la Inteligencia Artificial]]
Anterior: [[IIA 02 - Búsqueda no informada e informada]]
Siguiente: [[IIA 04 - Juegos, minimax y poda alfa-beta]]

## Contexto y objetivo
En muchos problemas (n-reinas, horarios, rutas del viajante, diseño) no importa el camino sino el estado final, y el espacio es enorme. La búsqueda local mantiene uno o pocos estados y los mejora iterativamente, usando memoria constante. Objetivo: implementar ascenso de colinas, recocido simulado y un algoritmo genético, y entender sus trampas.

## Paisaje de búsqueda
Cada estado tiene un valor $f(s)$ (objetivo a maximizar, o costo a minimizar) y un vecindario. Estructuras problemáticas: **máximos locales**, **mesetas** (planicies) y **crestas**. El óptimo global puede quedar oculto.

## Ascenso de colinas (hill climbing)
Mover siempre al mejor vecino; parar si ninguno mejora. Variantes: estocástico (elegir entre los que mejoran), primera elección, **reinicio aleatorio** (reiniciar desde estados aleatorios; si la probabilidad de éxito por intento es $p$, se esperan $1/p$ intentos). Rápido pero se atasca.

## Recocido simulado (simulated annealing)
Permite movimientos de empeoramiento con probabilidad decreciente. Para minimizar el costo $E$, un vecino con $\Delta E=E'-E>0$ se acepta con probabilidad

$$P=e^{-\Delta E/T},$$

y la temperatura $T$ desciende según un calendario (p. ej. $T\leftarrow\alpha T$, $\alpha\in[0{,}9;0{,}999]$). Con $T$ alta se explora; con $T$ baja se explota. Con enfriamiento suficientemente lento converge al óptimo global (en teoría).

## Otros métodos
- **Búsqueda tabú:** lista de movimientos prohibidos recientes para escapar de ciclos.
- **Búsqueda de haz local ($k$ estados):** conserva los $k$ mejores sucesores de todos los estados.
- Optimización con enjambres (PSO) y colonias de hormigas.

## Algoritmos genéticos (AG)
Población de individuos codificados (cadenas de bits, permutaciones, reales). Ciclo: evaluar la aptitud, **seleccionar** (ruleta, torneo), **cruzar** (un punto, uniforme; para permutaciones, cruce de orden) y **mutar** (con probabilidad pequeña), con **elitismo**. El balance entre exploración (mutación, población grande) y explotación (presión de selección) decide el éxito. Se aplican en horarios, diseño, ajuste de parámetros (véase también [[RNLD 07 - Sistemas neuro-difusos y algoritmos genéticos]]).

## Ejemplo resuelto: 4 reinas con ascenso de colinas
Estado: columna $i$ tiene una reina en la fila $s_i$. Costo $h$ = pares de reinas que se atacan. Estado $(1,1,2,2)$ (filas por columna).
1. Pares que se atacan: columnas 1-2 (misma fila 1): sí; 3-4 (fila 2): sí; 2-3 (filas 1 y 2, diagonal adyacente): sí; 1-4 (filas 1 y 2, distancia de columna 3): no; 1-3 (filas 1 y 2, columnas distan 2): no; 2-4 (filas 1 y 2, distan 2): no. Costo $h=3$.
2. Se evalúan los 12 vecinos (mover cada reina en su columna) y se elige el de menor $h$. Por ejemplo, mover la reina de la columna 2 a la fila 3 da $(1,3,2,2)$: ataques 3-4 (misma fila) y 2-3 (filas 3 y 2, adyacentes): $h=2$.
3. Se repite hasta $h=0$ o hasta quedar sin mejora (máximo local). Una solución es $(2,4,1,3)$ con $h=0$.

Cálculo de aceptación en recocido: $\Delta E=2$, $T=1$: $P=e^{-2}=0{,}135$; con $T=0{,}2$: $P=e^{-10}=4{,}5\times10^{-5}$.

## Código
```python
import math, random

def conflictos(s):
    n = len(s)
    return sum(1 for i in range(n) for j in range(i + 1, n)
               if s[i] == s[j] or abs(s[i] - s[j]) == j - i)

def vecino(s):
    t = s[:]
    t[random.randrange(len(s))] = random.randrange(len(s))
    return t

def ascenso(n, iters=2000):
    s = [random.randrange(n) for _ in range(n)]
    for _ in range(iters):
        v = vecino(s)
        if conflictos(v) <= conflictos(s):    # acepta iguales para cruzar mesetas
            s = v
    return s

def recocido(n, T=2.0, alfa=0.995, iters=20000):
    s = [random.randrange(n) for _ in range(n)]
    for _ in range(iters):
        v = vecino(s)
        d = conflictos(v) - conflictos(s)
        if d <= 0 or random.random() < math.exp(-d / T):
            s = v
        T = max(T * alfa, 1e-3)               # enfriamiento
        if conflictos(s) == 0:
            break
    return s

random.seed(0)
for f in (ascenso, recocido):
    s = f(8)
    print(f.__name__, s, "conflictos:", conflictos(s))

# AG para 8 reinas
def ag(n=8, N=100, G=300):
    pob = [[random.randrange(n) for _ in range(n)] for _ in range(N)]
    for _ in range(G):
        pob.sort(key=conflictos)
        if conflictos(pob[0]) == 0:
            return pob[0]
        nueva = pob[:5]                       # elitismo
        while len(nueva) < N:
            a, b = (min(random.sample(pob, 3), key=conflictos) for _ in range(2))
            c = random.randrange(1, n)
            hijo = a[:c] + b[c:]              # cruce de un punto
            if random.random() < 0.2:
                hijo[random.randrange(n)] = random.randrange(n)  # mutación
            nueva.append(hijo)
        pob = nueva
    return pob[0]
print("AG", ag())
```

## Errores comunes
- Pensar que el ascenso de colinas encuentra el óptimo global.
- Enfriar demasiado rápido en recocido (equivale a ascenso).
- Mutación nula o población pequeña en AG: convergencia prematura.
- Codificar permutaciones y usar cruce de un punto (genera duplicados).
- No fijar semilla ni repetir ejecuciones: evaluar un método con una sola corrida.

## Ejercicios propuestos
1. ¿Cuál es la probabilidad de aceptar un empeoramiento de $\Delta E=1$ con $T=0{,}5$? *Respuesta: $e^{-2}\approx0{,}135$.*
2. Si cada reinicio del ascenso de colinas tiene $p=0{,}14$ de éxito, ¿cuántos reinicios se esperan? *Respuesta: $1/0{,}14\approx7$.*
3. ¿Por qué el elitismo es útil? *Respuesta: asegura que la mejor aptitud no decrezca entre generaciones.*

## Conexiones
- Optimización combinatoria y metaheurísticas: [[Investigación de Operaciones II]].
- Representaciones y cálculo de costos: [[Estructura de Datos]].
- Optimización neuro-difusa: [[RNLD 07 - Sistemas neuro-difusos y algoritmos genéticos]].

## Fuente
Conocimiento general (Russell y Norvig, cap. 4; Kirkpatrick et al. 1983; Holland 1975). Verificar el temario con el programa oficial.
