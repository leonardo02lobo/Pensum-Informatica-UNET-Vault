---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 2- Factores y Amortización/Presentación IE-2.pdf (parte de amortización)
---
# Ingeniería Económica - Tema 2: Amortización de deudas

Materia: [[Ingeniería Económica]]
Anterior: [[Ingeniería Económica - Tema 2 Factores de interés compuesto y gradientes]]
Siguiente: [[Ingeniería Económica - Tablas de interés compuesto]]

## Contexto y objetivo
**Amortizar** una deuda es pagar todas las obligaciones derivadas de ella: el capital (principal) y los intereses. El pago periódico se llama **cuota de amortización**. Partes: *prestatario* (recibe el dinero y paga interés) y *prestamista*. El Tema 2 enseña a armar la **tabla de amortización** y a tratar casos especiales: períodos de gracia y muertos, cuotas extras y amortización constante de capital.

## Conceptos
- **Período de gracia:** durante cierto tiempo se pagan solo los intereses; la deuda permanece constante.
- **Período muerto:** no hay pagos; los intereses se acumulan y la deuda **crece** $P(1+i)^k$.
- **Cuota uniforme (sistema francés):** $A=P\,(A/P,i,n)$ constante; el interés baja y la amortización de capital sube cada período.
- **Amortización constante (sistema alemán):** amortización de capital $=P/n$ fija; la cuota baja con el tiempo.

## Formato de la tabla (columnas)
(1) Período; (2) capital pendiente al inicio; (3) cuota; interés $=i\times(2)$; (4) amortización de principal $=(3)-\text{interés}$; (5) capital pendiente al final $=(2)-(4)$. Control: el saldo final del último período debe ser 0 (la presentación obtiene 27,18 por redondeo).

## Ejemplo 1 (cuota uniforme, resuelto)
Préstamo de 100.000 al 10% anual en 4 cuotas anuales. $A=100.000(A/P,10\%,4)=31.547{,}08$.

| Año | Saldo inicial | Cuota | Interés | Amortización | Saldo final |
|---|---|---|---|---|---|
| 1 | 100.000,00 | 31.547,08 | 10.000,00 | 21.547,08 | 78.452,92 |
| 2 | 78.452,92 | 31.547,08 | 7.845,29 | 23.701,79 | 54.751,13 |
| 3 | 54.751,13 | 31.547,08 | 5.475,11 | 26.071,97 | 28.679,16 |
| 4 | 28.679,16 | 31.547,08 | 2.867,92 | 28.679,16 | 0 |

Verificación: la suma de amortizaciones es 100.000 y los intereses totales son 26.188,32.

## Ejemplo 2 (de la presentación): pagos extra pactados
Deuda de 600.000 en 8 trimestres, con pagos extra de 80.000 (trimestre 3) y 100.000 (trimestre 5). La cuota ordinaria resulta 85.498,46 y la tabla muestra cuotas de 165.498,46 y 185.498,46 en esos trimestres; el saldo del final queda en ≈0 (27,18 por redondeo). El interés del período 1 es 54.000, lo que implica una tasa de 9% trimestral.

## Ejemplo 3: cuota extra no pactada
Deuda 1.800.000 en 6 pagos semestrales al 20% capitalizado semestralmente ($i=10\%$). Cuota: $A=1.800.000(0{,}2296)=413.280$. En el pago 3 se abona un extra de 780.000 (cuota 3 = 1.193.280). Saldo tras el pago 3: 247.843,20. Dos opciones:
- **a) Reliquidar la cuota** conservando el plazo: $A'=247.843{,}20\,(A/P,10\%,3)=99.657{,}75$ para los períodos 4-6.
- **b) Mantener la cuota y acortar el plazo:** en el período 4 se paga interés 24.784,32 + saldo 247.843,20 = 272.627,50 y la deuda termina en 4 pagos.

## Ejemplo 4: amortización constante con año de gracia
Crédito de 500.000 a 6 años, primer año de gracia, interés 30%, amortización igual de principal en los 5 años restantes: $500.000/5=100.000$.
- Año 1 (gracia): cuota = interés 150.000, saldo 500.000.
- Año 2: interés 150.000 + amortización 100.000 = 250.000; saldo 400.000.
- Última cuota (año 6): interés $100.000\times0{,}30=30.000$ + amortización 100.000 = 130.000.

## Ejemplo propio: período muerto
Se piden 10.000 al 2% mensual con 3 meses muertos y 12 cuotas mensuales posteriores. Deuda al fin del período muerto: $10.000(1{,}02)^3=10.612{,}08$. Cuota: $10.612{,}08(A/P,2\%,12)=10.612{,}08(0{,}09456)=1.003{,}5$.

## Errores comunes
- Confundir período de gracia (se pagan intereses) con muerto (se capitalizan).
- Reliquidar usando el capital inicial en vez del saldo vigente.
- Usar la tasa anual con cuotas semestrales o mensuales.

## Ejercicios propuestos
1. Tabla de un préstamo de 50.000 al 12% anual en 3 cuotas anuales iguales. (Resp.: A=20.817,45.)
2. Con amortización constante, 90.000 en 3 años al 10%: cuotas. (Resp.: 39.000, 36.000, 33.000.)

## Conexiones
[[Ingeniería Económica - Guía de ejercicios Tema 2 resuelta]], [[Finanzas para Ingenieros]] (PAGO, PAGOINT, PAGOPRIN en Excel), [[Fórmulas de Matemática Financiera]].

## Fuente
`Presentación IE-2.pdf`, diapositivas de amortización; ejemplos 1 y de período muerto son propios.
