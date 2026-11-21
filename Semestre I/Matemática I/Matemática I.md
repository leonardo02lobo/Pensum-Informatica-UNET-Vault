---
tags: [materia, semestre-I]
semestre: I
---
# Matemática I

**Semestre:** [[Semestre I]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- _Ninguna_

## Desbloquea
- [[Física I]]
- [[Matemática II]]

## Apuntes

### Descripción general y objetivos
Matemática I (código 0826101T según el cronograma 2023-1) es el curso de **precálculo y cálculo diferencial de una variable**. Desbloquea [[Física I]] y [[Matemática II]]. Objetivos: manejar el plano cartesiano y la recta, analizar funciones y sus gráficas, calcular límites y continuidad, derivar y aplicar la derivada (razón de cambio, optimización, trazado de curvas). Programa oficial: verificar.

Nota hija: [[Matemática I - Optimización y trazado de gráficas]].

### Contenido programático (cronograma 2023-1 del Material)
**Unidad 1 (I parcial, 25%)**
- Conjuntos numéricos; plano cartesiano; distancia y punto medio.
- Línea recta: ángulo de inclinación, pendiente, ecuaciones, paralelismo y perpendicularidad, ángulo entre rectas, distancia punto-recta.
- Funciones: dominio, rango, gráficas, criterio de la recta vertical; lineal, cuadrática, potencias, radicales, racionales, valor absoluto, parte entera; traslaciones, reflexiones y escalamientos.
- Funciones trascendentes: exponencial, logarítmica, trigonométricas; definidas por partes; operaciones y composición; inyectividad, función inversa, trigonométricas inversas.

**Unidad 2 (II parcial, 25%)**: límites (laterales, propiedades, definición formal, indeterminaciones 0/0, ∞/∞, ∞-∞, 1^∞, límites infinitos y al infinito, asíntotas, teorema del encaje) y continuidad (tipos de discontinuidad, teorema del valor intermedio).

**Unidad 3 (III parcial, 25%)**: derivada (definición, interpretación geométrica, derivabilidad y continuidad), reglas, regla de la cadena, orden superior, derivación implícita y logarítmica, Rolle, Lagrange, recta tangente y normal, L'Hôpital.

**Unidad 4 (IV parcial, 25%)**: razón de cambio, extremos (criterios de primera y segunda derivada), monotonía, concavidad, puntos de inflexión, optimización y trazado de gráficas.

### Fórmulas clave
```
Distancia:      d = sqrt((x2-x1)^2 + (y2-y1)^2)
Pendiente:      m = (y2-y1)/(x2-x1);  y - y1 = m(x - x1)
Dist. punto-recta (Ax+By+C=0):  d = |Ax0+By0+C| / sqrt(A^2+B^2)
Derivada:       f'(x) = lim_{h->0} [f(x+h) - f(x)] / h
(xⁿ)' = n xⁿ⁻¹;  (sen x)' = cos x;  (eˣ)' = eˣ;  (ln x)' = 1/x
Cadena:         (f(g(x)))' = f'(g(x))·g'(x)
Límite notable: lim_{x->0} sen x / x = 1
L'Hôpital:      lim f/g = lim f'/g'  (formas 0/0 o ∞/∞)
```

### Ejemplos resueltos
1. lim_{x→2} (x²-4)/(x-2) = lim (x+2) = 4.
2. Derivar f(x)=x²·sen x: f'(x)=2x·sen x + x²·cos x.
3. Optimización: rectángulo de perímetro 40 con área máxima: A = x(20-x), A' = 20-2x = 0, x = 10 (cuadrado 10x10, A = 100; A''=-2 < 0, máximo).

### Relación con otras materias
Base de [[Matemática II]] (integrales) y [[Matemática III]], [[Matemática IV]], [[Física I]] (cinemática con derivadas), [[Análisis Numérico]], [[Estadística I]], [[Investigación de Operaciones I]] (optimización).

### Evaluación y consejos
Cuatro parciales de igual peso (25%) según el cronograma 2023-1; el primero consta de dos partes (1A y 1B, 50 pts cada una). Resuelve los ejercicios de menor a mayor dificultad como recomienda la guía, domina álgebra y trigonometría antes de límites, grafica siempre.

### Bibliografía recomendada
- Sullivan, *Álgebra y Trigonometría* (9.ª ed.), texto de precálculo de las guías.
- Leithold, *El Cálculo*; Stewart, *Cálculo*; Purcell, Varberg y Rigdon, *Cálculo*; Larson, *Cálculo con geometría analítica*; Demidovich, *5000 problemas de análisis matemático*.

### Recursos del Material/ (carpeta GUIAS)
- [Cronograma - Matematica - 2023-1](Material/GUIAS/Cronograma%20-%20Matematica%20-%202023-1.docx): unidades, semanas y evaluaciones.
- [Temas - contenidos y ejercicios](Material/GUIAS/Temas%20-%20contenidos%20y%20ejercicios.docx): ejercicios por sección del Sullivan.
- [GRÁFICAS](Material/GUIAS/GRÁFICAS.pdf): gráficas de funciones.
- [Ejercicios de Límites](Material/GUIAS/Ejercicios%20de%20Límites.pdf): práctica de límites.
- [Guía de APLICACIONES DE DERIVADAS](Material/GUIAS/Guía%20de%20APLICACIONES%20DE%20DERIVADAS.pdf): problemas de derivadas.
- `_Material I parcial - Línea recta- Semana 1.pdf_`: material del primer parcial (línea recta).
