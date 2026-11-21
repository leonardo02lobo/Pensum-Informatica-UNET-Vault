---
tags: [clase, semestre-VI]
materia: Investigación de Operaciones I
---
# Investigación de Operaciones I - Introducción y Metodología de la IO

Materia: [[Investigación de Operaciones I]]  
Anterior: —  
Siguiente: [[Investigación de Operaciones I - Formulación de Programación Lineal]]

## Contexto y objetivo

Introducir la **Investigación de Operaciones (IO)** como disciplina científica de toma de decisiones cuantitativas, describir su metodología de cinco fases y distinguir los modelos determinísticos de optimización lineal frente a los modelos probabilísticos.

## 1. ¿Qué es la Investigación de Operaciones?

La **Investigación de Operaciones** aplica el método científico y herramientas matemáticas (álgebra lineal, cálculo, probabilidad, algoritmos) para asignar recursos escasos de forma **óptima** en sistemas complejos de ingeniería, logística, manufactura y servicios.

- **IO I (determinística)**: todos los parámetros ($c_j, a_{ij}, b_i$) se conocen con certeza. Se centra en **Programación Lineal (PL)** y **modelos de redes**.
- **IO II (probabilística)**: incorpora incertidumbre (cadenas de Markov, colas, inventarios estocásticos, teoría de juegos).

## 2. Metodología de la Investigación de Operaciones

El abordaje sistemático de un problema real sigue cinco fases iterativas:

1. **Definición del problema**: identificar al tomador de decisiones, las **alternativas** controlables, el **criterio de desempeño** (maximizar utilidad o minimizar costo) y las **restricciones** físicas, legales o presupuestarias.
2. **Construcción del modelo matemático**: traducir el problema verbal en ecuaciones e inecuaciones mediante variables de decisión, función objetivo y restricciones.
3. **Solución del modelo**: aplicar algoritmos exactos (método gráfico, símplex, transporte) o software (Solver, LINGO, Python/PuLP).
4. **Validación del modelo**: verificar que el modelo represente adecuadamente la realidad (análisis dimensional, prueba con datos históricos, revisión de supuestos).
5. **Implementación y monitoreo**: traducir la solución matemática en políticas operativas comprensibles y vigilar cambios en los parámetros (análisis de sensibilidad).

## 3. Estructura general de un modelo de optimización

Todo modelo de optimización determinística consta de tres componentes:

$$\text{Optimizar (Max o Min)} \quad Z = f(x_1, x_2, \dots, x_n)$$
$$\text{sujeto a:} \quad g_i(x_1, x_2, \dots, x_n) \le, =, \ge b_i \quad (i = 1, \dots, m)$$
$$x_j \in D_j \quad (j = 1, \dots, n)$$

- **Variables de decisión ($x_j$)**: incógnitas cuantificables sobre las que decide el ingeniero.
- **Función objetivo ($Z$)**: medida cuantitativa de eficacia.
- **Restricciones**: limitaciones sobre los recursos o requerimientos mínimos.

## Errores comunes

- Saltar directamente al software sin validar las unidades de medida o el sentido lógico de las restricciones.
- Confundir parámetros (datos fijos del problema) con variables de decisión (lo que se desea hallar).

## Ejercicios propuestos

1. En una empresa de desarrollo de software que decide cuántas horas asignar a soporte técnico y cuántas a nuevos proyectos durante un sprint de 160 horas, identifica: *(a)* variables de decisión, *(b)* función objetivo y *(c)* al menos dos restricciones.
   - *Respuesta:* *(a)* $x_1$: horas de soporte, $x_2$: horas de nuevos proyectos. *(b)* Maximizar ingreso o valor entregado $Z = c_1 x_1 + c_2 x_2$. *(c)* $x_1 + x_2 \le 160$ y cuota mínima de soporte $x_1 \ge 40$.

## Conexiones

- Siguiente: [[Investigación de Operaciones I - Formulación de Programación Lineal]]
- Materia: [[Investigación de Operaciones I]]
- Materias relacionadas: [[Matemática IV]], [[Análisis Numérico]], [[Estadística I]], [[Economía]], [[Investigación de Operaciones II]]

## Fuente

- Programa de [[Investigación de Operaciones I]] (Taha, *Investigación de Operaciones*; Hillier & Lieberman).
