---
tags: [clase, electiva]
materia: Introducción a las Telecomunicaciones
fuente: "conocimiento general"
---
# ITC 03 - Modulación digital y capacidad del canal

Materia: [[Introducción a las Telecomunicaciones]]
Anterior: [[ITC 02 - Modulación analógica AM y FM]]
Siguiente: [[ITC 04 - Medios de transmisión guiados]]

## Contexto y objetivo
Los datos digitales se envían variando amplitud, frecuencia o fase de una portadora. Objetivo: conocer ASK, FSK, PSK y QAM, calcular tasa de símbolos y de bits, y aplicar los límites de Nyquist y Shannon.

## Teoría

### Esquemas básicos
- **ASK**: la amplitud representa el bit (OOK: 0 = sin portadora). Sensible al ruido.
- **FSK**: dos o más frecuencias (BFSK). Robusto, menos eficiente en ancho de banda.
- **PSK**: la fase codifica los bits. BPSK (0°, 180°), QPSK (4 fases, 2 bits/símbolo), 8-PSK.
- **QAM**: combina amplitud y fase; 16-QAM (4 bits/símbolo), 64-QAM (6), 256-QAM (8). Constelación: puntos en el plano I/Q.

### Tasa de símbolos y de bits
$$R_b = R_s\log_2 M$$
con $R_s$ en baudios y $M$ niveles posibles. Ancho de banda mínimo (Nyquist, canal ideal pasa bajos): $B \ge R_s/2$; con pasa banda y filtro de coseno alzado de factor $\alpha$:
$$B = R_s(1+\alpha)$$
Eficiencia espectral $\eta=R_b/B$ (bit/s/Hz).

### Límites del canal
**Nyquist** (sin ruido): $C = 2B\log_2 M$.
**Shannon** (con ruido gaussiano):
$$C = B\log_2(1+\text{SNR})$$
con SNR en razón lineal, no en dB: $\text{SNR}=10^{\text{SNR}_{dB}/10}$. Es el techo teórico: ningún esquema lo supera sin error.

### Calidad: BER y $E_b/N_0$
La tasa de error de bit depende de $E_b/N_0$ y del esquema. Para BPSK/QPSK: $\text{BER}=Q\big(\sqrt{2E_b/N_0}\big)$. Más puntos en la constelación (mayor $M$) exige más SNR para el mismo BER; por eso los sistemas adaptan la modulación al enlace (modulación adaptativa en Wi-Fi, LTE).

### Codificación de línea y de canal
Banda base: NRZ, Manchester, AMI. Corrección de errores (FEC): Hamming, Reed-Solomon, convolucional, LDPC.

## Ejemplo resuelto
Canal telefónico de $B=3100$ Hz y SNR de 30 dB.

1. Razón lineal: $\text{SNR}=10^{30/10}=1000$.
2. Shannon: $C=3100\log_2(1001)\approx3100\times9{,}967=30\,900$ b/s (≈ 31 kb/s). Por eso los módems analógicos se acercaron a 33,6 kb/s.
3. Nyquist con $M=16$: $C=2\times3100\times4=24\,800$ b/s, que es alcanzable porque está por debajo de Shannon.
4. Con $M=64$ Nyquist daría $37\,200$ b/s, mayor que Shannon: no es viable con esa SNR.

Enlace de radio con 20 MHz, 64-QAM, $\alpha=0{,}25$:
1. $R_s = B/(1+\alpha)=20/1{,}25=16$ Msímb/s.
2. $R_b=16\times6=96$ Mb/s.
3. Eficiencia: $96/20=4{,}8$ bit/s/Hz.
4. SNR mínima de Shannon para esa eficiencia: $2^{4{,}8}-1\approx 26$, es decir 14,2 dB; en la práctica se necesitan unos 3-6 dB más.

Simulación de QPSK con ruido:
```python
import numpy as np
rng = np.random.default_rng(1)
N = 200_000
bits = rng.integers(0, 2, (N, 2))
# Gray: 00,01,11,10 -> puntos en I/Q
I = 1 - 2*bits[:, 0]
Q = 1 - 2*bits[:, 1]
s = (I + 1j*Q) / np.sqrt(2)                   # energía de símbolo = 1

for ebn0_db in (0, 4, 8):
    ebn0 = 10**(ebn0_db/10)
    n0 = 1/(2*ebn0)                            # Es=1, Eb=1/2
    ruido = np.sqrt(n0/2)*(rng.normal(size=N) + 1j*rng.normal(size=N))
    r = s + ruido
    bi = (r.real < 0).astype(int); bq = (r.imag < 0).astype(int)
    ber = (np.sum(bi != bits[:, 0]) + np.sum(bq != bits[:, 1])) / (2*N)
    print(ebn0_db, "dB  BER =", ber)
# Teoría: Q(sqrt(2*Eb/N0)) -> 0.079, 0.0125, 1.9e-4 aprox.
```
Herramientas: GNU Radio (constelaciones en vivo), Matlab/Scilab.

## Errores comunes
- Usar SNR en dB dentro de $\log_2(1+\text{SNR})$.
- Suponer que más niveles siempre aumentan la velocidad (suben los errores).
- Confundir baudios con bit/s.
- Ignorar el factor de filtro $\alpha$ en el ancho de banda real.
- Creer que Shannon indica cómo construir el sistema (solo marca el límite).

## Ejercicios propuestos
1. Canal de 1 MHz y SNR 20 dB: capacidad de Shannon. *Respuesta: $10^6\log_2(101)\approx 6{,}66$ Mb/s.*
2. Bit/s de un enlace de 2400 baudios con 16-QAM. *Respuesta: 9600 b/s.*
3. ¿Cuántos puntos tiene una constelación de 256-QAM y cuántos bits por símbolo? *Respuesta: 256 puntos; 8 bits.*

## Conexiones
[[Comunicaciones I]] y [[Comunicaciones II]] (transmisión digital, errores), [[Administración de Redes]] (tasas de enlace Wi-Fi/Ethernet), [[Matemática IV]] (probabilidad y Fourier).

## Fuente
Conocimiento general: Stallings, *Data and Computer Communications*; Haykin; Tomasi. Verificar con el programa oficial.
