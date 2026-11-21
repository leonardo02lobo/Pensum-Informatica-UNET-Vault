---
tags: [materia, semestre-III]
semestre: III
---
# Matemática III

**Semestre:** [[Semestre III]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Matemática II]]

## Desbloquea
- [[Matemática IV]]
- [[Estadística I]]

## Apuntes

### Descripción general y objetivos

Matemática III es el curso de **cálculo en varias variables** (cálculo multivariable): extiende derivadas e integrales de [[Matemática II]] a funciones vectoriales, superficies y funciones de varias variables. Es prelación de [[Matemática IV]] (cálculo vectorial, variable compleja, ecuaciones diferenciales) y de [[Estadística I]] (integrales múltiples para distribuciones continuas). Verificar con el programa oficial el sinóptico exacto; el temario siguiente es el estándar del curso y el que se infiere del Material.

Objetivos: describir curvas y superficies en el espacio, calcular derivadas parciales y optimizar funciones de varias variables, y evaluar integrales dobles y triples en distintos sistemas de coordenadas.

### Contenido programático (referencial)

#### Unidad 1. Vectores, curvas y funciones vectoriales
- Vectores en R² y R³: producto escalar, producto vectorial, rectas y planos.
- Ecuaciones paramétricas y curvas en el plano y el espacio.
- Funciones vectoriales: límite, derivada, integral.
- **Velocidad, aceleración y rapidez**; vector tangente unitario; longitud de arco; curvatura (componentes tangencial y normal de la aceleración).

#### Unidad 2. Superficies y funciones de varias variables
- Superficies cuádricas: elipsoide, hiperboloides, paraboloide elíptico, **paraboloide hiperbólico**, conos y cilindros; trazas y curvas de nivel.
- Funciones de varias variables, dominios, límites y continuidad.
- Derivadas parciales, plano tangente, diferencial total, regla de la cadena.
- Derivada direccional y gradiente.
- Extremos: puntos críticos, criterio de la segunda derivada (hessiano) y multiplicadores de Lagrange.

#### Unidad 3. Integración múltiple
- Integrales dobles sobre rectángulos y regiones generales; cambio a coordenadas polares.
- Integrales triples; coordenadas cilíndricas y esféricas.
- Aplicaciones: área, volumen, masa, centro de masa, momentos de inercia.
- Cambio de variables y jacobiano.

### Conceptos clave

- **Función vectorial** `r(t) = x(t) i + y(t) j + z(t) k`.
- **Gradiente**: `∇f = (f_x, f_y, f_z)` apunta en la dirección de máximo crecimiento.
- **Traza**: intersección de una superficie con un plano coordenado o paralelo a él.
- **Jacobiano**: factor de cambio de área/volumen al cambiar de coordenadas.

### Fórmulas

```
Velocidad:   v(t) = r'(t) = x'(t) i + y'(t) j + z'(t) k
Aceleración: a(t) = r''(t)
Rapidez:     ||v(t)|| = sqrt( x'² + y'² + z'² )
Long. arco:  s = ∫_a^b ||r'(t)|| dt
Derivada direccional: D_u f = ∇f · u        (u unitario)
Plano tangente:  f_x(x0,y0)(x-x0) + f_y(x0,y0)(y-y0) - (z-z0) = 0
Hessiano:   D = f_xx f_yy - (f_xy)²   (D>0, f_xx>0 mínimo; D>0, f_xx<0 máximo; D<0 silla)
Polares:    dA = r dr dθ
Cilíndricas: dV = r dz dr dθ
Esféricas:   dV = ρ² sen φ dρ dφ dθ
Paraboloide hiperbólico:  z = x²/a² - y²/b²
```

### Ejemplos resueltos

1. **Velocidad y aceleración** (ejemplo del Material): `r(t) = 2 sen(t/2) i + 2 cos(t/2) j`. Entonces `v = cos(t/2) i - sen(t/2) j`, `a = -½ sen(t/2) i - ½ cos(t/2) j`. Como `x² + y² = 4`, la partícula recorre una circunferencia de radio 2 con rapidez constante 1.
2. **Gradiente**: `f(x,y) = x² y`, `∇f(1,2) = (2xy, x²) = (4, 1)`.
3. **Paraboloide hiperbólico** `z = x² - y²`: traza en `z = 0` son las rectas `y = ±x`; traza en `y = 0` es la parábola `z = x²`; en `x = 0`, `z = -y²`. Punto silla en el origen.
4. **Integral doble**: `∬_D (x + y) dA` con D = [0,1]x[0,2] = `∫0^1 ∫0^2 (x+y) dy dx = ∫0^1 (2x + 2) dx = 3`.

### Relación con otras materias

- Prelación: [[Matemática II]] (derivadas e integrales de una variable, series).
- Desbloquea [[Matemática IV]] (campos vectoriales, integrales de línea y superficie) y [[Estadística I]] (densidades de probabilidad e integrales).
- Aplica en [[Física II]] (campos eléctricos y magnéticos), [[Análisis Numérico]] y [[Investigación de Operaciones I]] (optimización con restricciones).

### Evaluación y consejos de estudio

- Visualizar siempre: dibujar la región de integración antes de plantear los límites; usar GeoGebra o Desmos 3D para superficies.
- Elegir el sistema de coordenadas según la simetría (círculos -> polares, esferas -> esféricas).
- Practicar muchas integrales iteradas; el error típico es el orden o los límites.
- Parciales: hay un segundo parcial con ejercicios y exposiciones de grupo (ver Material). Ponderación: verificar con el programa oficial.

### Bibliografía recomendada

- Larson, Hostetler, Edwards. *Cálculo*, Vol. 2 (capítulos 11 a 14: vectores, funciones vectoriales, varias variables, integración múltiple).
- Stewart, J. *Cálculo de varias variables*.
- Purcell, Varberg, Rigdon. *Cálculo*.
- Thomas. *Cálculo: varias variables*.

### Recursos del Material/

- [Exposicion de Mate III, velocidad y aceleracion.docx](Material/Exposicion%20de%20Mate%20III,%20velocidad%20y%20aceleracion.docx): exposición basada en Larson sobre movimiento a lo largo de una curva, con ejemplos de velocidad, aceleración y rapidez.
- [paraboloide hiperbolica.docx](Material/paraboloide%20hiperbolica.docx): trabajo sobre cómo se construye y actúa el paraboloide hiperbólico y sus trazas.
- [ejercicios segundo parcial.docx](Material/ejercicios%20segundo%20parcial.docx): ejercicios para el segundo parcial (el documento contiene principalmente imágenes).
