---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 2- Factores y Amortización/Presentación IE-2.pdf (primera parte)
---
# Ingeniería Económica - Tema 2: Interés, tasas y equivalencia

Materia: [[Ingeniería Económica]]
Anterior: [[Ingeniería Económica - Tema 1 Enfoque sistémico y flujos monetarios]]
Siguiente: [[Ingeniería Económica - Tema 2 Factores de interés compuesto y gradientes]]

## Contexto y objetivo
La presentación IE-2 abre con los conceptos de interés, costo de capital y tasa mínima de rendimiento, y las dos formas de calcular intereses. Es la base del **valor del dinero en el tiempo**: un bolívar hoy vale más que un bolívar mañana porque puede invertirse.

## Definiciones
- **Interés:** manifestación del valor del dinero en el tiempo; diferencia entre una cantidad final y la original. Interés pagado = cantidad que se debe ahora - cantidad original (préstamo); interés ganado = cantidad total actual - cantidad original (ahorro).
- **Tasa de interés** $i=\dfrac{\text{interés acumulado por unidad de tiempo}}{\text{suma original}}\times 100$. La unidad de tiempo es el *período de interés*.
- **Costo de capital (CC):** lo que cuesta usar un capital. Con capital propio $C_p$ (costo de oportunidad $i_p$) y deuda $C_d$ (tasa activa $i_d$):
$$CC=\frac{C_p\,i_p+C_d\,i_d}{C_p+C_d}$$
- **Tasa mínima de rendimiento (TMR o $i_{min}$):** menor rendimiento aceptable; $TMR\ge CC$, típicamente $TMR=CC+\text{riesgo}$.

Ejemplo: proyecto con 60% de capital propio (costo de oportunidad 15%) y 40% de deuda al 24%: $CC=0{,}6(15)+0{,}4(24)=18{,}6\%$. Con prima de riesgo de 4%, $TMR=22{,}6\%$.

## Interés simple vs compuesto
- **Simple:** el interés se calcula siempre sobre el capital inicial: $F=P(1+ni)$. Crece linealmente (1000 al 10%: 1100, 1200, 1300...). Se usa en operaciones menores de un año.
- **Compuesto:** el interés se calcula sobre el capital acumulado: $F=P(1+i)^n$ (1000 al 10%: 1100, 1210, 1331...). Es el que se usa en ingeniería económica.
- **Capitalización:** llevar una cantidad al futuro; **actualización (descuento):** traerla al presente, $P=F(1+i)^{-n}$.

## Tasa efectiva y nominal
- **Efectiva ($i_e$):** la que realmente se carga en el período considerando la acumulación de intereses.
- **Nominal ($i_n$):** expresión anual de una tasa de período menor al año: $i_n=i_e\cdot m$ (m períodos por año). Ej.: 4% trimestral equivale a 16% nominal capitalizado trimestralmente; 6% semestral = 12% nominal capitalizado semestralmente.
- **Equivalencia entre efectivas:** $(1+i_{anual})=(1+i_{mensual})^{12}$, es decir $i_{anual}=(1+i_{mens})^{12}-1$. En general $i_{ef}=(1+i_n/m)^m-1$.

### Ejemplo A: de nominal a efectiva
18% nominal capitalizado mensualmente: $i_{mens}=1{,}5\%$, $i_{ef}=1{,}015^{12}-1=19{,}56\%$ (es el problema 3 de la guía, al revés; ver [[Ingeniería Económica - Guía de ejercicios Tema 2 resuelta]]).

### Ejemplo B: tasa mensual a partir de un crecimiento
200 crecen a 212,64 en un año con capitalización mensual: $i_{mens}=(212{,}64/200)^{1/12}-1=0{,}512\%$ y $i_{ef}=6{,}32\%$ anual.

## Símbolos del tema
$P$: suma en el presente; $F$: suma en el período $n$; $A$: cuota de una serie uniforme al final de cada período; $g$: gradiente aritmético; $n$: número de períodos; $i$: tasa por período. Regla de oro: **$i$ y $n$ deben estar en la misma unidad de tiempo**.

## Errores comunes
- Dividir la tasa efectiva anual entre 12 (solo vale para la nominal).
- Usar interés simple en horizontes largos.
- Mezclar $n$ en años con $i$ mensual.

## Ejercicios propuestos
1. ¿Efectiva anual de 24% nominal capitalizado trimestralmente? (Resp.: $1{,}06^4-1=26{,}25\%$.)
2. 5.000 al 8% simple durante 3 años y al 8% compuesto. (Resp.: 6.200 y 6.298,56.)
3. Capital propio 300 al 12% y deuda 200 al 20%: CC. (Resp.: 15,2%.)

## Conexiones
[[Fórmulas de Matemática Financiera]], [[Economía]], [[Finanzas para Ingenieros]] (funciones financieras en Excel).

## Fuente
Presentación `Presentación IE-2.pdf`, diapositivas de flujos monetarios, interés, costo de capital, tasas. Ejemplos A, B y de CC: resolución propia con las fórmulas de la presentación.
