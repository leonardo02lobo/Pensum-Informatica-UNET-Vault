---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/CT14-1_imprimir.pdf (y CT14-1.pps)
---
# Física I - Tema 4 Leyes de Newton

Materia: [[Física I]]
Anterior: [[Física I - Tema 3 Problemas de movimiento circular]]
Siguiente: [[Física I - Tema 4 Problemas de Leyes de Newton]]

## Contexto y objetivo
Hasta aquí se describió el movimiento; el Tema 4 (noviembre 2009) estudia **las causas que originan los cambios en el movimiento**. Objetivo: aplicar las tres leyes de Newton con diagramas de cuerpo libre (DCL) a cuerpos sobre superficies, planos inclinados, poleas, y con fuerzas de roce.

## 1. Concepto de fuerza
Una fuerza es la interacción entre cuerpos que puede cambiar su estado de movimiento o deformarlos. Es un vector (N = kg·m/s²). Dos tipos:
- **Fuerzas de contacto**: se generan por contacto directo (el bate sobre la pelota, la normal, la tensión, el roce).
- **Fuerzas de campo (acción a distancia)**: no requieren contacto (gravitatoria: la Tierra atrae al cuerpo con el **peso** $\vec P=m\vec g$; fuerza de la Tierra sobre la Luna).

## 2. Las tres leyes
**Primera ley (inercia)**: si $\sum\vec F=0$ la partícula permanece en reposo o con velocidad constante ($\vec v=\text{cte}$). La inercia es la tendencia a conservar el estado de movimiento y depende de la **masa**, no de las fuerzas aplicadas. Es válida en sistemas inerciales.

**Segunda ley**: $\sum\vec F=\dfrac{d\vec p}{dt}$ con $\vec p=m\vec v$; si la masa es constante, $\sum\vec F=m\vec a$. Se aplica por componentes: $\sum F_x=ma_x$, $\sum F_y=ma_y$. La aceleración tiene la dirección de la fuerza neta.

**Tercera ley (acción-reacción)**: $\vec F_{A,B}=-\vec F_{B,A}$: igual módulo, misma dirección, sentidos opuestos, **actúan sobre cuerpos distintos** (por eso no se cancelan en un DCL). Ejemplo: el peso de un libro sobre una mesa y la normal **no** son par acción-reacción (actúan sobre el mismo cuerpo); la reacción del peso es la atracción del libro sobre la Tierra.

Masa inercial (resistencia a acelerar) y masa gravitacional (interacción con la gravedad) tienen el mismo valor numérico.

## 3. Fuerzas habituales
- **Peso**: $P=mg$, vertical hacia abajo.
- **Normal** $N$: perpendicular a la superficie de contacto; su valor lo determina el equilibrio (no es siempre $mg$).
- **Tensión** $T$: fuerza de una cuerda ideal (masa despreciable, inextensible): igual en todos sus puntos si la polea no tiene masa ni roce.
- **Roce (fricción)**: paralela a la superficie de contacto, opuesta al movimiento o a su tendencia.
 - **Estático** $f_e\le\mu_eN$; vale $\mu_eN$ en el instante de **movimiento inminente** ($f_{e,max}$).
 - **Cinético** $f_c=\mu_cN$, con $\mu_c<\mu_e$ típicamente.

## 4. Diagrama de cuerpo libre y método
1. Aislar cada cuerpo y representarlo como un punto.
2. Dibujar **solo fuerzas externas** actuando sobre ese cuerpo (peso, normal, tensión, roce, aplicadas).
3. Elegir ejes (en planos inclinados: $x$ a lo largo del plano, $y$ perpendicular).
4. Aplicar $\sum\vec F=m\vec a$ a cada cuerpo y escribir las ecuaciones de ligadura (misma aceleración si hay cuerda tensa).
5. Resolver el sistema de ecuaciones y verificar unidades y signos.

