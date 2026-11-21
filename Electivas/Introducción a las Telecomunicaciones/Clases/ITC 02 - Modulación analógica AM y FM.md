---
tags: [clase, electiva]
materia: Introducción a las Telecomunicaciones
fuente: "conocimiento general"
---
# ITC 02 - Modulación analógica AM y FM

Materia: [[Introducción a las Telecomunicaciones]]
Anterior: [[ITC 01 - Señales, Fourier y ancho de banda]]
Siguiente: [[ITC 03 - Modulación digital y capacidad del canal]]

## Contexto y objetivo
Una señal de información (banda base) rara vez puede transmitirse directamente: las antenas razonables exigen altas frecuencias y varios usuarios deben compartir el medio. La **modulación** traslada la información a una portadora. Objetivo: comprender AM y FM, calcular índice de modulación, ancho de banda y potencia.

## Teoría

### Portadora y modulante
Portadora $c(t)=A_c\cos(2\pi f_c t)$; mensaje $m(t)$ con ancho de banda $W$ (frecuencia máxima).

### AM (modulación de amplitud)
$$s(t)=A_c\big[1+\mu\,m_n(t)\big]\cos(2\pi f_c t),\quad |m_n|\le 1$$
Para un tono $m(t)=A_m\cos(2\pi f_m t)$ el **índice** es $\mu=A_m/A_c$. Si $\mu>1$ hay sobremodulación (distorsión). Espectro: portadora más bandas laterales en $f_c\pm f_m$.
- Ancho de banda: $B_{AM}=2W$.
- Potencia total: $P_t=P_c\left(1+\dfrac{\mu^2}{2}\right)$; potencia en bandas laterales $P_c\mu^2/2$.
- Eficiencia: $\eta=\dfrac{\mu^2/2}{1+\mu^2/2}$, máxima 33,3 % con $\mu=1$.
Variantes: DSB-SC (sin portadora), SSB (una banda lateral, mitad de ancho de banda), VSB (TV analógica antigua). Demodulación: detector de envolvente (AM) o coherente.

### FM (modulación de frecuencia)
$$s(t)=A_c\cos\Big(2\pi f_c t+2\pi k_f\!\int_0^t m(\tau)d\tau\Big)$$
Desviación máxima $\Delta f=k_f A_m$; índice $\beta=\Delta f/f_m$. Amplitud constante: más inmunidad al ruido que AM, a costa de ancho de banda. **Regla de Carson**:
$$B_{FM}\approx 2(\Delta f+W)=2W(\beta+1)$$
Radiodifusión FM comercial: $\Delta f=75$ kHz, $W=15$ kHz, canales de 200 kHz, banda 88-108 MHz. AM comercial: 530-1700 kHz, canales de 10 kHz (varía por región; verificar con el ente regulador). Receptor superheterodino: mezcla con oscilador local para pasar a una frecuencia intermedia.

### PM
Modulación de fase; relacionada con FM por la integral.

## Ejemplo resuelto
**AM**: portadora de 1 MHz, 100 W de potencia sin modular, mensaje de 5 kHz con $\mu=0{,}8$.

1. Frecuencias: $f_c\pm f_m = 995$ kHz y 1005 kHz.
2. Ancho de banda: $2\times5=10$ kHz.
3. Potencia total: $100\,(1+0{,}64/2)=132$ W.
4. Potencia de bandas laterales: 32 W; eficiencia $32/132=24{,}2\,\%$.
5. Si el mensaje se reduce a $\mu=0{,}4$: $P_t=108$ W y eficiencia 7,4 %; la modulación profunda es más eficiente.

**FM**: tono de 10 kHz con $\Delta f = 50$ kHz.

1. $\beta = 50/10 = 5$.
2. Carson: $B \approx 2(50+10)=120$ kHz.
3. Comparación: AM con el mismo mensaje usaría 20 kHz; FM usa 6 veces más ancho de banda, a cambio de mayor relación señal a ruido.

Simulación:
```python
import numpy as np
fs = 1_000_000
t = np.arange(0, 0.002, 1/fs)
fm, fc = 5_000, 100_000
m = np.cos(2*np.pi*fm*t)

mu = 0.8
am = (1 + mu*m) * np.cos(2*np.pi*fc*t)          # AM

kf = 20_000                                     # Hz por unidad de m -> desviación 20 kHz
fase = 2*np.pi*kf*np.cumsum(m)/fs
fmod = np.cos(2*np.pi*fc*t + fase)              # FM

for nombre, s in (("AM", am), ("FM", fmod)):
    S = np.abs(np.fft.rfft(s)); f = np.fft.rfftfreq(len(s), 1/fs)
    print(nombre, "pico principal:", f[S.argmax()])
# beta = 20k/5k = 4 -> Carson: 2*(20k+5k) = 50 kHz
```
Medición típica en laboratorio: analizador de espectro o GNU Radio (bloques "AM Demod", "WBFM Receive") con un SDR.

## Errores comunes
- Calcular el ancho de banda de FM como en AM.
- Sobremodulación ($\mu>1$) que recorta la envolvente.
- Olvidar que en AM la mayor parte de la potencia está en la portadora (no lleva información).
- Confundir desviación de frecuencia $\Delta f$ con ancho de banda.
- Aplicar Carson en $\beta$ muy pequeños sin criterio (aproximación).

## Ejercicios propuestos
1. Mensaje de voz de 4 kHz en AM DSB: ancho de banda. *Respuesta: 8 kHz.*
2. AM con $A_c=10$ V, $A_m=7$ V: índice y eficiencia. *Respuesta: $\mu=0{,}7$; $\eta=0{,}245/1{,}245=19{,}7\,\%$.*
3. FM con $\Delta f=75$ kHz y $W=15$ kHz: $\beta$ y ancho de banda de Carson. *Respuesta: $\beta=5$; $B=180$ kHz.*

## Conexiones
[[Comunicaciones I]] (modulación y ruido), [[Matemática IV]] (transformada de Fourier, convolución), [[Física II]] (ondas EM), [[Multimedia]] (audio y radio).

## Fuente
Conocimiento general: Tomasi; Haykin. Valores de canalización comerciales: verificar con CONATEL y el programa oficial.
