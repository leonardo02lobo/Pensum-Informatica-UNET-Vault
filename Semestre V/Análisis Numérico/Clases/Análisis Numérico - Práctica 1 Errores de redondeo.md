---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/Tema 1-APROXIMACIONES Y ERRORES/Practica 1 Errores.pdf
---
# Análisis Numérico - Práctica 1 Errores de redondeo

Materia: [[Análisis Numérico]]
Anterior: [[Análisis Numérico - Instructivo de asignaciones]]
Siguiente: [[Análisis Numérico - Bisección]]

## Contexto y objetivo
La Práctica 1 (Prof. Jenny E. Pérez R.) es un PDF **escaneado** (sin capa de texto); se leyó convirtiendo las 2 páginas a imagen. Su objetivo es que el estudiante comprenda el efecto de los **errores de redondeo** en los cálculos y cómo pueden conducir a resultados erróneos. Se usa una "computadora imaginaria" decimal con mantisa de **cuatro dígitos** y característica de dos dígitos, más un dígito para el signo del número (palabra de 7 bits), para visualizar en un ambiente controlado las dificultades que en una máquina real aparecen con más dígitos.

## Teoría necesaria
**Cifras significativas y errores.** Si $x$ es el valor exacto y $x^*$ la aproximación: error absoluto $E_a=|x-x^*|$; error relativo $E_r=|x-x^*|/|x|$; porcentual $100E_r$. Una máquina decimal con $t$ dígitos de mantisa representa $x=\pm0.d_1d_2\dots d_t\times10^e$ con $d_1\neq0$. El **redondeo** produce un error relativo máximo $\tfrac12 10^{1-t}$ (aquí $5\times10^{-4}$).

**Causas graves de error** (las cuatro de la práctica):
1. Suma de números muy distintos en magnitud: el menor se pierde al alinear exponentes.
2. Resta de números casi iguales: **cancelación catastrófica**; se pierden dígitos significativos.
3. Overflow (desbordamiento) y underflow (desbordamiento negativo).
4. División entre un número muy pequeño: amplifica el error del divisor.

## Los ejercicios, resueltos
Nota sobre la máquina del enunciado: mantisa de 4 dígitos y característica de 2 dígitos, **uno de los cuales se usa para el signo**; por tanto el exponente decimal queda en el rango $-9\ldots9$. Cualquier resultado con exponente fuera de ese rango es overflow (arriba) o underflow (abajo).

**a) Suma de números muy distintos** ($x=5$, $y=0.8712\times10^{7}$). La suma exacta es $8\,712\,005$. Para sumar, la máquina alinea exponentes: $5=0.0000005\times10^{7}$, que con 4 dígitos de mantisa se trunca a $0.0000$. Resultado almacenado: $0.8712\times10^{7}=8\,712\,000$. El 5 **desaparece**: error absoluto 5, relativo $5.7\times10^{-7}$ (pequeño en relativo, pero el sumando pequeño queda completamente ignorado). Si hay que sumar muchos términos pequeños, conviene acumularlos primero entre sí: $5+5+\dots$ (cien veces) sí llegaría a pesar $500$, que ya se vería. Conclusión: el orden de suma importa; suma de menor a mayor.

**b) Resta de números casi iguales** ($a=0.1943$, $b=0.1942$). $a-b=0.0001=0.1000\times10^{-3}$: aunque la máquina la guarda con cuatro dígitos, solo **un dígito significativo** es real (los tres restantes son ceros de relleno), porque los dígitos que coincidían se cancelaron. Con $c=0.1\times10^{5}$: $d=(a-b)c=10^{-4}\cdot10^{4}=1$. Si $a^*=0.1944$: error absoluto en $a$ $=10^{-4}$, relativo $=10^{-4}/0.1943=5.1\times10^{-4}$. Entonces $a^*-b=0.0002$ y $d^*=2$: el error relativo de $a$ ($0.05\%$) se convierte en error relativo de **100%** en $d$ (factor de amplificación $a/(a-b)\approx1943$). No se debe confiar en el resultado: es cancelación catastrófica.

