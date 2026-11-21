---
tags: [clase, semestre-VI]
materia: Investigación de Operaciones I
---
# Investigación de Operaciones I - Modelos de Transporte, Asignación y Transbordo

Materia: [[Investigación de Operaciones I]]  
Anterior: [[Investigación de Operaciones I - Dualidad y Análisis de Sensibilidad]]  
Siguiente: —

## Contexto y objetivo

Resolver modelos especiales de redes de flujo de costo mínimo: **transporte** (solución básica inicial y optimización MODI), **asignación** (método húngaro) y **transbordo** (con nodos intermedios, aplicando el ejercicio del Material).

## 1. Modelo de Transporte

Consiste en enviar un bien homogéneo desde $m$ orígenes (con ofertas $a_i$) hacia $n$ destinos (con demandas $b_j$) minimizando el costo total de envío $\sum_i \sum_j c_{ij} x_{ij}$.

- **Condición de equilibrio**: $\sum_{i=1}^m a_i = \sum_{j=1}^n b_j$. Si no está equilibrado, se agrega un origen o destino **ficticio** con costo $0$.
- Una solución básica tiene exactamente $m + n - 1$ celdas básicas (asignaciones independientes).

### Métodos para hallar la solución básica inicial
1. **Esquina Noroeste**: asigna lo máximo posible empezando en la celda $(1,1)$ y avanzando hacia la derecha o abajo. Rápido, pero ignora los costos.
2. **Costo Mínimo**: asigna primero a la celda de menor costo $c_{ij}$ disponible.
3. **Aproximación de Vogel (VAM)**: calcula la **penalización** de cada fila y columna (diferencia entre los dos menores costos), elige la fila/columna con mayor penalización y asigna a su celda más barata. Suele dar una solución muy cercana al óptimo.

### Optimización: Método MODI (Multiplicadores $u_i, v_j$)
1. Para cada celda básica $(i,j)$, resolver $u_i + v_j = c_{ij}$ fijando $u_1 = 0$.
2. Para cada celda *no básica*, calcular el costo reducido $\Delta_{ij} = c_{ij} - u_i - v_j$.
3. Si todos $\Delta_{ij} \ge 0$, la solución es **óptima**. Si hay $\Delta_{ij} < 0$, entra la celda más negativa formando un **circuito cerrado (Stepping-Stone)** alternando signos $+, -, +, -$ y se reasigna el mínimo valor de las celdas con signo $-$.

## 2. Modelo de Asignación (Método Húngaro)

Caso particular del transporte donde $m = n$, todas las ofertas y demandas valen $1$, y $x_{ij} \in \{0, 1\}$.

**Algoritmo Húngaro (minimización):**
1. Restar el mínimo de cada fila a todos los elementos de esa fila.
2. Restar el mínimo de cada columna a todos los elementos de esa columna.
3. Cubrir todos los ceros con el **mínimo número de líneas** (horizontales o verticales). Si el número de líneas $= n$, ya existe una asignación óptima en los ceros.
4. Si líneas $< n$, hallar el menor elemento $k$ no cubierto: restar $k$ a los no cubiertos, sumar $k$ a las intersecciones de dos líneas y volver al paso 3.

## 3. Modelo de Transbordo (Ejercicio del Material)

En un problema de **transbordo**, la mercancía puede pasar por nodos intermedios con oferta/demanda neta igual a $0$. Ver también [[Problema de transbordo - Investigación de Operaciones]].

**Enunciado del Material:**
- Plantas: $A$ (oferta $100$), $B$ (oferta $150$). Total $= 250$.
- Centros de transbordo: $X, Y$ (oferta/demanda neta $0$).
- Supermercados: $SM_1 (80)$, $SM_2 (90)$, $SM_3 (80)$. Total $= 250$.

**Truco del buffer para tabla de transporte:**
Se suma un *buffer* $B = 250$ (el flujo total) a los nodos de transbordo (que actúan como orígenes y destinos a la vez):
- Ofertas: $A=100, B=150, X=250, Y=250$.
- Demandas: $X=250, Y=250, SM_1=80, SM_2=90, SM_3=80$.
- Costos en diagonal $X \to X$ y $Y \to Y$ iguales a $0$ (unidades del buffer que *no* pasan por el nodo); rutas imposibles con costo $M$.

## Errores comunes

- Tener menos de $m + n - 1$ celdas básicas por **degeneración** (cuando una asignación satisface fila y columna simultáneamente): debe colocarse un $\varepsilon = 0$ en una celda independiente para poder calcular todos los $u_i, v_j$ en MODI.
- Olvidar equilibrar la tabla de transporte con una fila o columna ficticia antes de aplicar Vogel o MODI.

## Ejercicios propuestos

1. En el ejercicio de transbordo del Material ($A\to X:4, A\to Y:6, B\to X:5, B\to Y:3$; $X\to SM_1:3, X\to SM_2:4, X\to SM_3:2$; $Y\to SM_1:6, Y\to SM_2:3, Y\to SM_3:5$), halla el envío óptimo intuitivo o por tabla.
   - *Respuesta:* $A$ envía $100$ a $X$ (costo 400); $B$ envía $60$ a $X$ (300) y $90$ a $Y$ (270). Luego $X$ envía $80$ a $SM_1$ (240) y $80$ a $SM_3$ (160); $Y$ envía $90$ a $SM_2$ (270). Costo total mínimo $= 1640$.

## Conexiones

- Anterior: [[Investigación de Operaciones I - Dualidad y Análisis de Sensibilidad]]
- Nota relacionada: [[Problema de transbordo - Investigación de Operaciones]]
- Materia: [[Investigación de Operaciones I]]
- Materias relacionadas: [[Estructuras Discretas]], [[Investigación de Operaciones II]], [[Simulación de Sistemas]]

## Fuente

- `Material/transbordo ejercicio.pdf` y `Material/transbordo ejercicio.docx`.
- Programa de [[Investigación de Operaciones I]] (Taha, Cap. 5).
