---
tags: [materia, semestre-VI]
semestre: VI
---
# Investigación de Operaciones I

**Semestre:** [[Semestre VI]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Matemática IV]]
- [[Análisis Numérico]]
- [[Estadística I]]

## Desbloquea
- [[Investigación de Operaciones II]]

## Apuntes

### Descripción general y objetivos
Investigación de Operaciones I introduce la **optimización determinística** con modelos de programación lineal (PL): formulación, solución gráfica y símplex, dualidad, análisis de sensibilidad y modelos de redes (transporte, asignación, transbordo). Objetivo: traducir un problema real de decisión en un modelo matemático, resolverlo con método y software, e interpretar la solución. El curso (Prof. Mariela Borges, aula virtual UNET) usa un libro de formulación con ejercicios de producción, mezclas, distribución y agrícolas. Verificar con el programa oficial el sinóptico exacto.

### Contenido programático
1. **Introducción a la IO**: metodología (definir problema, modelar, resolver, validar, implementar).
2. **Tema 2. Formulación de programación lineal**: variables de decisión, función objetivo, restricciones; supuestos de **proporcionalidad y aditividad** (más divisibilidad y certeza); modelos de producción, mezclas, distribución y agrícola.
3. **Solución gráfica** y casos especiales (óptimos alternativos, infactible, no acotado, redundancia).
4. **Método símplex**: forma estándar, variables de holgura/exceso/artificiales, tabla símplex, Big M y dos fases.
5. **Dualidad y análisis de sensibilidad**: modelo dual, precios sombra, rangos de optimalidad y factibilidad.
6. **Modelos de transporte, asignación y transbordo**: solución inicial (esquina noroeste, costo mínimo, Vogel), optimización (MODI/Stepping-Stone), método húngaro.

### Conceptos clave
- **Región factible**: conjunto de puntos que cumplen todas las restricciones; el óptimo está en un vértice.
- **Solución básica factible**: vértice de la región factible.
- **Precio sombra**: cambio en la función objetivo por unidad adicional del recurso.
- **Degeneración**: solución básica con variable básica en cero.
- **Transbordo**: red donde los envíos pasan por nodos intermedios con oferta/demanda cero.

### Modelo general
```
Max (o Min)  Z = c1 x1 + c2 x2 + ... + cn xn
sujeto a     a_i1 x1 + ... + a_in xn  (<=, =, >=)  b_i ,  i = 1..m
             x_j >= 0
```
Ejemplo de formulación (producción): una fábrica produce mesas (x1) y sillas (x2); utilidad 50 y 30; madera: 4x1+3x2 ≤ 240; horas: 2x1+x2 ≤ 100.
```
Max Z = 50 x1 + 30 x2
s.a.  4 x1 + 3 x2 <= 240
      2 x1 +   x2 <= 100
      x1, x2 >= 0
```
Vértices: (0,0), (50,0), (0,80), e intersección 4x1+3x2=240 con 2x1+x2=100: x1=30, x2=40 -> Z = 1500+1200 = 2700 (óptimo; (50,0) da 2500 y (0,80) da 2400).

### Ejemplo del Material: transbordo
Plantas A (100) y B (150), centros X e Y, supermercados SM1 (80), SM2 (90), SM3 (80); costos planta-centro y centro-supermercado. Ver [[Problema de transbordo - Investigación de Operaciones]].

### Relación con otras materias
Requiere [[Matemática IV]] (álgebra lineal), [[Análisis Numérico]] y [[Estadística I]]; es prelación de [[Investigación de Operaciones II]]; se vincula con [[Simulación de Sistemas]], [[Ingeniería Económica]] y [[Gerencia de Proyectos]].

### Evaluación y consejos
- Parciales con formulación y resolución; verificar ponderaciones oficiales.
- Formular bien vale más que calcular: define variables con unidades, verifica que cada restricción tenga sentido.
- Comprueba con una solución gráfica o con software (Solver, LINGO, Python con PuLP).

### Bibliografía recomendada
- Taha, H. *Investigación de Operaciones*. Pearson.
- Hillier y Lieberman. *Introducción a la Investigación de Operaciones*. McGraw-Hill.
- Winston, W. *Investigación de Operaciones*.

### Recursos del Material/
- [Tema 2. Libro sobre Formulación de PL](Material/Tema%202.%20Libro%20sobre%20Formulaci%C3%B3n%20de%20Programaci%C3%B3n%20Lineal%20%28P.L.%29.%20_%20AULAVIRTUAL.pdf): libro del aula virtual (21 págs) con modelo general y ejercicios de producción, mezclas, distribución y agrícolas.
- [transbordo ejercicio.pdf](Material/transbordo%20ejercicio.pdf) y [transbordo ejercicio.docx](Material/transbordo%20ejercicio.docx): ejercicio de transbordo logístico planteado como tablero de transporte.
