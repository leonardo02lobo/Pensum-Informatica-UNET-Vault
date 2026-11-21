---
tags: [materia, semestre-V]
semestre: V
---
# Análisis Numérico

**Semestre:** [[Semestre V]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Matemática IV]]

## Desbloquea
- [[Investigación de Operaciones I]]

## Apuntes

### Descripción general y objetivos
Análisis Numérico (también llamado *Métodos Numéricos* en el aula virtual de la UNET) estudia algoritmos que aproximan soluciones de problemas matemáticos que no tienen solución analítica práctica: raíces de ecuaciones, ajuste de datos, sistemas lineales y no lineales, integrales y ecuaciones diferenciales. Se trabaja con MATLAB (o Scilab/Octave) y se pone énfasis en **convergencia, error y costo computacional**. Los objetivos son: (1) elegir el método adecuado según el problema, (2) implementarlo en código propio, (3) cuantificar el error y fijar criterios de parada, (4) interpretar resultados en problemas de ingeniería.

La materia sigue seis temas (según las carpetas del Material; verificar con el programa oficial el sinóptico exacto) y se evalúa por parciales más asignaciones grupales con video + script y coevaluación entre grupos (ver `Instructivo para realizar las asignaciones.pdf`).

### Contenido programático
1. **Tema 1. Aproximaciones y errores**
   - Cifras significativas, exactitud y precisión.
   - Error absoluto, relativo y porcentual; error de redondeo y de truncamiento.
   - Serie de Taylor y propagación de errores; aritmética de punto flotante (épsilon de máquina).
2. **Tema 2. Solución de ecuaciones de una variable**
   - Bisección, falsa posición, punto fijo, Newton-Raphson, secante.
   - Orden de convergencia, criterios de parada, raíces múltiples.
3. **Tema 3. Interpolación y aproximación polinomial**
   - Polinomio de Lagrange, diferencias divididas de Newton, trazadores (splines).
   - Mínimos cuadrados (regresión lineal y polinomial).
4. **Tema 4. Sistemas de ecuaciones lineales y no lineales**
   - Eliminación gaussiana con pivoteo, factorización LU (Doolittle, Crout), matrices tridiagonales.
   - Métodos iterativos: Jacobi, Gauss-Seidel, SOR; normas vectoriales/matriciales; número de condición.
   - Sistemas no lineales: punto fijo multivariable y Newton con matriz jacobiana.
5. **Tema 5. Integración numérica**
   - Fórmulas de Newton-Cotes cerradas/abiertas: trapecio, Simpson 1/3 y 3/8; versiones compuestas.
   - Cuadratura de Gauss-Legendre, integración de Romberg.
6. **Tema 6. Ecuaciones diferenciales**
   - Problemas de valor inicial: Euler, Euler mejorado/Heun, Runge-Kutta (orden 2 y 4), sistemas de EDO.
   - Introducción a EDP (elípticas, parabólicas, hiperbólicas) por diferencias finitas y elementos finitos (Práctica 7).

### Conceptos clave y definiciones
- **Error absoluto**: `E = |x - x*|`; **relativo**: `E/|x|`.
- **Convergencia de orden p**: `|e_{n+1}| ≈ C |e_n|^p`. Bisección: lineal; secante: ≈1.618; Newton: cuadrática (raíz simple).
- **Condición** de un problema: sensibilidad de la salida a perturbaciones de la entrada; `cond(A)=||A||·||A^-1||`.
- **Estabilidad** de un algoritmo y **consistencia** de un método en EDO.
- **Diagonal dominante**: condición suficiente de convergencia de Jacobi/Gauss-Seidel.

