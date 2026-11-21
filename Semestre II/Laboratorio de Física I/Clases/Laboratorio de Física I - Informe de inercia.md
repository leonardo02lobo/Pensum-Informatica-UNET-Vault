---
tags: [clase, semestre-II]
materia: Laboratorio de Física I
fuente: Material/informe de inercia.docx
---
# Laboratorio de Física I - Informe de inercia

Materia: [[Laboratorio de Física I]]
Anterior: [[Laboratorio de Física I - Teoría de errores y mediciones]]
Siguiente: [[Laboratorio de Física I - Informe de choques]]

## Contexto y objetivo
Informe del Laboratorio de Física I (código 0842204L, Departamento de Matemática y Física, UNET), fechado el 24 de mayo de 2024. El objetivo declarado es "determinar cómo se comporta la inercia respecto al peso": se cuelga una masa $m$ de una cuerda enrollada en un disco (polea) de radio $R = 0{,}10$ m, se deja caer una altura $H = 0{,}95$ m y se cronometra el tiempo $t$. A partir de $t$ se obtienen aceleración lineal, tensión, aceleración angular y torque, y con la gráfica torque-aceleración angular se estima el momento de inercia del disco. (Los valores $H$ y $R$ se deducen de las fórmulas del informe, que usan 0,95 y 0,10.)

## Teoría de fondo
### Dinámica del sistema disco + masa colgante
Masa colgante (traslación): $mg - T = ma$, de donde $T = m(g-a)$.
Disco (rotación): $\tau = TR = I\alpha$.
Cuerda sin deslizar: $a = \alpha R$.

Combinando: $m(g-a)R = I\,\frac{a}{R}$, y despejando la aceleración:
$$a = \frac{mg}{m + I/R^2}$$
Si $I/R^2 \gg m$ la aceleración es casi proporcional a $m$ ($a \approx mgR^2/I$); a medida que crece $m$ el denominador cambia y la relación se curva. Como la masa parte del reposo y cae con aceleración constante: $H = \tfrac12 a t^2 \Rightarrow a = 2H/t^2$.

Momento de inercia experimental:
$$I = \frac{\tau}{\alpha} = \frac{T R}{a/R} = mR^2\frac{g-a}{a}$$
La pendiente de la gráfica $\tau$ vs $\alpha$ es $I$ (modelo lineal $\tau = I\alpha + \tau_0$) y el corte con $y$, $\tau_0$, es el torque de fricción en el eje cuando $\alpha \to 0$.

## Datos y cálculos del informe
Tabla (tiempo medido para caer $H = 0{,}95$ m). Los resultados que figuran en el informe se comparan con una recalculación hecha aquí con las fórmulas del informe:

| m (kg) | t (s) | a (m/s²) | T (N) | α (rad/s²) | τ (N·m) |
|---|---|---|---|---|---|
| 0,10 | 7,20 | 0,037 | 0,977 | 0,37 | 0,0977 |
| 0,20 | 4,20 | 0,108 | 1,94 | 1,08 | 0,194 |
| 0,30 | 3,31 | 0,173 | 2,94 | 1,73 | 0,289 |
| 0,40 | 3,30 | 0,174 | 3,85 | 1,74 | 0,385 |
| 0,50 | 2,39 | 0,333 | 4,73 | 3,33 | 0,473 |
| 0,60 | 2,33 | 0,350 | 5,67 | 3,50 | 0,567 |
| 0,70 | 1,99 | 0,480 | 6,52 | 4,80 | 0,652 |
| 0,80 | 1,92 | 0,515 | 7,43 | 5,15 | 0,743 |
| 0,90 | 1,88 | 0,537 | 8,33 | 5,37 | 0,834 |

Ejemplo paso a paso (m = 0,50 kg, t = 2,39 s):
1. $a = 2(0{,}95)/2{,}39^2 = 1{,}90/5{,}712 = 0{,}333$ m/s².
2. $T = 0{,}50(9{,}8-0{,}333) = 4{,}73$ N.
3. $\alpha = 0{,}333/0{,}10 = 3{,}33$ rad/s².
4. $\tau = 0{,}10\cdot 4{,}73 = 0{,}473$ N·m.
5. $I = \tau/\alpha = 0{,}473/3{,}33 = 0{,}142$ kg·m².

### Observaciones sobre la tabla del informe
- El informe del documento tiene inconsistencias de transcripción: en la fila de 10 g escribe $a = 0{,}997$ m/s² en la fórmula pero usa 0,03 después; el valor correcto de $2H/t^2$ es 0,037. Además da $T=0{,}997$ N con $m=0{,}10$ (el 0,997 es $0{,}10\cdot 9{,}77 = 0{,}977$, con dígitos intercambiados) y $\alpha = 0{,}5$ en vez de 0,37. En las filas de 20, 40 y 50 g las tensiones del informe (1,98; 3,93; 4,83 N) difieren ligeramente de las recalculadas por redondeo de $a$. Se recomienda corregir esas celdas.
- Los tiempos de 30 g (3,31 s) y 40 g (3,3 s) casi coinciden: eso indica error aleatorio en el cronometraje; debería repetirse la medición.

