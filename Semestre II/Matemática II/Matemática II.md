---
tags: [materia, semestre-II]
semestre: II
---
# Matemática II

**Semestre:** [[Semestre II]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Matemática I]]

## Desbloquea
- [[Matemática III]]

## Apuntes

### Descripción general y objetivos
Matemática II continúa el cálculo de una variable con **cálculo integral** y sus aplicaciones, series y (según el programa) introducción a ecuaciones o funciones de varias variables. Prelación: [[Matemática I]]; desbloquea [[Matemática III]]. Esta carpeta no contiene Material; el temario es el habitual y debe **verificarse con el programa oficial** de la UNET.

### Contenido programático (típico)
1. **Integral indefinida**: antiderivada, tabla de integrales, sustitución (cambio de variable).
2. **Técnicas de integración**: por partes, trigonométricas, sustitución trigonométrica, fracciones parciales.
3. **Integral definida**: sumas de Riemann, Teorema Fundamental del Cálculo, propiedades.
4. **Aplicaciones**: área entre curvas, volúmenes (discos, arandelas, cascarones), longitud de arco, trabajo, valor promedio.
5. **Integrales impropias**: límites infinitos e integrandos no acotados, convergencia.
6. **Sucesiones y series**: convergencia, criterios (razón, raíz, comparación, integral), series de potencias, Taylor y Maclaurin (si el programa lo incluye).

### Fórmulas clave
```
∫ xⁿ dx = xⁿ⁺¹/(n+1) + C  (n ≠ -1);   ∫ 1/x dx = ln|x| + C
∫ eˣ dx = eˣ + C;  ∫ sen x dx = -cos x + C;  ∫ cos x dx = sen x + C
Por partes:  ∫ u dv = u v - ∫ v du
TFC:  ∫_a^b f(x)dx = F(b) - F(a)
Área entre curvas: A = ∫_a^b [f(x) - g(x)] dx
Volumen por discos: V = π ∫_a^b [f(x)]² dx
Taylor: f(x) = Σ f⁽ⁿ⁾(a)/n! · (x-a)ⁿ
```

### Ejemplos resueltos
1. ∫ x·eˣ dx: u=x, dv=eˣdx → x eˣ - ∫ eˣ dx = eˣ(x-1) + C.
2. Área entre y=x y y=x² en [0,1]: ∫(x - x²)dx = 1/2 - 1/3 = 1/6.
3. ∫_1^∞ 1/x² dx = lim_{b→∞}(1 - 1/b) = 1 (converge).

### Relación con otras materias
Requiere derivación de [[Matemática I]]; base de [[Matemática III]], [[Matemática IV]], [[Física I]] y [[Física II]] (trabajo, centros de masa, campos), [[Estadística I]] (distribuciones continuas) y [[Análisis Numérico]] (integración numérica).

### Evaluación y consejos
Evaluación por parciales; practica muchos ejercicios por técnica, memoriza la tabla de integrales y las identidades trigonométricas, y verifica derivando el resultado.

### Bibliografía recomendada
- Stewart, *Cálculo de una variable*; Leithold, *El Cálculo*; Purcell, Varberg y Rigdon, *Cálculo*; Larson, *Cálculo*; Demidovich, *Problemas de análisis matemático*.

### Recursos del Material/
No hay carpeta `Material/` para esta materia.
