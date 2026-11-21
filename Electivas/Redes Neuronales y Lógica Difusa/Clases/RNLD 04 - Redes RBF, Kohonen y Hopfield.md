---
tags: [clase, electiva]
materia: Redes Neuronales y Lógica Difusa
fuente: "conocimiento general"
---
# RNLD 04 - Redes RBF, Kohonen y Hopfield

Materia: [[Redes Neuronales y Lógica Difusa]]
Anterior: [[RNLD 03 - Entrenamiento, sobreajuste y regularización]]
Siguiente: [[RNLD 05 - Conjuntos difusos y funciones de pertenencia]]

## Contexto y objetivo
Además del MLP existen arquitecturas con otros principios: las redes de base radial (aproximación local supervisada), los mapas autoorganizados de Kohonen (aprendizaje no supervisado y competitivo) y las redes de Hopfield (memoria asociativa recurrente). Objetivo: entender su estructura, regla de aprendizaje y usos.

## 1. Redes de base radial (RBF)
Arquitectura de tres capas: entrada, una capa oculta de $m$ neuronas radiales y una salida lineal.

$$\phi_j(\mathbf{x})=\exp\!\Big(-\frac{\|\mathbf{x}-\mathbf{c}_j\|^2}{2\sigma_j^2}\Big),\qquad y(\mathbf{x})=\sum_{j=1}^{m}w_j\phi_j(\mathbf{x})+b$$

$\mathbf{c}_j$ son los centros y $\sigma_j$ los anchos. Cada neurona responde solo cerca de su centro (respuesta local), a diferencia del MLP (respuesta global).

**Entrenamiento en dos fases (rápido):**
1. Centros por k-means (o seleccionando muestras); anchos $\sigma\approx d_{max}/\sqrt{2m}$ o la distancia media a vecinos.
2. Pesos de salida por mínimos cuadrados: con la matriz de diseño $\Phi$ ($N\times m$), $\mathbf{w}=(\Phi^T\Phi)^{-1}\Phi^T\mathbf{t}$ (mejor con regularización Ridge).

El teorema de Cover justifica las RBF: un problema no separable en baja dimensión tiene más probabilidad de serlo al proyectarlo a alta dimensión.

## 2. Mapas autoorganizados (SOM, Kohonen)
Una rejilla (1D o 2D) de neuronas, cada una con un vector de pesos $\mathbf{w}_j$ del tamaño de la entrada. Aprendizaje competitivo no supervisado:

1. Presentar $\mathbf{x}$ y hallar la neurona ganadora (BMU): $c=\arg\min_j\|\mathbf{x}-\mathbf{w}_j\|$.
2. Actualizar la ganadora y sus vecinas en la rejilla:
$$\mathbf{w}_j\leftarrow\mathbf{w}_j+\eta(t)\,h_{cj}(t)\,(\mathbf{x}-\mathbf{w}_j),\quad h_{cj}=\exp\!\Big(-\frac{d(c,j)^2}{2\sigma(t)^2}\Big)$$
3. Reducir $\eta(t)$ y $\sigma(t)$ con el tiempo.

El mapa preserva la topología: datos parecidos activan neuronas cercanas. Usos: visualización de datos de alta dimensión, agrupamiento, cuantización vectorial.

## 3. Redes de Hopfield
Red recurrente totalmente conectada de $N$ neuronas bipolares ($s_i\in\{-1,+1\}$), pesos simétricos $w_{ij}=w_{ji}$ y $w_{ii}=0$. Funciona como memoria asociativa: dado un patrón ruidoso, recupera el almacenado.

- **Almacenamiento (regla de Hebb)** para $P$ patrones $\boldsymbol{\xi}^\mu$: $w_{ij}=\frac1N\sum_{\mu}\xi_i^\mu\xi_j^\mu$.
- **Recuperación (asíncrona):** $s_i\leftarrow\mathrm{sgn}\big(\sum_j w_{ij}s_j\big)$.
- **Energía:** $E=-\frac12\sum_{i,j}w_{ij}s_is_j$. Cada actualización no aumenta $E$, así que la red converge a un mínimo local (atractor).
- **Capacidad:** aproximadamente $0{,}138N$ patrones; más allá aparecen atractores espurios.

