---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/PR12-1_imprimir.pdf; PR12-1.pps; PP12-0.pdf
---
# Física I - Tema 2 Problemas de proyectiles

Materia: [[Física I]]
Anterior: [[Física I - Tema 2 Movimiento de proyectiles]]
Siguiente: [[Física I - Tema 3 Movimiento circular]]

## Contexto y objetivo
Documenta el problema resuelto PR12-1 ("Problema 2", Neyra Tellez, octubre 2009) y la guía PP12-0 (6 páginas, "Problemas propuestos para movimiento parabólico"). Sirve para practicar la separación en ejes y el cálculo del tiempo de vuelo a partir del alcance.

## 1. Problema resuelto: el balón y la pared
**Enunciado.** Jugador de fútbol golpea una pelota de masa $m=0{,}45$ kg desde 1 m de altura con $\vec v_0=14{,}14\hat i+14{,}14\hat j$ m/s ($\vec g=-9{,}8\hat j$) para estrellarla contra una pared de $H=23$ m ubicada a $L=20$ m. Se piden: (1) ángulo de salida; (2) posición a 0,52 s; (3) altura de impacto; (4) velocidad de impacto.

**Leyes y conceptos**: cinemática de la partícula, trigonometría, MRU y MRUV, sistema de referencia con origen en el pie del jugador, $y_0=1$ m.

1. **Ángulo**: $\tan\theta=v_{0y}/v_{0x}=1\Rightarrow\theta=45°$ (la magnitud es $v_0=\sqrt{2}\cdot14{,}14=20$ m/s).
2. **Posición a 0,52 s**: $x=14{,}14\,t$, $y=1+14{,}14\,t-4{,}9t^2$. Con $t=0{,}52$: $x=7{,}35$ m, $y=7{,}03$ m, es decir $\vec r=7{,}35\hat i+7{,}03\hat j$ m.
3. **Altura en la pared**: el tiempo de vuelo se obtiene del eje $x$ porque se conoce el alcance: $t_v=\dfrac{L}{v_{0x}}=\dfrac{20}{14{,}14}=1{,}41$ s. Luego $y=1+14{,}14(1{,}41)-4{,}9(1{,}41)^2=11{,}2$ m $<23$ m: la pelota **sí golpea la pared** y lo hace en la altura 11,2 m.
4. **Velocidad al chocar**: $v_x=14{,}14$ m/s (constante), $v_y=14{,}14-9{,}8(1{,}41)=0{,}32$ m/s. $\vec v=14{,}14\hat i+0{,}32\hat j$ m/s; la pelota está casi en el punto más alto y el módulo es $14{,}14$ m/s.

Observación pedagógica: el tiempo de vuelo se calcula con la variable del eje que **más información tiene** (aquí $x$); con él se evalúa el otro eje.

## 2. Guía de problemas propuestos (PP12-0)
Estructura:
- **Comprensión (V/F)**: "si la rapidez es constante también lo es la velocidad" (F: la dirección puede cambiar); "la velocidad de una partícula con aceleración constante puede variar en dirección pero no en magnitud" (F; el proyectil cambia ambas); "el tiempo máximo es aquel en que la velocidad del proyectil es cero" (F: se anula solo $v_y$).
- **Selección múltiple** con trayectorias dibujadas (por ejemplo puntos C, D, E de la parábola: velocidad nula en C solo si C es el vértice y $v_x=0$, lo que no ocurre; en puntos simétricos D y E la **rapidez** es igual pero no la velocidad vectorial).
- **Desarrollo**: moneda que cae en un plato; salto entre dos edificios (anchura 4 m, desnivel 3 m); automóvil que cae por un acantilado de 50 m tras acelerar 4 m/s² durante 50 m; balón que debe pasar por la parte superior de una portería (24 m de distancia, 2,75 m de altura); lanzamiento desde 1 m de altura (módulo de la velocidad inicial, altura máxima, velocidad sobre la portería, tiempo en el aire).

### Ejemplo de resolución (automóvil por el acantilado, reconstrucción)
El auto parte del reposo y acelera 4 m/s² durante 50 m: $v^2=2(4)(50)=400\Rightarrow v=20$ m/s. Sale horizontalmente del borde de un acantilado de 50 m: $t=\sqrt{2(50)/9{,}8}=3{,}19$ s; alcance horizontal $R=20(3{,}19)=63{,}9$ m; $v_y=-9{,}8(3{,}19)=-31{,}3$ m/s; rapidez al chocar $\sqrt{20^2+31{,}3^2}=37{,}1$ m/s. (La guía incluye datos adicionales: verificar enunciado exacto en el PDF.)

### Ejemplo (salto entre edificios)
Edificio más bajo 3 m y a 4 m: tiempo de caída $t=\sqrt{2(3)/9{,}8}=0{,}78$ s; velocidad horizontal mínima $v=4/0{,}78=5{,}1$ m/s para llegar al borde.

## Errores comunes
- Evaluar $y$ con el tiempo de vuelo de otro problema.
- Olvidar que $y_0\ne0$ cambia $t_v$.
- Calcular el ángulo con $\arctan(v_0/ \dots)$ usando $v_0$ total.

## Ejercicios propuestos
1. Con los datos del problema resuelto, ¿qué altura tendría a 20 m si $v_{0y}=10$ y $v_{0x}=14{,}14$? *Resp.: $t=1{,}41$ s; $y=1+10(1{,}41)-4{,}9(1{,}41)^2=5{,}4$ m.*
2. Pelota lanzada a 12 m/s, 60°, desde el suelo: alcance. *Resp.: 12,7 m.*
3. ¿Qué rapidez horizontal permite cruzar un foso de 8 m desde una altura de 2 m? *Resp.: 12,5 m/s.*

## Conexiones
[[Física I - Tema 2 Movimiento de proyectiles]]; práctica experimental en [[Laboratorio de Física I]].

## Fuente
Material/Parcial 1/PR12-1_imprimir.pdf y PR12-1.pps (resuelto), PP12-0.pdf (propuestos; enunciados parcialmente extraídos).
