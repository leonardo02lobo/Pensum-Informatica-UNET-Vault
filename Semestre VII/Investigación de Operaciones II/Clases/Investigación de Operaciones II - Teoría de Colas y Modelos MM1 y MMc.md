---
tags: [clase, semestre-VII]
materia: Investigación de Operaciones II
---
# Investigación de Operaciones II - Teoría de Colas y Modelos MM1 y MMc

Materia: [[Investigación de Operaciones II]]  
Anterior: [[Investigación de Operaciones II - Procesos de Decisión Markovianos]]  
Siguiente: [[Investigación de Operaciones II - Teoría de Inventarios EOQ y Modelos Probabilísticos]]

## Contexto y objetivo

Desarrollar la **Unidad II (Teoría de Colas)**: describir los elementos de un sistema de líneas de espera, la **notación de Kendall**, las **fórmulas de Little**, los modelos markovianos **$M/M/1$**, **$M/M/c$** y variantes ($M/M/1/K$, $M/G/1$), y la optimización económica del número de servidores.

## 1. Elementos y notación de Kendall

Un sistema de colas se describe mediante la notación **$A/B/c/K/N/D$**:
- **$A$**: distribución de tiempos entre llegadas ($M$: Markoviana/Exponencial, $D$: Determinística, $G$: General).
- **$B$**: distribución de tiempos de servicio ($M, D, G$).
- **$c$**: número de servidores en paralelo.
- **$K$**: capacidad máxima del sistema (por defecto $\infty$).
- **$N$**: tamaño de la población fuente (por defecto $\infty$).
- **$D$**: disciplina de atención (por defecto FIFO).

**Parámetros básicos:**
- $\lambda$: tasa media de llegadas (clientes/unidad de tiempo).
- $\mu$: tasa media de servicio por servidor (clientes/unidad de tiempo).
- $\rho = \frac{\lambda}{c\mu}$: factor de utilización. **Condición de estabilidad**: $\rho < 1$ (si $\rho \ge 1$ en un sistema de capacidad infinita, la cola crece indefinidamente).

## 2. Relaciones de Little (válidas en estado estable)

Relacionan el número esperado de clientes con el tiempo esperado de permanencia:
$$L = \lambda W, \qquad L_q = \lambda W_q, \qquad W = W_q + \frac{1}{\mu}, \qquad L = L_q + \frac{\lambda}{\mu}$$

## 3. Modelos $M/M/1$ y $M/M/c$

| Medida | $M/M/1$ ($c=1$, $\rho = \lambda/\mu < 1$) | $M/M/c$ ($a = \lambda/\mu$, $\rho = a/c < 1$) |
|---|---|---|
| $P_0$ | $1 - \rho$ | $\left[\sum_{n=0}^{c-1}\frac{a^n}{n!} + \frac{a^c}{c!(1-\rho)}\right]^{-1}$ |
| $L_q$ | $\frac{\rho^2}{1-\rho}$ | $\frac{P_0\, a^c\, \rho}{c!(1-\rho)^2}$ |
| $W_q$ | $\frac{L_q}{\lambda} = \frac{\rho}{\mu - \lambda}$ | $\frac{L_q}{\lambda}$ |
| $W$ | $\frac{1}{\mu - \lambda}$ | $W_q + \frac{1}{\mu}$ |
| $L$ | $\frac{\rho}{1-\rho} = \frac{\lambda}{\mu-\lambda}$ | $L_q + a$ |

- **Fórmula de Erlang C** (probabilidad de que un cliente que llega tenga que esperar en $M/M/c$):
  $$P(W_q > 0) = \frac{a^c}{c!(1-\rho)} P_0$$

### Variantes del programa
- **$M/M/1/K$** (capacidad finita $K$): siempre es estable aunque $\lambda \ge \mu$. La tasa efectiva de llegadas es $\lambda_{\text{ef}} = \lambda(1 - P_K)$.
- **$M/G/1$** (Pollaczek-Khinchine): servicio general con media $1/\mu$ y varianza $\sigma^2$:
  $$L_q = \frac{\lambda^2\sigma^2 + \rho^2}{2(1-\rho)}$$

## 4. Ejemplo trabajado y análisis de costos

En un centro de soporte técnico llegan $\lambda = 8$ tickets/hora y un técnico atiende $\mu = 10$ tickets/hora ($M/M/1$):
- $\rho = 8/10 = 0.8 < 1$ (estable).
- $L = \frac{0.8}{1 - 0.8} = 4$ tickets en el sistema.
- $W_q = \frac{0.8}{10 - 8} = 0.4\text{ h} = 24\text{ min}$ en cola.

Para elegir el número óptimo de servidores $c$, se minimiza el **costo total por unidad de tiempo**:
$$CT(c) = c \cdot C_s + C_w \cdot L(c)$$
donde $C_s$ es el costo por servidor y $C_w$ el costo de espera por cliente.

## Errores comunes

- Mezclar unidades de $\lambda$ y $\mu$ (ej. $\lambda$ en clientes/hora y $1/\mu$ en minutos sin convertir ambos a la misma base).
- Confundir $L$ (clientes en el *sistema*: cola + servicio) con $L_q$ (clientes solo en la *cola*).

## Ejercicios propuestos

1. Llegan $\lambda = 20$ clientes/h y cada cajero atiende $\mu = 6$ clientes/h. ¿Cuál es el mínimo número de cajeros $c$ para que el sistema sea estable?
   - *Respuesta:* Se requiere $c\mu > \lambda \implies 6c > 20 \implies c \ge 4$ ($\rho = 20/24 \approx 0.833$). Con $c=3$ sería $\rho = 1.11$ (inestable).

## Conexiones

- Anterior: [[Investigación de Operaciones II - Procesos de Decisión Markovianos]]
- Siguiente: [[Investigación de Operaciones II - Teoría de Inventarios EOQ y Modelos Probabilísticos]]
- Notas relacionadas: Teoría de Colas e Inventarios Fórmulas IO2, [[MVP Colas]]
- Materia: [[Investigación de Operaciones II]]
- Materias relacionadas: [[Estadística II]], [[Simulación de Sistemas]]

## Fuente

- `Material/ProgramaInvOperacionesII.doc` (Unidad II) y Taha (Cap. 18).
