---
tags: [clase, semestre-III]
materia: Laboratorio de Física II
---
# Laboratorio de Física II - Carga y Descarga de Capacitores (Circuito RC)

Materia: [[Laboratorio de Física II]]
Anterior: [[Laboratorio de Física II - Circuitos Serie, Paralelo y Leyes de Kirchhoff]]
Siguiente: [[Laboratorio de Física II - Campo Magnético e Inducción Electromagnética]]

## Contexto y objetivo

A diferencia de los circuitos puramente resistivos, un circuito con un resistor $R$ y un capacitor $C$ presenta una respuesta **transitoria** que evoluciona con el tiempo. Esta práctica estudia experimentalmente la carga y descarga de un capacitor, la determinación de la **constante de tiempo** $\tau = RC$ y la linealización semilogarítmica de datos exponenciales.

## 1. Ecuaciones del circuito RC

Aplicando LVK a una malla con fuente DC $V_0$, resistencia $R$ y capacitor $C$:

- **Proceso de carga** (capacitor inicialmente descargado, $V_C(0) = 0$):
  $$V_C(t) = V_0 \left(1 - e^{-t/(RC)}\right), \qquad I(t) = \frac{V_0}{R} e^{-t/(RC)}$$
- **Proceso de descarga** (sin fuente, capacitor con voltaje inicial $V_0$):
  $$V_C(t) = V_0\, e^{-t/(RC)}, \qquad I(t) = -\frac{V_0}{R} e^{-t/(RC)}$$

La **constante de tiempo** es $\tau = R \cdot C$ (unidades: $\Omega \cdot \text{F} = \text{s}$):
- En $t = \tau$ durante la carga, el capacitor alcanza $1 - e^{-1} \approx 63{,}2\%$ de $V_0$.
- En $t = \tau$ durante la descarga, el voltaje cae al $e^{-1} \approx 36{,}8\%$ de $V_0$.
- Para fines prácticos, el transitorio se considera completo en $t \approx 5\tau$ ($99{,}3\%$).

## 2. Linealización para obtener $\tau$ experimentalmente

En la descarga $V_C(t) = V_0 e^{-t/\tau}$, aplicando logaritmo natural a ambos lados:
$$\ln\left(\frac{V_C(t)}{V_0}\right) = -\frac{1}{\tau}\,t$$
Al graficar $\ln(V_C)$ en función de $t$, se obtiene una recta de pendiente $m = -\frac{1}{\tau}$, de modo que:
$$\tau_{\text{exp}} = -\frac{1}{m}$$

## 3. Métodos de medición en el laboratorio

- **Método lento (cronómetro + voltímetro)**: usar valores grandes de $R$ y $C$ (ej. $R = 100\,\text{k}\Omega$, $C = 470\,\mu\text{F} \implies \tau = 47\,\text{s}$) para registrar $V_C(t)$ cada $5\,\text{s}$.
- **Método rápido (generador de funciones + osciloscopio)**: aplicar una onda cuadrada de baja frecuencia con $\tau$ pequeño (ej. $R = 1\,\text{k}\Omega$, $C = 1\,\mu\text{F} \implies \tau = 1\,\text{ms}$) y observar directamente la curva exponencial en pantalla.

## Ejemplo resuelto

Se carga un capacitor con $R = 47\,\text{k}\Omega$, $C = 1000\,\mu\text{F}$ y $V_0 = 10{,}0\,\text{V}$:
- Constante de tiempo: $\tau = (47 \times 10^3\,\Omega)(1000 \times 10^{-6}\,\text{F}) = 47\,\text{s}$.
- Voltaje en $t = 47\,\text{s}$: $V_C(47) = 10{,}0(1 - e^{-1}) \approx 6{,}32\,\text{V}$.
- Voltaje en $t = 94\,\text{s}$ ($2\tau$): $V_C(94) = 10{,}0(1 - e^{-2}) \approx 8{,}65\,\text{V}$.

## Errores comunes

- Conectar un **capacitor electrolítico con la polaridad invertida** (la pata más corta / franja `-` debe ir al potencial menor; invertirlo puede dañarlo o hacerlo estallar).
- Olvidar la **resistencia interna del voltímetro** (típicamente $10\,\text{M}\Omega$): si se usa $R$ muy grande (del orden de megaohmios), el voltímetro descarga parcialmente el capacitor y altera $\tau_{\text{exp}}$.
- No descargar completamente el capacitor (cortocircuitando sus terminales con una resistencia de protección) antes de iniciar una nueva medición.

## Ejercicios propuestos

1. ¿Qué valor de $\tau$ se obtiene con $R = 22\,\text{k}\Omega$ y $C = 470\,\mu\text{F}$?
2. En una descarga con $V_0 = 12\,\text{V}$, ¿cuánto tiempo tarda el capacitor en bajar a $4{,}41\,\text{V}$ si $\tau = 10\,\text{s}$?

**Respuestas:**
1. $\tau = 22 \times 10^3 \times 470 \times 10^{-6} = 10{,}34\,\text{s}$.
2. $4{,}41 / 12 \approx 0{,}3675 \approx e^{-1}$, por lo tanto $t \approx \tau = 10\,\text{s}$.

## Conexiones

- Continúa desde [[Laboratorio de Física II - Circuitos Serie, Paralelo y Leyes de Kirchhoff]].
- Complementa la teoría de [[Física II]] y las ecuaciones diferenciales de primer orden de [[Matemática III]].

## Fuente

Elaborado siguiendo el programa referencial de [[Laboratorio de Física II]] (Práctica 5: Carga y descarga de un circuito RC).
