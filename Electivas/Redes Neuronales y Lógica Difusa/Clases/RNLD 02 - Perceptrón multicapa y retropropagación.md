---
tags: [clase, electiva]
materia: Redes Neuronales y Lógica Difusa
fuente: "conocimiento general"
---
# RNLD 02 - Perceptrón multicapa y retropropagación

Materia: [[Redes Neuronales y Lógica Difusa]]
Anterior: [[RNLD 01 - Neurona y perceptrón]]
Siguiente: [[RNLD 03 - Entrenamiento, sobreajuste y regularización]]

## Contexto y objetivo
Un perceptrón simple solo separa linealmente. Al apilar capas con activaciones no lineales se obtiene el perceptrón multicapa (MLP), un aproximador universal. El reto es entrenarlo: ¿cómo se reparte el error entre pesos de capas ocultas? La respuesta es la retropropagación (backpropagation), que no es más que la regla de la cadena aplicada de forma ordenada. Objetivo: derivar y programar el algoritmo.

## Arquitectura y activaciones
Un MLP con una capa oculta de $m$ neuronas:

$$\mathbf{h}=f(W_1\mathbf{x}+\mathbf{b}_1),\qquad \hat{\mathbf{y}}=g(W_2\mathbf{h}+\mathbf{b}_2)$$

Funciones de activación habituales:

| Nombre | Fórmula | Derivada |
|---|---|---|
| Sigmoide | $\sigma(z)=\frac{1}{1+e^{-z}}$ | $\sigma(z)(1-\sigma(z))$ |
| Tanh | $\tanh z$ | $1-\tanh^2 z$ |
| ReLU | $\max(0,z)$ | $1$ si $z>0$, $0$ si no |
| Softmax | $\frac{e^{z_k}}{\sum_j e^{z_j}}$ | salida de clasificación multiclase |

**Teorema de aproximación universal (Cybenko, Hornik):** una red con una capa oculta suficientemente ancha y activación no lineal acotada puede aproximar cualquier función continua en un compacto. Dice que existe, no cómo encontrarla.

## Función de error
- Regresión: $E=\frac12\sum_k (t_k-y_k)^2$.
- Clasificación binaria: entropía cruzada $E=-[t\ln y+(1-t)\ln(1-y)]$.

## Retropropagación
Sea $z^{(l)}=W^{(l)}a^{(l-1)}+b^{(l)}$ y $a^{(l)}=f(z^{(l)})$. Se define el error local $\boldsymbol{\delta}^{(l)}=\partial E/\partial z^{(l)}$.

1. **Paso hacia adelante:** calcular todas las $a^{(l)}$ y el error.
2. **Capa de salida (MSE y sigmoide):** $\delta^{(L)}=(a^{(L)}-t)\odot a^{(L)}(1-a^{(L)})$.
3. **Hacia atrás:** $\delta^{(l)}=\big((W^{(l+1)})^T\delta^{(l+1)}\big)\odot f'(z^{(l)})$.
4. **Gradientes:** $\partial E/\partial W^{(l)}=\delta^{(l)}(a^{(l-1)})^T$, $\partial E/\partial b^{(l)}=\delta^{(l)}$.
5. **Actualización:** $W\leftarrow W-\eta\,\partial E/\partial W$.

Con entropía cruzada y sigmoide/softmax en la salida, $\delta^{(L)}=a^{(L)}-t$ (se cancela la derivada), lo que evita saturación y acelera el entrenamiento.

### Variantes de descenso
Por lotes (todo el conjunto), estocástico (una muestra) y minilotes (lo habitual).

## Ejemplo resuelto numérico
Red 1-1-1 con sigmoide, $x=1$, $t=0$, $w_1=0{,}5$, $w_2=0{,}5$, sin sesgos, $\eta=1$.

