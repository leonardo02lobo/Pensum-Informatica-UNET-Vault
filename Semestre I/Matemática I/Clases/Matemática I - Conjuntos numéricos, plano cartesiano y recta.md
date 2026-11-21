---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/_Material I parcial - Línea recta- Semana 1.pdf_
---
# Matemática I - Conjuntos numéricos, plano cartesiano y recta

Materia: [[Matemática I]]
Anterior: [[Matemática I - Cronograma y temario 2023-1]]
Siguiente: [[Matemática I - Funciones y sus gráficas]]

## Contexto y objetivo
El archivo es un PDF escaneado de 11 páginas, tomado del libro **Sullivan, Álgebra y Trigonometría (9.ª ed.)**, titulado "I Parcial - Introducción al conjunto de los números reales - Línea recta - Semana 1". Lo leí como imágenes (el texto no es extraíble). Contiene: clasificación de los números (naturales, enteros, racionales, irracionales, reales), coordenadas rectangulares, fórmulas de distancia y punto medio (teoremas con ejercicios 13-42) y la definición de pendiente con una "visualización del concepto" (rectas con pendientes 0, ±1/4, ±1/2, ±1, ±2, ±6). Estas notas amplían esos temas y completan lo que sigue (ecuaciones de la recta, paralelismo, ángulo y distancia punto-recta) del cronograma.

## 1. Los números reales
- **Naturales** $\mathbb N=\{1,2,3,\dots\}$; **enteros** $\mathbb Z=\{\dots,-2,-1,0,1,2,\dots\}$.
- **Racionales** $\mathbb Q=\{a/b : a,b\in\mathbb Z,\ b\neq0\}$. Su expansión decimal termina o es periódica ($3/4=0{,}75$; $-2/3=-0{,}\overline6$).
- **Irracionales:** decimales que no terminan ni se repiten ($\pi,\sqrt2$); no se escriben como $a/b$.
- **Reales** $\mathbb R=\mathbb Q\cup$ irracionales. Cadena: $\mathbb N\subset\mathbb Z\subset\mathbb Q\subset\mathbb R$.
- Un número no puede ser racional e irracional a la vez.

**Orden de operaciones:** paréntesis, potencias/raíces, multiplicación y división de izquierda a derecha, suma y resta. Ejemplo: $6-[3\cdot5+2\cdot(3-2)]=6-[15+2]=-11$.

## 2. Plano cartesiano
Dos rectas numéricas perpendiculares (eje $x$ horizontal, eje $y$ vertical) con origen $O=(0,0)$. Cada punto es un par ordenado $(x,y)$: abscisa y ordenada. Cuadrantes: I ($x>0,y>0$), II ($x<0,y>0$), III ($x<0,y<0$), IV ($x>0,y<0$). Los puntos sobre los ejes no pertenecen a ningún cuadrante.

## 3. Distancia y punto medio
$$d(P_1,P_2)=\sqrt{(x_2-x_1)^2+(y_2-y_1)^2},\qquad M=\left(\frac{x_1+x_2}{2},\frac{y_1+y_2}{2}\right)$$
La distancia es el teorema de Pitágoras sobre el triángulo rectángulo con catetos $|x_2-x_1|$ y $|y_2-y_1|$.

**Ejemplo 1.** $P_1=(3,-4)$, $P_2=(5,4)$: $d=\sqrt{2^2+8^2}=\sqrt{68}=2\sqrt{17}\approx8{,}25$; $M=(4,0)$.

**Ejemplo 2 (triángulo rectángulo).** $A=(-2,5),B=(1,3),C=(-1,0)$: $d(AB)^2=9+4=13$, $d(BC)^2=4+9=13$, $d(AC)^2=1+25=26=13+13$. Es rectángulo e isósceles (Pitágoras inverso).

## 4. Pendiente
$$m=\frac{y_2-y_1}{x_2-x_1},\quad x_1\ne x_2$$
Si $x_1=x_2$ la recta es vertical y la pendiente no está definida. Interpretación: $m=\tan\theta$ con $\theta$ el ángulo de inclinación ($0\le\theta<180^\circ$). $m>0$ sube, $m<0$ baja, $m=0$ horizontal. Mientras mayor $|m|$, más empinada.

## 5. Ecuaciones de la recta
- **Punto-pendiente:** $y-y_1=m(x-x_1)$.
- **Pendiente-ordenada:** $y=mx+b$.
- **General:** $Ax+By+C=0$ (con $A,B$ no ambos nulos); $m=-A/B$.
- **Horizontal** $y=b$; **vertical** $x=a$.

**Ejemplo 3.** Recta por $(1,2)$ y $(4,-1)$: $m=\frac{-1-2}{4-1}=-1$; $y-2=-(x-1)\Rightarrow y=-x+3$, es decir $x+y-3=0$.

## 6. Paralelismo, perpendicularidad, ángulo y distancia punto-recta
- Paralelas: $m_1=m_2$. Perpendiculares: $m_1m_2=-1$ (si una es vertical, la otra es horizontal).
- Ángulo entre rectas: $\tan\varphi=\left|\dfrac{m_2-m_1}{1+m_1m_2}\right|$.
- Distancia de $P_0=(x_0,y_0)$ a $Ax+By+C=0$: $d=\dfrac{|Ax_0+By_0+C|}{\sqrt{A^2+B^2}}$.

**Ejemplo 4.** Recta perpendicular a $2x-y+5=0$ por $(0,1)$: $m_1=2\Rightarrow m_2=-\tfrac12$; $y=-\tfrac12x+1$.

**Ejemplo 5.** Distancia de $(1,2)$ a $3x+4y-10=0$: $d=\frac{|3+8-10|}{5}=\frac15=0{,}2$.

**Ejemplo 6 (ángulo).** $m_1=1$, $m_2=3$: $\tan\varphi=\frac{2}{4}=0{,}5\Rightarrow\varphi\approx26{,}57^\circ$.

## Errores comunes
- Restar coordenadas en distinto orden en numerador y denominador de $m$.
- Olvidar el valor absoluto o la raíz en la distancia.
- Afirmar que dos rectas con pendiente $2$ y $-2$ son perpendiculares (producto $-4\neq-1$).
- Confundir recta vertical (pendiente indefinida) con pendiente cero.

## Ejercicios propuestos
1. Distancia entre $(-3,2)$ y $(6,-1)$. (R: $\sqrt{90}=3\sqrt{10}$.)
2. Punto medio entre $(a,b)$ y $(0,0)$. (R: $(a/2,b/2)$.)
3. Ecuación de la recta de pendiente $-2$ por $(3,1)$. (R: $y=-2x+7$.)
4. ¿Son paralelas $2x-3y=5$ y $4x-6y=1$? (R: sí, ambas $m=2/3$.)
5. Distancia de $(0,0)$ a $5x+12y-26=0$. (R: $2$.)

## Conexiones
La recta es la base de la **recta tangente** ([[Matemática I - Derivación: reglas, Rolle, Lagrange y tangentes]]) y de las asíntotas. En [[Física I]] aparece como gráficas posición-tiempo; la pendiente es la velocidad.

## Fuente
`Material/GUIAS/_Material I parcial - Línea recta- Semana 1.pdf_` (PDF escaneado de Sullivan, leído como imágenes de las 11 páginas; solo se alcanzaron a leer con claridad las primeras 6-7). El resto del desarrollo (ángulo, distancia punto-recta) es conocimiento general.