### Fórmulas y algoritmos
```
Bisección:       c = (a+b)/2 ; si f(a)f(c)<0 -> b=c, si no a=c
                 iteraciones n >= log2((b-a)/tol)
Newton-Raphson:  x_{n+1} = x_n - f(x_n)/f'(x_n)
Secante:         x_{n+1} = x_n - f(x_n)(x_n - x_{n-1})/(f(x_n)-f(x_{n-1}))
Newton sistemas: J(x_k) * d = -F(x_k) ; x_{k+1} = x_k + d
Gauss-Seidel:    x_i^{(k+1)} = (b_i - sum_{j<i} a_ij x_j^{(k+1)} - sum_{j>i} a_ij x_j^{(k)})/a_ii
SOR:             x_i^{(k+1)} = (1-w) x_i^{(k)} + w * (valor de Gauss-Seidel),  0<w<2
Trapecio:        I ≈ (b-a)(f(a)+f(b))/2        Simpson 1/3: (b-a)(f(a)+4f(m)+f(b))/6
Euler:           y_{n+1} = y_n + h f(t_n,y_n)
RK4:             y_{n+1} = y_n + h/6 (k1+2k2+2k3+k4)
```
Ejemplo de código MATLAB (bisección, en la línea de los scripts del Material):
```matlab
function [x, it] = biseccion(f, a, b, tol, itmax)
  for it = 1:itmax
    x = (a+b)/2;
    if abs(f(x)) < tol || (b-a)/2 < tol, return; end
    if f(a)*f(x) < 0, b = x; else a = x; end
  end
end
```

### Ejemplo resuelto
Raíz de `f(x)=x^2-2` con Newton y `x0=1`: `x1 = 1 - (-1)/2 = 1.5`; `x2 = 1.5 - 0.25/3 = 1.41667`; `x3 = 1.41422`. El error pasa de ~1e-1 a ~1e-3 a ~1e-6 (convergencia cuadrática). Con bisección en [1,2] y tol=1e-6 se necesitan `ceil(log2(1/1e-6)) = 20` iteraciones.

### Relación con otras materias
Se apoya en [[Matemática II]], [[Matemática III]] y [[Matemática IV]] (cálculo, álgebra lineal, EDO) y en [[Programación II]] para la implementación. Es prelación de [[Investigación de Operaciones I]] (símplex = álgebra lineal numérica) y se vincula con [[Simulación de Sistemas]]. Notas hijas: [[Análisis Numérico - Newton-Raphson y Secante]] y [[Análisis Numérico - Gauss con pivoteo y factorización LU]].

### Evaluación y consejos de estudio
- Tres parciales con ejercicios resueltos a mano y en MATLAB; asignaciones grupales (video y script) con coevaluación. Verificar ponderaciones con el programa oficial.
- Programa cada algoritmo desde cero al menos una vez; las prácticas piden funciones propias (`biseccion.m`, `newtonse.m`).
- Practica la tabla de iteraciones a mano (parciales) y fija siempre el criterio de parada.
- Revisa las normas (Práctica 4) antes de los métodos iterativos.

### Bibliografía recomendada
- Burden, R. y Faires, J. *Análisis Numérico*. Cengage.
- Chapra, S. y Canale, R. *Métodos Numéricos para Ingenieros*. McGraw-Hill.
- Mathews, J. y Fink, K. *Métodos Numéricos con MATLAB*. Prentice Hall.

### Recursos del Material/
- [Instructivo para realizar las asignaciones](Material/Instructivo%20para%20realizar%20las%20asignaciones.pdf): pautas de video, script y coevaluación.
- [Asignación 1 (2024-III)](Material/Asignac_1_2024-IIIa.pdf): problemas de bisección/Newton/secante (ala NACA 0012, equilibrio químico).
- [Asignación 2](Material/Asignacion2_S4.pdf) y [Asignación 3](Material/Asignacion3_2.pdf): enunciados de las asignaciones grupales siguientes.
- Carpeta `Tema 1` a `Tema 6`: prácticas en PDF (errores, ecuaciones no lineales, mínimos cuadrados, Gauss con pivote y LU, Gauss-Seidel, SOR, sistemas no lineales, integración, EDO), scripts .m (`metodo_biseccion.m`, `metodo_Newthon.m`, `metodo_secante.m`) y zips con scripts de los temas 4 y 5.
- Ejemplos: [Ejercicios resueltos Parcial 1](Material/Parcial%201/Ejercicio_resueltos%20Parcial%201.docx), [ejercicio resuelto Parcial 2](Material/Parcial%202/ejercicio-resuelto%20parcial%202.docx) y [Parcial2.m](Material/Parcial%202/Parcial2.m) (reordenamiento con symrcm y factorización de Crout de un sistema tridiagonal).
