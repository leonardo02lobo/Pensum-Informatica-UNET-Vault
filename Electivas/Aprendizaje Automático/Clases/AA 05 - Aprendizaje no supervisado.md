---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general"
---
# AA 05 - Aprendizaje no supervisado

Materia: [[Aprendizaje Automático]]
Anterior: [[AA 04 - SVM, k-NN y Naive Bayes]]
Siguiente: [[AA 06 - Métricas y validación de modelos]]

## Contexto y objetivo
Sin etiquetas, el objetivo es descubrir estructura: grupos naturales (clustering) y representaciones compactas (reducción de dimensión). Se usa en segmentación de clientes, detección de anomalías, compresión y exploración. Objetivo: dominar k-means, clustering jerárquico, DBSCAN y PCA, y saber evaluar resultados sin etiquetas.

## k-means
Minimiza la inercia (suma de distancias cuadráticas al centroide):

$$J=\sum_{k=1}^K\sum_{\mathbf{x}_i\in C_k}\|\mathbf{x}_i-\boldsymbol{\mu}_k\|^2.$$

Algoritmo de Lloyd: (1) inicializar $K$ centroides (k-means++ los dispersa); (2) asignar cada punto al centroide más cercano; (3) recalcular centroides como la media; (4) repetir hasta que las asignaciones no cambien. Siempre converge, pero a un mínimo local: se repite con varias semillas (`n_init`). Supone grupos convexos, de tamaño similar, y es sensible a la escala y a los atípicos. Elegir $K$: método del codo (inercia vs. $K$) y coeficiente de silueta.

## Clustering jerárquico
Aglomerativo: cada punto empieza como un grupo y se fusionan los dos más cercanos hasta quedar uno. Criterio de enlace: simple (mínimo), completo (máximo), promedio, **Ward** (minimiza el aumento de varianza). El resultado es un **dendrograma**; cortarlo a una altura da los grupos. No requiere fijar $K$ de antemano; coste $O(N^2)$ en memoria.

## DBSCAN
Basado en densidad: parámetros $\varepsilon$ (radio) y `minPts`. Un punto es *núcleo* si tiene al menos `minPts` vecinos en su $\varepsilon$-vecindad; los grupos son componentes conexos de puntos núcleo más sus bordes; el resto es ruido. Encuentra formas arbitrarias y detecta atípicos, pero le cuesta con densidades variables.

## PCA (Análisis de Componentes Principales)
Proyecta a direcciones ortogonales de máxima varianza. Con datos centrados y matriz de covarianza $\Sigma=\frac1{N-1}X^TX$, los componentes son los autovectores $\mathbf{v}_j$ ($\Sigma\mathbf{v}_j=\lambda_j\mathbf{v}_j$), ordenados por autovalor decreciente. Varianza explicada del componente $j$: $\lambda_j/\sum_i\lambda_i$. La proyección a $q$ dimensiones es $Z=X V_q$. Equivalente a la SVD $X=U S V^T$. Requiere estandarizar si las unidades difieren. Es lineal; para estructura no lineal existen t-SNE y UMAP (útiles para visualizar, no para modelar sin cuidado).

## Evaluación sin etiquetas
- **Silueta** de un punto: $s=\frac{b-a}{\max(a,b)}$, con $a$ la distancia media intragrupo y $b$ la distancia media al grupo vecino más cercano. Rango $[-1,1]$; cercano a 1 es bueno.
- Davies-Bouldin (menor es mejor), Calinski-Harabasz (mayor es mejor).
- Con etiquetas de referencia: índice de Rand ajustado, información mutua normalizada.
- Estabilidad: repetir con submuestras.

## Ejemplo resuelto: una iteración de k-means
Puntos 1D: 1, 2, 3, 10, 11, 12; $K=2$, centroides iniciales $\mu_1=2$, $\mu_2=11$ (si se inicializaran en 1 y 2, se llegaría al mismo resultado).
1. Asignación: $\{1,2,3\}\to1$, $\{10,11,12\}\to2$.
2. Nuevos centroides: $\mu_1=2$, $\mu_2=11$. Sin cambios: convergió.
3. Inercia: $(1+0+1)+(1+0+1)=4$.

PCA con datos centrados $(−1,−1),(0,0),(1,1)$: covarianza $\begin{pmatrix}1&1\\1&1\end{pmatrix}$ (2 filas). Autovalores 2 y 0; el primer componente $(1,1)/\sqrt2$ explica el 100 % de la varianza.

## Código
```python
import numpy as np
from sklearn.datasets import make_blobs, make_moons, load_iris
from sklearn.cluster import KMeans, AgglomerativeClustering, DBSCAN
from sklearn.metrics import silhouette_score, adjusted_rand_score
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

X, y = make_blobs(400, centers=4, cluster_std=0.8, random_state=0)
for k in range(2, 7):                                    # elegir K
    lab = KMeans(k, n_init=10, random_state=0).fit_predict(X)
    print(k, round(silhouette_score(X, lab), 3))

lab = KMeans(4, n_init=10, random_state=0).fit_predict(X)
print("ARI:", adjusted_rand_score(y, lab).round(3))

Xm, _ = make_moons(300, noise=0.07, random_state=0)       # forma no convexa
print("k-means:", silhouette_score(Xm, KMeans(2, n_init=10).fit_predict(Xm)).round(3))
db = DBSCAN(eps=0.2, min_samples=5).fit(Xm)
print("DBSCAN grupos:", len(set(db.labels_) - {-1}), "ruido:", (db.labels_ == -1).sum())

# PCA sobre Iris (estandarizado)
Xi = StandardScaler().fit_transform(load_iris().data)
pca = PCA().fit(Xi)
print("varianza explicada:", pca.explained_variance_ratio_.round(3))
Z = PCA(2).fit_transform(Xi)                              # proyección 2D
```

## Errores comunes
- Aplicar k-means sin escalar variables.
- Elegir $K$ solo por el codo, sin otro criterio ni conocimiento del dominio.
- Interpretar los ejes de t-SNE/UMAP como distancias reales.
- Ajustar PCA con todo el conjunto antes de dividir (fuga en supervisado).
- Esperar que k-means encuentre grupos alargados o de densidades distintas.

## Ejercicios propuestos
1. ¿Cuántos grupos produce DBSCAN con `minPts` enorme? *Respuesta: ninguno; todos los puntos se marcan como ruido.*
2. Si los 3 primeros componentes explican 70 %, 20 % y 5 %, ¿cuántos retener para el 90 %? *Respuesta: 2.*
3. ¿Por qué usar k-means++? *Respuesta: reduce la sensibilidad a la inicialización y mejora la inercia final.*

## Conexiones
- Autovalores, autovectores y SVD: [[Matemática III]] y [[Matemática IV]].
- Covarianza y varianza: [[Estadística I]].
- Mapas autoorganizados como agrupamiento neuronal: [[RNLD 04 - Redes RBF, Kohonen y Hopfield]].
- Exploración previa al modelado: [[APD 03 - Análisis exploratorio y estadística descriptiva]].

## Fuente
Conocimiento general (Hastie et al., *ESL* cap. 14; Géron; Ester et al. 1996 para DBSCAN). Verificar el temario con el programa oficial.
