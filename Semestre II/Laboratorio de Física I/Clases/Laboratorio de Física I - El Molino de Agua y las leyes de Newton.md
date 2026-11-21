---
tags: [clase, semestre-II]
materia: Laboratorio de Física I
fuente: Material/El Molino de Agua y las Leyes de Newton.docx
---
# Laboratorio de Física I - El Molino de Agua y las leyes de Newton

Materia: [[Laboratorio de Física I]]
Anterior: [[Laboratorio de Física I - Informe de choques]]
Siguiente: [[Laboratorio de Física I - Presentación del Molino de Agua]]

## Contexto y objetivo
Trabajo escrito del proyecto del curso (Departamento de Ingeniería Informática, UNET; integrantes Leonardo Lobo y Moisés Zambrano). Propone construir con materiales reciclados un molino de agua a escala y explicar su funcionamiento con las tres leyes de Newton. Esta nota reconstruye y amplía el contenido: describe el aparato, desarrolla la teoría de cada ley con el molino, y añade el análisis cuantitativo (fuerza del chorro, torque y energía) que el documento solo enuncia cualitativamente.

## Descripción del molino
Un molino de agua es una máquina que convierte la energía del agua en movimiento (y de la caída desde una altura) en energía mecánica de rotación. La pieza central es la rueda hidráulica, que gira cuando el agua incide sobre sus paletas o aspas; el movimiento se transmite por un eje a engranajes o piedras de molienda (harina, papel, aserrío) o a un generador. Tipos: de rueda por debajo (corriente de río, usa la energía cinética), por encima (el agua cae sobre la parte superior, usa la energía potencial) y de pecho. En el proyecto una botella situada por encima de la rueda suministra un flujo de agua constante que cae sobre las aspas hechas de palos de helado.

## Las tres leyes de Newton y su aplicación
### Primera ley (inercia)
Un cuerpo en reposo o en movimiento rectilíneo uniforme mantiene su estado salvo que una fuerza neta externa lo modifique. El documento afirma que el molino permanece en reposo hasta que el agua actúa sobre él. Para la rotación la versión es: un cuerpo rígido mantiene su velocidad angular salvo que actúe un torque neto externo. Matiz: el molino en reposo no solo está sin fuerza neta; las fuerzas de fricción estática del eje deben ser superadas, lo que da un torque mínimo para arrancar.

### Segunda ley
$\sum\vec F = m\vec a$. Para la rueda, $\sum\tau = I\alpha$. Si el chorro aumenta su caudal o velocidad, aumenta la fuerza sobre las aspas, el torque y la aceleración angular. El documento lo expresa así: si se reduce la aceleración del agua, disminuye la fuerza sobre el molino. La segunda ley en forma de momento lineal es la más útil para el chorro: $F=\frac{dp}{dt}=\dot m\,\Delta v$, donde $\dot m=\rho Q$ es el flujo másico.

### Tercera ley (acción y reacción)
El agua empuja la aspa con $\vec F$ y la aspa empuja el agua con $-\vec F$ (aplicadas en cuerpos distintos). El documento señala que la acción del agua al caer produce la reacción de rotación; precisión: la rotación es el efecto de la fuerza sobre la rueda, la reacción es la fuerza que la rueda ejerce sobre el agua, que la frena y la desvía.

## Análisis cuantitativo (ejemplos resueltos)
**Ejemplo 1: fuerza del chorro.** Una botella suministra $Q=2\times10^{-5}$ m³/s ($20$ mL/s) que cae $h=0{,}30$ m sobre las aspas.
1. Velocidad de impacto: $v=\sqrt{2gh}=\sqrt{2(9{,}8)(0{,}30)}=2{,}42$ m/s.
2. Flujo másico: $\dot m=\rho Q=1000\times2\times10^{-5}=0{,}02$ kg/s.
3. Si el agua se detiene al golpear la aspa: $F=\dot m v=0{,}02\times2{,}42=0{,}048$ N.
4. Con radio efectivo $R=0{,}05$ m: $\tau=FR=2{,}4\times10^{-3}$ N·m.

**Ejemplo 2: potencia disponible.** $P=\rho Q g h=1000(2\times10^{-5})(9{,}8)(0{,}30)=0{,}059$ W. Con eficiencia de 20 % la potencia mecánica es $\approx0{,}012$ W. Por eso un molino de juguete no mueve una piedra de molienda, pero sí gira lentamente.

**Ejemplo 3: aceleración angular.** Rueda de $I=1{,}0\times10^{-4}$ kg·m² con el torque anterior (menos fricción de $1{,}0\times10^{-3}$ N·m): $\alpha=(2{,}4-1{,}0)\times10^{-3}/1{,}0\times10^{-4}=14$ rad/s². La velocidad angular se estabiliza cuando el torque del chorro iguala al de fricción y de arrastre del agua (equilibrio, primera ley rotacional).

## Conversión de energía
Energía potencial del agua en la botella $\rightarrow$ energía cinética del chorro $\rightarrow$ energía cinética de rotación de la rueda $\rightarrow$ trabajo útil. Una parte se disipa en salpicadura, turbulencia y fricción del eje. Se cumple $\Delta E_{mec}=-W_{disipado}$.

## Materiales reciclables
El documento resalta el uso de materiales reciclados (botella de plástico, tubos, palitos), lo que demuestra conciencia ambiental y creatividad; la botella sobre la rueda garantiza un flujo constante. El criterio de ingeniería es que el flujo sea estable y el eje tenga baja fricción.

## Errores comunes
- Decir que "la acción y la reacción se anulan": actúan sobre cuerpos distintos.
- Pensar que la rueda necesita una fuerza para seguir girando a velocidad constante: solo la necesita para compensar la fricción.
- Llamar "fuerza cinética" a la energía (ver la presentación); la energía cinética es $\tfrac12mv^2$, no una fuerza.
- Confundir fuerza con torque: lo que acelera la rotación es $\tau=Fr\sin\theta$.

## Ejercicios propuestos
1. Calcula la velocidad del chorro al caer 0,45 m. (Resp. 2,97 m/s.)
2. Si la fuerza sobre una aspa de 4 cm de radio es 0,05 N, ¿cuánto torque? (Resp. $2\times10^{-3}$ N·m.)
3. Una rueda de $I=2\times10^{-4}$ kg·m² recibe un torque neto de $4\times10^{-3}$ N·m; halla $\alpha$ y $\omega$ a los 3 s. (Resp. 20 rad/s²; 60 rad/s.)
4. Explica con la tercera ley por qué una manguera con mucha presión "retrocede". (Resp. el agua expulsada recibe fuerza de la manguera; la manguera recibe la reacción.)

## Conexiones
Aplicación de leyes de Newton y dinámica rotacional de [[Física I]]; véase la numérica del molino en [[Laboratorio de Física I - Presentación del Molino de Agua]] y el [[Laboratorio de Física I - Proyecto Molino de Agua]].

## Fuente
`Material/El Molino de Agua y las Leyes de Newton.docx`. Los ejemplos numéricos de las secciones "Análisis cuantitativo" son de esta nota (no figuran en el documento) y usan valores supuestos.
