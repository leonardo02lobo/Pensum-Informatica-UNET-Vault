---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/CT13-1, imprimir.pdf (y CT13-1.pps)
---
# Física I - Tema 3 Movimiento circular

Materia: [[Física I]]
Anterior: [[Física I - Tema 2 Problemas de proyectiles]]
Siguiente: [[Física I - Tema 3 Problemas de movimiento circular]]

## Contexto y objetivo
Tercer tipo de movimiento bidimensional del curso: la partícula describe una **circunferencia**. Se establece la **analogía** con el movimiento rectilíneo: posición angular $\theta$, velocidad angular $\omega$ y aceleración angular $\alpha$ juegan el papel de $x$, $v$ y $a$. Objetivo: manejar movimiento circular uniforme (MCU) y uniformemente variado (MCUV) y descomponer la aceleración en centrípeta y tangencial.

## 1. Magnitudes angulares
- **Posición angular** $\theta$ (rad), medida desde el eje $+X$ antihorario; $\theta=s/R$ ($s$ longitud de arco). $2\pi$ rad $=360°$.
- **Velocidad angular media/instantánea**: $\omega=d\theta/dt$ (rad/s). Vectorialmente $\vec\omega$ apunta según la regla de la mano derecha (eje de giro).
- **Aceleración angular**: $\alpha=d\omega/dt$ (rad/s²).
- **Periodo** $T$ (tiempo de una vuelta) y **frecuencia** $f=1/T$; $\omega=2\pi f=2\pi/T$.
- **Número de vueltas**: $N=\dfrac{\Delta\theta}{2\pi}$.

## 2. Analogía lineal-angular
| Rectilíneo (MRUV) | Circular (MCUV) |
|---|---|
| $x=x_0+v_0t+\tfrac12at^2$ | $\theta=\theta_0+\omega_0t+\tfrac12\alpha t^2$ |
| $v=v_0+at$ | $\omega=\omega_0+\alpha t$ |
| $v^2=v_0^2+2a\Delta x$ | $\omega^2=\omega_0^2+2\alpha\Delta\theta$ |
| $a=\text{cte}$ | $\alpha=\text{cte}$ |

MCU: $\alpha=0$, $\theta=\theta_0+\omega t$.

## 3. Vectores del movimiento circular (radio $r$)
- **Posición**: $\vec r=r\cos\theta\,\hat i+r\sin\theta\,\hat j$, $|\vec r|=R$ constante.
- **Velocidad**: $\vec v=-\omega r\sin\theta\,\hat i+\omega r\cos\theta\,\hat j$; módulo $v=\omega r$; es **tangente** a la trayectoria (perpendicular a $\vec r$).
 Deducción: derivando $\vec r(t)$ con $\dot\theta=\omega$ se obtiene $\vec v$; y $\vec r\cdot\vec v=0$.
- **Aceleración**: $\vec a=\vec a_c+\vec a_T$.
 - **Centrípeta**: $\vec a_c=-\omega^2r\cos\theta\,\hat i-\omega^2r\sin\theta\,\hat j=-\omega^2\vec r$; módulo $a_c=\omega^2r=v^2/r$; apunta al centro; cambia la **dirección** de $\vec v$.
 - **Tangencial**: $\vec a_T=-\alpha r\sin\theta\,\hat i+\alpha r\cos\theta\,\hat j$; módulo $a_T=\alpha r$; cambia el **módulo** de $\vec v$ (si $\alpha=0$, no hay).
 - Módulo total: $a=\sqrt{a_c^2+a_T^2}$.

Observación clave: en el MCU la aceleración **no es cero** aunque la rapidez sea constante; $\vec a_c$ es de módulo constante, pero su dirección cambia: **no es un vector constante**.

## 4. Relación con puntos de un cuerpo
Dos puntos de un disco que gira comparten $\omega$ y $\alpha$, pero la rapidez lineal $v=\omega r$ crece con la distancia al eje. Dos poleas unidas por una correa que no resbala comparten $v$ (no $\omega$).

## 5. Ejemplos resueltos
**A. Disco.** Un disco de $r=0{,}20$ m gira a 120 rpm. $\omega=120\cdot2\pi/60=12{,}57$ rad/s; $v=2{,}51$ m/s; $a_c=\omega^2r=31{,}6$ m/s²; $T=0{,}5$ s.

**B. MCUV.** Una rueda parte del reposo con $\alpha=2$ rad/s². A $t=5$ s: $\omega=10$ rad/s; $\Delta\theta=\tfrac12(2)(25)=25$ rad $=3{,}98$ vueltas. Si $r=0{,}3$ m: $a_T=0{,}6$ m/s²; $a_c=\omega^2r=30$ m/s²; $a=30{,}01$ m/s².

**C. Frenado.** Un ventilador pasa de 40 rad/s a 0 en 20 s: $\alpha=-2$ rad/s², $\Delta\theta=\frac{0-1600}{2(-2)}=400$ rad (63,7 vueltas).

## 6. Funciones por tramos
Si $\omega(t)$ es una poligonal se construyen $\theta$ y $\omega$ por tramos, igual que en [[Física I - Tema 1 Movimiento en una dimensión]]: el área bajo $\omega(t)$ es $\Delta\theta$ y la pendiente es $\alpha$.

## Errores comunes
1. Usar grados en las fórmulas con $\omega$ en rad/s.
2. Creer que $\vec a_c$ es constante en el MCU.
3. Confundir rpm con rad/s ($1\text{ rpm}=\pi/30$ rad/s).
4. Sumar $a_c$ y $a_T$ algebraicamente (son perpendiculares).
5. Olvidar el signo de $\alpha$ cuando el movimiento frena.

## Ejercicios propuestos
1. Una rueda de 0,5 m de radio gira a 3 rad/s. $v$ y $a_c$. *Resp.: 1,5 m/s; 4,5 m/s².*
2. Satélite con $T=90$ min: $\omega$. *Resp.: $1{,}16\times10^{-3}$ rad/s.*
3. $\theta(t)=2t+t^2$ (rad). $\omega$ y $\alpha$. *Resp.: $2+2t$; 2 rad/s².*
4. ¿Cuántas vueltas da un CD que acelera de 0 a 50 rad/s en 4 s? *Resp.: $\Delta\theta=100$ rad, 15,9 vueltas.*

## Conexiones
La dinámica del movimiento circular ($F_c=ma_c$) aparece en [[Física I - Tema 4 Leyes de Newton]]; la rotación del cuerpo rígido reutiliza estas ecuaciones en [[Física I - Tema 9 Cuerpo rígido y momento de inercia]].

## Fuente
Material/Parcial 1/CT13-1, imprimir.pdf y CT13-1.pps; fórmulas del [[Física I - Formulario I parcial]].
