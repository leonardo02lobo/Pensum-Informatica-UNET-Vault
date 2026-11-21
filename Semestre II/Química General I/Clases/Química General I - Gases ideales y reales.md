---
tags: [clase, semestre-II]
materia: Química General I
fuente: conocimiento general
---
# Química General I - Gases ideales y reales

Materia: [[Química General I]]
Anterior: [[Química General I - Estequiometría]]
Siguiente: [[Química General I - Disoluciones y unidades de concentración]]

## Contexto y objetivo
Los gases son el estado de la materia más sencillo de describir con ecuaciones. Esta nota presenta presión, las leyes de Boyle, Charles, Gay-Lussac y Avogadro, la ecuación del gas ideal, mezclas de gases, teoría cinética y desviaciones (van der Waals). Objetivo: resolver problemas de cambios de estado de un gas, cálculo de moles y masa molar, y presiones parciales.

## 1. Presión
$P = F/A$. Unidades: 1 atm = 760 mmHg = 760 torr = 101 325 Pa = 1,013 bar. La presión de una columna de fluido es $P=\rho g h$ (manómetros; ver el problema 4 de [[Química General I - Conversión de unidades y análisis dimensional]]). **Condiciones normales (CN o STP)**: 0 °C (273,15 K) y 1 atm. Temperatura siempre en kelvin.

## 2. Leyes de los gases (cantidad de gas fija)
- **Boyle** (T constante): $P_1V_1 = P_2V_2$ (inversa).
- **Charles** (P constante): $V_1/T_1 = V_2/T_2$.
- **Gay-Lussac** (V constante): $P_1/T_1 = P_2/T_2$.
- **Combinada**: $\dfrac{P_1V_1}{T_1}=\dfrac{P_2V_2}{T_2}$.
- **Avogadro** (P y T constantes): $V/n$ = constante; 1 mol ocupa 22,414 L en CN (y 24,5 L a 25 °C y 1 atm).

## 3. Ecuación del gas ideal
$$PV = nRT$$
con $R = 0{,}08206\ \dfrac{\text{atm·L}}{\text{mol·K}} = 8{,}314\ \dfrac{\text{J}}{\text{mol·K}}$. Consecuencias:
- Densidad: $\rho = \dfrac{PM}{RT}$.
- Masa molar: $M = \dfrac{mRT}{PV}$.

## 4. Mezclas: ley de Dalton
$P_{total} = \sum P_i$, con $P_i = x_i P_{total}$ y $x_i = n_i/n_{total}$ (fracción molar). Al recoger un gas sobre agua, $P_{gas} = P_{atm} - P_{vapor\ H_2O}$.

## 5. Teoría cinética
Moléculas puntuales en movimiento aleatorio, sin fuerzas entre ellas y con choques elásticos. La energía cinética promedio es proporcional a T: $\bar{E}_c = \tfrac32 k_BT$. Velocidad cuadrática media $v_{rms}=\sqrt{3RT/M}$. **Ley de Graham**: velocidad de efusión inversamente proporcional a $\sqrt{M}$.

## 6. Gases reales
A alta presión y baja temperatura las moléculas tienen volumen propio y se atraen. Ecuación de van der Waals:
$$\left(P + \frac{an^2}{V^2}\right)(V - nb) = nRT$$
$a$ corrige las atracciones, $b$ el volumen excluido. Factor de compresibilidad $Z = PV/nRT$ (=1 para ideal).

## 7. Ejemplos resueltos (con los problemas del cuadernillo)
**1 (Boyle)**: 1 L de CO₂ a 1 atm (760 mmHg) pasa a 140 mmHg a T constante: $V_2 = 1\times760/140 = 5{,}43$ L. Y a 10 mmHg: 76 L.

**2 (Charles)**: Globo de 4 L a 27 °C asciende donde hace -5 °C a igual presión: $V_2 = 4\times268{,}15/300{,}15 = 3{,}57$ L.

**3 (moles)**: 5 L de O₂ a 273 K y 10 atm: $n = 10\times5/(0{,}0821\times273) = 2{,}23$ mol; moléculas: $2{,}23\times6{,}022\times10^{23}=1{,}34\times10^{24}$.

**4**: 5 L de N₂ a 215 K y 1 atm: $n = 5/(0{,}0821\times215)=0{,}283$ mol → $1{,}71\times10^{23}$ moléculas.

**5**: $3\times10^{20}$ moléculas de O₂ pasan de CN a 473 K (a la misma presión): $n = 4{,}98\times10^{-4}$ mol; $V = nRT/P = 4{,}98\times10^{-4}\times0{,}0821\times473 = 1{,}93\times10^{-2}$ L.

**6 (bombonas)**: depósito de 500 m³ a 4 atm; bombonas de 200 L a 2 atm. Con T constante, $P_1V_1 = 4\times500\,000$ L = $2\times10^6$ L·atm; cada bombona 400 L·atm → 5000 bombonas.

**7 (masa molar)**: 0,500 g de un gas ocupan 0,2 L a 1 atm y 300 K: $M = mRT/PV = 0{,}500\times0{,}0821\times300/0{,}2 = 61{,}6$ g/mol.

**8 (Dalton)**: 2 mol de N₂ y 1 mol de O₂ en un recipiente a 3 atm: $P_{N_2} = (2/3)\times3 = 2$ atm; $P_{O_2}=1$ atm.

## Errores comunes
- Usar °C en lugar de K.
- Mezclar unidades de R con unidades de P y V (atm·L vs J).
- Aplicar 22,4 L/mol sin que sean CN.
- Olvidar que al mantener la masa y cambiar T, la densidad cambia.
- Confundir presión parcial con total.

## Ejercicios propuestos
1. Volumen de 0,1 mol de gas ideal a CN y a 25 °C, 1 atm. (2,24 L; 2,45 L)
2. Densidad del CO₂ a CN. (1,96 g/L)
3. Una muestra de 2,0 L a 300 K y 1 atm se calienta a 450 K a volumen constante: ¿P? (1,5 atm)
4. Moléculas en 3 cm³ a 760 mmHg y 25 °C. ($7{,}4\times10^{19}$)
5. ¿Qué gas efunde más rápido, H₂ o O₂ y cuántas veces? (H₂, 4 veces)

## Conexiones
- El gas ideal y la presión parcial se usan en la [[Química General I - Estequiometría]] de gases y en la química atmosférica ([[Ecología y Contaminación Ambiental]]).
- La temperatura y la energía cinética conectan con la termodinámica de [[Física I]].
- Los problemas completos están en [[Química General I - Problemas de concentración, densidad y gases]].

## Fuente
Conocimiento general; ejemplos tomados de los ítems 13, 18, 20, 23, 27-32 de `Material/DOC-20221123-WA0015.pdf`.
