---
tags: [materia, semestre-IV]
semestre: IV
---
# Estadística I

**Semestre:** [[Semestre IV]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Matemática III]]

## Desbloquea
- [[Estadística II]]
- [[Investigación de Operaciones I]]

## Apuntes

### Descripción general y objetivos

Estadística I (código 0834405T, Departamento de Matemática y Física) introduce la **estadística descriptiva, la probabilidad y las distribuciones de probabilidad**, con apoyo de Excel y software estadístico (Statgraphics). Prelación: [[Matemática III]]. Desbloquea [[Estadística II]] (inferencia) e [[Investigación de Operaciones I]].

Objetivos: organizar y resumir datos, calcular e interpretar medidas de tendencia central y dispersión, aplicar las reglas de probabilidad, y modelar fenómenos con distribuciones discretas y continuas. Los tres cortes del Material siguen ese orden (descriptiva, probabilidad, distribuciones). Verificar con el programa oficial la distribución exacta de unidades.

### Contenido programático

#### Tema 1. Estadística descriptiva
- Concepto de estadística; población (N) y muestra (n); parámetro vs. estadístico; censo.
- Variables: cualitativas; cuantitativas discretas y continuas; escalas de medición.
- Tablas de frecuencias (absoluta, relativa, acumulada), histograma, diagrama de barras, circular, Pareto.
- Medidas de tendencia central: media, mediana, moda. Posición: cuartiles, percentiles.
- Medidas de dispersión: rango, rango intercuartílico, varianza, desviación típica, coeficiente de variación.
- Diagrama de caja (boxplot), asimetría y valores atípicos.
- Uso de Excel: Análisis de datos, histograma, estadística descriptiva.

#### Tema 2. Análisis de datos con Excel
Carga del complemento "Herramientas para análisis", tablas de frecuencia con clases manuales, resumen numérico, `PROMEDIO`, `MEDIANA`, `CUARTIL.EXC`, `DESVEST`, `CONTAR`.

#### Tema 3. Probabilidad
- Experimento aleatorio, espacio muestral, eventos; operaciones entre eventos (unión, intersección, complemento).
- Axiomas de Kolmogorov; probabilidad clásica, frecuentista y subjetiva.
- Reglas de la suma y del complemento; probabilidad condicional, independencia, regla del producto.
- Teorema de la probabilidad total y **teorema de Bayes**.
- Técnicas de conteo: permutaciones y combinaciones.

#### Tema 4. Distribuciones de probabilidad
- Variable aleatoria discreta: función de masa, función acumulada, esperanza y varianza.
- **Binomial**, **Poisson**, hipergeométrica, geométrica.
- Variable continua: función de densidad; uniforme, **normal**, exponencial; estandarización y tablas Z.
- Aproximaciones (normal a la binomial) y Teorema del Límite Central (introducción).

### Conceptos clave

- **Parámetro**: valor de la población (μ, σ). **Estadístico**: valor de la muestra (x̄, s).
- **Evento mutuamente excluyente**: A ∩ B = vacío.
- **Independencia**: P(A ∩ B) = P(A) P(B).
- **Esperanza**: promedio ponderado de una variable aleatoria.

### Fórmulas

```
Media muestral:   x̄ = Σ xi / n
Varianza muestral: s² = Σ (xi - x̄)² / (n - 1)
Coef. de variación: CV = s / x̄ · 100 %
Kolmogorov: P(A) >= 0;  P(Ω) = 1;  P(A ∪ B) = P(A)+P(B) si A∩B = ∅
Unión:        P(A ∪ B) = P(A) + P(B) - P(A ∩ B)
Complemento:  P(A') = 1 - P(A)
Condicional:  P(A|B) = P(A ∩ B) / P(B)
Bayes:        P(Ai|B) = P(B|Ai) P(Ai) / Σ P(B|Aj) P(Aj)
Combinaciones: C(n,k) = n! / (k!(n-k)!)
Binomial:     P(X=x) = C(n,x) p^x (1-p)^(n-x);  μ = np;  σ² = np(1-p)
Poisson:      P(X=x) = e^(-λ) λ^x / x!;  μ = σ² = λ
Normal:       Z = (X - μ)/σ
Esperanza discreta: E(X) = Σ xi P(X=xi);  Var(X) = E(X²) - E(X)²
```

### Ejemplos resueltos

