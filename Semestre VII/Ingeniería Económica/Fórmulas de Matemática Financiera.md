---
tags: [tema, semestre-VII]
semestre: VII
---
# Fórmulas de Matemática Financiera

Nota hija de [[Ingeniería Económica]]; útil también en [[Finanzas para Ingenieros]].

## Interés
- Simple: F = P(1 + in). Compuesto: F = P(1 + i)ⁿ.
- Nominal a efectivo: i_ef = (1 + r/m)^m − 1. Efectiva a nominal: r = m[(1 + i_ef)^(1/m) − 1].
- Continuo: i_ef = e^r − 1.

## Factores (notación estándar)
| Factor | Fórmula | Convierte |
|---|---|---|
| (F/P, i, n) | (1+i)ⁿ | P a F |
| (P/F, i, n) | 1/(1+i)ⁿ | F a P |
| (F/A, i, n) | ((1+i)ⁿ − 1)/i | A a F |
| (A/F, i, n) | i/((1+i)ⁿ − 1) | F a A |
| (P/A, i, n) | ((1+i)ⁿ − 1)/(i(1+i)ⁿ) | A a P |
| (A/P, i, n) | i(1+i)ⁿ/((1+i)ⁿ − 1) | P a A |

Gradiente aritmético: P = G/i · [ (P/A,i,n) − n/(1+i)ⁿ ]; A = G[1/i − n/((1+i)ⁿ − 1)].
Gradiente geométrico (g ≠ i): P = A₁[1 − ((1+g)/(1+i))ⁿ]/(i − g).

## Criterios de rentabilidad
- VA(i) = Σ Fₜ/(1+i)ᵗ. EA = VA·(A/P, i, n). EC = A/i.
- TIR: i* tal que VA(i*) = 0 (interpolar o iterar). Aceptar si TIR > TMR.
- B/C = VA(beneficios)/VA(costos); aceptar si > 1.
- Alternativas excluyentes: comparar VA o EA; con TIR usar análisis **incremental**.

## Amortización (cuota fija)
Cuota A = P(A/P, i, n); interés del período = i·saldo; abono a capital = A − interés.

## Depreciación e impuesto
Línea recta D = (CI − VS)/n. Saldo decreciente d = 1 − (VS/CI)^(1/n). Flujo después de impuesto: FCND = FCAI − ISR, con ISR = T·(ING − depreciación).

## Inflación
(1 + i_ap) = (1 + i_real)(1 + f). Convertir flujos corrientes a constantes dividiendo entre (1+f)ᵗ.

## Ejemplo
Préstamo 5.000 al 12 % anual, 4 años: A = 5000·(0,3292) = 1.646,2 por año; primer año interés 600, capital 1.046,2.
