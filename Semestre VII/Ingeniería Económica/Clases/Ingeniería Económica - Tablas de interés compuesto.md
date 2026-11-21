---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 2- Factores y Amortización/Tablas_de_Interes_Compuesto.pdf
---
# Ingeniería Económica - Tablas de interés compuesto

Materia: [[Ingeniería Económica]]
Anterior: [[Ingeniería Económica - Tema 2 Amortización de deudas]]
Siguiente: [[Ingeniería Económica - Guía de ejercicios Tema 2 resuelta]]

## Contexto y objetivo
`Tablas_de_Interes_Compuesto.pdf` es el Apéndice B ("Compound Interest Tables") de un texto de ingeniería económica en inglés (el encabezado del archivo indica *newn42040_appB*, formato de la obra de Newnan; verificar edición). Contiene, para cada tasa tabulada, ocho factores en función de $n$. Es el recurso permitido para resolver los ejercicios del curso en lugar de la calculadora financiera.

## Estructura
- **Tasas tabuladas** (porcentaje por período): 1/4, 1/2, 3/4, 1, 1 1/4, 1 1/2, 1 3/4, 2, 2 1/2, 3, 3 1/2, 4, 4 1/2, 5, 6, 7, 8, 9, 10, 12, 15, 18, 20, 25, 30, 35, 40, 45, 50 y 60%.
- **Columnas** (en inglés → español):
  - Single Payment: Compound Amount F/P (capitalización) y Present Worth P/F (actualización).
  - Uniform Payment Series: Sinking Fund A/F, Capital Recovery A/P, Compound Amount F/A, Present Worth P/A.
  - Arithmetic Gradient: Gradient Uniform Series A/G y Gradient Present Worth P/G.
- **Filas:** $n=1,2,\dots$ hasta valores grandes.
- **Caso $n\to\infty$** (primera página): $(F/P)=\infty$, $(P/F)=0$, $(A/F)=0$, $(A/P)=i$, $(F/A)=\infty$, $(P/A)=1/i$, $(A/G)=1/i$, $(P/G)=1/i^2$. Es la base del **equivalente capitalizado** $EC=A/i$ ([[Ingeniería Económica - Tema 3 Comparación de alternativas, costos y proyectos públicos]]).

## Cómo usarlas (procedimiento)
1. Identifique qué se da y qué se pide (P, F, A o G).
2. Elija el factor $(X/Y,i,n)$.
3. Ubique la página de la tasa por período $i$ (no la anual si los períodos son meses).
4. Lea la fila $n$ y la columna del factor.
5. Multiplique por el dato.

Ejemplo de lectura (tabla del 1/4%): $n=6$: F/P 1,015; P/F 0,9851; A/F 0,1656; A/P 0,1681; F/A 6,038; P/A 5,948; A/G 2,498; P/G 14,861. Del 6%, $n=10$: F/P 1,791 (usado en la presentación para 60.000 Bs).

## Interpolación
Para tasas no tabuladas (p. ej. TIR): se evalúa el VA en dos tasas que lo encierren y se interpola linealmente:
$$i^*\approx i_1+(i_2-i_1)\frac{VA(i_1)}{VA(i_1)-VA(i_2)}.$$
Ejemplo: $VA(15\%)=+4.000$ y $VA(20\%)=-2.000$ → $i^*\approx15+5\cdot\frac{4}{6}=18{,}33\%$ (aproximación; la exacta se obtiene por tanteo).

## Limitaciones y errores comunes
- Las tablas tienen 3-4 decimales: los resultados difieren en centésimas respecto a la fórmula (la guía de ejercicios ya lo refleja: 2.494,25 vs 2.493,19 en un mismo problema).
- Usar la tabla de la tasa anual con períodos mensuales.
- Confundir A/F (fondo de amortización) con A/P (recuperación de capital).

## Ejercicios propuestos
1. Con tablas: $P=2.000$ al 5%, $n=8$; hallar F. (F/P=1,477 → 2.954.)
2. Calcule $(P/A,8\%,10)$ por fórmula y compare con 6,710.
(Resp. 2: $[(1{,}08)^{10}-1]/(0{,}08\cdot1{,}08^{10})=6{,}7101$.)

## Conexiones
[[Ingeniería Económica - Tema 2 Factores de interés compuesto y gradientes]], [[Fórmulas de Matemática Financiera]].

## Fuente
`Tablas_de_Interes_Compuesto.pdf` (≈1.700 líneas de texto extraído; se revisó su estructura y las primeras tablas, no se transcribieron los valores).
