---
tags: [clase, semestre-VI]
materia: Comunicaciones I
fuente: conocimiento general
---
# Comunicaciones I - 02 Señales y análisis de Fourier

Materia: [[Comunicaciones I]]
Anterior: [[Comunicaciones I - 01 Modelo de comunicación y redes]]
Siguiente: [[Comunicaciones I - 03 Medios de transmisión]]

## Contexto y objetivo
Toda señal puede verse en el **tiempo** y en la **frecuencia**. El análisis de Fourier explica por qué un canal con ancho de banda limitado deforma los pulsos digitales y fija los límites de la tasa de datos.

## Señales
- **Periódica**: $s(t+T) = s(t)$, frecuencia $f = 1/T$. **Senoidal**: $s(t) = A\sin(2\pi f t + \varphi)$ con amplitud A, frecuencia f y fase φ.
- Longitud de onda $\lambda = v/f$ (en el vacío $v = c = 3\times10^8$ m/s).
- Analógica (continua) y digital (niveles discretos). Potencia promedio de una senoidal sobre 1 Ω: $A^2/2$.

## Serie de Fourier
Una señal periódica de periodo T es suma de senoidales armónicas de $f_0 = 1/T$:
$$s(t) = \frac{a_0}{2} + \sum_{n=1}^{\infty} \left[a_n\cos(2\pi n f_0 t) + b_n\sin(2\pi n f_0 t)\right]$$
$$a_n = \frac{2}{T}\int_0^T s(t)\cos(2\pi n f_0 t)\,dt,\quad b_n = \frac{2}{T}\int_0^T s(t)\sin(2\pi n f_0 t)\,dt$$

### Ejemplo: onda cuadrada
Onda cuadrada de amplitud ±A: solo armónicos impares con $b_n = \dfrac{4A}{\pi n}$ (n impar):
$$s(t) = \frac{4A}{\pi}\left[\sin(2\pi f_0 t) + \tfrac{1}{3}\sin(6\pi f_0 t) + \tfrac{1}{5}\sin(10\pi f_0 t) + \dots\right]$$
Si el canal solo deja pasar hasta el 3.er armónico, la señal recibida es redondeada. Para una secuencia binaria 1010... a R bps, $f_0 = R/2$; con un ancho de banda B = 3 f_0 pasan los armónicos 1 y 3.

## Dominio de la frecuencia
- **Espectro**: amplitud (y fase) frente a frecuencia. **Ancho de banda de la señal**: rango de frecuencias significativas; ancho de banda **absoluto** (infinito para pulsos ideales) vs **efectivo**.
- **Transformada de Fourier** para señales no periódicas: $S(f) = \int s(t)e^{-j2\pi f t}dt$. Un pulso rectangular de duración τ tiene espectro tipo $\mathrm{sinc}(f\tau)$ con primer cero en $f = 1/\tau$: pulsos más cortos -> más ancho de banda.
- **Componente DC**: $a_0$; varios sistemas (transformadores, acoplamiento capacitivo) no la pasan, de ahí la importancia de códigos sin componente DC.

## Efectos del canal
- **Atenuación** (depende de f), **distorsión de retardo** (distintas f viajan a distinta velocidad), **ruido**.
- Un canal es un **filtro**: pasa-bajas (cable, fibra), pasa-banda (radio, telefonía 300-3400 Hz).
- Relación de pérdida/ganancia en decibelios: $G_{dB} = 10\log_{10}(P_2/P_1) = 20\log_{10}(V_2/V_1)$. Ejemplo: potencia baja de 100 mW a 25 mW: $10\log(0.25) = -6$ dB.

## Ejemplo resuelto: ancho de banda de una señal digital
Un sistema transmite 2 Mbps con NRZ. La frecuencia fundamental de la alternancia 1010 es $R/2$ = 1 MHz. Si se exige conservar hasta el 5.º armónico, B = 5 MHz. Con B = 3 MHz solo llegan fundamental y 3.er armónico: se verá la onda redondeada pero aún se puede decidir 0/1 si el ruido es bajo.

## Errores comunes
- Confundir frecuencia fundamental con ancho de banda.
- Olvidar que dB de potencia usa 10 log y de voltaje 20 log.
- Pensar que una señal digital tiene ancho de banda finito (pulsos ideales: infinito).

## Ejercicios propuestos
1. Periodo 0.5 ms: frecuencia. *Resp.: 2 kHz.*
2. Onda cuadrada de 1 kHz: frecuencias de sus primeros tres armónicos presentes. *Resp.: 1, 3 y 5 kHz.*
3. Señal baja de 20 mW a 2 mW: dB. *Resp.: -10 dB.*

## Conexiones
[[Comunicaciones I - 03 Medios de transmisión]], [[Comunicaciones I - 04 Límites del canal Nyquist y Shannon]]; muestreo en [[Comunicaciones I - 07 Digitalización PCM y muestreo]]; señales de audio/imagen en [[Multimedia]].

## Fuente
Conocimiento general (Stallings cap. 3; Forouzan cap. 3).
