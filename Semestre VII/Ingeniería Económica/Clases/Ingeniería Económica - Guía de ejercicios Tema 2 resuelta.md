---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 2- Factores y Amortización/guia ejercicios 1-1.pdf
---
# Ingeniería Económica - Guía de ejercicios Tema 2 resuelta

Materia: [[Ingeniería Económica]]
Anterior: [[Ingeniería Económica - Tablas de interés compuesto]]
Siguiente: [[Ingeniería Económica - Parcial 1 resuelto]]

## Contexto
"Guía Ingeniería Económica y Análisis Económico - Primer Parcial" (UNET, Núcleo de Técnicas Cuantitativas): 44 problemas con respuesta. Aquí se resuelven paso a paso los más representativos y se verifica la respuesta de la guía por fórmula. Los demás se listan con su respuesta oficial.

## Problemas resueltos
**P1.** $F=1.000(1{,}06)^{12}=2.012{,}20$. Guía: 2.012. ✓

**P2.** 6% compuesto trimestralmente → $i=1{,}5\%$ trimestral. Para ganar 100 sobre 300: $300(1{,}015)^n=400$; $n=\ln(4/3)/\ln1{,}015=19{,}3$ → 19 trimestres (guía: 19).

**P3.** $i_{ef}=19{,}56\%$, $m=12$: $i_n=12[(1{,}1956)^{1/12}-1]=18{,}0\%$ capitalizado mensualmente. ✓

**P4.** 200 → 212,64 en un año con interés mensual: $i_{mens}=(1{,}0632)^{1/12}-1=0{,}512\%$; efectiva anual $=6{,}32\%$. La guía indica 6,16%; con los datos dados la fórmula da 6,32% (verificar el enunciado; 6,16% corresponde a otro balance, p. ej. 212,32).

**P5.** $P=75\text{ M}/(1{,}18)^2=53{,}86\text{ M}$ (guía 53.865.000 ✓).

**P6.** 50 aviones × 20 M = 1.000 M de costo al final del trimestre 1 (mes 3); $i=1{,}5\%$ mensual: $P_0=1.000/(1{,}015)^3=956{,}3$ M. La guía publica 95.630.000, que parece omitir un cero (verificar).

**P7.** $1.000=238{,}50\,(P/A,i,10)$ → $(A/P,i,10)=0{,}2385$ → $i=20\%$ ✓.

**P8.** Fondo 30.000 al 7%: $F_5=30.000(1{,}07)^5-10.000(1{,}07)^3-15.000(1{,}07)=42.076{,}55-12.250{,}43-16.050=13.776{,}1$. La guía dice 13.790 (diferencia por tablas) y etiqueta "F6" por error tipográfico.

**P9.** $P=2.215{,}17\,(P/A,3\%,6)=2.215{,}17(5{,}4172)=12.000$ ✓.

**P10a.** Primera cuota al final del mes 5 → la serie arranca en $t=5$, así que se lleva el precio a $t=4$: $12.000(1{,}03)^4=13.506{,}1$; $A=13.506{,}1(A/P,3\%,6)=2.493{,}2$ (guía 2.494,25 con tablas).
**P10b.** Pagos en 1-3 y 8-10: $12.000=A[(P/A,3\%,3)+(P/A,3\%,3)(P/F,3\%,7)]$ → $A=12.000/(2{,}8286+2{,}8286\cdot0{,}8131)=2.339{,}9$ (guía 2.339,52).

**P11.** 1.000/mes meses 1-6 al 2%: $F_6=1.000(F/A,2\%,6)=6.308{,}1$; a $t=9$: $\times1{,}02^3=6.694{,}2$ (guía 6.692,79).

**P13.** Cuota inicial $A=10.000(A/P,3\%,24)=590{,}47$. Saldo tras la cuota 10 (quedan 14): $590{,}47(P/A,3\%,14)=6.670{,}0$. Nueva cuota al 2%: $6.670{,}0(A/P,2\%,14)=551{,}0$ (guía 551,48).

**P36 (gradiente).** Herencia 100.000: retiros 10.000, 11.000,... durante 18 años. $100.000=10.000(P/A,i,18)+1.000(P/G,i,18)$; por tanteo $i=13{,}8\approx14\%$ ✓.

**P38.** Ingresos 15.000, 12.000, 9.000... 6 años al 15%: $A=15.000-3.000(A/g,15\%,6)=8.708{,}4$; $P_0=8.708{,}4(P/A,15\%,6)=32.957$ (guía 32.949 ✓).

**P42.** Costos 40.000 + 5.000 por año, 10 años, 15%: $A=40.000+5.000(A/g,15\%,10)=40.000+5.000(3{,}3832)=56.916$ ✓ (guía 56.915).

**P41 (comparación de planes).** Plan 1: pago inmediato 10.000. Plan 2: pagos al *inicio* de cada año 1.200, +100 anual, 10 años al 12%. Guía: $P_0=9.862{,}05<10.000$ → elegir el plan 2.

## Problemas con respuesta oficial (no re-derivados)
P12 última cuota 1/08/2013; P14-P35 (retiros trimestrales, fondos, arrendamiento financiero P35 $P_0=124.683{,}5$); P37 $A=472{,}11$; P39 $P_0=7.026.200$, $A=909.892{,}9$; P40 7 meses; P43 $F_8=-17.966.600{,}61$ Bs; P44 (fondo de 20 millones a 5 años con depósitos crecientes; el texto de la respuesta está truncado en el PDF extraído). Las páginas centrales del PDF extraído quedaron truncadas; ver el original.

## Estrategia general
1. Dibuje el diagrama. 2. Unifique $i$ y $n$. 3. Ubique $t=0$ de la serie (el factor P/A da el valor un período antes del primer pago). 4. Traslade con P/F o F/P. 5. Verifique con la tabla.

## Errores comunes
Calcular P/A con el primer pago en $t=5$ sin trasladar; omitir que "n" en gradientes cuenta el período 0 del gradiente; redondear factores antes de multiplicar.

## Ejercicios propuestos
1. Reproduzca P10a con tablas y compare. 2. Plantee P37 con ecuación de equivalencia en $t=15$.

## Conexiones
[[Ingeniería Económica - Tema 2 Factores de interés compuesto y gradientes]], [[Ingeniería Económica - Tema 2 Amortización de deudas]], [[Fórmulas de Matemática Financiera]].

## Fuente
`guia ejercicios 1-1.pdf` (44 problemas; parte central del texto truncada en la extracción).
