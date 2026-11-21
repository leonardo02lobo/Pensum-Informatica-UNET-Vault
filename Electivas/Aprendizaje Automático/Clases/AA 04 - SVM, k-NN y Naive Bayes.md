---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general"
---
# AA 04 - SVM, k-NN y Naive Bayes

Materia: [[Aprendizaje Automático]]
Anterior: [[AA 03 - Árboles y métodos de ensamble]]
Siguiente: [[AA 05 - Aprendizaje no supervisado]]

## Contexto y objetivo
Tres clasificadores de filosofías distintas: geométrico (máquinas de vectores de soporte), basado en instancias (k vecinos más cercanos) y probabilístico generativo (Naive Bayes). Objetivo: conocer el principio de cada uno, sus hiperparámetros y cuándo conviene.

## Máquinas de vectores de soporte (SVM)
Para clases $y_i\in\{-1,+1\}$, el SVM lineal busca el hiperplano $\mathbf{w}^T\mathbf{x}+b=0$ de **margen máximo**. El margen es $2/\|\mathbf{w}\|$. Formulación de margen blando:

$$\min_{\mathbf{w},b,\xi}\ \tfrac12\|\mathbf{w}\|^2+C\sum_i\xi_i\quad\text{s.a. }y_i(\mathbf{w}^T\mathbf{x}_i+b)\ge1-\xi_i,\ \xi_i\ge0.$$

- $C$ grande: poca tolerancia a errores (riesgo de sobreajuste). $C$ pequeño: margen amplio.
- Solo los **vectores de soporte** (puntos en o dentro del margen) determinan la solución.
- **Truco del núcleo (kernel):** el problema dual depende solo de productos punto $K(\mathbf{x},\mathbf{x}')=\phi(\mathbf{x})^T\phi(\mathbf{x}')$. Kernels: lineal, polinómico $(\gamma\mathbf{x}^T\mathbf{x}'+r)^d$, **RBF** $\exp(-\gamma\|\mathbf{x}-\mathbf{x}'\|^2)$.
- Con RBF, $\gamma$ grande da fronteras muy locales (sobreajuste). Hay que escalar las variables.
- Extensión a regresión (SVR) con tubo $\varepsilon$. Entrena en $O(N^2$ a $N^3)$: costoso con muchos datos.

## k vecinos más cercanos (k-NN)
Sin entrenamiento explícito ("aprendizaje perezoso"). Para un punto nuevo: hallar sus $k$ vecinos más cercanos y votar (clasificación) o promediar (regresión), opcionalmente ponderando por $1/d$.
- Distancias: euclídea $\sqrt{\sum(x_j-x'_j)^2}$, Manhattan, Minkowski, coseno.
- $k$ pequeño: varianza alta; $k$ grande: sesgo alto. Elegir por validación cruzada ($k$ impar en binario).
- Sensible a la escala y a variables irrelevantes; sufre la maldición de la dimensionalidad (las distancias pierden contraste). Predicción lenta: $O(Nd)$ sin índices (kd-tree, ball-tree).

## Naive Bayes
Aplica el teorema de Bayes con la suposición "ingenua" de independencia condicional de las variables dada la clase:

$$P(c\mid\mathbf{x})\propto P(c)\prod_{j=1}^dP(x_j\mid c),\qquad \hat c=\arg\max_c\Big[\ln P(c)+\sum_j\ln P(x_j\mid c)\Big].$$

Variantes: Gaussiano (variables continuas), multinomial (conteos de palabras), Bernoulli. **Suavizado de Laplace** evita probabilidades cero: $P(x_j\mid c)=\frac{n_{jc}+\alpha}{n_c+\alpha V}$. Muy rápido, buen modelo de referencia en texto aunque la independencia sea falsa; sus probabilidades suelen estar mal calibradas.

## Ejemplo resuelto: Naive Bayes
Clasificar correos con la palabra "oferta" (O) y "reunión" (R). Datos de entrenamiento: spam (4 correos: 3 con O, 0 con R), normal (6 correos: 1 con O, 4 con R). Correo nuevo con O y sin R. Usar Laplace $\alpha=1$ (dos valores por variable).
1. Priors: $P(spam)=0{,}4$, $P(norm)=0{,}6$.
2. Spam: $P(O\mid s)=\frac{3+1}{4+2}=0{,}667$; $P(\neg R\mid s)=\frac{4+1}{4+2}=0{,}833$. Producto con prior: $0{,}4\cdot0{,}667\cdot0{,}833=0{,}222$.
3. Normal: $P(O\mid n)=\frac{1+1}{6+2}=0{,}25$; $P(\neg R\mid n)=\frac{2+1}{6+2}=0{,}375$. Producto: $0{,}6\cdot0{,}25\cdot0{,}375=0{,}0563$.
4. Normalizando: $P(spam\mid\mathbf{x})=0{,}222/(0{,}222+0{,}0563)=0{,}80$. Se clasifica como spam.

## Código
```python
from sklearn.datasets import load_wine
from sklearn.model_selection import GridSearchCV, cross_val_score
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC
from sklearn.neighbors import KNeighborsClassifier
from sklearn.naive_bayes import GaussianNB

X, y = load_wine(return_X_y=True)

# SVM con RBF: ajustar C y gamma dentro de validación cruzada
svm = make_pipeline(StandardScaler(), SVC(kernel="rbf"))
grid = GridSearchCV(svm, {"svc__C": [0.1, 1, 10, 100],
                          "svc__gamma": [0.001, 0.01, 0.1, 1]}, cv=5)
grid.fit(X, y)
print("SVM:", grid.best_params_, grid.best_score_.round(3))

# k-NN: elegir k
for k in [1, 3, 5, 11, 21]:
    m = make_pipeline(StandardScaler(), KNeighborsClassifier(k))
    print("k =", k, cross_val_score(m, X, y, cv=5).mean().round(3))

# Naive Bayes gaussiano (no necesita escalado)
print("NB:", cross_val_score(GaussianNB(), X, y, cv=5).mean().round(3))
```

## Errores comunes
- No escalar para SVM y k-NN.
- Ajustar $C$ y $\gamma$ sin validación cruzada anidada ni `Pipeline` (fuga).
- Usar k-NN con cientos de variables sin reducir dimensión.
- Confundir probabilidad de Naive Bayes con probabilidad calibrada.
- Olvidar el suavizado de Laplace (una palabra no vista anula la clase).

## Ejercicios propuestos
1. ¿Qué ocurre con $C\to\infty$? *Respuesta: margen duro, sin tolerancia; sobreajuste si hay ruido.*
2. k-NN con $k=N$, ¿qué predice? *Respuesta: siempre la clase mayoritaria.*
3. ¿Por qué se suman logaritmos en Naive Bayes? *Respuesta: evita desbordamiento por underflow del producto de probabilidades pequeñas.*

## Conexiones
- Teorema de Bayes y probabilidad condicional: [[Estadística I]].
- Optimización con restricciones (SVM dual, multiplicadores de Lagrange): [[Investigación de Operaciones II]], [[Matemática IV]].
- Modelo probabilístico más general: [[IIA 06 - Razonamiento con incertidumbre y redes bayesianas]].

## Fuente
Conocimiento general (Cortes y Vapnik 1995; Hastie et al., *ESL*; Bishop, PRML; documentación de scikit-learn). Verificar el temario con el programa oficial.
