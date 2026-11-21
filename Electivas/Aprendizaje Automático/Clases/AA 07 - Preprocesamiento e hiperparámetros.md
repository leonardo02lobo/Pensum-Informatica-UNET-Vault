---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general; rutas leídas: /home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/02 - Variables categoricas y preprocesamiento.md y 03 - Hiperparametros y HPO.md"
---
# AA 07 - Preprocesamiento e hiperparámetros

Materia: [[Aprendizaje Automático]]
Anterior: [[AA 06 - Métricas y validación de modelos]]
Siguiente: [[AA 08 - MLOps y despliegue]]

## Contexto y objetivo
Los datos reales traen valores faltantes, categorías y escalas dispares, y los modelos tienen hiperparámetros que cambian radicalmente su rendimiento. Objetivo: construir un `Pipeline` con `ColumnTransformer` correcto (sin fuga) y ajustar hiperparámetros con búsqueda en malla, aleatoria y bayesiana.

## Preprocesamiento
**Valores faltantes:** imputación por media/mediana (numéricas) o moda (categóricas); un indicador booleano de "faltaba" puede aportar señal. Los árboles basados en histogramas (`HistGradientBoosting`) admiten NaN de forma nativa.

**Escalado numérico:** estandarización $z=(x-\mu)/\sigma$ o min-max $(x-\min)/(\max-\min)$. Necesario para modelos basados en distancias o gradiente (k-NN, SVM, regresión regularizada, redes); innecesario para árboles. `RobustScaler` usa mediana y rango intercuartílico (robusto a atípicos).

**Variables categóricas** (según [[02 - Variables categoricas y preprocesamiento]]):
1. Eliminarlas (casi siempre pierde señal).
2. **Ordinal:** correcto si hay orden natural (S/M/L); los árboles la toleran aun sin orden.
3. **One-hot:** una columna binaria por categoría; útil con cardinalidad baja (la nota sugiere menos de unas 15 categorías) y con `handle_unknown="ignore"` para categorías no vistas.
4. Cardinalidad alta: target encoding (hacerlo dentro de los pliegues o filtra la etiqueta), frecuencia o embeddings.

**Importante:** esa misma nota advierte que cada framework quiere los datos distinto (auto-sklearn y AutoGluon gestionan su propio preprocesamiento; TabPFN prefiere datos sin one-hot ni escalado). Mantén el DataFrame crudo como fuente de verdad.

**Otros:** transformaciones logarítmicas para sesgo, ingeniería de variables (fechas, razones, interacciones), selección de variables (filtro por varianza o correlación, L1, importancia de modelos), desbalance (pesos de clase, submuestreo, SMOTE solo dentro del pliegue).

## Hiperparámetros y HPO
Un **parámetro** se aprende en `fit` (pesos); un **hiperparámetro** se fija antes (profundidad, $C$, `learning_rate`). Método de [[03 - Hiperparametros y HPO]]: (0) línea base sin ajuste; (1) definir el espacio de búsqueda; (2) buscar con validación cruzada; (3) reevaluar el mejor en prueba una sola vez.

- **Grid search:** prueba todas las combinaciones; coste exponencial en el número de hiperparámetros.
- **Random search:** muestrea combinaciones al azar (Bergstra y Bengio 2012); con el mismo presupuesto explora más valores de los hiperparámetros importantes y suele ganar a la malla.
- **Optimización bayesiana** (Optuna, scikit-optimize): modela el rendimiento con un sustituto (procesos gaussianos o TPE) y propone puntos prometedores.
- **Halving/Hyperband:** descartar pronto las configuraciones malas con poco presupuesto.
- Escalas logarítmicas para tasas y regularización ($10^{-4}$ a $10^{2}$).

## Ejemplo resuelto: coste de una búsqueda
Malla con 4 valores de `max_depth`, 5 de `n_estimators` y 3 de `min_samples_leaf`, validación cruzada de 5 pliegues.
1. Combinaciones: $4\cdot5\cdot3=60$.
2. Entrenamientos: $60\cdot5=300$ (más 1 reajuste final).
3. Si cada uno tarda 2 s: 600 s = 10 min. Con `RandomizedSearchCV(n_iter=20)`: 100 entrenamientos, 3,3 min.

Fuga típica: calcular la media para imputar con todo el conjunto y luego hacer CV. Con el `Pipeline`, la media se recalcula con los datos de entrenamiento de cada pliegue.

## Código
```python
import numpy as np
import pandas as pd
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import RandomizedSearchCV, train_test_split
from scipy.stats import randint

rng = np.random.default_rng(0)
n = 600
df = pd.DataFrame({
    "edad": rng.integers(18, 70, n).astype(float),
    "ingreso": rng.lognormal(10, 0.5, n),
    "ciudad": rng.choice(["A", "B", "C", None], n),
})
df.loc[rng.random(n) < 0.1, "edad"] = np.nan             # faltantes
y = ((df.ingreso > df.ingreso.median()) ^ (rng.random(n) < 0.1)).astype(int)

num, cat = ["edad", "ingreso"], ["ciudad"]
pre = ColumnTransformer([
    ("num", Pipeline([("imp", SimpleImputer(strategy="median")),
                      ("esc", StandardScaler())]), num),
    ("cat", Pipeline([("imp", SimpleImputer(strategy="most_frequent")),
                      ("oh", OneHotEncoder(handle_unknown="ignore"))]), cat),
])
pipe = Pipeline([("pre", pre), ("rf", RandomForestClassifier(random_state=0))])

Xtr, Xte, ytr, yte = train_test_split(df, y, stratify=y, random_state=0)
print("línea base:", pipe.fit(Xtr, ytr).score(Xte, yte).round(3))

busqueda = RandomizedSearchCV(
    pipe,
    {"rf__n_estimators": randint(50, 400),
     "rf__max_depth": randint(2, 12),
     "rf__min_samples_leaf": randint(1, 10)},
    n_iter=15, cv=5, scoring="roc_auc", random_state=0, n_jobs=-1)
busqueda.fit(Xtr, ytr)
print(busqueda.best_params_, busqueda.best_score_.round(3))
print("prueba:", busqueda.score(Xte, yte).round(3))
```

## Errores comunes
- Ajustar imputadores, escaladores o codificadores antes de dividir los datos.
- One-hot de una columna con miles de categorías.
- Olvidar `handle_unknown="ignore"` y fallar en producción.
- Mirar la métrica de prueba durante la búsqueda.
- Buscar en escala lineal hiperparámetros que varían en órdenes de magnitud.

## Ejercicios propuestos
1. ¿Cuántas columnas genera one-hot de una variable con 7 categorías (sin eliminar una)? *Respuesta: 7.*
2. ¿Por qué random search puede superar a grid search? *Respuesta: prueba más valores distintos de cada hiperparámetro relevante con el mismo presupuesto.*
3. ¿Hace falta escalar para un bosque aleatorio? *Respuesta: no.*

## Conexiones
- Limpieza y calidad previas: [[APD 02 - Limpieza y transformación de datos]].
- Estadísticos de imputación y escalado: [[Estadística I]].
- Optimización de funciones costosas: [[Investigación de Operaciones II]].
- AutoML que automatiza estos pasos: [[04 - AutoML - conceptos clave]] y [[09 - Comparativa frameworks AutoML]].

## Fuente
Rutas leídas: `/home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/02 - Variables categoricas y preprocesamiento.md` y `.../03 - Hiperparametros y HPO.md`. Complemento: conocimiento general (documentación de scikit-learn; Bergstra y Bengio 2012). Verificar el temario con el programa oficial.
