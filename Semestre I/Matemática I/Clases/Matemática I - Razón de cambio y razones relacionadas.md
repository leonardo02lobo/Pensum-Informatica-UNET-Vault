---
tags: [clase, semestre-1]
materia: Matemática I
fuente: Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf (sección V, ejercicios 68-87)
---
# Matemática I - Razón de cambio y razones relacionadas

Materia: [[Matemática I]]
Anterior: [[Matemática I - Regla de L'Hôpital]]
Siguiente: [[Matemática I - Extremos, monotonía y concavidad]]

## Contexto y objetivo
La sección V de la guía contiene 20 problemas (68-87) de **la derivada como razón de cambio**: movimiento rectilíneo (68-70) y **razones relacionadas** (71-87): áreas, volúmenes, triángulos rectángulos, escaleras, conos, ángulos de elevación. Objetivo: traducir una situación a una relación entre variables y derivarla respecto al tiempo.

## 1. Teoría
Si $y=f(x)$, $\frac{dy}{dx}$ mide cuánto cambia $y$ por unidad de $x$. En cinemática: posición $s(t)$, velocidad $v=s'$, aceleración $a=v'=s''$, rapidez $|v|$.
**Razones relacionadas:** si dos o más variables dependen de $t$ y están ligadas por una ecuación, derivar implícitamente respecto de $t$ (regla de la cadena).

**Método:** (1) dibujar y nombrar variables; (2) anotar datos y la razón pedida; (3) escribir la ecuación que relaciona las variables **antes** de sustituir valores numéricos; (4) derivar respecto a $t$; (5) sustituir los valores del instante; (6) interpretar signo y unidades.

## 2. Movimiento rectilíneo
**#68 (caída de la piedra).** $s(t)=-16t^2+v_0t+s_0$ con $v_0=0$, $s_0=256$ pies. $v(t)=-32t$: $v(1)=-32$ pie/s, $v(2)=-64$ pie/s. Llega al piso cuando $-16t^2+256=0\Rightarrow t=4$ s; $v(4)=-128$ pie/s; $a=-32$ pie/s².
**#70.** $d_1=4t-3t^2$, $d_2=t^2-2t$: $v_1=4-6t$, $v_2=2t-2$. Igual velocidad: $4-6t=2t-2\Rightarrow t=\tfrac34$ s. Igual posición: $4t-3t^2=t^2-2t\Rightarrow4t^2-6t=0\Rightarrow t=0,\ \tfrac32$ s. A $t=2$: $v_1=-8$, $v_2=2$. Aceleraciones: $a_1=-6$, $a_2=2$.
**#69.** $s=\sqrt{4t^2+3}$: $v=\frac{4t}{\sqrt{4t^2+3}}$; $v=0\Rightarrow t=0$; $v=1\Rightarrow16t^2=4t^2+3\Rightarrow t=\tfrac12$; $v=2$ imposible (siempre $v<2$).

## 3. Razones relacionadas resueltas
**#71 (onda circular).** $A=\pi r^2\Rightarrow A'=2\pi rr'=2\pi(4)(16)=128\pi$ cm²/s ✓.

**#73 (avión).** Altura 3 mi, $x'=480$ mi/h. Tras 30 s ($\tfrac1{120}$ h): $x=4$ mi, $d=\sqrt{x^2+9}=5$. $d^2=x^2+9\Rightarrow dd'=xx'\Rightarrow d'=\frac{4\cdot480}{5}=384$ mi/h ✓.

**#76 (aviones convergentes).** $x=150,\,y=200$ mi a $450$ y $600$ mi/h; $d^2=x^2+y^2$, $d=250$. $d'=\frac{xx'+yy'}{d}=\frac{150(-450)+200(-600)}{250}=-750$ mi/h. Tiempo hasta el punto: $\frac{250}{750}=\frac13$ h $=20$ min ✓.

**#77 (escalera).** $x^2+y^2=64$, $x'=2$ m/s, $x=5\Rightarrow y=\sqrt{39}$. $y'=-\frac{xx'}{y}=-\frac{10}{\sqrt{39}}\approx-1{,}6$ m/s ✓ (baja).

**#78 (tanque cónico).** Altura 10, radio 5 $\Rightarrow r=h/2$; $V=\frac13\pi r^2h=\frac{\pi h^3}{12}$. $V'=\frac{\pi h^2}{4}h'$. Con $V'=2$, $h=6$: $h'=\frac{8}{36\pi}\approx0{,}0707$ pie/min ✓.

**#80 (pila de arena).** Diámetro $=3h\Rightarrow r=\tfrac32h$; $V=\frac13\pi\frac94h^3=\frac{3\pi}4h^3$; $V'=\frac{9\pi}{4}h^2h'$. $3=\frac{9\pi}4(16)h'\Rightarrow h'=\frac1{12\pi}$ m/min ✓.

**#82.** $V=a^3\Rightarrow V'=3a^2a'=3(100)(4)=1200$ cm³/min ✓.

**#74 (cono).** $V=\frac13\pi r^2h\Rightarrow V'=\frac\pi3(2rr'h+r^2h')=\frac\pi3(2\cdot4\cdot2\cdot6+16\cdot(-3))=\frac\pi3(96-48)=16\pi$ cm³/s (aumenta) ✓.

**#72 (barcos).** Elegir origen en el cruce; $d^2=x^2+y^2$ con posiciones lineales; la distancia deja de variar cuando $d'=0$ (mínima): resultado de la guía a las 3 h 16 min 48 s p.m.

**#86 (globo).** $\tan\theta=\frac{h}{30}\Rightarrow\sec^2\theta\,\theta'=\frac{h'}{30}$. Con $h=10\sqrt3$: $\tan\theta=\frac{\sqrt3}{3}$, $\theta=30^\circ$, $\sec^2\theta=\frac43$; $\theta'=\frac{5/30}{4/3}=0{,}125$ rad/s ✓.

Otras respuestas de la guía: #81 $\frac1{2\pi}$ m/min; #84 $40\pi$ cm²/s; #75 $\frac{105}{2}\sqrt2$ km/h (según la guía); #85 $-1{,}89$ m/s; #79 $\frac18$ m/min.

## Errores comunes
- Sustituir valores numéricos antes de derivar (convierte variables en constantes).
- No ajustar unidades (30 s a horas).
- Perder el signo: alejarse es positivo, acercarse negativo.
- Confundir una razón constante con la variable (la altura no crece a razón constante en un cono con caudal constante).

## Ejercicios propuestos
1. Una esfera crece con $r'=2$ cm/s: $V'$ cuando $r=5$. (R: $200\pi$ cm³/s.)
2. Escalera de 10 m, base alejándose a 1 m/s: velocidad de la cima cuando la base está a 6 m. (R: $-0{,}75$ m/s.)
3. Rectángulo con lados $x'=3$, $y'=-2$ m/s: $A'$ si $x=4,y=5$. (R: $7$ m²/s.)
4. $s(t)=t^3-6t^2$: ¿cuándo se detiene? (R: $t=0,4$.)

## Conexiones
La relación posición-velocidad-aceleración es el núcleo de [[Física I]]. Para los problemas de máximos y mínimos véase [[Matemática I - Optimización y trazado de gráficas]]. Su inversa (integrar) está en [[Matemática II]].

## Fuente
`Material/GUIAS/Guía de APLICACIONES DE DERIVADAS.pdf`, sección V. Los enunciados se parafrasearon; resultados confirmados con los de la guía (el #75 se transcribe tal cual aparece en la extracción).
