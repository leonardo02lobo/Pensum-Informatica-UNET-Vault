---
tags: [materia, semestre-IV]
semestre: IV
---
# Matemática IV

**Semestre:** [[Semestre IV]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Matemática III]]

## Desbloquea
- [[Análisis Numérico]]
- [[Investigación de Operaciones I]]

## Apuntes

### Descripción general y objetivos

Matemática IV (código 0826401, 4 UC, 4 h de teoría y 2 h de práctica semanales, programa vigente desde agosto de 2004 según el analítico del Material) cubre **cálculo vectorial, variable compleja y ecuaciones diferenciales**. Prelación: [[Matemática III]]. Desbloquea [[Análisis Numérico]] e [[Investigación de Operaciones I]].

Objetivo terminal (analítico): definir e interpretar geométricamente los conceptos del cálculo vectorial y calcular derivadas e integrales de funciones vectoriales; aplicar los teoremas integrales; trabajar con funciones de variable compleja (límites, derivadas, integrales); y plantear y resolver ecuaciones diferenciales.

### Contenido programático (según el programa analítico)

#### Unidad I. Cálculo vectorial
1. Campos vectoriales y escalares; gradiente de un campo escalar.
2. Divergencia y rotacional.
3. Integral de línea: masa de un alambre, trabajo.
4. Campos conservativos, función potencial e independencia de la trayectoria.
5. **Teorema de Green** en el plano y sus formas vectoriales; flujo a través de una curva.
6. Integrales de superficie y flujo de un campo vectorial.
7. **Teorema de la divergencia (Gauss)** y **Teorema de Stokes**.

#### Unidad II. Variable compleja
1. Números complejos: forma binómica, módulo, propiedades, plano complejo.
2. Forma polar, **teorema de De Moivre**, raíces n-ésimas, fórmula de Euler; ecuaciones polinómicas.
3. Funciones de variable compleja, límites, continuidad y derivada.
4. **Funciones analíticas**, ecuaciones de Cauchy-Riemann, funciones armónicas, puntos singulares (aislado, polo, removible, esencial, de ramificación).
5. Integrales complejas de línea, teorema de Cauchy-Goursat, fórmulas integrales de Cauchy.
6. **Teorema del residuo**.

#### Unidad III. Ecuaciones diferenciales de primer orden
- Definición, clasificación (tipo, orden, linealidad), solución y problema de valor inicial; modelado.
- Variables separables, exactas, lineales (factor integrante/variación de parámetros), sustituciones (homogéneas, Bernoulli).
- Aplicaciones: crecimiento y decaimiento, mezclas, circuitos, enfriamiento.

#### Unidad IV. Ecuaciones diferenciales de orden superior
- Lineales homogéneas y no homogéneas; principio de superposición; wronskiano; conjunto fundamental.
- Reducción de orden; coeficientes constantes; coeficientes indeterminados (anulador); variación de parámetros; ecuación de Cauchy-Euler.
- Soluciones por series, sistemas de ecuaciones lineales.
- Modelado: movimiento libre no amortiguado, amortiguado, forzado y sistemas análogos (circuito RLC).

Según el analítico, las evaluaciones están asociadas a hitos como el Parcial I en la semana 5, Parcial II en la semana 8, Parcial III en la semana 12 y Parcial IV en la semana 16 (verificar con el docente del lapso).

### Conceptos clave

- **Campo conservativo**: `F = ∇φ`; equivale a `rot F = 0` en una región simplemente conexa; la integral de línea no depende del camino.
- **Analiticidad**: f(z) = u + iv es analítica si u, v cumplen Cauchy-Riemann.
- **Residuo** de f en z0: coeficiente a_{-1} de la serie de Laurent.
- **Solución general** de una EDO lineal de orden n: combinación de n soluciones linealmente independientes más una particular.

### Fórmulas