### Momento de inercia estimado por fila
Con $I = mR^2(g-a)/a$ se obtienen valores entre 0,14 y 0,27 kg·m²; para $m \ge 0{,}2$ kg el promedio es aproximadamente 0,16 kg·m² (recalculación de esta nota). Si todos los ensayos corresponden al mismo disco, $I$ debería ser constante; la dispersión revela errores de tiempo, fricción en el eje y que $R$ efectivo (radio del carrete donde se enrolla la cuerda) puede diferir de 0,10 m. Verificar con el docente el radio real.

## Gráficas y modelos
El cuestionario pide elegir entre tres modelos:
- Lineal $y=mx+b$, $m=\frac{y_2-y_1}{x_2-x_1}$.
- Semilogarítmico $y=b\,e^{2{,}3mx}$.
- Bilogarítmico $y=bx^m$.

Para $\tau$ vs $\alpha$ se espera el modelo lineal: $\tau = I\alpha + \tau_0$. Con los puntos extremos de la recta (0,37; 0,098) y (5,37; 0,834): pendiente $=(0{,}834-0{,}098)/(5{,}37-0{,}37) = 0{,}147$ kg·m². Es del orden del $I$ promedio obtenido y coherente con un disco macizo de ~3 kg y $R\approx 0{,}3$ m, aunque estos datos geométricos no están en el informe. Para $t$ vs $m$ el modelo adecuado es bilogarítmico: $t \propto m^{-1/2}$ aproximadamente cuando $I/R^2 \ll m$.

## Respuestas al cuestionario (explicadas)
1. **DCL**: sobre la masa, peso $mg$ hacia abajo y tensión $T$ hacia arriba; sobre el disco, la tensión tangencial $T$ en el borde (brazo $R$), peso del disco y reacción del eje (no producen torque respecto al eje).
2. **Ecuaciones**: las cuatro de la tabla, $a=2H/t^2$, $T=m(g-a)$, $\alpha=a/R$, $\tau=R\,m(g-a)$, más $\tau=I\alpha$.
3. **Corte con el eje $Y$**: el informe lo describe de forma vaga ("el corte del cálculo"). Físicamente es el torque que existe aun con $\alpha=0$: el torque necesario para vencer la fricción estática/cinética del eje.
4. **Pendiente**: el momento de inercia $I$ del sistema rotante, con unidades kg·m²; mide la resistencia a cambiar el estado de rotación y depende de la masa y de su distribución respecto al eje.

La conclusión del informe es genérica; una conclusión más sólida: "$\tau$ crece linealmente con $\alpha$; la pendiente da $I$; la dispersión se atribuye al cronometraje manual y a la fricción".

## Errores comunes
- Usar $T = mg$ (ignorar que la masa acelera): sobreestima $T$ y $\tau$ hasta 5 % en las masas grandes.
- Mezclar masa en gramos con g en m/s².
- Tomar la masa del disco como la masa colgante.
- Cronometrar con el instrumento mal sincronizado: para $t\approx2$ s, un error de 0,2 s es 10 % de $t$ y 20 % en $a$.
- Confundir $\alpha$ con $a$: $\alpha=a/R$.

## Ejercicios propuestos
1. Disco de $I = 0{,}15$ kg·m², $R=0{,}10$ m, $m=0{,}50$ kg. Calcula $a$. (Resp. $a = 0{,}5\cdot9{,}8/(0{,}5+15)=0{,}316$ m/s².)
2. Con $a$ anterior, tiempo en caer 0,95 m. (Resp. $t=\sqrt{1{,}9/0{,}316}=2{,}45$ s.)
3. Tensión del caso 1. (Resp. $4{,}74$ N.)
4. Dado $I=\tau/\alpha$, si $\tau=0{,}56$ N·m y $\alpha=3{,}5$ rad/s², halla $I$. (Resp. $0{,}16$ kg·m².)
5. Si se duplica el radio $R$ manteniendo $m$ e $I$, ¿cómo cambia $a$? (Resp. aumenta, porque $I/R^2$ disminuye.)

## Conexiones
Aplica la dinámica rotacional de [[Física I]] (torque, momento de inercia, segunda ley para rotación) y el análisis de gráficas de [[Laboratorio de Física I - Teoría de errores y mediciones]].

## Fuente
`Material/informe de inercia.docx` (informe del 24 de mayo de 2024; las fórmulas estaban en objetos incrustados y se reconstruyeron del texto del documento).