1. **Binomial** (del Material): 1/4 de los higos están contaminados; se inspeccionan 10. `X ~ Bin(10; 0,25)`. `P(X=1) = 10 · 0,25 · 0,75^9 = 0,1877`. Número esperado de contaminados: `np = 2,5`.
2. **Probabilidad condicional**: en el ejercicio de desarrolladores (100 iniciales + 50 nuevos: Front-End, Back-End, Bases de datos, Full-Stack) se calculan P(A), P(B), P(C) y combinaciones entre eventos; por ejemplo, la probabilidad de elegir a un Full-Stack es 50/150 = 1/3.
3. **Descriptiva**: datos 2, 4, 4, 6, 9: `x̄ = 5`, mediana 4, moda 4, `s² = (9+1+1+1+16)/4 = 7`, `s ≈ 2,65`.
4. **Normal**: X ~ N(100, 15). `P(X > 115) = P(Z > 1) = 0,1587`.

### Relación con otras materias

- Requiere integrales de [[Matemática III]] para variables continuas.
- Base de [[Estadística II]] (intervalos de confianza, pruebas de hipótesis, regresión) e [[Investigación de Operaciones I]] (teoría de colas y modelos probabilísticos).
- Útil en [[Análisis y Procesamiento de Datos]], [[Simulación de Sistemas]] (generación de variables aleatorias) y [[Introducción a la Inteligencia Artificial]].

### Evaluación y consejos de estudio

- Tres parciales alineados con los temas: descriptiva (trabajo en Excel, Parcial 1), probabilidad (Parcial 2) y distribuciones (Parcial 3). Ponderación exacta: verificar con el programa oficial.
- Definir siempre la variable aleatoria y su distribución antes de calcular.
- Dibujar diagramas de Venn y árboles de probabilidad.
- Usar Excel (`DISTR.BINOM.N`, `POISSON.DIST`, `DISTR.NORM.N`) y Statgraphics para verificar resultados manuales.

### Bibliografía recomendada

- Anderson, Sweeney, Williams. *Estadística aplicada a los negocios y la economía* (citada en las guías de la Profa. Mayle Leal).
- Walpole, Myers, Myers. *Probabilidad y estadística para ingeniería y ciencias*.
- Montgomery, Runger. *Probabilidad y estadística aplicadas a la ingeniería*.
- Devore, J. *Probabilidad y estadística para ingeniería y ciencias*.

### Recursos del Material/

- [Guia Resumen Tema 1.pdf](Material/Guia%20Resumen%20Tema%201.pdf): conceptos de estadística, población, muestra, variables.
- [Guia Resumen Tema 2.pdf](Material/Guia%20Resumen%20Tema%202.pdf): análisis de datos con Excel (histogramas, Pareto, resumen numérico, boxplot).
- [Guía Resumen Tema 3.pdf](Material/Gu%C3%ADa%20Resumen%20Tema%203.pdf): probabilidad, axiomas y operaciones entre eventos.
- [Trabajo estadística descriptiva (PDF)](Material/Estadistica%20Descriptiva-Parcial%201/Trabajo%20estadistica%20descriptiva-Leonardo%20Lobo%20y%20Ivan%20Mochniy.pdf) y [hoja Excel](Material/Estadistica%20Descriptiva-Parcial%201/Estadistica%20descriptiva-Leonardo%20Lobo%20y%20Ivan%20Mochniy.xlsx): estudio descriptivo con tablas y gráficos.
- [Ejercicio de Probabilidad (PDF)](Material/Probabilidad-Parcial%202/Ejercicio%20de%20Probabilidad.pdf) y su [versión docx](Material/Probabilidad-Parcial%202/Ejercicio%20de%20Probabilidad.docx): ejercicio de eventos con desarrolladores.
- [Distribuciones de Probabilidad.docx](Material/Distribuciones-Parcial%203/Distribuciones%20de%20Probabilidad.docx) y [Unidad 4.1 distribución discreta (PDF)](Material/Distribuciones-Parcial%203/Distribuci%C3%B3n_Probabilidades_U4.1_Distribucion%20discreta_contenido%20(2).pdf): binomial, esperanza y varianza.
- [Ejercicios de Estadistica.xlsx](Material/Distribuciones%20de%20Probabilidad/Ejercicios%20de%20Estadistica.xlsx): ejercicios de distribuciones en Excel.
- [video estadistica.docx](Material/3er%20parcial/video%20estadistica.docx): nota sobre el video del tercer parcial.
