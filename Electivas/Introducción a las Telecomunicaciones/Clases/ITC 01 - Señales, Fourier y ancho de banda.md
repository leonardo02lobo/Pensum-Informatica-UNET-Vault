---
tags: [clase, electiva]
materia: Introducción a las Telecomunicaciones
fuente: "conocimiento general"
---
# ITC 01 - Señales, Fourier y ancho de banda

Materia: [[Introducción a las Telecomunicaciones]]
Anterior: (inicio de la serie)
Siguiente: [[ITC 02 - Modulación analógica AM y FM]]

## Contexto y objetivo
Un sistema de telecomunicaciones transmite información mediante señales a través de un canal. Objetivo: describir señales en el tiempo y la frecuencia, usar series y transformada de Fourier, y calcular ancho de banda y decibelios.

## Teoría

### Señales
Analógica (continua en amplitud y tiempo) frente a digital (valores discretos). Periódica o no, de energía o de potencia. Senoide: $x(t)=A\cos(2\pi f t+\varphi)$, con amplitud $A$, frecuencia $f$ (Hz), periodo $T=1/f$ y fase $\varphi$.

### Serie de Fourier
Toda señal periódica de periodo $T$ y frecuencia fundamental $f_0=1/T$ es suma de armónicos:
$$x(t)=a_0+\sum_{n=1}^{\infty}\left[a_n\cos(2\pi n f_0 t)+b_n\sin(2\pi n f_0 t)\right]$$
Para una onda cuadrada simétrica de amplitud $\pm A$ solo hay armónicos impares:
$$x(t)=\frac{4A}{\pi}\sum_{k=0}^{\infty}\frac{\sin\big(2\pi (2k+1) f_0 t\big)}{2k+1}$$

### Transformada de Fourier
Para señales no periódicas:
$$X(f)=\int_{-\infty}^{\infty} x(t)\,e^{-j2\pi f t}\,dt$$
Un pulso rectangular de duración $\tau$ tiene espectro $\tau\,\mathrm{sinc}(\pi f\tau)$, con primer nulo en $1/\tau$: pulsos más cortos ocupan más ancho de banda. Esto conecta con [[Matemática IV]].

### Ancho de banda
Rango de frecuencias donde se concentra la energía útil (p. ej. donde la potencia cae menos de 3 dB). Voz telefónica: 300-3400 Hz (≈ 3,1 kHz; canal de 4 kHz). Audio de alta fidelidad: 20 Hz-20 kHz.

### Decibelios
$$G_{dB}=10\log_{10}\frac{P_2}{P_1},\qquad G_{dB}=20\log_{10}\frac{V_2}{V_1}$$
$\text{dBm}=10\log_{10}(P/1\,\text{mW})$. Referencias útiles: 3 dB ≈ factor 2 en potencia; 10 dB = factor 10.

### Muestreo
Teorema de Nyquist-Shannon: para reconstruir una señal de ancho de banda $B$ se muestrea a $f_s \ge 2B$. Por debajo ocurre *aliasing*.

## Ejemplo resuelto
Señal digital en banda base: onda cuadrada de 1 kHz, amplitud ±1 V. ¿Qué ancho de banda hace falta para pasar hasta el 5.º armónico?

1. Fundamental $f_0 = 1$ kHz. Armónicos impares: 1, 3, 5 kHz.
2. Ancho de banda hasta el 5.º armónico: $B = 5$ kHz.
3. Amplitudes: $\dfrac{4A}{\pi n}$ con $A=1$: $n=1$: 1,273 V; $n=3$: 0,424 V; $n=5$: 0,255 V.
4. Potencia relativa del armónico $n$ respecto al fundamental: $1/n^2$. Para $n=5$: 0,04, es decir, $10\log_{10}(0{,}04) = -14$ dB.
5. Conclusión: con 5 kHz se conserva casi toda la potencia, pero con 1 kHz solo llega una senoide.

Cálculo de potencia fraccional con los tres primeros armónicos: $\dfrac{1+1/9+1/25}{\pi^2/8} = \dfrac{1{,}151}{1{,}234}=0{,}933$, o sea el 93 % de la potencia.

Simulación numérica:
```python
import numpy as np
fs, T = 100_000, 1.0
t = np.arange(0, 0.01, 1/fs)
f0 = 1000
x = np.sign(np.sin(2*np.pi*f0*t))            # onda cuadrada
X = np.fft.rfft(x)
f = np.fft.rfftfreq(len(x), 1/fs)
mag = 2*np.abs(X)/len(x)
for n in (1, 3, 5, 7):
    k = np.argmin(abs(f - n*f0))
    print(n*f0, round(mag[k], 3))
# esperado aprox: 1.273, 0.424, 0.255, 0.182
```
Decibelios: una señal de 0,5 W entra a un cable y salen 0,125 W. Pérdida: $10\log_{10}(0{,}5/0{,}125)=6$ dB.

## Errores comunes
- Confundir dB con dBm (uno es relación, otro absoluto).
- Usar 10log en lugar de 20log para tensiones.
- Creer que ancho de banda y velocidad (bps) son lo mismo.
- Muestrear sin filtro antialiasing.
- Olvidar que las señales digitales también tienen espectro ancho.

## Ejercicios propuestos
1. Un amplificador lleva 2 mW a 200 mW; ganancia en dB. *Respuesta: 20 dB.*
2. Frecuencia mínima de muestreo para voz de 3,4 kHz. *Respuesta: 6,8 kHz (la telefonía usa 8 kHz).*
3. Potencia en dBm de 100 mW. *Respuesta: 20 dBm.*

## Conexiones
[[Matemática IV]] (Fourier), [[Física II]] (ondas, electromagnetismo), [[Comunicaciones I]] (señales y sistemas), [[Administración de Redes]] (capa física).

## Fuente
Conocimiento general: Haykin, *Communication Systems*; Tomasi, *Sistemas de Comunicaciones Electrónicas*; Stallings. Verificar con el programa oficial.