**c) Overflow.** $a=0.2289\times10^{7}$, $b=0.2314\times10^{8}$. Producto: $0.2289\cdot0.2314=0.05297$, es decir $0.5297\times10^{14}$ tras normalizar; el exponente 14 excede 9 y la máquina no puede representarlo: **overflow**. La división de $b$ entre $c=0.2289\times10^{-7}$ da $1.011\times10^{15}$, que también desborda: cambiar $c$ no resuelve nada porque dividir por un número muy pequeño equivale a multiplicar por uno muy grande.

**c bis) Underflow** ($x=a\,b\,c$ con $a=0.1235\times10^{-4}$, $b=0.9477\times10^{-6}$, $c=0.1942\times10^{5}$). Si se evalúa $(ab)c$: $ab=0.1170\times10^{-10}$, exponente $-10<-9$: **underflow**, la máquina lo reemplaza por 0 y devuelve $x=0$ (sin aviso). Cambiando el orden, $a(bc)$: $bc=0.9477\cdot0.1942=0.1840\times10^{-1}$ y $a\cdot(bc)=0.1235\cdot0.1840\times10^{-5}=0.2273\times10^{-5}$ (representable). Valor correcto $x=2.273\times10^{-6}$. Conclusión: reordenar las operaciones (agrupar para mantener magnitudes intermedias moderadas) evita el underflow; el underflow rara vez da error del sistema pero conduce a resultados erróneos.

**d) División entre un número muy pequeño** ($a=0.8749\times10^{6}$, $b=0.1942\times10^{9}$, $c=0.2221\times10^{-3}$ exactos; la máquina guardó $c^*=0.2220$). Valor exacto: $b/c=8.744\times10^{11}$ y $x=a-b/c\approx-8.7439\times10^{11}$ (en la máquina imaginaria este cociente ya desborda; se calcula con aritmética de doble precisión para el análisis). Con $c^*$: $b/c^*=8.7477\times10^{11}$, de modo que el error absoluto en $x$ es $\approx3.8\times10^{8}$ y el relativo $\approx4.4\times10^{-4}$ (coincide con el error relativo de $c$, $4.5\times10^{-4}$: en cocientes el error relativo se propaga sin amplificar). El error absoluto es enorme porque el resultado es enorme; la confiabilidad se juzga por el relativo: 3 cifras válidas.

## Fórmulas de propagación (para el análisis)
Para $f(x,y)$: $\Delta f\approx|\partial_xf|\Delta x+|\partial_yf|\Delta y$. Suma: $\Delta(x+y)=\Delta x+\Delta y$. Producto y cociente: los errores relativos se suman. Resta: el error absoluto se suma, pero el relativo se **amplifica** por $|x|/|x-y|$, que es el factor de la cancelación.

## Errores comunes
- Creer que "más decimales impresos" implica más exactitud.
- Restar dos números casi iguales obtenidos a su vez con error.
- No reordenar operaciones para evitar overflow/underflow.
- Confundir error absoluto con relativo al juzgar la confiabilidad.

## Ejercicios propuestos
1. Calcule $\sqrt{x^2+1}-x$ para $x=10^{6}$ en doble precisión y compárelo con $1/(\sqrt{x^2+1}+x)$. (Resp.: la segunda forma, $5\times10^{-7}$, evita la cancelación.)
2. ¿Cuál es el épsilon de máquina en doble precisión? (Resp.: $2^{-52}\approx2.22\times10^{-16}$.)

## Conexiones
Los errores de truncamiento reaparecen en [[Análisis Numérico - Bisección]] (criterios de parada), en el número de condición ([[Análisis Numérico - Práctica 4 Sistemas lineales]]) y en el análisis de error de [[Análisis Numérico - Integración numérica Newton-Cotes]]. Requisito previo: [[Matemática IV]].

## Fuente
`Material/Tema 1-APROXIMACIONES Y ERRORES/Practica 1 Errores.pdf` (escaneado; leídas las 2 páginas como imagen). Los datos numéricos exactos de los incisos a), c) y d) deben contrastarse con el PDF original, porque la resolución de la imagen es baja.
