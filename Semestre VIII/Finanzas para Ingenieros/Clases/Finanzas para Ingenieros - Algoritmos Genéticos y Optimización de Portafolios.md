---
tags: [clase, semestre-VIII]
materia: Finanzas para Ingenieros
---
# Finanzas para Ingenieros - Algoritmos Genéticos y Optimización de Portafolios

Materia: [[Finanzas para Ingenieros]]
Anterior: [[Finanzas para Ingenieros - Rendimiento, Riesgo y Teoría de Portafolios de Markowitz]]
Siguiente: [[Finanzas para Ingenieros - Estados Financieros y Razones Financieras]]

## Contexto y objetivo
Aplicar **Algoritmos Genéticos (AG)** y **Optimización Evolutiva Multiobjetivo (MOEA)** para resolver la selección de portafolios de Markowitz cuando existen restricciones no lineales o datos de alta volatilidad (como criptoactivos), conectando directamente con el proyecto 2025 del curso.

## 1. Fundamentos de Algoritmos Genéticos
Los **Algoritmos Genéticos** (inspirados en la selección natural de Darwin y formalizados por John Holland) son metaheurísticas poblacionales que buscan soluciones óptimas o cercanas al óptimo en espacios complejos:
1. **Representación (cromosoma)**: cada individuo codifica una solución candidata. En portafolios, un cromosoma de longitud $n$ almacena genes reales $g_i \ge 0$ que se normalizan como pesos $x_i = \dfrac{|g_i|}{\sum_j |g_j|}$.
2. **Población inicial**: conjunto de $P$ individuos generados aleatoriamente.
3. **Función de aptitud (*fitness*)**: evalúa la calidad de cada individuo (p. ej., maximizar el Ratio de Sharpe o minimizar varianza penalizando desviaciones).
4. **Selección**: elige padres proporcionalmente a su aptitud (ruleta, torneo, rango).
5. **Cruce (*crossover*)**: combina genes de dos padres para producir descendencia (un punto, uniforme, aritmético).
6. **Mutación**: altera aleatoriamente algunos genes con probabilidad $p_m$ para mantener diversidad y evitar óptimos locales.
7. **Elitismo y reemplazo**: conserva los mejores individuos de una generación a la siguiente hasta cumplir el criterio de parada.

## 2. Optimización Multiobjetivo (MOEA)
En Markowitz existen dos objetivos en conflicto: **maximizar rendimiento** $E(R_p)$ y **minimizar riesgo** $\sigma_p$. En lugar de combinar ambos en un solo escalar (como Sharpe), un **MOEA** (p. ej., NSGA-II) busca simultáneamente el conjunto de soluciones **no dominadas** (**frente de Pareto**), que corresponde directamente a la **frontera eficiente**:
- Una solución $A$ *domina* a $B$ si $A$ es al menos igual en todos los objetivos y estrictamente mejor en al menos uno.

## 3. Implementación en Python (PyGAD + NumPy)
Siguiendo el proyecto 2025 (portafolio de criptomonedas: BTC, WLD, XRP, BNB, SOL, APT, SUI, ETH, 1MBABYDOGE con precios semanales de 8 meses):

```python
import numpy as np
import pygad

# precios: matriz (T x N) de precios semanales de N activos
R = np.log(precios[1:] / precios[:-1])
mu = R.mean(axis=0) * 52
S = np.cov(R.T) * 52
rf = 0.04

def fitness_func(ga_instance, solution, solution_idx):
    w = np.abs(solution)
    if w.sum() == 0:
        return 0.0
    w = w / w.sum()
    rend = w @ mu
    riesgo = np.sqrt(w @ S @ w)
    return (rend - rf) / riesgo if riesgo > 0 else 0.0

ga = pygad.GA(
    num_generations=200,
    sol_per_pop=50,
    num_genes=len(mu),
    num_parents_mating=10,
    fitness_func=fitness_func,
    gene_space={"low": 0.0, "high": 1.0},
    mutation_type="random",
    mutation_probability=0.2,
    keep_elitism=2
)
ga.run()
best_sol, best_fit, _ = ga.best_solution()
pesos_optimos = np.abs(best_sol) / np.abs(best_sol).sum()
```

## 4. Limitaciones prácticas en criptoactivos
- **Colas pesadas y asimetría**: los rendimientos cripto no siguen una distribución normal perfecta; la varianza penaliza por igual subidas y bajadas extremas.
- **Correlaciones inestables**: en caídas sistémicas del mercado, las correlaciones tienden a acercarse a $1$, reduciendo el efecto de diversificación.
- **Sobreajuste histórico**: optimizar sobre 8 meses pasados no garantiza el mismo desempeño futuro (*out-of-sample*).

## Errores comunes
- Usar los genes crudos de PyGAD sin normalizar ($\sum w_i \neq 1$), violando la restricción presupuestaria.
- Fijar una tasa de mutación demasiado alta ($>0{,}5$), convirtiendo el algoritmo en búsqueda aleatoria sin convergencia, o demasiado baja ($0$), causando convergencia prematura.
- Dividir entre cero en el Sharpe si todos los genes caen a cero.

## Ejercicios propuestos
1. Modifique la función `fitness_func` anterior para imponer un límite máximo de $30\,\%$ por activo ($w_i \le 0{,}30$) mediante penalización.
   - *Respuesta*: tras normalizar `w`, calcular `exceso = np.maximum(0, w - 0.30).sum()` y restar `10.0 * exceso` al Ratio de Sharpe retornado.
2. Explique la ventaja de usar un MOEA frente a maximizar únicamente el Ratio de Sharpe.
   - *Respuesta*: el Ratio de Sharpe devuelve un único punto tangente de la frontera eficiente, mientras que un MOEA entrega todo el frente de Pareto para que distintos perfiles de inversionista (conservador, moderado, agresivo) elijan su combinación riesgo-rendimiento.

## Conexiones
- Detalle del proyecto del semestre en [[Modelo de Markowitz y Algoritmo Genético]].
- Metaheurísticas y computación evolutiva en [[Introducción a la Inteligencia Artificial]] y [[Aprendizaje Automático]].
- Base matemática del portafolio en [[Finanzas para Ingenieros - Rendimiento, Riesgo y Teoría de Portafolios de Markowitz]].

## Fuente
Basado en [[Finanzas para Ingenieros]] y `Material/Tema 2/apuntes.pdf`, `algoritmosgeneticos.pdf`, `MOEA.pdf`, `algoritmoGenetico.py`, `PROYECTO FINANZAS PARA INGENIEROS2025.pdf` y `Algoritmo Genético Douglas Aliendres & Leonardo Lobo.pdf`.
