---
tags: [clase, semestre-II]
materia: Laboratorio de Física I
fuente: Material/Informe Choques.docx
---
# Laboratorio de Física I - Informe de choques

Materia: [[Laboratorio de Física I]]
Anterior: [[Laboratorio de Física I - Informe de inercia]]
Siguiente: [[Laboratorio de Física I - El Molino de Agua y las leyes de Newton]]

## Contexto y objetivo
Práctica "Choques o Colisiones" (informe del 24 de mayo de 2024). Se estudia la colisión de dos carritos sobre un riel registrando su posición con un timbre de chispas sobre una tira de papel (30 chispas por segundo). A partir de las marcas se calculan velocidades antes y después del choque, el coeficiente de restitución, el momento lineal y la energía cinética, para decidir el tipo de choque.

## Teoría de fondo
### Momento lineal e impulso
$\vec p = m\vec v$ (kg·m/s). Si la fuerza externa neta sobre el sistema es nula (o despreciable durante el choque), el momento total se conserva: $m_1\vec v_1 + m_2\vec v_2 = m_1\vec v_1' + m_2\vec v_2'$. El impulso $\vec J=\int \vec F\,dt=\Delta\vec p$.

### Tipos de choque y coeficiente de restitución
$$\varepsilon = -\frac{v_2' - v_1'}{v_2 - v_1} = \frac{\text{velocidad relativa de separación}}{\text{velocidad relativa de aproximación}}$$
- Elástico: $\varepsilon = 1$; se conservan momento y energía cinética.
- Inelástico: $0<\varepsilon<1$; se conserva el momento, no la energía.
- Perfectamente inelástico: $\varepsilon=0$; los cuerpos quedan unidos con $v'=\frac{m_1v_1+m_2v_2}{m_1+m_2}$.

### Fórmulas del choque elástico unidimensional
Resolviendo conservación del momento y de energía:
$$v_1' = \frac{m_1-m_2}{m_1+m_2}v_1 + \frac{2m_2}{m_1+m_2}v_2,\qquad v_2' = \frac{2m_1}{m_1+m_2}v_1 + \frac{m_2-m_1}{m_1+m_2}v_2$$
Con masas iguales ($m_1=m_2$): $v_1'=v_2$ y $v_2'=v_1$; los cuerpos intercambian velocidades.

### Velocidad a partir de la tira
Si el timbre marca con frecuencia $f$, el intervalo entre marcas es $\Delta t=1/f$. La velocidad media entre dos marcas es $v=\Delta x/\Delta t = f\,\Delta x$.

## Datos y cálculos del informe
Masas: $m_1=m_2=271{,}5$ g $=0{,}2715$ kg.
Distancias entre marcas consecutivas (cm), tomando los 4 primeros puntos:
- Carro 1: 4; 1,5; 1,4; 1,5, total 8,4 cm = 0,084 m.
- Carro 2: 1; 1; 1,5; 1,1, total 4,6 cm = 0,046 m. (En el documento se escribe "1+11+1,5+1,1", error tipográfico; la suma 4,6 es correcta.)

El informe calcula $v = (\text{chispas/s})\times\text{distancia}$:
- $v_1 = 30\cdot0{,}084 = 2{,}52$ m/s, vector $\vec v_1=-2{,}52\,\hat i$ m/s.
- $v_2 = 30\cdot0{,}046 = 1{,}38$ m/s, vector $\vec v_2=+1{,}38\,\hat i$ m/s.

Velocidades finales (fórmula elástica con $m_1=m_2$, numerador $m_1-m_2=0$, denominador $0{,}543$):
- $v_1' = 0 + \frac{2(0{,}2715)}{0{,}543}(1{,}38)=+1{,}38$ m/s.
- $v_2' = \frac{2(0{,}2715)}{0{,}543}(-2{,}52) + 0 = -2{,}52$ m/s.

Coeficiente de restitución: $\varepsilon=-\frac{(-2{,}52)-(1{,}38)}{1{,}38-(-2{,}52)}=\frac{3{,}90}{3{,}90}=1$.

