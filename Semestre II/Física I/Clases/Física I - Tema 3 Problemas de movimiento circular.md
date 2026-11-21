---
tags: [clase, semestre-II]
materia: Física I
fuente: Material/Parcial 1/PR13-1_imprimir.pdf; PR13-1.pps; PP13-0.pdf
---
# Física I - Tema 3 Problemas de movimiento circular

Materia: [[Física I]]
Anterior: [[Física I - Tema 3 Movimiento circular]]
Siguiente: [[Física I - Tema 4 Leyes de Newton]]

## Contexto y objetivo
Documenta el problema resuelto "Problema 3" (PR13-1, Neyra Tellez, marzo 2009, 7 páginas) y la guía de propuestos PP13-0 (8 páginas). Es el equivalente circular del problema de las atletas del Tema 1.

## 1. Problema resuelto
**Enunciado.** Una partícula $m$ describe una circunferencia de radio $R=0{,}50$ m sobre una mesa de aire sin fricción. En $t=0$ pasa por $(R,0)$ con rapidez angular constante $\pi/6$ rad/s. A los 20 s comienza a disminuir uniformemente su rapidez angular hasta detenerse a los 60 s (gráfica $\omega(t)$). Se piden:
1. posición angular en $t=20$ s; 2. vector posición en $t=20$ s; 3. $\omega$ en $t=30$ s; 4. velocidad en $t=30$ s; 5. módulo de $a_T$ en 30 s; 6. aceleración en 30 s; 7. número de vueltas totales; 8. ¿es constante $a_c$ en $0\le t\le20$ s?

**Solución.**
1. Tramo MCU: $\theta_{20}=\theta_0+\omega t=0+\frac{\pi}{6}(20)=\frac{10\pi}{3}$ rad $=10{,}47$ rad (área del rectángulo bajo $\omega(t)$), equivalente a 1,67 vueltas.
2. $\vec r=R(\cos\theta\,\hat i+\sin\theta\,\hat j)$ con $\theta=\frac{10\pi}{3}\equiv\frac{4\pi}{3}$ (240°): $\vec r=0{,}5(-0{,}5\hat i-0{,}866\hat j)=-0{,}25\hat i-0{,}433\hat j$ m.
3. Tramo 20–60 s: pendiente $\alpha=\dfrac{0-\pi/6}{60-20}=-\dfrac{\pi}{240}=-0{,}0131$ rad/s². $\omega_{30}=\frac{\pi}{6}-\frac{\pi}{240}(10)=\frac{\pi}{8}=0{,}393$ rad/s.
4. Rapidez $v=\omega R=0{,}196$ m/s; $\theta_{30}=\theta_{20}+\frac{\pi}{6}(10)-\tfrac12\frac{\pi}{240}(100)=10{,}47+5{,}24-0{,}65=15{,}05$ rad $=862{,}6°\equiv142{,}6°$ (módulo $2\pi$ → $862{,}6-720=142{,}6°$). Dirección de $\vec v$: tangente, $\vec v=-\omega R\sin\theta\,\hat i+\omega R\cos\theta\,\hat j=-0{,}196(0{,}610)\hat i+0{,}196(-0{,}792)\hat j=-0{,}120\hat i-0{,}155\hat j$ m/s.
5. $a_T=|\alpha|R=0{,}0131\cdot0{,}5=6{,}5\times10^{-3}$ m/s².
6. $a_c=\omega^2R=0{,}154\cdot0{,}5=0{,}0771$ m/s² (hacia el centro); $a=\sqrt{a_c^2+a_T^2}=0{,}0774$ m/s²; el vector se obtiene sumando $\vec a_c=-\omega^2\vec r$ y $\vec a_T=\alpha R(-\sin\theta\,\hat i+\cos\theta\,\hat j)$ (con $\alpha<0$ apunta contra la velocidad).
7. $\Delta\theta_{0-20}=\frac{10\pi}{3}$; $\Delta\theta_{20-60}=\tfrac12\cdot\frac{\pi}{6}\cdot40=\frac{10\pi}{3}$. Total $\frac{20\pi}{3}=20{,}94$ rad $\Rightarrow N=\frac{20\pi/3}{2\pi}=3{,}33$ vueltas.
8. En 0–20 s $a_c=\omega^2R$ es constante **en módulo** ($0{,}137$ m/s²) pero **no** como vector, porque su dirección cambia con $\theta$.

(Los valores numéricos son cálculos propios con los datos del enunciado; la guía original contiene el desarrollo gráfico paso a paso.)

## 2. Guía de propuestos PP13-0
- **V/F**: "una partícula en MCU con centro en el origen tiene $\vec r$ paralelo a $\vec a$" (V, antiparalelo: $\vec a=-\omega^2\vec r$); "la velocidad en el MCU apunta al centro" (F, es tangente); "la aceleración en el MCU apunta al centro" (V).
- Preguntas de **selección**: puntos A y B a distintas distancias del eje (misma $\omega$, distinta $v$; con $d=R/2$ se cumple $v_B=v_A/2$ si B está a mitad de radio).
- **Desarrollo**: clavo fijo en el borde de un disco de $r=2$ m (posición angular a $t=4$ s, aceleración del clavo a $t=6$ s, velocidad a $t=17$ s con $\omega(t)$ gráfica); partícula en mesa de aire de radio $0{,}50$ m o $14$ m (instante en que la rapidez alcanza cierto valor, $\omega$ y $\alpha$ en $t=40$ s, velocidad en ese instante); vector posición $\vec r=-5\hat i$ m con velocidad tangente (determinar $\vec v$ a los 5 s).

### Ejemplo en estilo de la guía
Clavo en un disco de $r=2$ m con $\omega=3$ rad/s constante entre 0 y 10 s: aceleración en $t=6$ s: sólo centrípeta, $a=\omega^2r=18$ m/s² dirigida al centro.

## Errores comunes
- Dar la aceleración como $\omega^2R$ sin vector cuando hay $\alpha\ne0$.
- Usar el ángulo acumulado (10,47 rad) sin reducirlo a $[0,2\pi)$ al calcular componentes (en realidad $\sin$ y $\cos$ son periódicas, pero conviene reducirlo para interpretar el cuadrante).
- Olvidar que el signo de $\alpha$ depende del sentido de giro.

## Ejercicios propuestos
1. Con $\omega(t)$: sube de 0 a 4 rad/s en 4 s y luego constante 6 s. $\Delta\theta$. *Resp.: 8+24=32 rad.*
2. Radio 0,4 m, $\omega=5$ rad/s, $\alpha=3$ rad/s². $a_c,a_T,a$. *Resp.: 10; 1,2; 10,07 m/s².*
3. Número de vueltas en el ejercicio 1. *Resp.: 5,09.*

## Conexiones
[[Física I - Tema 3 Movimiento circular]]; $a_c$ se usa en [[Física I - Tema 4 Leyes de Newton]].

## Fuente
Material/Parcial 1/PR13-1_imprimir.pdf, PR13-1.pps (resuelto) y PP13-0.pdf (propuestos).
