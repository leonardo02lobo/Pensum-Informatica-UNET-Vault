---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/Conceptos_Basicos-1 imprimir.pdf
---
# Física I - Conceptos previos y magnitudes físicas

Materia: [[Física I]]
Siguiente: [[Física I - Vectores]]

## Contexto y objetivo
Esta clase abre el curso de Física I de la UNET (diapositivas de la Ing. Neyra Tellez, 2009). Fija el lenguaje con el que se describirá toda la mecánica: qué es una **magnitud física**, cómo se mide, qué sistema de unidades se usa y por qué algunas magnitudes necesitan dirección (vectores) y otras no (escalares). Sin esto, ninguna fórmula posterior (cinemática, dinámica, rotación) tiene sentido físico. El objetivo es que al terminar puedas: clasificar magnitudes, convertir unidades con seguridad, verificar una fórmula por análisis dimensional y representar un vector con módulo, dirección y sentido.

## 1. Magnitud física y medición
Una **magnitud física** es cualquier cantidad empleada para describir cuantitativamente un fenómeno: temperatura, presión, desplazamiento, tiempo, velocidad. Se expresa siempre como *número + unidad*. Hay dos clases:

- **Magnitudes medidas directamente**: se comparan con un patrón (tiempo con un cronómetro, longitud con una regla).
- **Magnitudes determinadas (derivadas)**: se calculan a partir de otras medidas. La velocidad se obtiene midiendo distancia y tiempo: $v=\Delta x/\Delta t$.

**Medir** es comparar la magnitud con un patrón de referencia que define la unidad. Un resultado sin unidad carece de significado físico ("la mesa mide 2" no dice nada).

## 2. Sistema Internacional (SI)
El curso usa el SI. Las tres magnitudes fundamentales de la mecánica son:

| Magnitud | Unidad | Símbolo |
|---|---|---|
| Longitud | metro | m |
| Masa | kilogramo | kg |
| Tiempo | segundo | s |

Las demás (derivadas) se forman combinándolas:

| Magnitud | Unidad SI | En unidades base |
|---|---|---|
| Velocidad | m/s | m·s⁻¹ |
| Aceleración | m/s² | m·s⁻² |
| Fuerza | newton (N) | kg·m·s⁻² |
| Energía / trabajo | joule (J) | kg·m²·s⁻² |
| Potencia | watt (W) | kg·m²·s⁻³ |
| Momento de una fuerza (torque) | N·m | kg·m²·s⁻² |
| Momento de inercia | kg·m² | kg·m² |

Prefijos comunes: kilo (k, $10^3$), centi (c, $10^{-2}$), mili (m, $10^{-3}$), micro (μ, $10^{-6}$), mega (M, $10^6$).

## 3. Escalares y vectores
- **Magnitud escalar**: cantidad algebraica ordinaria con unidad, sin dirección ni sentido. Ejemplo: temperatura $T=37\,°C$, masa, tiempo, energía, rapidez.
- **Magnitud vectorial**: necesita **módulo** (tamaño), **dirección** (recta de acción), **sentido** (hacia qué lado de la recta apunta la flecha) y **punto de aplicación** (origen). Ejemplo: la fuerza que ejerce una cuerda sobre un objeto, la velocidad, la aceleración, el desplazamiento.

Gráficamente un vector es una flecha: su longitud (a escala) es el módulo, la recta que la contiene es la dirección y la punta indica el sentido. Los **vectores unitarios** $\hat i,\hat j,\hat k$ tienen módulo 1 y apuntan en los ejes $x,y,z$ positivos; todo vector se escribe $\vec A = A_x\hat i + A_y\hat j + A_z\hat k$.

### Componentes de un vector (ejemplo de la clase)
Un vector $\vec r$ de módulo 5 m que forma $\beta=30°$ con el eje $X$:

$$r_x = r\cos\beta = 5\cos 30° = 4{,}33\ \text{m},\qquad r_y = r\sin\beta = 5\sin 30° = 2{,}5\ \text{m}$$

$$\vec r = 4{,}33\,\hat i + 2{,}5\,\hat j\ \ \text{m}$$

Recíprocamente, $|\vec A|=\sqrt{A_x^2+A_y^2}$ y $\tan\beta = A_y/A_x$. (Cuidado: el ángulo con la horizontal es $\beta$; el que forma con el eje vertical es $\alpha=90°-\beta$.)