```
Gradiente: ∇f = (f_x, f_y, f_z)
Divergencia: div F = ∂P/∂x + ∂Q/∂y + ∂R/∂z
Rotacional:  rot F = ∇ × F
Integral de línea:  ∫_C F·dr = ∫_a^b F(r(t))·r'(t) dt
Green:   ∮_C P dx + Q dy = ∬_D (∂Q/∂x - ∂P/∂y) dA
Gauss:   ∯_S F·n dS = ∭_V div F dV
Stokes:  ∮_C F·dr = ∬_S (rot F)·n dS

De Moivre:  z^n = r^n (cos nθ + i sen nθ)
Euler:      e^{iθ} = cos θ + i sen θ
Raíces:     z^{1/n} = r^{1/n} [cos((θ+2πk)/n) + i sen((θ+2πk)/n)], k=0..n-1
Cauchy-Riemann:  u_x = v_y,   u_y = -v_x
Fórmula integral de Cauchy:  f(a) = (1/2πi) ∮ f(z)/(z-a) dz
Residuos:   ∮_C f(z) dz = 2πi Σ Res(f, z_k)

Lineal 1.er orden: y' + P(x)y = Q(x)   ->   μ = e^{∫P dx},  y = (1/μ)∫ μQ dx
Coef. constantes: a y'' + b y' + c y = 0  ->  ecuación característica a r² + b r + c = 0
```

### Ejemplos resueltos

1. **Campo conservativo**: `F = (2xy, x²)`; `∂P/∂y = 2x = ∂Q/∂x`, entonces `φ = x² y`. Trabajo de (0,0) a (1,2) = φ(1,2) - φ(0,0) = 2.
2. **Green**: `∮ -y dx + x dy` sobre una curva cerrada = `∬ 2 dA = 2·Área`.
3. **Complejos**: `(1+i)^4 = (√2)^4 (cos π + i sen π) = -4`.
4. **EDO**: `y' + 2y = e^{-x}`: `μ = e^{2x}`, `(e^{2x}y)' = e^{x}`, `y = e^{-x} + C e^{-2x}`.
5. **Orden 2**: `y'' - 3y' + 2y = 0`, raíces 1 y 2, `y = C1 e^{x} + C2 e^{2x}`.

### Relación con otras materias

- Continúa [[Matemática III]] (integrales múltiples y funciones vectoriales).
- Desbloquea [[Análisis Numérico]] (métodos numéricos para EDO) e [[Investigación de Operaciones I]].
- Se vincula con [[Física II]] (Maxwell, Gauss, Stokes) y con control en [[Automatización]] (transformadas y EDO), además de [[Simulación de Sistemas]].

### Evaluación y consejos de estudio

- Hacer los ejercicios recomendados del programa (Purcell, Spiegel, Zill) por tema.
- Dominar la parametrización de curvas y superficies; casi todo error en integrales de línea y superficie nace ahí.
- En complejos, dibujar siempre el plano y los contornos.
- En EDO, clasificar primero la ecuación (separable, exacta, lineal...) antes de elegir método.
- La modalidad intensiva sigue la guía didáctica del Prof. Gerson Barazarte (marzo 2024) con reuniones virtuales y foros.

### Bibliografía recomendada (según el programa)

- Purcell, E. y Varberg, D. *Cálculo y geometría analítica*.
- Larson, Hostetler. *Cálculo*; Stewart, J. *Cálculo multivariable*.
- Churchill. *Variables complejas con aplicaciones*; Spiegel. *Variables complejas* (Schaum).
- Edwards y Penney. *Ecuaciones diferenciales elementales*; Zill, D. *Ecuaciones diferenciales*.
- Kreyszig, E. *Matemática avanzada para ingeniería*.

### Recursos del Material/

- [Programa Analítico Matematica IV.pdf](Material/Programa%20Anal%C3%ADtico%20Matematica%20IV.pdf): objetivos, contenidos, ejercicios recomendados y semanas de parcial.
- [Guia Didactica intensivo (Autoguardado).pdf](Material/Guia%20Didactica%20intensivo%20%20(Autoguardado).pdf): guía didáctica de la modalidad intensiva (ruta de aprendizaje por unidades).
- [Unidad I.pdf](Material/Unidad%201/Unidad%20I.pdf): plan de actividades de la Unidad I (lecturas de Larson sobre campos vectoriales, integrales de línea).
- [CAP_15_LARSON.pdf](Material/libros/CAP_15_LARSON.pdf): capítulo 15 de Larson (cálculo vectorial).
- [Calculo_Vectorial_Stewart.pdf](Material/libros/Calculo_Vectorial_Stewart.pdf): cálculo vectorial de Stewart.
- [Ecuaciones Diferenciales_CAP1_2_Edwars Penney.pdf](Material/libros/Ecuaciones%20Diferenciales_CAP1_2_Edwars%20Penney.pdf): capítulos 1 y 2 de ecuaciones diferenciales.
