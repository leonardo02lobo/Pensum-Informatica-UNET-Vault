---
tags: [clase, semestre-III]
materia: Física II
fuente: Material/Tarea 1.docx
---
# Física II - Tarea 1 Valor absoluto en matemáticas y física

Materia: [[Física II]]
Anterior: [[Física II - Libro Sears-Zemansky y mapa del curso]]
Siguiente: [[Física II - Carga eléctrica y ley de Coulomb]]

## Contexto y objetivo
`Tarea 1.docx` es una tarea de Física 2 (Departamento de Matemática y Física, noviembre de 2024) sobre el **valor absoluto**: qué es, propiedades, interpretación geométrica y aplicaciones en física. Las fórmulas del docx no se conservaron en la conversión a texto; aquí se reconstruyen con las definiciones estándar. El valor absoluto es clave en Física II: la ley de Coulomb usa $|q_1q_2|$ para obtener la magnitud de la fuerza, y el signo se maneja aparte.

## 1. Definición formal
$$|x| = \begin{cases} x & \text{si } x \ge 0\\ -x & \text{si } x<0\end{cases}$$
Es el número sin su signo; geométricamente, su **distancia al cero** en la recta numérica (|-5| = |5| = 5).

## 2. Propiedades (las cinco de la tarea)
1. **No negatividad**: $|x|\ge0$, y $|x|=0 \iff x=0$.
2. **Identidad**: $|x|=|-x|$ (simetría, listada aparte en la tarea).
3. **Multiplicación**: $|xy|=|x||y|$.
4. **Desigualdad triangular**: $|x+y|\le|x|+|y|$.
5. Cociente: $|x/y|=|x|/|y|$ ($y\ne0$); y $|x|^2=x^2$, $\sqrt{x^2}=|x|$.

Demostración de la desigualdad triangular: como $-|x|\le x\le|x|$ y $-|y|\le y\le|y|$, sumando: $-(|x|+|y|)\le x+y\le|x|+|y|$, que equivale a $|x+y|\le|x|+|y|$.

## 3. Aplicaciones matemáticas
- **Distancia** entre $a$ y $b$: $d=|a-b|$. Ejemplo de la tarea: entre -3 y 4: $|4-(-3)|=7$.
- **Ecuaciones**: $|x-2|=5$ se divide en dos casos: $x-2=5\Rightarrow x=7$; $x-2=-5\Rightarrow x=-3$. Soluciones: $x=7$ y $x=-3$.
- **Desigualdades**: $|x-a|<r \iff a-r<x<a+r$; $|x-a|>r\iff x<a-r$ o $x>a+r$.
- **Función** $f(x)=|x|$: gráfica en forma de "V" con vértice en (0,0), abierta hacia arriba.

## 4. Valor absoluto en física
- **Distancia vs. desplazamiento**: si un objeto va de $x_1$ a $x_2$ el desplazamiento es $\Delta x=x_2-x_1$ (con signo) y la distancia en un solo tramo es $|x_2-x_1|$; si cambia de sentido, la distancia total es la suma de los valores absolutos de cada tramo.
- **Rapidez**: $|v|$ (magnitud del vector velocidad).
- **Magnitud de vectores**: fuerza, desplazamiento, aceleración: $|\vec F|=\sqrt{F_x^2+F_y^2+F_z^2}$.
- **Energía**: la cinética $\tfrac12 mv^2$ es siempre positiva (depende de $|v|^2$); para la potencial se usa |ΔU| cuando solo interesa la cantidad.
- **Electricidad (este curso)**: $F=k\dfrac{|q_1q_2|}{r^2}$ y $E=k\dfrac{|q|}{r^2}$ dan magnitudes; atracción o repulsión se decide por los signos ([[Física II - Carga eléctrica y ley de Coulomb]]).

## 5. Ejemplo práctico: movimiento rectilíneo
Un móvil va de $x=2$ m a $x=10$ m y luego regresa a $x=6$ m.
- Desplazamiento: $6-2=+4$ m.
- Distancia: $|10-2|+|6-10|=8+4=12$ m.
- Si el viaje total dura 6 s: velocidad media $+4/6=0{,}67$ m/s; rapidez media $12/6=2$ m/s.

## 6. Otros ejemplos
- $|3-8|-|{-2}|\cdot|4| = 5-8=-3$.
- Resolver $|2x+1|\le 5$: $-5\le2x+1\le5\Rightarrow-3\le x\le2$.
- Resolver $|x|>|x-4|$: elevar al cuadrado: $x^2>x^2-8x+16\Rightarrow x>2$.

## Errores comunes
- Pensar que $|a+b|=|a|+|b|$ (solo si tienen igual signo).
- Escribir $|x|=x$ sin condición.
- Resolver $|x|=-3$ (no tiene solución).
- Olvidar el segundo caso en ecuaciones con valor absoluto.
- Confundir rapidez con velocidad.

## Ejercicios propuestos
1. Resuelve $|x+3|=7$. ($x=4$, $x=-10$)
2. Resuelve $|3x-1|<8$. ($-7/3<x<3$)
3. Distancia entre -8 y -2,5. (5,5)
4. Un cuerpo va de 5 m a -3 m y luego a 1 m: desplazamiento y distancia. (-4 m; 12 m)
5. Demuestra $|xy|=|x||y|$ usando $|x|=\sqrt{x^2}$. ($\sqrt{x^2y^2}=\sqrt{x^2}\sqrt{y^2}$)

## Conexiones
Ver vectores en [[Física I]] y el cálculo en [[Matemática I]]. Continúa con [[Física II - Carga eléctrica y ley de Coulomb]].

## Fuente
`Material/Tarea 1.docx`. Texto leído por LibreOffice; las expresiones matemáticas no se extrajeron y se reconstruyeron con las definiciones estándar. La tarea es una investigación teórica, no tiene problemas numéricos propios; los ejemplos de las secciones 5 y 6 son adicionales.