Momento: antes $0{,}2715(-2{,}52)+0{,}2715(1{,}38)=-0{,}3095$ kg·m/s; después $0{,}2715(1{,}38)+0{,}2715(-2{,}52)=-0{,}3095$ kg·m/s. Se conserva.

Energía cinética: antes $\tfrac12(0{,}2715)(2{,}52^2)+\tfrac12(0{,}2715)(1{,}38^2)=0{,}862+0{,}259=1{,}12$ J; después igual, 1,12 J. Conclusión del informe: choque elástico.

## Análisis crítico (a considerar al repetir la práctica)
1. **Cálculo de la velocidad.** Cuatro distancias consecutivas abarcan 4 intervalos de tiempo, así que $v=\frac{8{,}4\ \text{cm}}{4/30\ \text{s}}=63$ cm/s $=0{,}63$ m/s, no 2,52 m/s. La expresión $v=f\,\Delta x$ solo vale si $\Delta x$ es la distancia de un único intervalo. Con el criterio de promediar los cuatro intervalos: $v_1=0{,}63$ m/s y $v_2=0{,}345$ m/s (el procedimiento queda igual, solo cambian los números, y todos los resultados de conservación se mantienen). Verificar con el profesor la convención del timbre antes de entregar.
2. **Las velocidades finales no se midieron**: se calcularon con la fórmula del choque elástico, de modo que la conservación está garantizada por construcción. Un análisis experimental correcto mide las marcas después del choque y compara con la predicción; la diferencia es el error experimental.
3. Un coeficiente exactamente 1 no es realista; debería reportarse con incertidumbre (por ejemplo $0{,}9\pm0{,}1$) y se debería justificar la pérdida de energía por fricción y por deformación.

### Reproducción con el criterio alternativo (v = d/(4Δt))
- $v_1 = 0{,}63$ m/s (dirección $-\hat i$), $v_2=0{,}345$ m/s.
- Tras el choque elástico con masas iguales: $v_1'=0{,}345$, $v_2'=-0{,}63$ m/s.
- $p$ antes $=0{,}2715(-0{,}63+0{,}345)=-0{,}0774$ kg·m/s; $E_c=\tfrac12(0{,}2715)(0{,}63^2+0{,}345^2)=0{,}0701$ J.

## Ejemplos adicionales
1. Choque perfectamente inelástico: $m_1=0{,}2715$ kg a 0,63 m/s contra $m_2$ idéntica en reposo. $v'=0{,}315$ m/s; $E_c$ inicial $=0{,}0539$ J, final $=0{,}0270$ J: se pierde 50 %.
2. $\varepsilon$ medido: si $v_1=0{,}60$, $v_2=0$ y después $v_1'=0{,}05$, $v_2'=0{,}55$: $\varepsilon=(0{,}55-0{,}05)/0{,}60=0{,}83$.

## Errores comunes
- Olvidar el signo de la velocidad (en el informe $v_1$ es negativa porque va hacia la izquierda).
- Aplicar conservación de energía a un choque inelástico.
- No nivelar el riel: aparece una fuerza externa y el momento no se conserva.
- Medir distancias desde el origen de la tira cuando la primera marca tiene más ruido.

## Ejercicios propuestos
1. Carro de 0,5 kg a 2 m/s choca elásticamente con otro de 1 kg en reposo. Halla velocidades finales. (Resp. $-0{,}67$ y $+1{,}33$ m/s.)
2. Mismos cuerpos, choque perfectamente inelástico. (Resp. 0,67 m/s; pérdida de energía 1,0 J·(2/3)=0,67 J.)
3. Un carro de masa $m$ choca elásticamente con un carro de $3m$ en reposo; ¿en qué proporción cede energía? (Resp. 75 %.)
4. Coeficiente de restitución de una pelota que cae de 1,00 m y rebota a 0,64 m. (Resp. $\varepsilon=\sqrt{0{,}64}=0{,}8$.)

## Conexiones
Tema de momento lineal y colisiones en [[Física I]]; análisis de errores en [[Laboratorio de Física I - Teoría de errores y mediciones]].

## Fuente
`Material/Informe Choques.docx` (24 de mayo de 2024). Las fórmulas se leyeron del XML del documento.
