---
tags: [clase, semestre-II]
materia: Química General I
fuente: conocimiento general
---
# Química General I - Materia y medición

Materia: [[Química General I]]
Siguiente: [[Química General I - Conversión de unidades y análisis dimensional]]

## Contexto y objetivo
La química estudia la composición, estructura, propiedades y transformaciones de la materia. Todo curso de Química General I comienza clasificando la materia y estableciendo el lenguaje cuantitativo (unidades, cifras significativas, densidad). Al terminar esta nota debes poder clasificar un sistema material, expresar mediciones con las cifras significativas correctas y calcular densidades. Es la base de todo lo demás: sin unidades correctas no hay estequiometría ni disoluciones. (Programa oficial UNET: verificar.)

## 1. Clasificación de la materia
**Materia** es todo lo que tiene masa y ocupa un lugar en el espacio. Se clasifica así:

- **Sustancia pura**: composición fija y propiedades definidas.
  - **Elemento**: no se descompone en sustancias más simples por métodos químicos (H2, Fe, O2).
  - **Compuesto**: dos o más elementos combinados en proporción fija de masa (H2O, NaCl, CO2). Se separa en elementos solo por reacciones químicas.
- **Mezcla**: dos o más sustancias sin proporción fija; conservan sus propiedades y se separan por métodos físicos.
  - **Homogénea** (disolución): una sola fase visible (agua salada, aire filtrado, latón).
  - **Heterogénea**: varias fases (arena y agua, granito, aceite y agua). Incluye mezclas groseras y suspensiones; los coloides están en el límite (ver [[Química General I - Coloides, suspensiones y mezclas groseras]]).

**Métodos de separación de mezclas**: filtración (sólido-líquido insoluble), decantación (líquidos inmiscibles o sólido sedimentado), destilación (líquidos de distinto punto de ebullición), cristalización/evaporación (soluto sólido disuelto), cromatografía (distinta afinidad por una fase), imantación (material ferromagnético), tamizado (sólidos de distinto tamaño).

## 2. Propiedades físicas y químicas
- **Físicas**: se miden sin alterar la identidad de la sustancia (color, punto de fusión, densidad, conductividad).
- **Químicas**: describen cómo reacciona (inflamabilidad, oxidación).
- **Intensivas**: no dependen de la cantidad (densidad, temperatura, punto de ebullición).
- **Extensivas**: dependen de la cantidad (masa, volumen, energía).

**Estados de agregación**: sólido (forma y volumen fijos), líquido (volumen fijo, forma del recipiente), gas (ni forma ni volumen fijos, compresible). Cambios de estado: fusión, solidificación, vaporización, condensación, sublimación y deposición.

## 3. Sistema Internacional de unidades
| Magnitud | Unidad SI | Símbolo |
|---|---|---|
| Longitud | metro | m |
| Masa | kilogramo | kg |
| Tiempo | segundo | s |
| Temperatura | kelvin | K |
| Cantidad de sustancia | mol | mol |
| Corriente | amperio | A |

Prefijos habituales: tera (T, 10^12), giga (G, 10^9), mega (M, 10^6), kilo (k, 10^3), hecto (h, 10^2), deca (da, 10^1), deci (d, 10^-1), centi (c, 10^-2), mili (m, 10^-3), micro (µ, 10^-6), nano (n, 10^-9), pico (p, 10^-12).

Unidades derivadas: volumen en m³ (1 L = 1 dm³ = 10^-3 m³; 1 mL = 1 cm³), fuerza en newton, presión en pascal (1 atm = 101 325 Pa = 760 mmHg), energía en julio.

**Temperatura**: $T(\text{K}) = T(^\circ\text{C}) + 273{,}15$; $T(^\circ\text{F}) = 1{,}8\,T(^\circ\text{C}) + 32$.

## 4. Notación científica
Se escribe $a \times 10^n$ con $1 \le |a| < 10$. Ejemplo: 0,000 045 = $4{,}5\times10^{-5}$; 602 200 000 000 000 000 000 000 = $6{,}022\times10^{23}$.

## 5. Exactitud, precisión y cifras significativas
- **Exactitud**: cercanía al valor verdadero. **Precisión**: reproducibilidad de las medidas.
- **Cifras significativas (CS)**: dígitos ciertos más el primer incierto.

Reglas:
1. Todo dígito distinto de cero es significativo.
2. Los ceros entre dígitos significativos cuentan (2005 tiene 4 CS).
3. Los ceros a la izquierda no cuentan (0,0034 tiene 2 CS).
4. Los ceros finales cuentan si hay coma decimal (2,500 tiene 4 CS); en 1500 sin coma es ambiguo, se aclara en notación científica ($1{,}5\times10^3$: 2 CS).
5. **Suma y resta**: el resultado tiene tantos decimales como el sumando con menos decimales.
6. **Multiplicación y división**: el resultado tiene tantas CS como el factor con menos CS.
7. Los números exactos (conteos, definiciones) no limitan las CS.

## 6. Densidad
$$\rho = \frac{m}{V}\quad [\text{g/cm}^3,\ \text{g/mL},\ \text{kg/m}^3]$$
Equivalencia útil: $1\ \text{g/cm}^3 = 1000\ \text{kg/m}^3$. Densidad relativa = $\rho/\rho_{agua}$ (adimensional; el agua a 4 °C tiene 1,00 g/cm³).

### Ejemplo 1
Un bloque de aluminio de 500 g tiene densidad 2700 kg/m³. ¿Volumen?
1. Convertir: 500 g = 0,500 kg.
2. $V = m/\rho = 0{,}500/2700 = 1{,}85\times10^{-4}\ \text{m}^3$.
3. En cm³: $1{,}85\times10^{-4}\times10^{6} = 185\ \text{cm}^3$.

### Ejemplo 2 (picnómetro)
Botella vacía 800 g; con agua 960 g; con queroseno 931 g.
1. Masa de agua = 160 g, y como $\rho_{agua}=1$ g/mL, capacidad = 160 mL.
2. Masa de queroseno = 131 g en 160 mL: $\rho = 131/160 = 0{,}819$ g/mL.

### Ejemplo 3
Cifras significativas: $12{,}5 \times 3{,}2 = 40{,}0 \to 40$ (2 CS, por el 3,2). $12{,}55 + 0{,}7 = 13{,}25 \to 13{,}3$ (un decimal).

## Errores comunes
- Usar °C en fórmulas de gases (debe ser K).
- Confundir masa (kg) con peso (N).
- Redondear en pasos intermedios (redondear solo al final).
- Pensar que un cambio de fase es una reacción química.
- Olvidar convertir mL a L antes de calcular concentraciones.

## Ejercicios propuestos
1. Clasifica: agua de mar, oro 24 K, aire, CO2, jugo con pulpa. (Mezcla homogénea, elemento, mezcla homogénea, compuesto, mezcla heterogénea.)
2. ¿Cuántas CS tiene 0,004 050 m? (4.)
3. Densidad de un líquido: 25,0 mL pesan 31,5 g. (1,26 g/mL.)
4. Convierte 25 °C a K y a °F. (298,15 K; 77 °F.)
5. Masa de 2,0 L de mercurio (ρ = 13,6 g/mL). (27,2 kg.)

## Conexiones
- Las conversiones y el análisis dimensional continúan en [[Química General I - Conversión de unidades y análisis dimensional]].
- Los mismos conceptos de magnitud, unidades y vectores aparecen en [[Física I]]; el manejo de potencias de diez y álgebra viene de [[Matemática I]].

## Fuente
Conocimiento general de química general universitaria (Chang; Brown-LeMay). Contenido programático UNET: verificar con el programa oficial.
