---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 2- Factores y Amortización/Presentación IE-2.pdf y Tablas_de_Interes_Compuesto.pdf
---
# Ingeniería Económica - Tema 2: Factores de interés compuesto y gradientes

Materia: [[Ingeniería Económica]]
Anterior: [[Ingeniería Económica - Tema 2 Interés, tasas y equivalencia]]
Siguiente: [[Ingeniería Económica - Tema 2 Amortización de deudas]]

## Contexto y objetivo
Los **factores** convierten series de flujos en un solo valor equivalente. Cada factor se escribe $(X/Y,i\%,n)$: "hallar X dado Y". Se evalúan con fórmula o con tablas (ver [[Ingeniería Económica - Tablas de interés compuesto]]).

## Deducciones
**F/P y P/F.** Un pago único crece $F=P(1+i)^n$, por tanto $P=F(1+i)^{-n}$.

**F/A (serie uniforme).** Con $A$ al final de cada período 1..n: $F=A[(1+i)^{n-1}+\dots+(1+i)+1]$. Multiplicando por $(1+i)$ y restando: $F(1+i)-F=A(1+i)^n-A$, luego
$$F=A\frac{(1+i)^n-1}{i},\qquad A=F\frac{i}{(1+i)^n-1}\ (\text{fondo de amortización}).$$

**P/A.** $P=F(1+i)^{-n}$ con la F anterior:
$$P=A\frac{(1+i)^n-1}{i(1+i)^n},\qquad A=P\frac{i(1+i)^n}{(1+i)^n-1}\ (\text{recuperación de capital}).$$

**Gradiente aritmético.** Serie $0,g,2g,\dots,(n-1)g$. Su equivalente uniforme:
$$A=g\left[\frac1i-\frac{n}{(1+i)^n-1}\right]=g\,(A/g,i,n),\qquad P=A\,(P/A,i,n).$$
Si los flujos son $A_1,A_1+g,\dots$: se descompone en una serie uniforme $A_1$ más el gradiente.

| Factor | Hallar | Dado | Expresión |
|---|---|---|---|
| (F/P,i,n) | F | P | $(1+i)^n$ |
| (P/F,i,n) | P | F | $(1+i)^{-n}$ |
| (F/A,i,n) | F | A | $[(1+i)^n-1]/i$ |
| (A/F,i,n) | A | F | $i/[(1+i)^n-1]$ |
| (P/A,i,n) | P | A | $[(1+i)^n-1]/[i(1+i)^n]$ |
| (A/P,i,n) | A | P | $i(1+i)^n/[(1+i)^n-1]$ |
| (A/g,i,n) | A | g | $1/i-n/[(1+i)^n-1]$ |

Nota: la presentación escribe el factor P/F a interés simple como $P=F(1+ni)^{-1}$ (la forma "P=F(1+(i*n))^n" que aparece en la tabla resumen de las diapositivas es un error tipográfico; el correcto a interés compuesto es $(1+i)^{-n}$).

## Ejemplos de la presentación (con tablas)
1. 60.000 Bs al 6% durante 10 años: $F=60.000(F/P,6\%,10)=60.000(1{,}791)=107.460$ Bs.
2. Para tener 180.000 en 12 años al 10%: $P=180.000(0{,}3186)=57.348$ Bs.
3. Depósitos de 5.000/año, 5 años, 5%: $F=5.000(5{,}526)=27.630$ Bs.
4. Formar 28.000 en 4 años al 15%: $A=28.000(0{,}2003)=5.608{,}4$ Bs/año.
5. Préstamo pagado con 2.300/mes durante 24 meses al 2% mensual: $P=2.300(18{,}914)=43.502{,}2$ Bs.
6. Inversión 100.000 al 8%, 10 años: $A=100.000(0{,}1490)=14.900$ Bs/año.
7. Gradiente: costos de operación 10.000, +1.000 por año, 6 años, 10%: $A=1.000(A/g,10\%,6)=1.000(2{,}330)$ (con fórmula 2,2236 daría 2.223,6; la tabla usada en clase da 2.330; ver nota) y $C_{op}=10.000+2.330=12.330$ Bs/año.

> Nota de verificación: con la fórmula exacta $(A/g,10\%,6)=2{,}2236$, no 2,330. La diferencia (~4%) parece ser una lectura de tabla en la presentación; verificar con la tabla oficial. Para exámenes use el valor de la tabla del curso.

## Ejemplo propio paso a paso (gradiente)
Una máquina tiene costos de 40.000 el primer año, que aumentan 5.000 anuales durante 10 años; $i=15\%$. $(A/g,15\%,10)=1/0{,}15-10/(1{,}15^{10}-1)=6{,}667-3{,}2955=3{,}3715$. $A=40.000+5.000(3{,}3715)=56.857$. (La guía da 56.915 por redondeo de tablas.)

## Errores comunes
- Aplicar P/A cuando el primer pago ocurre en $t=0$ (anualidad anticipada): se debe sumar el primer pago.
- En gradientes, el primer término del gradiente (0) cae en $t=1$: la serie de gradiente tiene $n$ períodos y el primer incremento aparece en $t=2$.
- Usar $n$ de la serie uniforme en lugar de $n$ del gradiente.

## Ejercicios propuestos
1. ¿Cuánto vale hoy una serie de 1.000/año por 8 años al 12%? (Resp.: 4.967,64.)
2. ¿Depósito anual para reunir 50.000 en 6 años al 9%? (Resp.: 6.645,6.)
3. Ingresos 15.000 que disminuyen 3.000 anuales durante 5 años al 15%: P. (Resp.: $A=15.000-3.000(1{,}7228)=9.831$; $P=9.831(3{,}3522)\approx 32.955$.)

## Conexiones
[[Fórmulas de Matemática Financiera]], [[Matemática II]] (series geométricas), [[Finanzas para Ingenieros]].

## Fuente
`Presentación IE-2.pdf`; deducciones y ejemplos 8-10 son desarrollo propio.
