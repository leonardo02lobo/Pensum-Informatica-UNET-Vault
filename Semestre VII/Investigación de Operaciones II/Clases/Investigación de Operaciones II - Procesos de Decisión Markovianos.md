---
tags: [clase, semestre-VII]
materia: Investigación de Operaciones II
---
# Investigación de Operaciones II - Procesos de Decisión Markovianos

Materia: [[Investigación de Operaciones II]]  
Anterior: [[Investigación de Operaciones II - Cadenas Absorbentes y Tiempos de Primera Pasada]]  
Siguiente: [[Investigación de Operaciones II - Teoría de Colas y Modelos MM1 y MMc]]

## Contexto y objetivo

Formular y resolver **Procesos de Decisión Markovianos (MDP)** sin descuento en horizonte infinito (según el programa de IO II): definir estados, decisiones, costos/beneficios esperados y hallar la **política óptima** mediante **enumeración exhaustiva** o **iteración de políticas**.

## 1. Componentes de un Proceso de Decisión Markoviano

Un MDP extiende las cadenas de Markov permitiendo que en cada estado $i \in S$ el tomador de decisiones elija una **acción $k \in K_i$**:
1. **Matriz de transición dependiente de la acción**: $p_{ij}(k)$ es la probabilidad de pasar de $i$ a $j$ si se toma la decisión $k$.
2. **Costo (o recompensa) esperado inmediato**: $C_i(k)$ (o $R_i(k)$) al estar en el estado $i$ y elegir $k$.
3. **Política estacionaria ($R$)**: una regla que asigna una decisión fija $d_i$ a cada estado $i$: $R = (d_1, d_2, \dots, d_m)$.

Cada política $R$ induce una cadena de Markov estándar con matriz $\mathbf{P}^R$ y vector de costos $\mathbf{C}^R$.

## 2. Evaluación de políticas: Enumeración exhaustiva

Cuando el número de estados y decisiones es pequeño, se listan todas las políticas posibles $R$:
1. Para cada política $R$, calcular su distribución estacionaria $\boldsymbol{\pi}^R$ resolviendo $\boldsymbol{\pi}^R \mathbf{P}^R = \boldsymbol{\pi}^R$ y $\sum \pi_i^R = 1$.
2. Calcular el **costo esperado por período a largo plazo** $g(R)$:
   $$g(R) = \sum_{i \in S} \pi_i^R \, C_i(d_i)$$
3. Seleccionar la política que minimiza $g(R)$ (o maximiza el beneficio esperado).

## 3. Algoritmo de Iteración de Políticas (Howard)

Para problemas más grandes, evita enumerar todas las combinaciones:

1. **Inicialización**: elegir una política inicial arbitraria $R_0$.
2. **Determinación del valor (Evaluación)**: resolver el sistema lineal de $m$ ecuaciones (fijando arbitrariamente $v_m = 0$) para hallar la ganancia $g$ y los valores relativos $v_i$:
   $$g + v_i = C_i(d_i) + \sum_{j=1}^m p_{ij}(d_i)\,v_j, \quad i = 1, \dots, m$$
3. **Mejoramiento de la política**: para cada estado $i$, buscar la acción $k \in K_i$ que minimice:
   $$C_i(k) + \sum_{j=1}^m p_{ij}(k)\,v_j$$
   Formar la nueva política $R_{\text{nueva}}$. Si $R_{\text{nueva}} = R_{\text{actual}}$, **detener: es óptima**. De lo contrario, volver al paso 2.

## 4. Ejemplo conceptual (Mantenimiento de máquina)

Una máquina tiene dos estados: $1 = \text{Buena}$, $2 = \text{Averiada}$.
- En estado $1$ solo hay una acción ($k=1$: operar): $C_1(1) = 0$, $p_{11}=0.7, p_{12}=0.3$.
- En estado $2$ hay dos acciones:
  - $k=1$ (reparación menor): $C_2(1) = 400$, $p_{21}=0.5, p_{22}=0.5$.
  - $k=2$ (reemplazo/overhaul): $C_2(2) = 600$, $p_{21}=1.0, p_{22}=0.0$.

**Política A** ($d_2 = 1$): $\mathbf{P}^A = \begin{pmatrix} 0.7 & 0.3 \\ 0.5 & 0.5 \end{pmatrix} \implies \pi_1 = 5/8, \pi_2 = 3/8$.
Costo esperado: $g(A) = \frac{5}{8}(0) + \frac{3}{8}(400) = 150$.

**Política B** ($d_2 = 2$): $\mathbf{P}^B = \begin{pmatrix} 0.7 & 0.3 \\ 1.0 & 0.0 \end{pmatrix} \implies \pi_1 = 10/13, \pi_2 = 3/13$.
Costo esperado: $g(B) = \frac{10}{13}(0) + \frac{3}{13}(600) \approx 138.46$.

La **Política B** (hacer reemplazo al averiarse) resulta más económica a largo plazo ($138.46 < 150$).

## Errores comunes

- Olvidar fijar un $v_m = 0$ en el paso de evaluación de la iteración de políticas (el sistema tendría $m$ ecuaciones y $m+1$ incógnitas: $g, v_1, \dots, v_m$).
- Confundir maximización de ingresos con minimización de costos en el paso de mejoramiento.

## Ejercicios propuestos

1. En el ejemplo anterior, si el costo de reemplazo $C_2(2)$ sube a $700$, ¿qué política conviene?
   - *Respuesta:* $g(B) = \frac{3}{13}(700) \approx 161.54 > 150 = g(A)$. Ahora conviene la **Política A** (reparación menor).

## Conexiones

- Anterior: [[Investigación de Operaciones II - Cadenas Absorbentes y Tiempos de Primera Pasada]]
- Siguiente: [[Investigación de Operaciones II - Teoría de Colas y Modelos MM1 y MMc]]
- Nota resumen: [[Investigación de Operaciones II - Cadenas de Markov y Matriz de Transición]]
- Materia: [[Investigación de Operaciones II]]
- Materias relacionadas: [[Investigación de Operaciones I]], [[Ingeniería Económica]]

## Fuente

- `Material/ProgramaInvOperacionesII.doc` (Unidad I: procesos markovianos de decisión) y Howard, R. *Dynamic Probabilistic Systems*; Taha (Cap. 19).
