---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/Instructivo para realizar las asignaciones.pdf
---
# Análisis Numérico - Instructivo de asignaciones

Materia: [[Análisis Numérico]]
Siguiente: [[Análisis Numérico - Práctica 1 Errores de redondeo]]

## Contexto y objetivo
El instructivo (Prof. Blanca L. Guillén V. y Prof. Jenny E. Pérez R., Departamento de Matemática y Física, UNET) fija las reglas de las **asignaciones colaborativas** de Métodos Numéricos. El objetivo declarado es que el estudiante desarrolle destrezas para resolver problemas de aplicación práctica: plantear la ecuación matemática a partir de los datos, seleccionar el método numérico adecuado, programarlo en MATLAB o Scilab, obtener la solución bajo un criterio de parada, calcular el error y analizar los resultados. Además busca fomentar el trabajo en equipo y la coevaluación entre pares, y sirve de entrenamiento para el cuestionario en línea (los parciales de esta materia son cuestionarios del aula virtual, ver [[Análisis Numérico - Parcial 1 cuestionario resuelto]] y [[Análisis Numérico - Parcial 2 cuestionario resuelto]]).

## Dinámica de trabajo
1. **Trabajo grupal**: la sección se divide aleatoriamente en grupos de a lo sumo 4 integrantes.
2. **Un ejercicio por grupo**: cada asignación tiene tantos problemas como grupos; el profesor asigna uno por grupo al azar.
3. **Un video y un script por grupo**: video de 3 a 5 minutos (Drive o YouTube) y un script en MATLAB o Scilab.
4. **Dos archivos de entrega**: (a) un documento Word con número de grupo, nombres completos y enlace del video; (b) el script `*.m` (o `*.sce`; si el aula no lo admite, renombrar a `.m`). Nomenclatura obligatoria: `Asignacion#Ejercicio#G#S#` (G = grupo, S = sección). Ejemplo del documento: `Asignacion1Ejercicio3G4S2.doc` y `.m`. Los scripts de [[Análisis Numérico - Asignación 1 NACA y ajuste de datos]] siguen esa regla (`Asignacion1Ejercicio1G1S4`).
5. **Coevaluación**: cada grupo evalúa el video de un grupo par con la planilla del profesor (ver [[Análisis Numérico - Formato de coevaluación]]), sube el documento al foro con la nomenclatura `Grupo#CoevaluaAGrupo#` (p. ej. `Grupo1CoevaluaAGrupo3.doc`) y da retroalimentación.
6. **Foro de coevaluación**: cada asignación tiene su foro, donde se comparte el enlace del video, el script y el documento de coevaluación, respetando la "regla de oro": respeto a todos.
7. **Fechas**: las fija el cronograma de la guía de evaluación; la hora límite es 23:55 del día indicado (para entrega y para coevaluación).

## Pautas de solución: las cinco etapas
El instructivo ilustra el procedimiento con un ejemplo práctico (tomado del libro de Nakamura, *Análisis numérico y visualización gráfica con Matlab*): hallar la intersección de $y=\sqrt{x^2+1}$ con $y=\tan x$, $0<x<\pi/2$.

1. **Planteamiento del problema matemático.** Se igualan ambas curvas: $\sqrt{x^2+1}-\tan x=0$.
2. **Planteamiento del problema numérico.** Se define con exactitud $f(x)=\sqrt{x^2+1}-\tan x$ y se reduce el problema a encontrar un cero de $f$.
3. **Método numérico a utilizar.** Se verifican las hipótesis. Para bisección: (a) $f$ continua en $[a,b]$ y (b) $f(a)f(b)<0$ (teorema de Bolzano). Se grafica para localizar un cambio de signo (la gráfica orienta, pero no sustituye la revisión del dominio de continuidad: $f$ es continua en $(0,\pi/2)$). Se elige el intervalo más corto posible, $[0.8,1.0]$, porque bisección converge lento. Se comprueba analíticamente: $f(0.8)=0.250986$, $f(1)=-0.143194$. Se fijan $tol=10^{-6}$, un máximo de 40 iteraciones y el criterio $|x_i-x_{i-1}|<\xi$.
4. **Solución y presentación de resultados** con tablas y gráficos. La función y el script se separan:
```matlab
function f = fraiz(x)
  f = sqrt(1+x.^2) - tan(x);
end
% script de llamada
a = 0.8; b = 1.0; tol = 0.000001; it = 40;
fprintf('\n\n Método de Bisección \n \n')
[raiz, iter] = biseccion('fraiz', a, b, tol, it)
```
5. **Análisis de resultados.** Preguntas guía: ¿tiene sentido la solución?, ¿es confiable?, ¿cuál es el error? En el ejemplo: 18 iteraciones, $x=0.941462$; se verifica evaluando ambas curvas: $\sqrt{0.941462^2+1}=1.3734$ y $\tan(0.941462)=1.3734$.

## Verificación del ejemplo
Con bisección sobre $[0.8,1]$ y tolerancia $10^{-6}$: la longitud del intervalo tras $n$ pasos es $0.2/2^n$; $0.2/2^{18}=7.6\times10^{-7}<10^{-6}$, de ahí las 18 iteraciones. Primera iteración: $x_1=0.9$, $f(0.9)=0.085204>0$, igual signo que $f(0.8)$, luego el nuevo intervalo es $[0.9,1]$.

## Qué evalúa el instructivo (y errores comunes)
- Entregar solo el script con salida sin planteamiento: se pide explícitamente verificar hipótesis del método.
- Explicar el código en el video: la planilla indica que el video debe mostrar resultados y análisis, **no** explicar el algoritmo ni el código.
- Incluir en el script funciones o datos innecesarios: la planilla evalúa que solo estén los necesarios.
- Nombres de archivo que no siguen la nomenclatura.

## Ejercicios propuestos
1. ¿Cuántas iteraciones mínimas de bisección garantizan error menor que $10^{-6}$ partiendo de $[0.8,1]$? (Resp.: 18.)
2. Plantee los cinco pasos para hallar la intersección de $y=e^{-x}$ con $y=x$. (Resp.: $f(x)=e^{-x}-x$, $[0,1]$, $f(0)=1>0$, $f(1)<0$, raíz $\approx0.5671$.)

## Conexiones
Aplica los métodos de [[Análisis Numérico - Bisección]] y [[Análisis Numérico - Newton-Raphson y Secante]]. Los enunciados concretos están en [[Análisis Numérico - Asignación 1 NACA y ajuste de datos]], [[Análisis Numérico - Asignación 2 Sistemas lineales]] y [[Análisis Numérico - Asignación 3 EDO y problemas de frontera]].

## Fuente
`Material/Instructivo para realizar las asignaciones.pdf` (texto extraído completo).
