---
tags: [electiva]
---
# Análisis y Procesamiento de Datos

Opción de [[Electivas]].

## Descripción
Cubre el ciclo de vida de los datos: adquisición, limpieza, transformación, análisis exploratorio, visualización y modelado básico. Objetivo: extraer información útil de datos reales con herramientas modernas.

## Temario típico (verificar con el programa oficial)
1. Fuentes y formatos (CSV, JSON, SQL, APIs); calidad de datos.
2. Limpieza: valores faltantes, duplicados, atípicos, codificación.
3. Análisis exploratorio y estadística descriptiva.
4. Visualización (matplotlib, seaborn, Power BI/Tableau).
5. Inferencia: pruebas de hipótesis, correlación, regresión.
6. Procesamiento a gran escala: ETL, introducción a Spark y almacenes de datos.
7. Introducción a la minería de datos.

## Código de ejemplo
```python
import pandas as pd
df = pd.read_csv("datos.csv")
df = df.drop_duplicates().dropna(subset=["edad"])
df["edad_z"] = (df.edad - df.edad.mean()) / df.edad.std()
print(df.groupby("carrera")["nota"].agg(["mean", "std", "count"]))
```

## Relación con el pensum
[[Estadística I]], [[Estadística II]], [[Base de Datos I]], [[Base de Datos II]], [[Investigación de Operaciones I]]. Se aplica en [[TAP Tesis]] para validar resultados y conecta con [[Aprendizaje Automático]].

## Recursos y bibliografía
- McKinney, W. *Python for Data Analysis*.
- Wickham y Grolemund. *R for Data Science* (gratuito).
- Kimball. *The Data Warehouse Toolkit*.
- Kaggle Learn, documentación de pandas.
