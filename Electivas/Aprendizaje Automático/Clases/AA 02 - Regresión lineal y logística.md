---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general"
---
# AA 02 - Regresión lineal y logística

Materia: [[Aprendizaje Automático]]
Anterior: [[AA 01 - Fundamentos del aprendizaje automático]]
Siguiente: [[AA 03 - Árboles y métodos de ensamble]]

## Contexto y objetivo
Los modelos lineales son el punto de partida: rápidos, interpretables y la base de muchos otros métodos (incluidas las redes neuronales). Objetivo: derivar mínimos cuadrados y la regresión logística, aplicar regularización Ridge y Lasso e interpretar coeficientes.

## Regresión lineal
Modelo: $\hat y=\mathbf{w}^T\mathbf{x}+b$. Con matriz de diseño $X$ ($N\times d$, con columna de unos para $b$), la pérdida es

$$J(\mathbf{w})=\frac1{2N}\|X\mathbf{w}-\mathbf{y}\|^2.$$

- **Ecuaciones normales:** $\nabla J=0\Rightarrow\mathbf{w}=(X^TX)^{-1}X^T\mathbf{y}$ (requiere $X^TX$ invertible; si hay colinealidad es mal condicionada).
- **Descenso de gradiente:** $\mathbf{w}\leftarrow\mathbf{w}-\eta\frac1NX^T(X\mathbf{w}-\mathbf{y})$.
- Supuestos clásicos (para inferencia): linealidad, errores independientes con varianza constante y media cero.
- **$R^2=1-\frac{\sum(y_i-\hat y_i)^2}{\sum(y_i-\bar y)^2}$.**

## Regularización
Penaliza coeficientes grandes para reducir varianza:
- **Ridge (L2):** $J+\lambda\|\mathbf{w}\|_2^2$, con solución cerrada $\mathbf{w}=(X^TX+\lambda I)^{-1}X^T\mathbf{y}$. Encoge coeficientes, sin anularlos.
- **Lasso (L1):** $J+\lambda\|\mathbf{w}\|_1$. Genera soluciones dispersas (selección de variables); sin forma cerrada.
- **Elastic Net:** mezcla de ambos.

Se estandarizan las variables antes de regularizar (la penalización depende de la escala) y no se penaliza el intercepto.

## Regresión logística
Para clasificación binaria $y\in\{0,1\}$, modela la probabilidad con la sigmoide:

$$p=P(y=1\mid\mathbf{x})=\sigma(\mathbf{w}^T\mathbf{x}+b),\quad \sigma(z)=\frac1{1+e^{-z}}.$$

Equivale a que el logaritmo de las apuestas (log-odds) sea lineal: $\ln\frac{p}{1-p}=\mathbf{w}^T\mathbf{x}+b$. Un incremento de una unidad en $x_j$ multiplica las apuestas por $e^{w_j}$.

Se estima por máxima verosimilitud, es decir minimizando la entropía cruzada:

$$L=-\frac1N\sum_i\big[y_i\ln p_i+(1-y_i)\ln(1-p_i)\big],\qquad \nabla_{\mathbf{w}}L=\frac1NX^T(\mathbf{p}-\mathbf{y}).$$

No tiene solución cerrada; se usa gradiente, Newton (IRLS) o L-BFGS. Es una función convexa (un único mínimo). Multiclase: softmax. Umbral de decisión por defecto 0,5, ajustable según costes (ver [[AA 06 - Métricas y validación de modelos]]).

## Ejemplo resuelto: mínimos cuadrados
Puntos $(1,2),(2,3),(3,5)$. Modelo $y=w_1x+w_0$.
1. $\bar x=2$, $\bar y=10/3\approx3{,}333$.
2. $S_{xy}=\sum(x-\bar x)(y-\bar y)=(-1)(-1{,}333)+0+(1)(1{,}667)=3$; $S_{xx}=1+0+1=2$.
3. $w_1=S_{xy}/S_{xx}=1{,}5$; $w_0=\bar y-w_1\bar x=3{,}333-3=0{,}333$.
4. Predicción para $x=4$: $\hat y=6{,}333$.

Ejemplo logístico: $w=1{,}2$, $b=-3$, $x=3$: $z=0{,}6$, $p=\sigma(0{,}6)=0{,}646$; se clasifica como 1. Odds ratio: $e^{1{,}2}=3{,}32$.

## Código
```python
import numpy as np
from sklearn.datasets import load_breast_cancer, make_regression
from sklearn.linear_model import LinearRegression, Ridge, Lasso, LogisticRegression
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline
from sklearn.model_selection import cross_val_score

# Regresión con 30 variables, solo 5 informativas
X, y = make_regression(200, 30, n_informative=5, noise=10, random_state=0)
for nombre, m in [("OLS", LinearRegression()),
                  ("Ridge", Ridge(alpha=10)),
                  ("Lasso", Lasso(alpha=1.0))]:
    pipe = make_pipeline(StandardScaler(), m)         # escalar dentro del pipeline
    print(nombre, cross_val_score(pipe, X, y, cv=5, scoring="r2").mean().round(3))
print("coef. no nulos Lasso:",
      (make_pipeline(StandardScaler(), Lasso(1.0)).fit(X, y)[-1].coef_ != 0).sum())

# Regresión logística; C = 1/lambda (a menor C, más regularización)
Xc, yc = load_breast_cancer(return_X_y=True)
logit = make_pipeline(StandardScaler(), LogisticRegression(C=1.0, max_iter=1000))
print("exactitud CV:", cross_val_score(logit, Xc, yc, cv=5).mean().round(3))

# Gradiente desde cero para logística
def entrenar(X, y, eta=0.1, it=2000):
    Xb = np.c_[np.ones(len(X)), X]
    w = np.zeros(Xb.shape[1])
    for _ in range(it):
        p = 1 / (1 + np.exp(-Xb @ w))
        w -= eta * Xb.T @ (p - y) / len(y)
    return w
```

## Errores comunes
- Extrapolar fuera del rango de datos.
- Interpretar coeficientes con variables correlacionadas (multicolinealidad inestabiliza los signos).
- No escalar antes de Ridge/Lasso.
- Tomar $p$ de la logística como calibrada sin verificar; separación perfecta hace divergir los pesos sin regularización.
- Usar exactitud con clases desbalanceadas.

## Ejercicios propuestos
1. Con $w_1=1{,}5$, $w_0=0{,}333$ del ejemplo, calcula el residuo en $(3,5)$. *Respuesta: $5-4{,}833=0{,}167$.*
2. Si $\lambda\to\infty$ en Ridge, ¿a qué tienden los coeficientes? *Respuesta: a cero (queda solo el intercepto).*
3. Si $z=0$, ¿cuál es $p$ y qué significa? *Respuesta: $p=0{,}5$, el punto exacto de la frontera de decisión.*

## Conexiones
- Estimación por mínimos cuadrados y máxima verosimilitud: [[Estadística I]], [[Estadística II]].
- Álgebra matricial y derivadas: [[Matemática III]].
- Una neurona sigmoide es una regresión logística: [[RNLD 01 - Neurona y perceptrón]].
- Optimización convexa: [[Investigación de Operaciones II]].

## Fuente
Conocimiento general (Hastie et al., *ESL*, caps. 3-4; documentación de scikit-learn). Verificar el temario con el programa oficial.
