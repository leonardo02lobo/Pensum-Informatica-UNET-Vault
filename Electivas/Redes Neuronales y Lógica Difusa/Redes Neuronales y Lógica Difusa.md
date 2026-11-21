---
tags: [electiva]
---
# Redes Neuronales y Lógica Difusa

Opción de [[Electivas]].

## Descripción
Introduce los dos pilares clásicos de la inteligencia computacional: las redes neuronales artificiales (RNA), modelos inspirados en el cerebro que aprenden de datos, y la lógica difusa, que razona con grados de verdad para modelar conocimiento impreciso. Se combinan en sistemas neuro-difusos (ANFIS). Objetivo: modelar, entrenar y aplicar ambos enfoques a problemas de clasificación, regresión y control.

## Temario típico (verificar con el programa oficial)
1. Neurona biológica y artificial; perceptrón y regla de aprendizaje.
2. Perceptrón multicapa, retropropagación, funciones de activación, sobreajuste y regularización.
3. Redes de base radial, mapas autoorganizados (Kohonen), redes de Hopfield; introducción a redes profundas.
4. Conjuntos difusos, funciones de pertenencia, operaciones (t-normas y t-conormas).
5. Reglas SI-ENTONCES, inferencia Mamdani y Sugeno, defuzzificación; controladores difusos.
6. Sistemas neuro-difusos y algoritmos genéticos.

## Fórmulas y código
Neurona: `y = f(sum(w_i * x_i) + b)`; actualización por descenso de gradiente: `w <- w - eta * dE/dw`.

```python
import numpy as np
def sigmoide(z): return 1/(1+np.exp(-z))
X = np.array([[0,0],[0,1],[1,0],[1,1]]); y = np.array([[0],[1],[1],[0]])
W1, W2 = np.random.randn(2,4), np.random.randn(4,1)
for _ in range(10000):
    h = sigmoide(X@W1); o = sigmoide(h@W2)
    d2 = (o-y)*o*(1-o); d1 = d2@W2.T*h*(1-h)
    W2 -= 0.5*h.T@d2; W1 -= 0.5*X.T@d1
```

Función triangular: `mu(x)=max(min((x-a)/(b-a),(c-x)/(c-b)),0)`; centroide: `x* = integral(x*mu)/integral(mu)`.

## Relación con el pensum
[[Matemática IV]] y [[Matemática III]] (cálculo y álgebra), [[Estadística I]], [[Investigación de Operaciones II]] (optimización), [[Automatización]] (control), [[Programación II]]. Se complementa con [[Aprendizaje Automático]] e [[Introducción a la Inteligencia Artificial]].

## Recursos y bibliografía
- Haykin, S. *Neural Networks and Learning Machines*.
- Jang, Sun y Mizutani. *Neuro-Fuzzy and Soft Computing*.
- Zadeh, L. "Fuzzy Sets" (1965).
- Goodfellow, Bengio, Courville. *Deep Learning* (gratuito en línea).
- Librerías: scikit-learn, TensorFlow/Keras, PyTorch, scikit-fuzzy; Matlab Fuzzy Logic Toolbox.
