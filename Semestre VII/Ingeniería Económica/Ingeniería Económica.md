---
tags: [materia, semestre-VII]
semestre: VII
---
# Ingeniería Económica

**Semestre:** [[Semestre VII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Economía]]

## Desbloquea
- [[Finanzas para Ingenieros]]

## Apuntes

### Descripción general y objetivos
Ingeniería Económica (dictada por el Núcleo de Técnicas Cuantitativas, Departamento de Ingeniería Industrial de la UNET, según el material) es la disciplina que **mide por anticipado la rentabilidad de proyectos de inversión** para recomendar la selección de inversiones con criterio económico. Se apoya en el **valor del dinero en el tiempo**. Prerrequisito: [[Economía]]; desbloquea [[Finanzas para Ingenieros]]. Fórmulas y ejercicios resumidos en [[Fórmulas de Matemática Financiera]].

### Contenido programático (según los 7 temas del Material)
1. **Introducción a la matemática financiera**: enfoque sistémico de la empresa, flujos monetarios, diagramas de flujo de caja, interés simple y compuesto, tasa nominal y efectiva, equivalencia.
2. **Factores y amortización**: factores F/P, P/F, F/A, A/F, P/A, A/P, gradientes (aritmético y geométrico), amortización de deudas, tablas de interés compuesto.
3. **Rentabilidad de un proyecto y decisión entre proyectos (parte I)**: proyectos privados y públicos; Valor Actual (VA), Equivalente Anual (EA), TIR, relación Beneficio/Costo; tasa mínima de rendimiento.
4. **Parte II**: proyectos con solo costos (VA es costo total), vida infinita (**equivalente capitalizado**), alternativas mutuamente excluyentes con vidas iguales y distintas, análisis incremental, análisis costo-beneficio.
5. **Reemplazo de equipos**: alternativas mutuamente excluyentes, reducción de costos, vidas distintas (usar Equivalente Anual), vida económica, defensor vs retador; **depreciación e impuesto sobre la renta**.
6. **Rentabilidad después de impuesto**: ISR, depreciación (línea recta, saldo decreciente, SMA/unidades producidas), flujo de caja neto, **inflación** y devaluación (caso de Venezuela como inflación mediana).
7. **Riesgo e incertidumbre**: **análisis de sensibilidad** (variables críticas, decisión sensible), escenarios, árboles y valor esperado.

### Conceptos clave
- **Flujo monetario Fₜ**: entradas (+) y salidas (-) en el instante t; t=0 es el inicio del período 1.
- **TMR/imin**: tasa mínima de rendimiento exigida al inversionista.
- **VA (i) > 0**: el proyecto supera la tasa mínima; **= 0** la iguala; **< 0** pierde.
- **TIR**: tasa que hace VA = 0; no existe en proyectos de solo costos.
- **Equivalente capitalizado**: VA con vida infinita, EC = A/i.
- **Vida económica**: duración que minimiza el costo anual equivalente.
- **Análisis de sensibilidad**: cambia una variable crítica a la vez (independencia) manteniendo el resto; **no es un modelo de decisión**.
- **Tasa real vs aparente**: (1+i_ap) = (1+i_real)(1+f).

### Fórmulas esenciales
```
F = P(1+i)^n           P = F/(1+i)^n
F = A[((1+i)^n - 1)/i]            A = F[i/((1+i)^n - 1)]
P = A[((1+i)^n - 1)/(i(1+i)^n)]   A = P[i(1+i)^n/((1+i)^n - 1)]
i_ef = (1 + i_nom/m)^m - 1
EC = A/i        EA = VA·[i(1+i)^n/((1+i)^n - 1)]
Depreciación línea recta: D = (CI - VS)/n
ISR_t = T·(ingreso neto gravable_t)
```

### Ejemplos resueltos
- Capitalización: $1.000 al 6 % efectivo anual durante 12 años: F = 1000(1,06)^12 = $2.012 (resultado de la guía del Tema 2).
- Tasa nominal: i efectiva anual 19,56 % con 12 capitalizaciones: i_nom = 12[(1,1956)^(1/12) - 1] = 18 % nominal compuesto mensualmente.
- VA: inversión 10.000, flujos 3.000 durante 5 años, i = 10 %: VA = -10.000 + 3.000(3,7908) = +1.372 → conviene.
- Reemplazo: comparar EA del defensor (valor de rescate actual, costos crecientes) contra EA del retador en su vida económica.

### Cómo se relaciona con otras materias
[[Economía]] (conceptos de capital, oferta y demanda), [[Matemática I]]/[[Matemática II]] (series y límites, exponenciales), [[Estadística I]] (valor esperado en riesgo), [[Gerencia de Proyectos]] (evaluación de proyectos), [[Formación de Emprendedores]]; continúa en [[Finanzas para Ingenieros]]. Se complementa con [[Investigación de Operaciones II]] (inventarios y decisiones bajo incertidumbre).

### Evaluación y consejos de estudio
El material incluye un **Parcial 1** resuelto por el estudiante (Tema 2) y guías de ejercicios con respuestas por tema; la evaluación es por parciales y tareas (verificar ponderaciones con el programa oficial). Consejos: dibuje siempre el diagrama de flujo; use la tasa y el período en las mismas unidades; verifique con tablas de interés; en reemplazo, compare por EA; no olvide impuestos e inflación al final.

### Bibliografía recomendada
- Blank, L. y Tarquin, A. *Ingeniería Económica*.
- Baca Urbina, G. *Evaluación de Proyectos*.
- Sapag Chain, N. *Preparación y Evaluación de Proyectos*.
- Notas del Núcleo de Técnicas Cuantitativas (Giugni; Alvarado y Betancourt, citados en las láminas).

### Recursos del Material/ (por tema)
**Tema 1** [Ingeniería Económica.pdf](Material/Tema%201-Introducción%20a%20la%20Matemática%20Financiera/Ingeniería%20Económica.pdf) (láminas introductorias) y `Tema 1-Tarea.docx`.
**Tema 2** [Presentación IE-2.pdf](Material/Tema%202-%20Factores%20y%20Amortización/Presentación%20IE-2.pdf), [guia ejercicios 1-1.pdf](Material/Tema%202-%20Factores%20y%20Amortización/guia%20ejercicios%201-1.pdf), [Tablas_de_Interes_Compuesto.pdf](Material/Tema%202-%20Factores%20y%20Amortización/Tablas_de_Interes_Compuesto.pdf), `Leonardo Lobo.pdf` y carpeta `Parcial 1` (parcial resuelto, .docx y .pdf).
**Temas 3 y 4** `Rentabilidad de Proyecto I.pdf`, `Rentabilidad de Proyecto II.pdf`, `Articulo Analisis Coste Beneficio.pdf`, `Guía de Ejercicios Tema 3.pdf`, `Guía de Ejercicios Tema 4-6.pdf` y tareas resueltas.
**Tema 5** `Reemplazo de Equipos.pdf`, `Impuesto Sobre la Renta - Depreciación.pdf` y sus guías de ejercicios.
**Tema 6** artículos sobre inflación (`Qué es la Inflación.pdf`, `La Inflación y disponibilidad de efectivo...pdf`, `Venezuela un caso de inflación mediana.pdf`).
**Tema 7** [Analisis de Sensibilidad.pdf](Material/Tema%207-Riesgo%20e%20incertidumbre%20en%20la%20evaluación%20económica%20de%20proyectos%20de%20inversión/Analisis%20de%20Sensibilidad.pdf).
