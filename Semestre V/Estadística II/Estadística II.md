---
tags: [materia, semestre-V]
semestre: V
---
# Estadística II

**Semestre:** [[Semestre V]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Estadística I]]

## Desbloquea
- [[Investigación de Operaciones II]]

## Apuntes

### Descripción general y objetivos
Estadística II (código 834501T, 4 horas semanales, Departamento de Matemática y Física, UNET; cronograma 2025 del Prof. Fernando A. Contreras J.) desarrolla la **inferencia estadística**: estimar parámetros poblacionales, contrastar hipótesis, modelar relaciones (regresión y correlación), comparar varias poblaciones (ANDEVA) y aplicar pruebas no paramétricas, con prácticas en SPSS. Objetivo: tomar decisiones con evidencia muestral controlando el error.

### Contenido programático (cronograma 2025)
**Unidad I (semanas 1-5, 1er parcial 35%)**
- Inferencia estadística y etapas del análisis; población y muestra; tipos de muestreo; muestra aleatoria y selección en población finita.
- Parámetros y estimadores puntuales; propiedades (MELI: insesgado, consistente, eficiente, suficiente).
- Distribución de la media muestral; intervalos de confianza para la media, proporciones, diferencia de medias y de proporciones, y varianza; error estándar; tamaño de muestra.

**Unidad II (semanas 6-10, 2do parcial 35%)**
- Contraste de hipótesis: H0/H1, errores tipo I (alfa) y tipo II (beta), pruebas de una y dos colas.
- Pruebas sobre una media, comparación de dos medias, homogeneidad y comparación de varianzas (F), proporciones y diferencia de proporciones.
- Ji cuadrada: bondad de ajuste, independencia, homogeneidad.

**Unidad III (semanas 11-16, 3er parcial 30%)**
- Regresión lineal simple y mínimos cuadrados; análisis de varianza de la regresión; correlación simple, múltiple y parcial.
- ANDEVA, diseño de bloques completos aleatorizados (DBCA), experimentos factoriales, pruebas de comparación múltiple (Duncan).
- No paramétricas: signo, Wilcoxon, Kruskal-Wallis, Friedman, corridas y Spearman. Prácticas con SPSS.

### Conceptos clave
- **Intervalo de confianza** al `(1-α)·100%`: rango que cubre el parámetro en ese porcentaje de muestras.
- **Valor p**: probabilidad, bajo H0, de un resultado al menos tan extremo; se rechaza H0 si `p < α`.
- **Potencia** `1-β`: probabilidad de rechazar H0 cuando es falsa.
- **Grados de libertad**, **región crítica**, **estadístico de prueba**.

### Fórmulas
```
IC media (σ conocida):   x̄ ± z_{α/2} σ/√n          (σ desconocida: t_{n-1}, s/√n)
IC proporción:           p̂ ± z_{α/2} √(p̂(1-p̂)/n)
Tamaño de muestra:       n = (z_{α/2} σ / E)^2
Prueba z / t:            Z = (x̄-μ0)/(σ/√n) ,  t = (x̄-μ0)/(s/√n)
Prueba F varianzas:      F = s1²/s2²  con (n1-1, n2-1) g.l.
Ji cuadrada ajuste:      χ² = Σ (o_i - e_i)² / e_i ,  g.l. = k-1 (menos parámetros estimados)
Independencia:           e_ij = (total fila · total columna)/N ,  g.l. = (f-1)(c-1)
Regresión:               b1 = Sxy/Sxx ,  b0 = ȳ - b1 x̄ ,  r = Sxy/√(Sxx Syy)
ANDEVA:                  F = CM_tratamientos / CM_error
```

### Ejemplo resuelto (del Material: dado legal)
Se lanza un dado 120 veces: observadas 20, 22, 17, 18, 19, 24; esperada de cada cara `e=20`. `χ² = (0+4+9+4+1+16)/20 = 1.7` con 5 g.l.; el crítico a α=0.05 es 11.07, luego no se rechaza H0: el dado es legal.

### Relación con otras materias
Continúa [[Estadística I]] (probabilidad, distribuciones) y se apoya en [[Matemática III]]. Es prelación de [[Investigación de Operaciones II]] y sirve a [[Simulación de Sistemas]], [[Análisis y Procesamiento de Datos]] y [[Aprendizaje Automático]]. Nota hija: [[Contraste de hipótesis y pruebas Ji cuadrada]].

### Evaluación y consejos
- Tres parciales (35%, 35%, 30%) según el cronograma 2025; verificar con el programa oficial.
- Memoriza la estructura: plantear H0/H1, elegir estadístico, región crítica con la tabla (normal, t, χ², F), calcular, concluir en lenguaje del problema.
- Lleva las tablas del Material al examen y practica los ejercicios de cada parcial.

### Bibliografía recomendada
- Walpole, Myers y Myers. *Probabilidad y Estadística para Ingenieros*.
- Canavos, G. *Probabilidad y Estadística*.
- Chao, L. *Estadística para Ciencias Administrativas*.
- Contreras, F. *Estadística Descriptiva y Análisis Descriptivo con SPSS* y guías de clase.

### Recursos del Material/
- Zip `1P 2025 Archivos PDF Estadística II.zip` y carpetas descomprimidas por parcial:
- 1P: [Cronograma 2025](Material/1P%202025%20Archivos%20PDF%20Estad%C3%ADstica%20II/2025%20Cronograma%20Estad%C3%ADstica%20II.pdf), [Guía Unidad I](Material/1P%202025%20Archivos%20PDF%20Estad%C3%ADstica%20II/Gu%C3%ADa%20Unidad%20I%202025%20Estad%C3%ADstica%20II.pdf), ejercicios del 1er parcial, esquema de Estadística I y tablas Normal, t-Student, Ji cuadrada y F.
- 2P: Guías de la Unidad II (varias partes A-D) y [Ejercicios 2 Parcial](Material/2P%202025%20Archivos%20PDF%20Estad%C3%ADstica%20II/2025%20Ejercicios%202%20Parcial%20Estad%C3%ADstica%20II.pdf).
- 3P: Guías de la Unidad III (A-D) con ji cuadrada, regresión y ANDEVA, y la tabla de la prueba de Duncan.
