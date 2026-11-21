---
tags: [materia, semestre-VII]
semestre: VII
---
# Investigación de Operaciones II

**Semestre:** [[Semestre VII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Estadística II]]
- [[Investigación de Operaciones I]]

## Desbloquea
- [[Simulación de Sistemas]]

## Notas en el vault
- [[MVP Colas]]

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Investigacion de Operacion 2`
- `~/Documentos/UNET/IO2`

## Apuntes

### Descripción general y objetivos
Según el programa sinóptico incluido en el Material (código 0425701T, vigencia septiembre 2007, núcleo Tecnología Aplicada, 3 UC; carga semanal: teoría 3, práctica 2, autoestudio 3), la materia enseña a formular, desarrollar y resolver problemas con **modelos simbólico-matemáticos probabilísticos**, aquellos donde los datos no se conocen con certeza. **Objetivo general**: analizar, interpretar y representar situaciones formulando modelos probabilísticos que den descripciones, políticas y alternativas de acción. **Contenidos**: Cadenas de Markov, Teoría de colas, Teoría de inventarios y Teoría de juegos. Continúa [[Investigación de Operaciones I]] y usa [[Estadística II]].

Resúmenes hijos: [[Investigación de Operaciones II - Cadenas de Markov y Matriz de Transición]] · [[Investigación de Operaciones II - Teoría de Colas y Modelos MM1 y MMc]]. Nota relacionada del vault: [[MVP Colas]].

### Contenido programático
**Unidad I – Cadenas de Markov** (según programa): proceso estocástico y propiedad markoviana; matriz de transición y vector inicial; clasificación topológica (ergódicas, semiergódicas, no ergódicas, cíclicas; periodicidad); comportamiento estacionario vs transitorio; cadenas absorbentes (matriz fundamental, probabilidades y tiempos de absorción); probabilidades y tiempos de primera pasada; procesos markovianos de decisión con costos/beneficios; cadenas de orden superior.

**Unidad II – Teoría de colas**: elementos (llegadas, servidores, disciplina, capacidad); notación de Kendall; procesos de nacimiento y muerte; modelos M/M/1, M/M/c, M/M/1/K, M/G/1; medidas L, Lq, W, Wq; análisis de costos.

**Unidad III – Teoría de inventarios**: costos de pedido, mantenimiento y faltante; EOQ determinístico, con descuentos por cantidad, con faltantes, con producción; modelos probabilísticos (punto de reorden, stock de seguridad, modelo del vendedor de periódicos).

**Unidad IV – Teoría de juegos**: juegos de suma cero de dos personas, estrategias puras y mixtas, punto de silla, dominancia, solución por programación lineal o método gráfico; conceptos de equilibrio de Nash.
(Detalle exacto de cada unidad: verificar con el programa oficial.)

### Conceptos clave
- **Propiedad de Markov**: P(Xₙ₊₁=j | Xₙ=i, …, X₀) = P(Xₙ₊₁=j | Xₙ=i) = pᵢⱼ.
- **Estado absorbente**: pᵢᵢ = 1.
- **Distribución estacionaria π**: πP = π, Σπᵢ = 1.
- **Utilización** ρ = λ/(cμ); el sistema es estable si ρ < 1.
- **Fórmula de Little**: L = λW, Lq = λWq.
- **EOQ**: cantidad de pedido que minimiza costo total.
- **Valor del juego** v: máx-mín = mín-máx en punto de silla.

### Fórmulas y ejemplos
```
Markov:   π(n) = π(0)·Pⁿ         estacionaria: π = πP
Absorbente: P = ( (Q R), (0 I) ),  N = (I - Q)⁻¹,  t = N·1,  B = N·R
M/M/1:   ρ=λ/μ  L=ρ/(1-ρ)  Lq=ρ²/(1-ρ)  W=1/(μ-λ)  Wq=ρ/(μ-λ)
M/M/c:   P0 = [Σ_{n=0}^{c-1} (λ/μ)ⁿ/n! + (λ/μ)^c/(c!(1-ρ))]⁻¹
         Lq = P0 (λ/μ)^c ρ / (c!(1-ρ)²)     Wq = Lq/λ     W = Wq+1/μ
         Erlang C: P(esperar) = (λ/μ)^c/(c!(1-ρ)) · P0
EOQ:     Q* = √(2DK/h)     T* = Q*/D     CT = DK/Q + hQ/2 + DC
Con producción: Q* = √( 2DK / (h(1 - D/P)) )
Punto de reorden: R = d·L + stock de seguridad
```
Ejemplo (colas): λ = 8 clientes/h, μ = 10/h, un servidor. ρ = 0.8; L = 4; Wq = 0.8/(10-8) = 0.4 h = 24 min.
Ejemplo (EOQ): D = 1200 u/año, K = 50, h = 6 → Q* = √(2·1200·50/6) = √20000 ≈ 141 u; pedidos/año ≈ 8.5.
Ejemplo (Markov): P = ((0.7, 0.3), (0.4, 0.6)) → π₁ = 0.4/(0.3+0.4) = 4/7 ≈ 0.571, π₂ = 3/7.
Ejemplo (juego): matriz de pagos ((3,1),(2,4)) para el jugador de filas. Maximin = 2, minimax = 3, no hay punto de silla. Estrategia mixta: p (fila 1) = (a22 − a21)/(a11 + a22 − a12 − a21) = 2/4 = 0.5; valor v = (a11·a22 − a12·a21)/(a11 + a22 − a12 − a21) = (12 − 2)/4 = 2.5. Comprobación: 3(0.5)+2(0.5) = 2.5 y 1(0.5)+4(0.5) = 2.5.

### Cómo se relaciona con otras materias
[[Investigación de Operaciones I]] (programación lineal para juegos), [[Estadística II]] (distribuciones Poisson, exponencial), [[Matemática IV]]/[[Matemática III]] (álgebra matricial). Desbloquea [[Simulación de Sistemas]] (validación de simulaciones contra fórmulas analíticas). Aplica en [[Gerencia de Proyectos]] y [[Ingeniería Económica]] (costos de espera e inventario).

### Evaluación y consejos
El programa indica: pruebas de desarrollo, pruebas cortas y **proyecto con defensa**; el material guardado incluye un caso de estudio de cadenas de Markov, de inventario y de teoría de juegos, y un MVP web de colas (ver [[MVP Colas]]). Consejos: domine el manejo matricial (inversa, potencias), identifique siempre λ y μ en las mismas unidades, y justifique la estabilidad (ρ<1).

### Bibliografía
- Taha, H. *Investigación de Operaciones* (9.ª ed., PDF en Material).
- Hillier y Lieberman. *Introducción a la Investigación de Operaciones*.
- Gross y Harris. *Fundamentals of Queueing Theory*.
- Binmore, K. *Teoría de Juegos*; Howard, R. *Dynamic Probabilistic Systems*.

### Recursos del Material/
- [investigación-de-operaciones-9na-edición-hamdy-a-taha (PDF)](Material/investigacic3b3n-de-operaciones-9na-edicic3b3n-hamdy-a-taha-fl.pdf): libro de Taha.
- [ProgramaInvOperacionesII.doc](Material/ProgramaInvOperacionesII.doc): programa sinóptico (fuente del contenido anterior).
- [presentación.m4a](Material/presentación.m4a) y [sesionSincrona2.mp4](Material/sesionSincrona2.mp4): audio y video de clases (no leídos).
- Fuera del vault: `~/Documentos/UNET/Investigacion de Operacion 2` (Markov objetivos 1-3, inventario, teoría de juegos, `mvpio2`) y `~/Documentos/UNET/IO2`.
