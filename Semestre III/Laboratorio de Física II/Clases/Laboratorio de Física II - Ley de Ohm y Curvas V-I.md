---
tags: [clase, semestre-III]
materia: Laboratorio de Física II
---
# Laboratorio de Física II - Ley de Ohm y Curvas V-I

Materia: [[Laboratorio de Física II]]
Anterior: [[Laboratorio de Física II - Electrostática y Líneas Equipotenciales]]
Siguiente: [[Laboratorio de Física II - Circuitos Serie, Paralelo y Leyes de Kirchhoff]]

## Contexto y objetivo

La **Ley de Ohm** establece la relación proporcional entre la diferencia de potencial aplicada a un conductor y la corriente que circula por él. En esta práctica se mide la curva característica $V\text{–}I$ para distinguir **elementos óhmicos** (resistores de carbón) de **elementos no óhmicos** (bombillo incandescente o diodo), y se determina la resistencia experimental mediante ajuste lineal por **mínimos cuadrados**.

## 1. Ley de Ohm y potencia eléctrica

Para un material óhmico a temperatura constante:
$$V = I \cdot R \qquad \Longleftrightarrow \qquad I = \frac{V}{R}$$
donde $V$ está en voltios ($\text{V}$), $I$ en amperios ($\text{A}$) y $R$ en ohmios ($\Omega$). La potencia eléctrica disipada en forma de calor (efecto Joule) es:
$$P = V \cdot I = I^2 R = \frac{V^2}{R}$$

- **Material óhmico**: la gráfica $V$ vs. $I$ es una línea recta que pasa por el origen, con pendiente constante $m = R$.
- **Material no óhmico**: la relación no es lineal (por ejemplo, en un filamento de tungsteno la temperatura aumenta con la corriente, incrementando la resistividad y curvando la gráfica $V$ vs. $I$; en un diodo semiconductor la conducción es exponencial a partir de $\approx 0{,}7\,\text{V}$).

## 2. Ajuste lineal por mínimos cuadrados

Dados $n$ pares experimentales $(I_i, V_i)$, la recta de mejor ajuste $V = m\,I + b$ tiene pendiente:
$$m = \frac{n \sum (I_i V_i) - (\sum I_i)(\sum V_i)}{n \sum I_i^2 - (\sum I_i)^2}, \qquad b = \frac{\sum V_i - m \sum I_i}{n}$$
La resistencia experimental corresponde a $R_{\text{exp}} = m$ (y el intercepto $b$ debe ser cercano a $0\,\text{V}$).

## 3. Montaje experimental y código de colores

1. Leer el valor nominal y la tolerancia de la resistencia mediante su código de colores (ej. marrón-negro-rojo-dorado $= 10 \times 10^2\,\Omega \pm 5\% = 1{,}0\,\text{k}\Omega \pm 5\%$) y verificarla con el óhmetro sin energía.
2. Armar el circuito serie: Fuente DC $\rightarrow$ Amperímetro $\rightarrow$ Resistencia $R$ $\rightarrow$ Fuente, con el Voltímetro en paralelo sobre $R$.
3. Variar la fuente en pasos regulares (ej. $1\,\text{V}$ a $10\,\text{V}$) y tabular $(I, V)$ sin superar la potencia máxima del resistor (típicamente $0{,}25\,\text{W}$ o $0{,}5\,\text{W}$).

## Ejemplo resuelto

Se miden los siguientes datos sobre un resistor nominal de $10\,\Omega$:

| $I\,(\text{A})$ | $0{,}10$ | $0{,}21$ | $0{,}29$ | $0{,}40$ |
|---|---|---|---|---|
| $V\,(\text{V})$ | $1{,}0$ | $2{,}0$ | $3{,}0$ | $4{,}0$ |

Calculando las sumas ($n = 4$): $\sum I = 1{,}00$, $\sum V = 10{,}0$, $\sum I^2 = 0{,}2982$, $\sum IV = 2{,}99$:
$$m = \frac{4(2{,}99) - (1{,}00)(10{,}0)}{4(0{,}2982) - (1{,}00)^2} = \frac{1{,}96}{0{,}1928} \approx 10{,}17\,\Omega$$
Error relativo respecto al nominal ($10\,\Omega$): $\varepsilon_r = \frac{|10{,}17 - 10|}{10} \times 100\% = 1{,}7\%$.

## Errores comunes

- Graficar $I$ en el eje vertical y $V$ en el horizontal y tomar la pendiente directamente como $R$ (en ese caso la pendiente es $1/R$, la conductancia).
- Exceder la potencia nominal de la resistencia ($P = V^2/R > 0{,}25\,\text{W}$), calentándola y alterando su valor óhmico (o quemándola).
- No considerar la resistencia interna del amperímetro/voltímetro en mediciones de resistencias muy bajas o muy altas.

## Ejercicios propuestos

1. ¿Qué potencia disipa una resistencia de $100\,\Omega$ conectada a $12\,\text{V}$? ¿Soportaría una resistencia estándar de $1/4\,\text{W}$?
2. Si al graficar $V$ (eje $y$) vs. $I$ (eje $x$) la curva se inclina hacia arriba a medida que aumenta $I$, ¿la resistencia está aumentando o disminuyendo?

**Respuestas:**
1. $P = 12^2 / 100 = 1{,}44\,\text{W}$. No, superaría ampliamente $0{,}25\,\text{W}$ y se quemaría.
2. Está aumentando (la pendiente instantánea $dV/dI$ crece, típico de un filamento que se calienta).

## Conexiones

- Continúa desde [[Laboratorio de Física II - Electrostática y Líneas Equipotenciales]].
- Fundamento directo para [[Laboratorio de Física II - Circuitos Serie, Paralelo y Leyes de Kirchhoff]] y [[Física II]].

## Fuente

Elaborado siguiendo el programa referencial de [[Laboratorio de Física II]] (Práctica 3: Ley de Ohm y curvas características).
