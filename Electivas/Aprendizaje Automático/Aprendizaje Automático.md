---
tags: [electiva]
---
# Aprendizaje Automático

Opción de [[Electivas]].

## Descripción
El aprendizaje automático (machine learning) estudia algoritmos que mejoran con la experiencia a partir de datos. La electiva cubre aprendizaje supervisado, no supervisado y evaluación de modelos, con práctica en Python. Objetivo: construir, validar y desplegar modelos predictivos.

## Temario típico (verificar con el programa oficial)
1. Fundamentos: tipos de aprendizaje, sesgo-varianza, sobreajuste, validación cruzada.
2. Regresión lineal y logística, regularización (Ridge, Lasso).
3. Árboles de decisión, bosques aleatorios, gradient boosting, SVM, k-NN, Naive Bayes.
4. No supervisado: k-means, clustering jerárquico, PCA.
5. Métricas: exactitud, precisión, recall, F1, ROC-AUC, RMSE.
6. Preprocesamiento de variables categóricas, selección de hiperparámetros y AutoML.
7. MLOps: seguimiento de experimentos, despliegue con API.

## Fórmulas y código
Regresión lineal por mínimos cuadrados: `w = (X^T X)^-1 X^T y`; función de pérdida logística: `L = -[y log p + (1-y) log(1-p)]`.

```python
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_breast_cancer
X, y = load_breast_cancer(return_X_y=True)
print(cross_val_score(RandomForestClassifier(200), X, y, cv=5).mean())
```

## Relación con el pensum
[[Estadística I]], [[Estadística II]], [[Matemática III]], [[Programación II]], [[Investigación de Operaciones II]]. Complementa [[Redes Neuronales y Lógica Difusa]], [[Introducción a la Inteligencia Artificial]] y [[Análisis y Procesamiento de Datos]].

## Material del estudiante
En `~/Documentos/UNET/Aprendizaje` hay proyectos prácticos: `autogluon_mlflow` (scripts de AutoGluon: `tabular_intro.py`, `multimodal_intro.py`, `transition_ei.py`), y `Genome-Transition-Auto-MLl` (extracción de datos, entrenamiento y API). Además, el vault tiene notas de AutoML tabular en `Aprendizaje automatico/` (scikit-learn, auto-sklearn, TabPFN, AutoGluon, MLflow, Docker y FastAPI) que sirven de guía de pipeline completo.

## Bibliografía
- Géron, A. *Hands-On Machine Learning with Scikit-Learn, Keras and TensorFlow*.
- Hastie, Tibshirani, Friedman. *The Elements of Statistical Learning* (gratuito).
- Bishop, C. *Pattern Recognition and Machine Learning*.
- Documentación de scikit-learn y curso Machine Learning de Andrew Ng.

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Aprendizaje`
