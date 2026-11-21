---
tags: [clase, semestre-II]
materia: Química General I
fuente: Material/DOC-20230614-WA0042.pdf
---
# Química General I - Conversión de unidades y análisis dimensional

Materia: [[Química General I]]
Anterior: [[Química General I - Materia y medición]]
Siguiente: [[Química General I - Estructura atómica]]

## Contexto y objetivo
El PDF "DOC-20230614-WA0042" es un cuadernillo de problemas resueltos, titulado "Coloquio N° 1, Parte B: Conversión de unidades" (material de Física de la carrera de Bioquímica y Farmacia de la F.C.E.Q. y N., U.Na.M., 2009, según su encabezado). Enseña el **método de los factores de conversión** y el **análisis dimensional**. El objetivo es que cualquier cambio de unidades se haga de forma sistemática y verificable, en lugar de "a ojo".

## 1. Procedimiento (los 4 pasos del documento)
1. Escribir la cantidad que se quiere convertir.
2. Definir cada unidad a convertir en términos de la unidad deseada (tabla de equivalencias).
3. Para cada definición formar **dos factores de conversión**, uno recíproco del otro (cada uno vale 1, porque numerador y denominador son la misma cantidad física).
4. Multiplicar la cantidad por los factores que **cancelan todas las unidades, salvo las deseadas**.

Idea clave: las unidades se tratan como cantidades algebraicas; si tras multiplicar no quedan las unidades buscadas, se eligió el factor equivocado (el documento lo muestra con un resultado "INCORRECTO" de unidades ft²/s²).

## 2. Problemas resueltos del documento

### Problema 2c: velocidad
Convertir 163,2 ft/s a m/s. Equivalencia: 1 ft = 0,3048 m.
$$163{,}2\ \frac{\text{ft}}{\text{s}}\times\frac{0{,}3048\ \text{m}}{1\ \text{ft}} = 49{,}74\ \frac{\text{m}}{\text{s}}$$
Si se elige el factor invertido, queda $163{,}2/0{,}3048 = 535\ \text{ft}^2/(\text{m·s})$: las unidades no son las pedidas. (Nota: el documento escribe por error "0,304" en algún paso; el valor correcto es 0,3048.)

### Problema 2b: energía
Convertir $2{,}18\times10^{14}$ eV a J con $1\ \text{eV}=1{,}602\times10^{-19}$ J:
$$2{,}18\times10^{14}\ \text{eV}\times\frac{1{,}602\times10^{-19}\ \text{J}}{1\ \text{eV}} = 3{,}49\times10^{-5}\ \text{J}$$

### Problema 2a: densidad
Convertir 3,8 lb/ft³ a kg/m³. Se convierte numerador y denominador por separado, pues $[\rho]=[m]/[L^3]$. Con 1 lb = 0,4536 kg y 1 ft³ = (0,3048 m)³ = 0,0283 m³:
$$3{,}8\ \frac{\text{lb}}{\text{ft}^3}\times\frac{0{,}4536\ \text{kg}}{1\ \text{lb}}\times\frac{1\ \text{ft}^3}{0{,}0283\ \text{m}^3}\approx 61\ \frac{\text{kg}}{\text{m}^3}$$
(el documento obtiene 61,5 kg/m³ usando 0,028 m³; con 0,0283 resulta 60,9). Observación importante: una unidad elevada al cubo se convierte elevando **también el factor** al cubo.

### Problema 3: volumen de un tanque
Tanque de 24 plg × 18 plg × 12 plg; hallar m³.
1. $V = 24\cdot18\cdot12 = 5184\ \text{plg}^3$ (primero se calcula en las unidades dadas: mezclar unidades no cumple la regla dimensional).
2. $1\ \text{plg}^3 = 1{,}639\times10^{-5}\ \text{m}^3$.
3. $V = 5184\times1{,}639\times10^{-5} = 0{,}085\ \text{m}^3$ (85 L).

### Problema 4: presión de un manómetro
Manómetro diferencial con mercurio ($\rho = 849\ \text{lb/ft}^3$), $h=7{,}8$ cm, $g=9{,}8\ \text{m/s}^2$. $\Delta P=\rho g h$.
1. $\rho = 849\ \text{lb/ft}^3\times16{,}02\ \frac{\text{kg/m}^3}{\text{lb/ft}^3} = 13\,601\ \text{kg/m}^3$.
2. $h = 7{,}8\ \text{cm}=0{,}078$ m.
3. $\Delta P = 13\,601\times9{,}8\times0{,}078 = 10\,397\ \text{Pa}$ (el documento da 10 396,6 Pa).
4. En hectopascales: $10\,396{,}6/100 = 103{,}97\ \text{hPa}$.
Los kg·m/s² / m² = N/m² = Pa confirman la coherencia dimensional.

### Problema 5: reglas de dimensiones
- **Regla 1**: solo se pueden sumar, restar o igualar cantidades de la misma dimensión.
- **Regla 2**: ambos lados de una igualdad tienen la misma dimensión.
Verificación de $s = vt + \tfrac12 at^2$: $[m] = [m/s][s] + [m/s^2][s^2] = [m]+[m]$. Es dimensionalmente correcta (el factor ½ es adimensional). Ojo: ser dimensionalmente correcta es condición necesaria, no suficiente (no detecta factores numéricos).

## 3. Tabla mínima de equivalencias útiles
| Magnitud | Equivalencia |
|---|---|
| Longitud | 1 in = 2,54 cm; 1 ft = 12 in = 0,3048 m; 1 mi = 1609 m |
| Masa | 1 lb = 0,4536 kg; 1 kg = 1000 g |
| Volumen | 1 L = 1000 cm³ = 10^-3 m³; 1 gal (EE.UU.) = 3,785 L |
| Tiempo | 1 h = 3600 s |
| Presión | 1 atm = 101 325 Pa = 760 mmHg |
| Energía | 1 eV = 1,602×10^-19 J; 1 cal = 4,184 J |

Atajo: km/h → m/s se divide entre 3,6.

## 4. Ejemplo adicional paso a paso (del cuadernillo de la clase)
Convertir 45 mg/mL a dag/m³: 45 mg = 0,045 g = 0,0045 dag; 1 mL = 10^-6 m³. Entonces $0{,}0045/10^{-6} = 4500$ dag/m³ = $4{,}5\times10^3$.

## Errores comunes
- Convertir unidades al cuadrado o cubo con el factor lineal (1 m² = 10⁴ cm², no 10²).
- Usar el factor invertido y no revisar la cancelación.
- Redondear antes de terminar.
- Mezclar sistemas (ft con m) dentro de una fórmula.

## Ejercicios propuestos
1. 90 km/h a m/s. (25 m/s)
2. 5817 pm a µm. ($5{,}817\times10^{-3}$ µm)
3. 3,7 dam a Tm. ($3{,}7\times10^{-11}$ Tm)
4. 1 atm a lb/in² sabiendo 1 lb = 4,448 N y 1 in = 0,0254 m. (≈ 14,7 psi)
5. ¿Es correcta $v^2 = v_0^2 + 2a x$ dimensionalmente? (Sí.)

## Conexiones
- Es el mismo ejercicio que se necesita en [[Física I]] para trabajar en SI.
- Se aplica a los problemas de [[Química General I - Problemas de concentración, densidad y gases]] (por ejemplo, el ítem 15 y 26 del cuadernillo).
- Antecede a la [[Química General I - Estructura atómica]].

## Fuente
Archivo `Material/DOC-20230614-WA0042.pdf` (extraído con pdftotext; texto legible). Los datos del encabezado (institución) corresponden al documento original, no a la UNET.
