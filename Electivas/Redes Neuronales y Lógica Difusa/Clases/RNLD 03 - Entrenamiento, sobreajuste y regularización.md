---
tags: [clase, electiva]
materia: Redes Neuronales y Lógica Difusa
fuente: "conocimiento general"
---
# RNLD 03 - Entrenamiento, sobreajuste y regularización

Materia: [[Redes Neuronales y Lógica Difusa]]
Anterior: [[RNLD 02 - Perceptrón multicapa y retropropagación]]
Siguiente: [[RNLD 04 - Redes RBF, Kohonen y Hopfield]]

## Contexto y objetivo
Una red con suficiente capacidad memoriza el conjunto de entrenamiento y falla con datos nuevos (sobreajuste). Esta clase trata cómo medir ese problema y los recursos prácticos para entrenar bien: división de datos, parada temprana, regularización, optimizadores, inicialización y una introducción a redes profundas.

## Generalización y sobreajuste
- **Error de entrenamiento** decrece siempre al entrenar más.
- **Error de validación** decrece y luego sube: ahí empieza el sobreajuste.
- Sesgo-varianza: modelos simples tienen alto sesgo (subajuste); modelos muy flexibles, alta varianza.

Protocolo: dividir en entrenamiento / validación / prueba (p. ej. 60/20/20). El conjunto de prueba se toca una sola vez al final.

## Técnicas de regularización
1. **Parada temprana (early stopping):** detener cuando la pérdida de validación no mejora durante $p$ épocas (paciencia) y restaurar los mejores pesos.
2. **Decaimiento de pesos (L2):** $E_{reg}=E+\frac{\lambda}{2}\|\mathbf{w}\|^2$, con gradiente extra $\lambda w$. L1 ($\lambda\sum|w|$) favorece pesos nulos.
3. **Dropout:** durante el entrenamiento se apaga cada neurona con probabilidad $p$; al inferir se usan todas (escaladas). Equivale a promediar muchas subredes.
4. **Aumento de datos** y **más datos**.
5. **Reducir la capacidad:** menos neuronas o capas.

## Optimizadores
- **Descenso de gradiente con momentum:** $v\leftarrow\beta v-\eta\nabla E,\ w\leftarrow w+v$. Suaviza oscilaciones.
- **RMSProp:** normaliza por la media móvil del cuadrado del gradiente.
- **Adam:** combina momentum y RMSProp con corrección de sesgo; $m_t=\beta_1m_{t-1}+(1-\beta_1)g_t$, $v_t=\beta_2v_{t-1}+(1-\beta_2)g_t^2$, $w\leftarrow w-\eta\,\hat m_t/(\sqrt{\hat v_t}+\epsilon)$. Valores típicos: $\eta=10^{-3}$, $\beta_1=0{,}9$, $\beta_2=0{,}999$.

## Inicialización y normalización
- Xavier/Glorot (tanh, sigmoide): varianza $2/(n_{ent}+n_{sal})$.
- He (ReLU): varianza $2/n_{ent}$.
- Estandarizar entradas ($\mu=0,\sigma=1$) y, en redes profundas, normalización por lotes (batch norm).

## Redes profundas (introducción)
Una red profunda tiene muchas capas ocultas. Aprenden representaciones jerárquicas. Familias: convolucionales (imágenes, comparten pesos por filtros), recurrentes/LSTM (secuencias) y transformadores (atención). Problemas clásicos: desvanecimiento/explosión del gradiente (se mitigan con ReLU, conexiones residuales, recorte de gradiente).

## Ejemplo resuelto: elegir el momento de parada
Pérdidas de validación por época: 0,90; 0,60; 0,45; 0,40; 0,41; 0,43; 0,46. Con paciencia 2:
1. Época 4 es el mínimo (0,40).
2. Épocas 5 y 6 no mejoran (2 consecutivas): se detiene en la época 6.
3. Se restauran los pesos de la época 4.

Efecto de L2 sobre un peso: con $\eta=0{,}1$, $\lambda=0{,}01$, $w=2$ y gradiente del error cero, $w\leftarrow2-0{,}1\cdot0{,}01\cdot2=1{,}998$: decae en cada paso.

## Código (scikit-learn y Keras)
```python
from sklearn.datasets import make_moons
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPClassifier
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import make_pipeline

X, y = make_moons(600, noise=0.3, random_state=0)
Xtr, Xte, ytr, yte = train_test_split(X, y, test_size=0.3, random_state=0)

for alpha in [0.0, 0.01, 1.0]:                       # alpha = coeficiente L2
    red = make_pipeline(
        StandardScaler(),                            # normalizar entradas
        MLPClassifier(hidden_layer_sizes=(64, 64), alpha=alpha,
                      early_stopping=True,           # parada temprana
                      validation_fraction=0.2, n_iter_no_change=10,
                      max_iter=500, random_state=0))
    red.fit(Xtr, ytr)
    print(alpha, "train", round(red.score(Xtr, ytr), 3),
          "test", round(red.score(Xte, yte), 3))
```

```python
# Keras (TensorFlow): dropout + Adam + parada temprana
import tensorflow as tf
m = tf.keras.Sequential([
    tf.keras.layers.Dense(64, activation="relu", kernel_regularizer=tf.keras.regularizers.l2(1e-3)),
    tf.keras.layers.Dropout(0.3),
    tf.keras.layers.Dense(1, activation="sigmoid")])
m.compile(optimizer=tf.keras.optimizers.Adam(1e-3), loss="binary_crossentropy", metrics=["accuracy"])
cb = tf.keras.callbacks.EarlyStopping(patience=10, restore_best_weights=True)
# m.fit(Xtr, ytr, validation_split=0.2, epochs=200, callbacks=[cb])
```

## Errores comunes
- Usar el conjunto de prueba para elegir hiperparámetros (fuga de información).
- Normalizar con estadísticos de todo el conjunto antes de dividir.
- Aplicar dropout también en inferencia.
- Comparar optimizadores sin ajustar la tasa de aprendizaje de cada uno.
- Interpretar un buen error de entrenamiento como éxito.

## Ejercicios propuestos
1. Si el error de entrenamiento es 2 % y el de validación 25 %, ¿qué ocurre? *Respuesta: sobreajuste (alta varianza); regularizar o conseguir más datos.*
2. ¿Qué inicialización usarías con ReLU? *Respuesta: He.*
3. ¿Cómo cambia $\lambda$ el sesgo y la varianza? *Respuesta: $\lambda$ mayor aumenta el sesgo y reduce la varianza.*

## Conexiones
- Misma teoría de regularización y validación en [[AA 02 - Regresión lineal y logística]] y [[AA 06 - Métricas y validación de modelos]].
- Estimación y varianza: [[Estadística I]].
- Optimización numérica: [[Investigación de Operaciones II]].

## Fuente
Conocimiento general (Goodfellow, Bengio, Courville, *Deep Learning*; Kingma y Ba 2015 para Adam). Verificar el temario con el programa oficial.
