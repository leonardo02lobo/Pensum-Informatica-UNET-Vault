---
tags: [clase, semestre-II]
materia: Laboratorio de Física I
fuente: Material/Presentacion Molino de Agua.pptx
---
# Laboratorio de Física I - Presentación del Molino de Agua

Materia: [[Laboratorio de Física I]]
Anterior: [[Laboratorio de Física I - El Molino de Agua y las leyes de Newton]]
Siguiente: [[Laboratorio de Física I - Proyecto Molino de Agua]]

## Contexto y objetivo
Presentación de 14 diapositivas (Leonardo Lobo y Moisés Zambrano) del proyecto del molino de agua. Contiene introducción histórica, materiales, las leyes de Newton, y cálculos de momento de inercia, torque, aceleración angular, velocidad angular y número de vueltas con datos de un molino "a escala real" hipotético. Esta nota documenta cada cálculo, comprueba las cuentas y señala interpretaciones dudosas. Las ecuaciones estaban en imágenes del pptx; se leyeron las diapositivas de torque, aceleración, velocidad y vueltas, y las del momento de inercia se reconstruyen a partir de los datos (verificar).

## Contenido de las diapositivas
1. Introducción: un molino aprovecha la energía cinética del viento, el agua o la tracción animal para moler o generar electricidad. Surgió en la antigüedad, durante la Revolución Neolítica, para moler cereales y harinas.
2. Materiales: recipiente para recoger agua, botella, tubos de plástico, palos de helado; extra: pega blanca.
3. Leyes de Newton y su aplicación: el molino permanece igual mientras no haya fuerza externa; más fuerza, más aceleración; la acción del agua al caer provoca la reacción de movimiento en el molino.
4. Magnitudes a calcular: momento de inercia, torque, aceleración angular, velocidad angular y número de vueltas.
5. Datos: número de aspas $N=6$, masa $m=5$ kg, longitud (radio) $R=1{,}5$ m, fuerza $F=200$ N.

## Teoría de fondo
- **Momento de inercia** de un sistema de cuerpos rígidos sobre un mismo eje: se suman. Una barra uniforme de masa $m$ y longitud $L$ girando por un extremo: $I=\tfrac13mL^2$. Un disco macizo por su centro: $I=\tfrac12mR^2$. Un aro: $mR^2$.
- **Torque**: $\vec\tau=\vec r\times\vec F$, $\tau=rF\sin\theta$ (N·m).
- **Segunda ley rotacional**: $\tau=I\alpha$.
- **Cinemática angular** con $\alpha$ constante: $\omega=\omega_0+\alpha t$, $\theta=\theta_0+\omega_0t+\tfrac12\alpha t^2$.
- **Frecuencia**: $f=\omega/2\pi$ (vueltas por segundo, Hz); vueltas en un tiempo $t$: $\theta/2\pi$.

## Cálculos de la presentación, paso a paso
**Momento de inercia.** Con los datos, el valor $I=22{,}5$ kg·m² (usado en la diapositiva de aceleración) se obtiene tratando cada aspa como barra de 5 kg pivotada en un extremo y sumando las seis:
$$I=N\cdot\tfrac13mR^2=6\cdot\tfrac13\cdot5\cdot(1{,}5)^2=6\cdot3{,}75=22{,}5\ \text{kg·m}^2.$$
Esto es una interpretación coherente con los números; confirmar contra la diapositiva 8.

**Torque.** $\tau=F\cdot R=200\ \text{N}\times1{,}5\ \text{m}=300$ N·m (la diapositiva lo calcula con la fuerza aplicada en el extremo de una aspa, perpendicular a ella).

**Aceleración angular.** $\alpha=\tau/I=300/22{,}5=13{,}33$ rad/s².

**Velocidad angular.** Desde el reposo, tras $t=1$ s: $\omega=\alpha t=13{,}33$ rad/s.

**Vueltas por segundo.** $N=\omega/2\pi=13{,}33/6{,}283=2{,}12$ vueltas por segundo (equivale a unas 127 rpm). La diapositiva escribe $N\approx2{,}12$ sin unidad; son revoluciones por segundo, no el número de vueltas totales.

### Comentarios de rigor
- Aplicar 200 N de forma constante solo a una aspa mientras las seis aspas aportan inercia; en un molino real la fuerza actúa sobre la aspa sumergida o bajo el chorro, y cambia de aspa y de brazo conforme gira, por lo que $\tau$ no es constante.
- Con $\alpha$ constante, $\omega$ crece sin límite; en la realidad el torque de arrastre y fricción crece con $\omega$ hasta la velocidad terminal.
- El número de vueltas en el primer segundo es $\theta/2\pi=\tfrac12\alpha t^2/2\pi=1{,}06$ vueltas, la mitad de $f$ final.
- La conclusión de la diapositiva dice que se aplican "conceptos de fuerza cinética": debe decir energía cinética.

## Ejemplo propio ampliado
Con los mismos datos, calcula la velocidad angular tras 3 s y las vueltas dadas:
1. $\omega=13{,}33\cdot3=40{,}0$ rad/s (6,37 vueltas/s).
2. $\theta=\tfrac12(13{,}33)(3)^2=60{,}0$ rad $=9{,}55$ vueltas.
3. Energía cinética: $\tfrac12I\omega^2=\tfrac12(22{,}5)(40^2)=18\,000$ J. Trabajo del torque: $\tau\theta=300\cdot60=18\,000$ J. Coinciden (teorema trabajo-energía rotacional).

## Errores comunes
- Usar $I=mR^2$ para una barra por el extremo (daría 11,25 por aspa).
- No convertir rad/s a vueltas dividiendo entre $2\pi$.
- Escribir la fuerza como "200 N·m" o torque en N.
- Olvidar que $\omega=\alpha t$ solo vale con $\alpha$ constante y $\omega_0=0$.

## Ejercicios propuestos
1. Con $N=4$ aspas de 2 kg y $R=1$ m, halla $I$. (Resp. 2,67 kg·m².)
2. Si $F=50$ N a 1 m, ¿qué $\alpha$ da ese $I$? (Resp. 18,7 rad/s².)
3. Calcula las rpm a $\omega=13{,}33$ rad/s. (Resp. 127,3 rpm.)
4. ¿Qué torque hace falta para que el molino de 22,5 kg·m² alcance 2 rad/s en 4 s? (Resp. 11,25 N·m.)

## Conexiones
Utiliza torque, momento de inercia y dinámica de rotación de [[Física I]]; teoría en [[Laboratorio de Física I - El Molino de Agua y las leyes de Newton]].

## Fuente
`Material/Presentacion Molino de Agua.pptx` (14 diapositivas; ecuaciones leídas como imágenes en las diapositivas de torque, aceleración, velocidad y vueltas; el cálculo del momento de inercia se reconstruyó).
