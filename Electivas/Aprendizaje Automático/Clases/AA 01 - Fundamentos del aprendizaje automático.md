---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general; ruta leída: /home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/01 - scikit-learn.md"
---
# AA 01 - Fundamentos del aprendizaje automático

Materia: [[Aprendizaje Automático]]
Anterior: (inicio de la serie)
Siguiente: [[AA 02 - Regresión lineal y logística]]

## Contexto y objetivo
Tom Mitchell define: un programa aprende de la experiencia $E$ respecto a una tarea $T$ y una medida de desempeño $P$ si su desempeño en $T$, medido por $P$, mejora con $E$. Esta clase fija el vocabulario y los tres problemas centrales: tipo de aprendizaje, sesgo-varianza y validación. Es la base de todo lo que sigue.

## Tipos de aprendizaje
- **Supervisado:** pares $(\mathbf{x},y)$. Regresión ($y$ continuo) y clasificación ($y$ discreto).
- **No supervisado:** solo $\mathbf{x}$; busca estructura (agrupamiento, reducción de dimensión).
- **Semisupervisado y autosupervisado:** pocas etiquetas o etiquetas derivadas de los propios datos.
- **Por refuerzo:** un agente aprende por recompensas al interactuar con un entorno.

## Formulación
Datos $\mathcal{D}=\{(\mathbf{x}_i,y_i)\}_{i=1}^N$ muestreados de una distribución desconocida. Se busca $f$ en una familia de hipótesis $\mathcal{H}$ que minimice el **riesgo esperado** $R(f)=\mathbb{E}[\ell(y,f(\mathbf{x}))]$. Como no se conoce la distribución, se minimiza el **riesgo empírico** $\hat R(f)=\frac1N\sum_i\ell(y_i,f(\mathbf{x}_i))$.

Pérdidas comunes: cuadrática $(y-\hat y)^2$, absoluta $|y-\hat y|$, 0-1, entropía cruzada.

## Sesgo, varianza y sobreajuste
Para pérdida cuadrática, el error esperado en un punto se descompone:

$$\mathbb{E}[(y-\hat f(x))^2]=\underbrace{\big(\mathbb{E}[\hat f(x)]-f(x)\big)^2}_{\text{sesgo}^2}+\underbrace{\mathrm{Var}[\hat f(x)]}_{\text{varianza}}+\underbrace{\sigma^2}_{\text{ruido}}$$

- Modelo muy simple: sesgo alto, varianza baja (**subajuste**).
- Modelo muy flexible: sesgo bajo, varianza alta (**sobreajuste**).
- El ruido $\sigma^2$ es irreducible. Objetivo: el punto intermedio de mínimo error de generalización.

## Validación
- **Hold-out:** dividir en entrenamiento y prueba (p. ej. 80/20), con `stratify` en clasificación.
- **Validación cruzada k-fold:** dividir en $k$ pliegues; entrenar con $k-1$ y validar en el restante; promediar. Estimación menos ruidosa que un solo hold-out.
- **Tres conjuntos:** entrenamiento (ajustar parámetros), validación (elegir hiperparámetros), prueba (estimación final, una sola vez).
- **Fuga de datos (data leakage):** usar información de validación/prueba durante el entrenamiento. Regla de oro de scikit-learn: `fit` solo con entrenamiento, `transform` con el resto; la nota del vault [[01 - scikit-learn]] insiste en usar `Pipeline` para que esto ocurra dentro de cada pliegue.

## Ejemplo resuelto: curva de complejidad
Se ajustan polinomios de grado 1, 3 y 15 a 30 puntos de $y=\sin(2\pi x)+\varepsilon$.
1. Grado 1: error de entrenamiento y de prueba altos y parecidos: subajuste.
2. Grado 3: ambos bajos y cercanos: buen ajuste.
3. Grado 15: error de entrenamiento casi nulo, de prueba muy alto: sobreajuste.

Conclusión: se elige el grado con menor error de validación cruzada, no de entrenamiento.

## Código
```python
import numpy as np
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression
from sklearn.pipeline import make_pipeline
from sklearn.model_selection import cross_val_score, train_test_split

rng = np.random.default_rng(0)
x = rng.uniform(0, 1, 60).reshape(-1, 1)
y = np.sin(2 * np.pi * x).ravel() + rng.normal(0, 0.25, 60)

Xtr, Xte, ytr, yte = train_test_split(x, y, test_size=0.3, random_state=0)
for grado in [1, 3, 15]:
    modelo = make_pipeline(PolynomialFeatures(grado), LinearRegression())
    cv = -cross_val_score(modelo, Xtr, ytr, cv=5,
                          scoring="neg_mean_squared_error").mean()
    modelo.fit(Xtr, ytr)
    ecm_tr = np.mean((modelo.predict(Xtr) - ytr) ** 2)
    ecm_te = np.mean((modelo.predict(Xte) - yte) ** 2)
    print(f"grado {grado:2d}  train={ecm_tr:.3f}  cv={cv:.3f}  test={ecm_te:.3f}")
```

## Flujo de trabajo típico
1. Definir el problema y la métrica de éxito.
2. Explorar los datos y dividirlos.
3. Línea base simple (modelo trivial o regresión).
4. Preprocesar con un `Pipeline`.
5. Entrenar, validar y ajustar hiperparámetros.
6. Evaluar una vez en prueba, documentar y desplegar (ver [[AA 08 - MLOps y despliegue]]).

El vault propone la misma idea como ruta de trabajo en [[13 - Ruta de trabajo y checklist]] y el marco general de AutoML en [[04 - AutoML - conceptos clave]].

## Errores comunes
- Reportar el error de entrenamiento como rendimiento.
- Escalar o imputar con todo el conjunto antes de dividir.
- Reutilizar el conjunto de prueba muchas veces para elegir modelo.
- Validación cruzada aleatoria en series temporales (usar `TimeSeriesSplit`).
- Ignorar el desbalance de clases al dividir.

## Ejercicios propuestos
1. Un modelo tiene 1 % de error de entrenamiento y 30 % de prueba. ¿Sesgo o varianza? *Respuesta: varianza alta (sobreajuste).*
2. ¿Cuántos modelos se entrenan en 5-fold CV con 10 combinaciones de hiperparámetros? *Respuesta: 50 (más el reajuste final).*
3. Clasifica: agrupar clientes sin etiquetas. *Respuesta: no supervisado.*

## Conexiones
- Estimadores, sesgo y varianza: [[Estadística I]] y [[Estadística II]].
- Programación del flujo: [[Programación II]].
- Parte de redes neuronales: [[RNLD 03 - Entrenamiento, sobreajuste y regularización]].

## Fuente
Conocimiento general (Mitchell 1997; Hastie, Tibshirani, Friedman, *ESL*; Géron). Material del vault leído: `/home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/01 - scikit-learn.md`. Verificar el temario con el programa oficial.
