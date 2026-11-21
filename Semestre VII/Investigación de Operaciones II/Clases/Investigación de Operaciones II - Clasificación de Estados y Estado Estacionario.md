---
tags: [clase, semestre-VII]
materia: Investigación de Operaciones II
---
# Investigación de Operaciones II - Clasificación de Estados y Estado Estacionario

Materia: [[Investigación de Operaciones II]]  
Anterior: [[Investigación de Operaciones II - Cadenas de Markov y Matriz de Transición]]  
Siguiente: [[Investigación de Operaciones II - Cadenas Absorbentes y Tiempos de Primera Pasada]]

## Contexto y objetivo

Realizar la **clasificación topológica de estados y cadenas** (accesibilidad, comunicación, recurrencia/transitoriedad, periodicidad, ergodicidad) y calcular la **distribución de estado estacionario $\boldsymbol{\pi}$** a largo plazo.

## 1. Clasificación de estados

- **Accesible ($i \to j$)**: el estado $j$ es accesible desde $i$ si existe $n \ge 0$ tal que $p_{ij}^{(n)} > 0$.
- **Comunicantes ($i \leftrightarrow j$)**: si $i \to j$ y $j \to i$. La comunicación es una relación de equivalencia que particiona $S$ en **clases comunicantes**.
- **Cadena irreducible**: posee una única clase comunicante (todos los estados se comunican entre sí).
- **Estado recurrente vs. transitorio**:
  - Un estado es **transitorio** si existe probabilidad positiva de no regresar nunca a él (por ejemplo, puede escapar hacia una clase cerrada).
  - Un estado es **recurrente** si, partiendo de él, regresará con probabilidad $1$. En cadenas finitas, toda clase cerrada (sin salidas hacia otras clases) es recurrente.
- **Estado absorbente**: estado $i$ tal que $p_{ii} = 1$.
- **Periodicidad**: el período de un estado $i$ es $d(i) = \text{mcd}\{n \ge 1 : p_{ii}^{(n)} > 0\}$. Si $d(i) = 1$, el estado es **aperiódico** (basta con que $p_{ii} > 0$). Si $d(i) > 1$, es **periódico** (cíclico).

## 2. Clasificación de cadenas (según programa)

- **Cadena ergódica**: cadena **irreducible**, **aperiódica** y con estados recurrentes positivos (en espacio finito, basta irreducible y aperiódica). Su distribución converge a un límite único independiente del estado inicial $\boldsymbol{\pi}(0)$.
- **Cadena cíclica**: irreducible pero periódica ($d > 1$).
- **Cadena no ergódica / semiergódica**: presenta múltiples clases o estados transitorios que impiden la convergencia única desde cualquier estado inicial.

## 3. Comportamiento estacionario ($\boldsymbol{\pi}$)

En una cadena ergódica, cuando $n \to \infty$, todas las filas de $\mathbf{P}^n$ convergen al mismo vector $\boldsymbol{\pi} = (\pi_1, \dots, \pi_m)$, llamado **distribución estacionaria** o de estado estable, que satisface el sistema lineal:

$$\boldsymbol{\pi}\mathbf{P} = \boldsymbol{\pi}, \qquad \sum_{i=1}^{m} \pi_i = 1$$

Como las ecuaciones de $\boldsymbol{\pi}\mathbf{P} = \boldsymbol{\pi}$ son linealmente dependientes (una es redundante), se sustituye **cualquiera** de ellas por la ecuación de normalización $\sum \pi_i = 1$.

### Ejemplo resuelto (del programa)
$$\mathbf{P} = \begin{pmatrix} 0.7 & 0.3 \\ 0.4 & 0.6 \end{pmatrix}$$
Planteamos $\boldsymbol{\pi}\mathbf{P} = \boldsymbol{\pi}$:
$$0.7\pi_1 + 0.4\pi_2 = \pi_1 \implies 0.4\pi_2 = 0.3\pi_1 \implies \pi_2 = \frac{3}{4}\pi_1$$
Usando $\pi_1 + \pi_2 = 1$:
$$\pi_1 + \frac{3}{4}\pi_1 = 1 \implies \frac{7}{4}\pi_1 = 1 \implies \pi_1 = \frac{4}{7} \approx 0.571, \quad \pi_2 = \frac{3}{7} \approx 0.429$$

## Errores comunes

- Intentar resolver las $m$ ecuaciones de $\boldsymbol{\pi}\mathbf{P} = \boldsymbol{\pi}$ sin reemplazar una por $\sum \pi_i = 1$ (el sistema homogéneo tiene infinitas soluciones).
- Asumir que existe un único estado estacionario en una cadena con dos clases cerradas absorbentes (en ese caso el límite depende de $\boldsymbol{\pi}(0)$).

## Ejercicios propuestos

1. Para la cadena del clima $\mathbf{P} = \begin{pmatrix} 0.8 & 0.2 \\ 0.4 & 0.6 \end{pmatrix}$, halla la proporción de días soleados y lluviosos a largo plazo.
   - *Respuesta:* $0.8\pi_1 + 0.4\pi_2 = \pi_1 \implies 0.2\pi_1 = 0.4\pi_2 \implies \pi_1 = 2\pi_2$. Con $\pi_1 + \pi_2 = 1$: $\pi_1 = 2/3$, $\pi_2 = 1/3$.

## Conexiones

- Anterior: [[Investigación de Operaciones II - Cadenas de Markov y Matriz de Transición]]
- Siguiente: [[Investigación de Operaciones II - Cadenas Absorbentes y Tiempos de Primera Pasada]]
- Nota resumen: [[Investigación de Operaciones II - Cadenas de Markov y Matriz de Transición]]
- Materia: [[Investigación de Operaciones II]]
- Materias relacionadas: [[Matemática IV]], [[Estadística II]]

## Fuente

- `Material/ProgramaInvOperacionesII.doc` (Unidad I) y Taha (Cap. 17).
