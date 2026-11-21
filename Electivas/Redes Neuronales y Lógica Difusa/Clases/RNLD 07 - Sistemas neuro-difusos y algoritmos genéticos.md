---
tags: [clase, electiva]
materia: Redes Neuronales y Lógica Difusa
fuente: "conocimiento general"
---
# RNLD 07 - Sistemas neuro-difusos y algoritmos genéticos

Materia: [[Redes Neuronales y Lógica Difusa]]
Anterior: [[RNLD 06 - Inferencia difusa y control]]
Siguiente: (fin de la serie)

## Contexto y objetivo
Las redes neuronales aprenden de datos pero son cajas negras; los sistemas difusos son interpretables pero requieren un experto que fije reglas y parámetros. Los sistemas neuro-difusos combinan ambas virtudes, y los algoritmos genéticos aportan una optimización global sin gradientes. Objetivo: entender ANFIS y programar un algoritmo genético sencillo.

## ANFIS (Adaptive Neuro-Fuzzy Inference System)
Jang (1993) implementa un FIS de Sugeno de primer orden como red de 5 capas. Con dos entradas $x,y$ y dos reglas:

1. **Capa 1 (fuzzificación):** $O_{1,i}=\mu_{A_i}(x)$, con parámetros de premisa (p. ej. centro $c$ y ancho $\sigma$ de gaussianas).
2. **Capa 2 (fuerza de disparo):** $w_k=\mu_{A_k}(x)\,\mu_{B_k}(y)$.
3. **Capa 3 (normalización):** $\bar w_k=w_k/\sum_j w_j$.
4. **Capa 4 (consecuentes):** $\bar w_k f_k=\bar w_k(p_kx+q_ky+r_k)$, con parámetros de consecuente $p,q,r$.
5. **Capa 5 (suma):** $z=\sum_k\bar w_kf_k$.

**Aprendizaje híbrido:** la salida es lineal en los parámetros de consecuente. En cada época:
- Paso hacia adelante: se fijan las premisas y se resuelven $p,q,r$ por mínimos cuadrados.
- Paso hacia atrás: se fijan los consecuentes y se ajustan las premisas por descenso de gradiente (retropropagación).

Esto converge más rápido que usar solo gradiente. Limitación: explosión de reglas con muchas entradas (maldición de la dimensionalidad); se mitiga con agrupamiento (subtractive clustering) para generar reglas.

Otras formas de combinar: redes que ajustan funciones de pertenencia, sistemas neuro-difusos cooperativos (la red ajusta parámetros del FIS fuera de línea) y de reglas extraídas de una red entrenada.

## Algoritmos genéticos (AG)
Metaheurística inspirada en la evolución. Una población de individuos (cromosomas) codifica soluciones; la aptitud (fitness) mide su calidad.

Ciclo:
1. **Inicializar** la población al azar.
2. **Evaluar** la aptitud.
3. **Selección:** ruleta, torneo o ranking; los mejores se reproducen con más probabilidad.
4. **Cruce:** combinar padres (un punto: se corta el cromosoma y se intercambian colas) con probabilidad $p_c\approx0{,}6$–$0{,}9$.
5. **Mutación:** cambiar genes con probabilidad pequeña $p_m\approx1/L$.
6. **Elitismo:** conservar los mejores individuos.
7. Repetir hasta cumplir un criterio de parada.

**Teorema de esquemas (Holland):** los esquemas cortos, de baja orden y con aptitud superior a la media reciben un número creciente de copias exponencialmente. Es una explicación heurística de por qué funcionan.

AG en este contexto: optimizar pesos de una red, seleccionar arquitectura, ajustar funciones de pertenencia y reglas de un FIS (sistemas neuro-genético-difusos).

## Ejemplo resuelto: AG a mano (OneMax)
Maximizar el número de unos en cadenas de 6 bits. Población: A=110100 (3), B=011011 (4), C=101010 (3), D=000111 (3).

1. Selección por torneo: en el torneo (A,B) gana B; en el torneo (A,D) gana A. Padres: B y A.
2. Cruce en la posición 3: B=011|011 y A=110|100 dan hijos 011100 (3) y 110011 (4).
3. Mutación del 4.º bit de 011100: 011000 (2) (la mutación puede empeorar; el elitismo conserva B).
4. La nueva población incluye B (4) y 110011 (4): la aptitud máxima no decrece.

## Código
```python
import numpy as np
rng = np.random.default_rng(1)

L, N, G = 30, 40, 60                       # longitud, población, generaciones
fit = lambda pob: pob.sum(axis=1)          # OneMax: contar unos
pob = rng.integers(0, 2, (N, L))

for g in range(G):
    f = fit(pob)
    nueva = [pob[f.argmax()].copy()]       # elitismo
    while len(nueva) < N:
        # torneo binario para elegir dos padres
        i = [max(rng.integers(0, N, 2), key=lambda k: f[k]) for _ in range(2)]
        p1, p2 = pob[i[0]], pob[i[1]]
        corte = rng.integers(1, L)         # cruce de un punto
        hijo = np.concatenate([p1[:corte], p2[corte:]])
        mut = rng.random(L) < 1 / L        # mutación bit a bit
        hijo[mut] ^= 1
        nueva.append(hijo)
    pob = np.array(nueva)
print("mejor aptitud:", fit(pob).max(), "de", L)
```

Para ANFIS en Python se usan librerías como `anfis` (implementaciones de la comunidad), o se construye con PyTorch una capa de gaussianas más una capa lineal; en Matlab, el comando `anfis` del Fuzzy Logic Toolbox.

## Errores comunes
- Población muy pequeña o mutación nula: convergencia prematura a un óptimo local.
- Mutación muy alta: el AG degenera en búsqueda aleatoria.
- Función de aptitud mal escalada (una dominante), causa presión de selección excesiva.
- ANFIS con demasiadas entradas: reglas explosivas y sobreajuste; validar con datos de prueba.

## Ejercicios propuestos
1. ¿Cuántos parámetros de consecuente tiene un ANFIS de Sugeno primer orden con 2 entradas y 4 reglas? *Respuesta: $4\times3=12$.*
2. Cruza 101|101 con 010|010. *Respuesta: 101010 y 010101.*
3. ¿Qué papel cumple el elitismo? *Respuesta: garantiza que la mejor solución no se pierda entre generaciones.*

## Conexiones
- Búsqueda local y metaheurísticas: [[IIA 03 - Búsqueda local y algoritmos genéticos]].
- Mínimos cuadrados y gradiente: [[Matemática III]], [[Investigación de Operaciones II]].
- Ajuste de hiperparámetros con búsqueda: [[AA 07 - Preprocesamiento e hiperparámetros]].

## Fuente
Conocimiento general (Jang 1993, "ANFIS: Adaptive-Network-Based Fuzzy Inference System"; Holland 1975; Goldberg 1989). Verificar el temario con el programa oficial.