## Ejemplo resuelto: Hopfield con 4 neuronas
Patrón almacenado $\xi=(1,-1,1,-1)$. Pesos: $w_{ij}=\frac14\xi_i\xi_j$, p. ej. $w_{12}=-\frac14$, $w_{13}=\frac14$, $w_{14}=-\frac14$.

Entrada ruidosa $s=(1,1,1,-1)$ (segundo bit errado).
1. Neurona 2: $w_{21}=-\frac14$, $w_{23}=-\frac14$, $w_{24}=+\frac14$. Suma $=-\frac14(1)-\frac14(1)+\frac14(-1)=-\frac34<0$, luego $s_2\leftarrow-1$.
2. Estado $(1,-1,1,-1)$: recupera el patrón. Las demás neuronas ya concuerdan, el estado es estable.

## Código
```python
import numpy as np

# --- Hopfield ---
P = np.array([[1,-1,1,-1,1,-1,1,-1],
              [1,1,1,1,-1,-1,-1,-1]])
N = P.shape[1]
W = (P.T @ P) / N
np.fill_diagonal(W, 0)

def recuperar(s, pasos=5):
    s = s.copy()
    for _ in range(pasos):
        for i in np.random.permutation(N):      # actualización asíncrona
            s[i] = 1 if W[i] @ s >= 0 else -1
    return s

ruido = P[0].copy(); ruido[[0, 3]] *= -1       # dos bits corrompidos
print(recuperar(ruido), P[0])

# --- RBF con k-means + mínimos cuadrados ---
from sklearn.cluster import KMeans
x = np.linspace(0, 2*np.pi, 80).reshape(-1, 1)
t = np.sin(x).ravel()
km = KMeans(8, n_init=10, random_state=0).fit(x)
C = km.cluster_centers_; sig = 0.5
Phi = np.exp(-((x - C.T) ** 2) / (2 * sig ** 2))   # matriz de diseño (80 x 8)
w = np.linalg.lstsq(Phi, t, rcond=None)[0]
print("ECM:", np.mean((Phi @ w - t) ** 2))

# --- SOM mínimo (rejilla 1D) ---
rng = np.random.default_rng(0)
datos = rng.random((500, 2))
W_som = rng.random((10, 2))
for it in range(2000):
    eta = 0.5 * (1 - it/2000); sg = 3 * (1 - it/2000) + 0.5
    x0 = datos[rng.integers(500)]
    c = np.argmin(((W_som - x0)**2).sum(1))
    h = np.exp(-((np.arange(10) - c)**2) / (2*sg**2))[:, None]
    W_som += eta * h * (x0 - W_som)
```

## Errores comunes
- RBF: poner $\sigma$ muy pequeño (picos aislados) o muy grande (todo se solapa y mal condiciona $\Phi$).
- SOM: no decaer $\eta$ y $\sigma$; no normalizar las entradas (domina la variable de mayor escala).
- Hopfield: guardar demasiados patrones o patrones muy correlacionados; usar actualización síncrona (puede oscilar).
- Confundir el SOM con k-means: el SOM impone una estructura de vecindad.

## Ejercicios propuestos
1. ¿Cuántos patrones puede almacenar con fiabilidad una red de Hopfield de 100 neuronas? *Respuesta: unos 14.*
2. Si $\mathbf{x}=\mathbf{c}_j$, ¿cuánto vale $\phi_j$? *Respuesta: 1 (el máximo).*
3. ¿Qué tipo de aprendizaje usa el SOM? *Respuesta: no supervisado, competitivo y cooperativo.*

## Conexiones
- k-means y reducción de dimensión: [[AA 05 - Aprendizaje no supervisado]].
- Mínimos cuadrados y matrices: [[Matemática III]].
- Búsqueda de mínimos de energía: [[IIA 03 - Búsqueda local y algoritmos genéticos]].

## Fuente
Conocimiento general (Haykin; Kohonen 1982; Hopfield 1982). Verificar el temario con el programa oficial.
