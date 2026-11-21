---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general; rutas leídas: /home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/10 - MLflow.md, 11 - Despliegue Docker y FastAPI.md, 07 - AutoGluon.md; /home/leonardo/Documentos/UNET/Aprendizaje/autogluon_mlflow/tabular_intro.py"
---
# AA 08 - MLOps y despliegue

Materia: [[Aprendizaje Automático]]
Anterior: [[AA 07 - Preprocesamiento e hiperparámetros]]
Siguiente: (fin de la serie)

## Contexto y objetivo
Un modelo que vive en un notebook no genera valor. MLOps es el conjunto de prácticas para llevar modelos a producción de forma reproducible: seguimiento de experimentos, versionado, empaquetado, despliegue y monitoreo. Objetivo: registrar experimentos con MLflow, exponer un modelo con FastAPI y empaquetarlo con Docker.

## Ciclo de vida
1. **Datos y código versionados** (Git; DVC para datos).
2. **Experimentos registrados:** parámetros, métricas, artefactos y entorno por cada ejecución.
3. **Registro de modelos** con versiones y alias (candidato, producción).
4. **Empaquetado:** modelo + dependencias en un contenedor.
5. **Servicio:** API REST (o por lotes).
6. **Monitoreo:** latencia, errores, deriva de datos (data drift: cambia la distribución de entrada) y deriva de concepto (cambia la relación entrada-salida); reentrenamiento programado o por alerta.

## MLflow
Según [[10 - MLflow]]: *Tracking* (parámetros, métricas, artefactos por *run*), *Models* (formato con *flavors*), *Model Registry* y *Serving* (`mlflow models serve -m runs:/<run_id>/model -p 5000`, endpoint `/invocations`). La interfaz `mlflow ui` permite comparar ejecuciones y promover la ganadora.

## FastAPI y Docker
Según [[11 - Despliegue Docker y FastAPI]]: FastAPI (con Uvicorn como servidor ASGI) valida entradas con Pydantic y genera documentación interactiva en `/docs`. Docker congela el sistema operativo y las librerías en una imagen, evitando el "en mi máquina funciona". Instrucciones del Dockerfile: `FROM`, `WORKDIR`, `COPY`, `RUN`, `EXPOSE`, `CMD`.

## Ejemplo resuelto: de experimento a API
1. Entrenar tres configuraciones y registrar cada una en MLflow con su AUC.
2. Elegir la de mayor AUC en la UI y guardar el modelo.
3. Cargarlo en una API con endpoint `/predict`.
4. Construir la imagen Docker y ejecutarla: `docker build -t modelo_app .` y `docker run -p 8000:8000 modelo_app`.
5. Probar: `curl -X POST localhost:8000/predict -H "Content-Type: application/json" -d '{"x": [5.1, 3.5, 1.4, 0.2]}'`.

Material del estudiante: el script `/home/leonardo/Documentos/UNET/Aprendizaje/autogluon_mlflow/tabular_intro.py` usa `TabularPredictor(label=...).fit(train_data)` de AutoGluon y su `leaderboard()`; es el paso 1 con AutoML (ver [[07 - AutoGluon]]).

## Código
```python
# entrenar.py: registrar experimentos con MLflow
import mlflow, mlflow.sklearn
from sklearn.datasets import load_iris
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

X, y = load_iris(return_X_y=True)
mlflow.set_experiment("iris-demo")
mejor = (0, None)
for n in [10, 100, 300]:
    with mlflow.start_run(run_name=f"rf-{n}"):
        modelo = RandomForestClassifier(n_estimators=n, random_state=0)
        acc = cross_val_score(modelo, X, y, cv=5).mean()
        mlflow.log_param("n_estimators", n)
        mlflow.log_metric("accuracy_cv", acc)
        modelo.fit(X, y)
        mlflow.sklearn.log_model(modelo, "model")
        if acc > mejor[0]:
            mejor = (acc, modelo)

import joblib
joblib.dump(mejor[1], "modelo.joblib")        # para la API
```

```python
# app.py: API con FastAPI (ejecutar con: uvicorn app:app --host 0.0.0.0 --port 8000)
from fastapi import FastAPI
from pydantic import BaseModel
import joblib

app = FastAPI(title="Clasificador de iris")
modelo = joblib.load("modelo.joblib")

class Entrada(BaseModel):
    x: list[float]               # 4 características

@app.post("/predict")
def predecir(e: Entrada):
    clase = int(modelo.predict([e.x])[0])
    proba = modelo.predict_proba([e.x])[0].tolist()
    return {"clase": clase, "probabilidades": proba}

@app.get("/health")
def salud():
    return {"estado": "ok"}
```

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py modelo.joblib ./
EXPOSE 8000
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

## Buenas prácticas
- Fijar versiones (`requirements.txt` con versiones exactas) y semillas.
- Guardar el `Pipeline` completo (preprocesamiento + modelo), no solo el estimador.
- Validar la entrada en la API y registrar las predicciones para monitoreo.
- Probar el contenedor antes de entregarlo; no incluir datos sensibles en la imagen.
- Separar entrenamiento (batch, pesado) de inferencia (ligera).

## Errores comunes
- Entrenar y servir con versiones distintas de scikit-learn (el modelo serializado puede fallar o cambiar).
- Guardar solo el modelo y no el preprocesamiento: la API recibe datos crudos.
- No monitorear: el rendimiento se degrada silenciosamente por deriva.
- Cargar el modelo en cada petición en lugar de al arrancar.
- Usar `pickle` con archivos de origen no confiable (ejecuta código arbitrario).

## Ejercicios propuestos
1. ¿Qué diferencia hay entre deriva de datos y de concepto? *Respuesta: la primera cambia $P(x)$; la segunda, $P(y\mid x)$.*
2. ¿Para qué sirve `EXPOSE` en un Dockerfile? *Respuesta: documenta/expone el puerto en que escucha el contenedor.*
3. ¿Qué registra MLflow Tracking por cada ejecución? *Respuesta: parámetros, métricas, artefactos y metadatos del código.*

## Conexiones
- Bases de datos para almacenar predicciones y experimentos: [[Base de Datos I]] y [[Base de Datos II]].
- Programación de servicios: [[Programación II]].
- Cierre del ciclo de datos: [[APD 06 - ETL, procesamiento a gran escala y almacenes de datos]].

## Fuente
Rutas leídas: `/home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/10 - MLflow.md`, `.../11 - Despliegue Docker y FastAPI.md`, `.../07 - AutoGluon.md` y el script `/home/leonardo/Documentos/UNET/Aprendizaje/autogluon_mlflow/tabular_intro.py` (solo lectura). Complemento: conocimiento general. No se leyeron los demás proyectos de `~/Documentos/UNET/Aprendizaje` en profundidad. Verificar el temario con el programa oficial.
