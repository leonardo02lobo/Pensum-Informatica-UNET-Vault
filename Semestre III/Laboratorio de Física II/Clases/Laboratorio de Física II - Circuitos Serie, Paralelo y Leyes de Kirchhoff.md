---
tags: [clase, semestre-III]
materia: Laboratorio de Física II
---
# Laboratorio de Física II - Circuitos Serie, Paralelo y Leyes de Kirchhoff

Materia: [[Laboratorio de Física II]]
Anterior: [[Laboratorio de Física II - Ley de Ohm y Curvas V-I]]
Siguiente: [[Laboratorio de Física II - Carga y Descarga de Capacitores (Circuito RC)]]

## Contexto y objetivo

Los circuitos reales combinan múltiples resistencias y mallas que no siempre pueden reducirse únicamente a serie y paralelo. Esta práctica verifica experimentalmente las reglas de **resistencia equivalente** y las **Leyes de Kirchhoff** (conservación de la carga en nodos y conservación de la energía en mallas).

## 1. Asociaciones serie, paralelo y divisor de tensión

| Conexión | Corriente | Voltaje | Resistencia equivalente |
|---|---|---|---|
| **Serie** | Igual en todos los elementos ($I_T = I_1 = I_2$) | Se reparte ($V_T = V_1 + V_2$) | $R_{\text{eq}} = \sum_{k=1}^{n} R_k$ |
| **Paralelo** | Se reparte ($I_T = I_1 + I_2$) | Igual en todas las ramas ($V_T = V_1 = V_2$) | $\frac{1}{R_{\text{eq}}} = \sum_{k=1}^{n} \frac{1}{R_k}$ |

Para dos resistencias en paralelo: $R_{\text{eq}} = \frac{R_1 R_2}{R_1 + R_2}$.

## 2. Leyes de Kirchhoff

1. **Ley de Corrientes de Kirchhoff (LCK — Nodos):** la suma algebraica de las corrientes que entran a un nodo es igual a la suma de las que salen:
   $$\sum I_{\text{entran}} = \sum I_{\text{salen}} \qquad \text{o} \qquad \sum_{k} I_k = 0$$
2. **Ley de Voltajes de Kirchhoff (LVK — Mallas):** la suma algebraica de todas las diferencias de potencial alrededor de cualquier lazo cerrado es cero:
   $$\sum_{\text{malla}} \Delta V_k = 0$$

## 3. Procedimiento de verificación en protoboard

1. Medir primero el valor real de cada resistencia ($R_1, R_2, R_3, \dots$) con el óhmetro antes de energizar.
2. Armar un circuito mixto (o puente con dos fuentes) sobre el protoboard.
3. Medir la tensión de la fuente $V_s$ y la caída de voltaje $V_k$ en cada resistencia respetando la polaridad (para comprobar signos en LVK).
4. Abrir cada rama para insertar el amperímetro en serie y medir $I_k$, verificando que en cada nodo $\sum I_{\text{entran}} \approx \sum I_{\text{salen}}$ dentro del margen de error instrumental.

## Ejemplo resuelto

En un circuito serie con $V_s = 12{,}0\,\text{V}$, $R_1 = 100\,\Omega$ y $R_2 = 200\,\Omega$:
- $R_{\text{eq}} = 100 + 200 = 300\,\Omega$.
- Corriente teórica: $I = \frac{12{,}0}{300} = 0{,}040\,\text{A} = 40\,\text{mA}$.
- Caídas de voltaje: $V_1 = I R_1 = 4{,}0\,\text{V}$, $V_2 = I R_2 = 8{,}0\,\text{V}$.
- Verificación LVK: $+12{,}0 - 4{,}0 - 8{,}0 = 0\,\text{V}$.

## Errores comunes

- Colocar dos terminales de una misma resistencia en la misma columna de 5 puntos del protoboard (queda cortocircuitada).
- Invertir las puntas del voltímetro en distintas ramas y luego sumar los voltajes sin respetar el sentido de recorrido de la malla.
- Olvidar cerrar el circuito después de retirar el amperímetro de una rama.

## Ejercicios propuestos

1. Dos resistencias de $120\,\Omega$ y $60\,\Omega$ se conectan en paralelo a una fuente de $6\,\text{V}$. Calcula $R_{\text{eq}}$ y la corriente total $I_T$.
2. En un nodo entran $I_1 = 25{,}2\,\text{mA}$ e $I_2 = 14{,}8\,\text{mA}$, y sale una sola rama $I_3$. ¿Qué valor debe medir el amperímetro en $I_3$?

**Respuestas:**
1. $R_{\text{eq}} = \frac{120 \times 60}{120 + 60} = 40\,\Omega$; $I_T = \frac{6}{40} = 0{,}15\,\text{A}$.
2. $I_3 = 25{,}2 + 14{,}8 = 40{,}0\,\text{mA}$.

## Conexiones

- Continúa desde [[Laboratorio de Física II - Ley de Ohm y Curvas V-I]].
- Aplica la teoría de circuitos de [[Física II]] y prepara los circuitos transitorios de [[Laboratorio de Física II - Carga y Descarga de Capacitores (Circuito RC)]].

## Fuente

Elaborado siguiendo el programa referencial de [[Laboratorio de Física II]] (Práctica 4: Circuitos serie, paralelo, mixtos y leyes de Kirchhoff).
