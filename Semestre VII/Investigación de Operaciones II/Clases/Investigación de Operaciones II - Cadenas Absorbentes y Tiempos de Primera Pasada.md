---
tags: [clase, semestre-VII]
materia: Investigación de Operaciones II
---
# Investigación de Operaciones II - Cadenas Absorbentes y Tiempos de Primera Pasada

Materia: [[Investigación de Operaciones II]]  
Anterior: [[Investigación de Operaciones II - Clasificación de Estados y Estado Estacionario]]  
Siguiente: [[Investigación de Operaciones II - Procesos de Decisión Markovianos]]

## Contexto y objetivo

Analizar **cadenas de Markov absorbentes** mediante la forma canónica y la **matriz fundamental $\mathbf{N}$** (visitas esperadas, tiempo hasta absorción y probabilidades de absorción), así como calcular **tiempos y probabilidades de primera pasada** en cadenas ergódicas.

## 1. Forma canónica de una cadena absorbente

Una cadena es **absorbente** si tiene al menos un estado absorbente ($p_{ii} = 1$) y desde todo estado no absorbente (transitorio) es posible alcanzar algún estado absorbente.

Reordenando los estados para colocar primero los $t$ estados **transitorios** y luego los $a$ estados **absorbentes**, $\mathbf{P}$ adopta la **forma canónica**:

$$\mathbf{P} = \begin{pmatrix} \mathbf{Q} & \mathbf{R} \\ \mathbf{0} & \mathbf{I} \end{pmatrix}$$

- $\mathbf{Q}$ ($t \times t$): transiciones entre estados transitorios.
- $\mathbf{R}$ ($t \times a$): transiciones desde estados transitorios hacia absorbentes.
- $\mathbf{I}$ ($a \times a$): matriz identidad (los estados absorbentes no salen).

## 2. Matriz fundamental $\mathbf{N}$, tiempos y probabilidades de absorción

La **matriz fundamental** se define como:
$$\mathbf{N} = (\mathbf{I} - \mathbf{Q})^{-1} = \mathbf{I} + \mathbf{Q} + \mathbf{Q}^2 + \dots$$

1. **Visitas esperadas**: el elemento $N_{ij}$ es el número esperado de veces que el proceso visita el estado transitorio $j$ antes de ser absorbido, partiendo del estado transitorio $i$.
2. **Tiempo esperado hasta la absorción ($\mathbf{t}$)**:
   $$\mathbf{t} = \mathbf{N} \cdot \mathbf{1}$$
   donde $\mathbf{1}$ es un vector columna de unos; $t_i$ es el número esperado de pasos hasta alcanzar cualquier estado absorbente partiendo de $i$.
3. **Probabilidades de absorción ($\mathbf{B}$)**:
   $$\mathbf{B} = \mathbf{N} \cdot \mathbf{R}$$
   donde $B_{ik}$ es la probabilidad de ser absorbido finalmente en el estado absorbente $k$ partiendo del estado transitorio $i$ (cada fila de $\mathbf{B}$ suma $1$).

### Ejemplo resuelto (Créditos bancarios / estudiantes)
Estados transitorios: $1 = \text{Al día}$, $2 = \text{Moroso}$; absorbentes: $3 = \text{Pagado}$, $4 = \text{Incobrable}$.
$$\mathbf{Q} = \begin{pmatrix} 0.5 & 0.2 \\ 0.3 & 0.4 \end{pmatrix}, \quad \mathbf{R} = \begin{pmatrix} 0.3 & 0.0 \\ 0.0 & 0.3 \end{pmatrix}$$
$$\mathbf{I} - \mathbf{Q} = \begin{pmatrix} 0.5 & -0.2 \\ -0.3 & 0.6 \end{pmatrix}, \quad \det(\mathbf{I}-\mathbf{Q}) = 0.30 - 0.06 = 0.24$$
$$\mathbf{N} = \frac{1}{0.24}\begin{pmatrix} 0.6 & 0.2 \\ 0.3 & 0.5 \end{pmatrix} = \begin{pmatrix} 2.50 & 0.833 \\ 1.25 & 2.083 \end{pmatrix}$$
- Tiempo esperado hasta absorción: $t_1 = 2.50 + 0.833 = 3.33$ períodos; $t_2 = 1.25 + 2.083 = 3.33$ períodos.
- Probabilidad de absorción:
  $$\mathbf{B} = \mathbf{N}\mathbf{R} = \begin{pmatrix} 0.75 & 0.25 \\ 0.375 & 0.625 \end{pmatrix}$$
  Un cliente que inicia *Al día* tiene $75\%$ de probabilidad de pagar totalmente y $25\%$ de resultar incobrable.

## 3. Tiempos medios de primera pasada ($\mu_{ij}$)

En una cadena ergódica, el **tiempo esperado de primera pasada** $\mu_{ij}$ es el número esperado de pasos para llegar por primera vez al estado $j$ partiendo de $i$:
$$\mu_{ij} = 1 + \sum_{k \neq j} p_{ik}\,\mu_{kj}$$
En particular, el **tiempo medio de recurrencia** (regresar a $i$ desde $i$) cumple:
$$\mu_{ii} = \frac{1}{\pi_i}$$

## Errores comunes

- No reordenar correctamente filas **y columnas** al construir $\mathbf{Q}$ y $\mathbf{R}$.
- Confundir $\mathbf{Q}^{-1}$ con $(\mathbf{I} - \mathbf{Q})^{-1}$ al calcular $\mathbf{N}$.
- Aplicar $\mu_{ii} = 1/\pi_i$ a estados transitorios (solo aplica a estados recurrentes de cadenas ergódicas).

## Ejercicios propuestos

1. Para la cadena del clima con $\boldsymbol{\pi} = (2/3, 1/3)$, ¿cuál es el tiempo medio de retorno a un día soleado? ¿Y a un día lluvioso?
   - *Respuesta:* $\mu_{11} = 1/(2/3) = 1.5$ días; $\mu_{22} = 1/(1/3) = 3$ días.

## Conexiones

- Anterior: [[Investigación de Operaciones II - Clasificación de Estados y Estado Estacionario]]
- Siguiente: [[Investigación de Operaciones II - Procesos de Decisión Markovianos]]
- Nota resumen: [[Investigación de Operaciones II - Cadenas de Markov y Matriz de Transición]]
- Materia: [[Investigación de Operaciones II]]
- Materias relacionadas: [[Matemática IV]], [[Análisis Numérico]]

## Fuente

- `Material/ProgramaInvOperacionesII.doc` (Unidad I) y Taha (Cap. 17).
