---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general"
---
# AA 06 - Métricas y validación de modelos

Materia: [[Aprendizaje Automático]]
Anterior: [[AA 05 - Aprendizaje no supervisado]]
Siguiente: [[AA 07 - Preprocesamiento e hiperparámetros]]

## Contexto y objetivo
Un modelo es tan bueno como la métrica con que se mide y el protocolo con que se valida. Elegir mal la métrica puede dar modelos "excelentes" que no sirven (p. ej. 99 % de exactitud prediciendo siempre la clase mayoritaria). Objetivo: calcular e interpretar métricas de clasificación y regresión y aplicar validación cruzada correcta.

## Matriz de confusión (binaria)
| | Pred. positivo | Pred. negativo |
|---|---|---|
| Real positivo | VP | FN |
| Real negativo | FP | VN |

- **Exactitud** $=\frac{VP+VN}{N}$.
- **Precisión** $=\frac{VP}{VP+FP}$ (de lo que predije positivo, cuánto lo era).
- **Exhaustividad (recall, sensibilidad)** $=\frac{VP}{VP+FN}$.
- **Especificidad** $=\frac{VN}{VN+FP}$.
- **F1** $=\frac{2PR}{P+R}$ (media armónica); $F_\beta$ pondera el recall $\beta$ veces más.
- **Multiclase:** promedio macro (clases por igual), micro (global) o ponderado.

## Curvas ROC y PR
Variando el umbral de decisión se obtienen pares (TPR, FPR). **ROC-AUC** es la probabilidad de que un positivo reciba mayor puntaje que un negativo (0,5 azar, 1 perfecto). Con clases muy desbalanceadas es más informativa la curva **precisión-recall** (AP). Otras: log-loss (calidad de las probabilidades), coeficiente de Matthews, curvas de calibración y puntaje de Brier.

## Métricas de regresión
- $\text{MAE}=\frac1N\sum|y_i-\hat y_i|$ (robusta a atípicos).
- $\text{RMSE}=\sqrt{\frac1N\sum(y_i-\hat y_i)^2}$ (penaliza errores grandes, misma unidad que $y$).
- $R^2=1-\text{SSR}/\text{SST}$ (puede ser negativo en prueba).
- MAPE (error porcentual; falla con $y$ cercano a cero).

## Validación
- k-fold (y `StratifiedKFold` para conservar proporciones de clase), `RepeatedKFold`, leave-one-out.
- **Series temporales:** `TimeSeriesSplit` (entrenar con el pasado, validar con el futuro).
- **Datos agrupados** (varias filas por paciente/cliente): `GroupKFold`.
- **Validación cruzada anidada:** bucle interno para elegir hiperparámetros y externo para estimar el error; evita el optimismo de reportar el mejor resultado de la búsqueda.
- Comparar contra una **línea base** (`DummyClassifier`, regresor de la media).
- Reportar media y desviación entre pliegues; la diferencia entre modelos debe superar el ruido.

## Ejemplo resuelto
Cribado de una enfermedad: 1000 personas, 50 enfermas. El modelo detecta 40 enfermas (VP=40, FN=10) y da 60 falsos positivos (FP=60, VN=890).
1. Exactitud $=(40+890)/1000=0{,}93$.
2. Precisión $=40/100=0{,}40$.
3. Recall $=40/50=0{,}80$.
4. Especificidad $=890/950=0{,}937$.
5. $F1=2\cdot0{,}4\cdot0{,}8/(1{,}2)=0{,}533$.

Un modelo trivial que dice "sano" siempre tendría exactitud 0,95 pero recall 0: la exactitud engaña. Si el coste de un FN es alto, se baja el umbral para subir el recall a costa de la precisión.

## Código
```python
import numpy as np
from sklearn.datasets import make_classification
from sklearn.model_selection import (StratifiedKFold, cross_validate,
                                     train_test_split)
from sklearn.ensemble import RandomForestClassifier
from sklearn.dummy import DummyClassifier
from sklearn.metrics import (classification_report, confusion_matrix,
                             roc_auc_score, average_precision_score,
                             precision_recall_curve)

X, y = make_classification(2000, 20, weights=[0.95, 0.05], random_state=0)
Xtr, Xte, ytr, yte = train_test_split(X, y, stratify=y, random_state=0)

modelo = RandomForestClassifier(300, class_weight="balanced", random_state=0)
cv = StratifiedKFold(5, shuffle=True, random_state=0)
res = cross_validate(modelo, Xtr, ytr, cv=cv,
                     scoring=["roc_auc", "average_precision", "f1"])
for k in ["test_roc_auc", "test_average_precision", "test_f1"]:
    print(k, res[k].mean().round(3), "+-", res[k].std().round(3))

base = DummyClassifier(strategy="most_frequent").fit(Xtr, ytr)
print("exactitud de la línea base:", base.score(Xte, yte).round(3))

modelo.fit(Xtr, ytr)
p = modelo.predict_proba(Xte)[:, 1]
print("AUC", roc_auc_score(yte, p).round(3), "AP", average_precision_score(yte, p).round(3))

# elegir umbral que maximiza F1
pr, rc, th = precision_recall_curve(yte, p)
f1 = 2 * pr * rc / (pr + rc + 1e-12)
umbral = th[np.argmax(f1[:-1])]
print("umbral:", umbral.round(3))
print(confusion_matrix(yte, p >= umbral))
print(classification_report(yte, p >= umbral))
```

## Errores comunes
- Usar exactitud con clases desbalanceadas.
- Elegir el umbral sobre el conjunto de prueba.
- Validación cruzada aleatoria con datos temporales o agrupados (fuga).
- Reportar la métrica de validación de la búsqueda de hiperparámetros como rendimiento final.
- Comparar modelos por diferencias menores que la desviación entre pliegues.

## Ejercicios propuestos
1. Con VP=30, FP=10, FN=20, calcula precisión, recall y F1. *Respuesta: 0,75; 0,60; 0,667.*
2. ¿Cuándo preferir PR sobre ROC? *Respuesta: cuando la clase positiva es rara.*
3. ¿Qué RMSE tiene un modelo que siempre predice la media? *Respuesta: la desviación estándar de $y$.*

## Conexiones
- Pruebas de hipótesis y comparación de modelos: [[Estadística II]].
- Probabilidades y errores tipo I/II (FP/FN): [[Estadística I]].
- Evaluación en proyectos de investigación: [[TAP Tesis]].
- Validación para el pipeline completo: [[01 - scikit-learn]].

## Fuente
Conocimiento general (documentación de scikit-learn, Géron, *ESL*). Verificar el temario con el programa oficial.