**Plano inclinado de ángulo $\varphi$**: $P_x=mg\sin\varphi$ (a lo largo), $P_y=mg\cos\varphi$ (perpendicular); $N=mg\cos\varphi$ si no hay otras fuerzas; $a=g\sin\varphi$ sin roce; con roce $a=g(\sin\varphi-\mu_c\cos\varphi)$.

## 5. Ejemplos de la clase y resueltos
**A. Coeficiente de roce estático (plano inclinado).** Bloque de 3 kg en reposo sobre un plano a 30° a punto de deslizar. $\sum F_x=0$: $mg\sin30°-f_{e,max}=0$; $N=mg\cos30°$; $\mu_e=\dfrac{mg\sin30°}{mg\cos30°}=\tan30°=0{,}577$. (Independiente de la masa.)

**B. Coeficiente de roce cinético (de la clase).** Bloque de 2 kg lanzado sobre superficie horizontal rugosa que recorre $\Delta x$ hasta detenerse. $-\mu_cmg=ma\Rightarrow a=-\mu_cg$; con $v^2=v_0^2+2a\Delta x$: $\mu_c=\dfrac{v_0^2}{2g\Delta x}$. Por ejemplo $v_0=6$ m/s, $\Delta x=9$ m: $\mu_c=36/(176{,}4)=0{,}204$.

**C. Dos bloques unidos (máquina de Atwood sobre mesa).** $m_1=4$ kg sobre mesa sin roce unido por cuerda y polea ideal a $m_2=2$ kg colgante. Para $m_2$: $m_2g-T=m_2a$; para $m_1$: $T=m_1a$. Sumando: $a=\dfrac{m_2g}{m_1+m_2}=3{,}27$ m/s²; $T=13{,}1$ N.

**D. Ascensor.** Persona de 70 kg en ascensor que sube con $a=2$ m/s²: $N-mg=ma\Rightarrow N=70(9{,}8+2)=826$ N (peso aparente mayor).

## 6. Dinámica del movimiento circular
La fuerza neta hacia el centro es la **fuerza centrípeta**: $\sum F_c=ma_c=\dfrac{mv^2}{r}$. No es una fuerza nueva: es la resultante de tensión, normal, roce, etc. Ejemplo: piedra de 0,5 kg en cuerda de 1 m a 4 m/s en un plano horizontal: $T=0{,}5\cdot16/1=8$ N.

## Errores comunes
1. Dibujar la fuerza centrípeta o la "fuerza de la aceleración" como fuerza adicional en el DCL.
2. Suponer $N=mg$ siempre (falla en inclinados, con fuerzas oblicuas y en ascensores).
3. Incluir en el DCL de un cuerpo fuerzas que éste ejerce sobre otros.
4. Usar $\mu N$ para el roce estático cuando el cuerpo no está en movimiento inminente.
5. Aplicar la 3.ª ley como si el par se cancelara.
6. Olvidar que cuerdas y poleas ideales transmiten la tensión sin cambio.

## Ejercicios propuestos
1. Bloque de 5 kg, $F=20$ N horizontal, $\mu_c=0{,}2$. $a$. *Resp.: 2,04 m/s².*
2. Plano a 37° sin roce: $a$. *Resp.: 5,9 m/s².*
3. $m_1=3$ kg y $m_2=5$ kg colgados de una polea ideal: $a$ y $T$. *Resp.: 2,45 m/s²; 36,8 N.*
4. Un cuerpo de 2 kg sobre un plano con $\mu_e=0{,}5$: ángulo crítico. *Resp.: 26,6°.*

## Conexiones
Fundamento de la dinámica rotacional ([[Física I - Tema 10 Dinámica rotacional]]) y de energía y momento lineal. Conecta con [[Física I - Tema 3 Movimiento circular]] por la fuerza centrípeta.

## Fuente
Material/Parcial 1/CT14-1_imprimir.pdf y CT14-1.pps; ecuaciones según el [[Física I - Formulario I parcial]].
