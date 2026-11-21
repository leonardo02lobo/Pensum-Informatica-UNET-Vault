---
tags: [materia, semestre-VIII]
semestre: VIII
---
# Simulación de Sistemas

**Semestre:** [[Semestre VIII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Investigación de Operaciones II]]

## Desbloquea
- _Ninguna_

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Simulacio  de Sistemas`

## Apuntes

### Descripción general y objetivos
Simulación de Sistemas (código 0425803T según los documentos del proyecto) enseña a **diseñar un modelo de un sistema real y experimentar con él** para comprenderlo o evaluar estrategias (definición de R. E. Shannon). Cubre modelado conceptual, modelado matemático, generación de variables aleatorias, simulación de eventos discretos con **Lista de Eventos Futuros (LEF)**, Montecarlo, verificación/validación y análisis de resultados. Prerrequisito: [[Investigación de Operaciones II]] (colas y Markov). Programa oficial: verificar con la UNET. Resumen del proyecto práctico en [[Age of Conquest Simulación de Eventos Discretos]].

### Contenido programático (orientativo)
1. **Introducción**: sistema, modelo, simulación frente a soluciones analíticas; ventajas y desventajas; cuándo simular (no hay formulación analítica, hipótesis simplificadoras inaceptables, procedimientos numéricos inviables, se desea observar la historia simulada, la experimentación real es costosa o peligrosa).
2. **Metodología de un estudio de simulación**: definición del problema, recolección de datos, modelo conceptual, modelo formal, programación, verificación, validación, experimentación, análisis y documentación.
3. **Tipos de simulación**: continua, discreta, combinada; estática/dinámica; determinista/estocástica; **Montecarlo**.
4. **Números aleatorios**: generadores congruenciales lineales, pruebas de uniformidad e independencia (chi-cuadrado, Kolmogorov-Smirnov, corridas).
5. **Variables aleatorias**: transformada inversa, aceptación-rechazo, convolución, composición; distribuciones uniforme, exponencial, normal (Box-Muller), Poisson.
6. **Simulación por eventos discretos**: reloj de simulación, estado, LEF, eventos, rutinas de inicialización y de temporización; enfoques por eventos, por procesos y por barrido de actividades.
7. **Análisis de salida**: réplicas, longitud de corrida, período de calentamiento, intervalos de confianza, comparación de alternativas, análisis de sensibilidad.
8. **Lenguajes y herramientas**: GPSS, Arena, SimPy, AnyLogic, programación en Python/Java.

### Conceptos clave
- **Variable de estado, de flujo y auxiliar; parámetro**.
- **LEF**: lista ordenada por tiempo de eventos pendientes; el reloj salta al próximo evento (reloj asíncrono).
- **Verificación**: el programa implementa bien el modelo. **Validación**: el modelo representa bien la realidad.
- **Semilla**: valor inicial del generador; fija la reproducibilidad.
- **Réplica independiente**: corrida con distinta semilla.

### Algoritmos y fórmulas
```
Congruencial lineal:  X_{n+1} = (a·X_n + c) mod m ,   U_n = X_n / m
Transformada inversa exponencial:  X = -(1/λ)·ln(1 - U)
Box-Muller:  Z = √(-2 ln U1)·cos(2π U2)
Intervalo de confianza (n réplicas):  x̄ ± t_{n-1,α/2}·s/√n
Ecuación de estado discreta:  S(τ+) = Ψ_e( S(τ-), Θ, U )
```

```python
import heapq, random, math
# Simulación M/M/1 por eventos con LEF (heap)
lef = [(random.expovariate(8), "llegada")]
reloj, cola, ocupado = 0, 0, False
while reloj < 1000:
    reloj, ev = heapq.heappop(lef)
    if ev == "llegada":
        heapq.heappush(lef, (reloj + random.expovariate(8), "llegada"))
        if ocupado: cola += 1
        else:
            ocupado = True
            heapq.heappush(lef, (reloj + random.expovariate(10), "salida"))
    else:
        if cola:
            cola -= 1
            heapq.heappush(lef, (reloj + random.expovariate(10), "salida"))
        else: ocupado = False
```

### Ejemplo resuelto breve
Generador a = 5, c = 3, m = 16, X₀ = 7: X₁ = (35+3) mod 16 = 6, U₁ = 0,375; X₂ = (30+3) mod 16 = 1, U₂ = 0,0625. Con λ = 2: tiempo exponencial = −0,5·ln(1 − 0,375) ≈ 0,235.
Montecarlo para π: lanzar puntos al cuadrado unidad; π ≈ 4·(puntos dentro del cuarto de círculo)/N.

### Cómo se relaciona con otras materias
Valida con resultados analíticos de [[Investigación de Operaciones II]] (colas M/M/c, Markov); usa [[Estadística I]] y [[Estadística II]] (distribuciones, pruebas de hipótesis), [[Programación II]] y [[Estructura de Datos]] (heap para la LEF), [[Teoría General de Sistemas]] (modelado), [[Matemática IV]]. Útil en [[Gerencia de Proyectos]] y [[Aprendizaje Automático]] (aprendizaje por refuerzo en entornos simulados).

### Evaluación y consejos
Los documentos muestran tres parciales encadenados: I modelo conceptual, II modelo formal (diccionario de variables, ecuaciones, LEF y algoritmos de eventos) y III implementación operacional (ingeniería inversa del juego). Verificar ponderaciones con el programa oficial. Consejos: fije semillas, valide con casos de borde y trazas "doradas", documente parámetros e informe sensibilidad.

### Bibliografía
- Law, A. y Kelton, D. *Simulation Modeling and Analysis*.
- Banks, Carson, Nelson. *Discrete-Event System Simulation*.
- Shannon, R. *Simulación de sistemas: diseño, desarrollo e implementación*.
- Coss Bu, R. *Simulación: un enfoque práctico*.
- Taha, H. *Investigación de Operaciones* (capítulo de simulación).

### Recursos (fuera del vault)
`~/Documentos/UNET/Simulacio  de Sistemas`: `Simulacion.pdf` y `Simulación (3).pdf` (teoría introductoria y enunciado del Parcial II), `README.md` y el proyecto `Age of Conquest - Clon/` (Python, escenarios JSON, ecuaciones, pruebas, resultados CSV). No hay `Material/` en el vault.