1. $z_1=0{,}5\Rightarrow h=\sigma(0{,}5)=0{,}6225$.
2. $z_2=0{,}5\cdot0{,}6225=0{,}3112\Rightarrow y=\sigma(0{,}3112)=0{,}5772$.
3. $E=\frac12(0-0{,}5772)^2=0{,}1666$.
4. $\delta_2=(y-t)\,y(1-y)=0{,}5772\cdot0{,}5772\cdot0{,}4228=0{,}1409$.
5. $\partial E/\partial w_2=\delta_2 h=0{,}0877$.
6. $\delta_1=w_2\delta_2\,h(1-h)=0{,}5\cdot0{,}1409\cdot0{,}2350=0{,}01656$.
7. $\partial E/\partial w_1=\delta_1 x=0{,}01656$.
8. Nuevos pesos: $w_2=0{,}4123$, $w_1=0{,}4834$. Con ellos el error baja.

Observa que $\delta_1\ll\delta_2$: el gradiente se atenúa en capas profundas con sigmoide (desvanecimiento del gradiente), una razón del uso de ReLU.

## Código: MLP para XOR desde cero
```python
import numpy as np
rng = np.random.default_rng(0)
sig = lambda z: 1/(1+np.exp(-z))

X = np.array([[0,0],[0,1],[1,0],[1,1]], float)
T = np.array([[0],[1],[1],[0]], float)

W1 = rng.normal(0, 1, (2, 4)); b1 = np.zeros((1, 4))
W2 = rng.normal(0, 1, (4, 1)); b2 = np.zeros((1, 1))
eta = 0.5

for ep in range(10000):
    # paso hacia adelante
    H = sig(X @ W1 + b1)
    Y = sig(H @ W2 + b2)
    # paso hacia atrás (MSE + sigmoide)
    d2 = (Y - T) * Y * (1 - Y)
    d1 = (d2 @ W2.T) * H * (1 - H)
    # actualización de parámetros
    W2 -= eta * H.T @ d2;  b2 -= eta * d2.sum(0, keepdims=True)
    W1 -= eta * X.T @ d1;  b1 -= eta * d1.sum(0, keepdims=True)

print(np.round(Y, 3).ravel())   # cercano a [0, 1, 1, 0]
```

Con scikit-learn: `MLPClassifier(hidden_layer_sizes=(8,), activation="tanh", max_iter=2000)`.

## Verificación del gradiente
Para depurar, compara con diferencias finitas: $\frac{E(w+\epsilon)-E(w-\epsilon)}{2\epsilon}$ con $\epsilon\approx10^{-5}$. La diferencia relativa debe ser menor que $10^{-6}$.

## Errores comunes
- Inicializar todos los pesos en cero (simetría: todas las neuronas ocultas aprenden lo mismo).
- Tasa de aprendizaje demasiado alta (divergencia) o demasiado baja (estancamiento).
- Usar sigmoide en capas ocultas profundas.
- Olvidar transponer matrices o sumar gradientes de sesgos sobre el lote.
- Quedar atrapado en mínimos locales o mesetas: reiniciar con otra semilla.

## Ejercicios propuestos
1. Calcula $\sigma'(0)$. *Respuesta: $0{,}25$.*
2. En la red del ejemplo, ¿qué signo tiene $\partial E/\partial w_2$ si $t=1$? *Respuesta: negativo (al restar el gradiente, $w_2$ aumenta).*
3. ¿Cuántos parámetros tiene un MLP 4-5-3 con sesgos? *Respuesta: $4\cdot5+5+5\cdot3+3=43$.*

## Conexiones
- Regla de la cadena y derivadas parciales: [[Matemática III]], [[Matemática IV]].
- Optimización por gradiente: [[Investigación de Operaciones II]].
- Comparación con regresión logística: [[AA 02 - Regresión lineal y logística]].

## Fuente
Conocimiento general (Rumelhart, Hinton y Williams 1986; Haykin; Goodfellow et al., *Deep Learning*). Verificar el temario con el programa oficial.
