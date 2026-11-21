---
tags: [clase, semestre-VII]
materia: Investigación de Operaciones II
---
# Investigación de Operaciones II - Cadenas de Markov y Matriz de Transición

Materia: [[Investigación de Operaciones II]]  
Anterior: —  
Siguiente: [[Investigación de Operaciones II - Clasificación de Estados y Estado Estacionario]]

## Contexto y objetivo

Iniciar la **Unidad I (Cadenas de Markov)** del programa sinóptico (código 0425701T): definir un proceso estocástico discreto, enunciar la **propiedad markoviana**, construir la **matriz de transición $P$** y calcular distribuciones de probabilidad en $n$ pasos mediante las ecuaciones de Chapman-Kolmogorov.

## 1. Proceso estocástico y propiedad de Markov

Un **proceso estocástico** $\{X_n, n = 0, 1, 2, \dots\}$ es una familia de variables aleatorias indexadas por el tiempo que toman valores en un espacio de estados finito o numerable $S = \{1, 2, \dots, m\}$.

El proceso es una **Cadena de Markov de primer orden** (homogénea en el tiempo) si la probabilidad del estado futuro depende únicamente del estado presente y no de la historia pasada:
$$P(X_{n+1} = j \mid X_n = i, X_{n-1} = i_{n-1}, \dots, X_0 = i_0) = P(X_{n+1} = j \mid X_n = i) = p_{ij}$$

## 2. Matriz de transición $P$ y vector inicial $\pi(0)$

Las probabilidades de transición en un paso se organizan en una **matriz estocástica** $\mathbf{P} = [p_{ij}]$ de tamaño $m \times m$:
- $0 \le p_{ij} \le 1$ para todo $i, j \in S$.
- Cada fila suma exactamente $1$: $\sum_{j \in S} p_{ij} = 1$.

El estado inicial se representa mediante el vector fila $\boldsymbol{\pi}(0) = (\pi_1(0), \dots, \pi_m(0))$ con $\sum_i \pi_i(0) = 1$.

## 3. Probabilidades en $n$ pasos (Chapman-Kolmogorov)

La probabilidad de pasar del estado $i$ al estado $j$ en exactamente $n$ pasos se denota $p_{ij}^{(n)} = P(X_n = j \mid X_0 = i)$ y corresponde al elemento $(i,j)$ de la potencia matricial $\mathbf{P}^n$:

$$\mathbf{P}^{(n)} = \mathbf{P}^n$$
$$\boldsymbol{\pi}(n) = \boldsymbol{\pi}(0)\,\mathbf{P}^n$$

### Ejemplo trabajado (Clima)
Supongamos dos estados: $1 = \text{Soleado}$, $2 = \text{Lluvioso}$, con matriz de transición diaria:
$$\mathbf{P} = \begin{pmatrix} 0.8 & 0.2 \\ 0.4 & 0.6 \end{pmatrix}$$
Si hoy está soleado, $\boldsymbol{\pi}(0) = (1, 0)$. Para dentro de 2 días:
$$\mathbf{P}^2 = \begin{pmatrix} 0.8 & 0.2 \\ 0.4 & 0.6 \end{pmatrix}\begin{pmatrix} 0.8 & 0.2 \\ 0.4 & 0.6 \end{pmatrix} = \begin{pmatrix} 0.72 & 0.28 \\ 0.56 & 0.44 \end{pmatrix}$$
$$\boldsymbol{\pi}(2) = (1, 0)\mathbf{P}^2 = (0.72, 0.28)$$
La probabilidad de que llueva pasado mañana dado que hoy está soleado es $0.28$.

## 4. Cadenas de orden superior (mención del programa)

Si el estado futuro depende de los últimos $k$ períodos ($X_n, X_{n-1}$ para $k=2$), puede reducirse a una cadena de primer orden ampliando el espacio de estados a pares $(X_{n-1}, X_n)$.

## Errores comunes

- Transponer la matriz $\mathbf{P}$ y multiplicar $\mathbf{P}^n \boldsymbol{\pi}(0)^T$ con columnas sumando 1 en lugar de filas sumando 1 (verificar siempre si $\boldsymbol{\pi}$ es vector fila o columna).
- Olvidar que $\sum_j p_{ij} = 1$ en cada fila al plantear el grafo de transición.

## Ejercicios propuestos

1. Un servidor tiene dos estados: Activo (1) y Falla (2). Si está Activo, sigue Activo con prob. $0.9$; si está en Falla, se repara al día siguiente con prob. $0.7$. Escribe $\mathbf{P}$ y calcula la probabilidad de que esté Activo en 2 días si hoy está en Falla.
   - *Respuesta:* $\mathbf{P} = \begin{pmatrix} 0.9 & 0.1 \\ 0.7 & 0.3 \end{pmatrix}$. $\boldsymbol{\pi}(1) = (0.7, 0.3)$; $\boldsymbol{\pi}(2) = (0.7\cdot 0.9 + 0.3\cdot 0.7,\; \dots) = (0.84, 0.16)$. Probabilidad $= 0.84$.

## Conexiones

- Siguiente: [[Investigación de Operaciones II - Clasificación de Estados y Estado Estacionario]]
- Nota resumen: Cadenas de Markov Resumen IO2
- Materia: [[Investigación de Operaciones II]]
- Materias relacionadas: [[Estadística II]], [[Matemática IV]], [[Simulación de Sistemas]]

## Fuente

- `Material/ProgramaInvOperacionesII.doc` (Unidad I) y `Material/investigacic3b3n-de-operaciones-9na-edicic3b3n-hamdy-a-taha-fl.pdf` (Taha, Cap. 17).
