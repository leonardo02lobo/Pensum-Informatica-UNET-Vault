---
tags: [tema, semestre-V]
---
# Contraste de hipótesis y pruebas Ji cuadrada

Nota hija de [[Estadística II]] (Unidades II y III).

## Estructura de un contraste
1. **H0**: afirmación con igualdad (p. ej. μ = 68; μ1 = μ2; σ1² = σ2²; X ~ Normal). **H1**: negación.
2. Nivel de significancia α (probabilidad del error tipo I).
3. Estadístico de prueba y su distribución (z, t, χ², F).
4. Región de rechazo (una o dos colas).
5. Decisión y conclusión.

|  | H0 verdadera | H0 falsa |
|---|---|---|
| Se rechaza H0 | Error tipo I (α) | Decisión correcta (1-β) |
| No se rechaza | Decisión correcta | Error tipo II (β) |

## Aplicaciones de la ji cuadrada (Guía III-A)
- **Bondad de ajuste**: ¿la población sigue una distribución dada? `χ²=Σ(o-e)²/e`, g.l. `k-1-m` (m parámetros estimados). Regla: frecuencias esperadas ≥ 5.
- **Independencia**: tabla de contingencia f×c; `e_ij = (fila_i · col_j)/N`; g.l. `(f-1)(c-1)`.
- **Homogeneidad**: mismo cálculo, comparando la distribución de una variable en varias poblaciones.

## Ejemplo (independencia)
Tabla 2×2: [30 20; 20 30], N=100. Esperadas = 25 en cada celda. `χ² = 4·(25/25) = 4`, g.l.=1, crítico 3.84 (α=0.05): se rechaza independencia.

## ANDEVA y comparaciones múltiples
Si el F del ANDEVA es significativo se aplican pruebas posteriores como **Duncan** (tabla en el Material) para ver qué medias difieren.