### Operaciones (resumen; detalle en [[Física I - Vectores]])
Suma y resta (gráfica y por componentes), producto por un escalar, producto punto (escalar) y producto cruz (vectorial). Ejemplos del material: excursionista que camina 4 km al sur y 6 km al este queda a $\sqrt{4^2+6^2}=7{,}21$ km del campamento; con $\vec r=9\hat i+10\hat j$ y $\vec p=-10\hat i+8\hat j$: $\vec r+\vec p=-\hat i+18\hat j$ (módulo 18,03), $\vec r-\vec p=19\hat i+2\hat j$ y $\vec p-\vec r=-19\hat i-2\hat j$ (mismo módulo, sentidos opuestos).

## 4. Análisis dimensional
Toda ecuación física debe ser **dimensionalmente homogénea**: ambos miembros y todos los sumandos tienen las mismas dimensiones. Usa $[L]$, $[M]$, $[T]$.

Ejemplo: comprobar $x = x_0 + v_0 t + \tfrac12 a t^2$.
- $[x]=L$, $[x_0]=L$.
- $[v_0 t] = (L/T)\,T = L$.
- $[a t^2]=(L/T^2)\,T^2 = L$. ✓

Ejemplo de detección de error: $v = a\,t^2$ da $[v]=L/T^2\cdot T^2 \cdot$ → $L$, pero la velocidad es $L/T$: la fórmula es falsa.

## 5. Conversión de unidades
Multiplica por factores de conversión iguales a 1 de modo que las unidades indeseadas se cancelen.

**Ejemplo 1**: $72\ \text{km/h}$ a m/s:
$$72\,\frac{\text{km}}{\text{h}}\cdot\frac{1000\,\text{m}}{1\,\text{km}}\cdot\frac{1\,\text{h}}{3600\,\text{s}} = 20\ \text{m/s}$$
(regla práctica: dividir entre 3,6).

**Ejemplo 2**: $5\ \text{g/cm}^3$ a kg/m³: $5\cdot\dfrac{10^{-3}\,\text{kg}}{10^{-6}\,\text{m}^3}=5000\ \text{kg/m}^3$.

**Ejemplo 3**: $2{,}5\ \text{h}$ a segundos: $2{,}5\cdot3600=9000$ s.

## 6. Cifras significativas y notación científica
Al multiplicar o dividir, el resultado conserva tantas cifras significativas como el dato que menos tiene; al sumar o restar, tantos decimales como el dato con menos decimales. Para números muy grandes o pequeños usa notación científica: $0{,}000\,45\ \text{m}=4{,}5\times10^{-4}\ \text{m}$. En el curso se suelen dar los resultados con 2–3 decimales.

## Errores comunes
1. Mezclar unidades (km con m, h con s) dentro de una misma fórmula.
2. Olvidar que el ángulo de la componente depende del eje de referencia: con respecto a la vertical se intercambian seno y coseno.
3. Tratar la rapidez como si fuera velocidad (la rapidez es el módulo, un escalar).
4. Escribir resultados vectoriales sin dirección o resultados escalares con signo vectorial.
5. Confundir masa (kg, escalar) con peso (N, vector, $\vec P = m\vec g$).

## Ejercicios propuestos
1. Convierte $90\ \text{km/h}$ a m/s. *Respuesta: 25 m/s.*
2. Un vector de 10 m forma 60° con el eje $X$. Escribe sus componentes. *Respuesta: $5\hat i+8{,}66\hat j$ m.*
3. Verifica dimensionalmente $v^2=v_0^2+2a\Delta x$. *Respuesta: todos los términos son $L^2/T^2$.*
4. ¿Cuál es la unidad SI de $\tfrac12 mv^2$ en unidades base? *Respuesta: kg·m²/s² = J.*
5. $\vec A = 3\hat i-4\hat j$: hallar módulo y ángulo con $X$. *Respuesta: 5; −53,1°.*

## Conexiones
- Los vectores son la base del [[Física I - Tema 1 Movimiento en una dimensión]] (posición, velocidad, aceleración vectoriales) y de la rotación (torque, momento angular).
- Las derivadas necesarias provienen de [[Matemática I]].

## Fuente
Material/Parcial 1/Conceptos_Basicos-1 imprimir.pdf (diapositivas "Conceptos previos", Neyra Tellez, UNET, 2009). Contenido ampliado con conocimiento general de Física.
