---
tags: [tema, semestre-VIII]
semestre: VIII
---
# Modelo de Markowitz y Algoritmo Genético

Nota hija de [[Finanzas para Ingenieros]]. Resume el proyecto 2025 (enunciado e informe en `Material/`).

## Enunciado
Investigar precios semanales de los **últimos 8 meses** de varias criptomonedas (BTC, WLD, XRP, BNB, SOL, APT, SUI, ETH y 1MBABYDOGE) y:
1. Aplicar el **modelo de Markowitz**: cartera eficiente = máximo rendimiento para un riesgo dado o mínimo riesgo para un rendimiento dado; pesos X = {xᵢ} solución del problema paramétrico: maximizar E(Rp) = Σ xᵢE(Rᵢ) y minimizar σ²(Rp) = ΣΣ xᵢxⱼσᵢⱼ sujeto a Σxᵢ = 1 y xᵢ ≥ 0.
2. Resolver la optimización con un **algoritmo genético**.

## Pasos
1. Descargar precios, calcular rendimientos (simples o logarítmicos).
2. Estimar vector de medias y matriz de covarianzas.
3. Codificar un individuo como vector de pesos normalizado.
4. Función de aptitud (fitness): Sharpe, o rendimiento penalizando riesgo.
5. Operadores: selección (torneo/ruleta), cruce, mutación, elitismo; iterar generaciones.
6. Comparar con la solución analítica/numérica (mínima varianza, frontera eficiente).

## Algoritmo genético (resumen)
Población inicial aleatoria → evaluar fitness → seleccionar padres → cruce → mutación → nueva generación → criterio de parada. Útil cuando el espacio de soluciones es amplio y la función no es lineal (cripto con comportamiento no lineal y dependiente de factores tecnológicos, regulatorios y especulativos, según el informe).

```python
import pygad, numpy as np
def f(ga, x, idx):
    w = np.abs(x) / np.abs(x).sum()
    return (w @ mu) / np.sqrt(w @ S @ w)
ga = pygad.GA(num_generations=200, sol_per_pop=50, num_genes=len(mu),
              num_parents_mating=10, fitness_func=f,
              mutation_type="random", mutation_probability=0.2)
ga.run()
```

## Advertencias
Los datos cripto tienen colas pesadas y correlaciones inestables; Markowitz asume rendimientos aproximadamente normales y covarianzas estables. Es un ejercicio académico, no asesoría financiera.

Relacionado: [[Aprendizaje Automático]], [[Estadística II]].
