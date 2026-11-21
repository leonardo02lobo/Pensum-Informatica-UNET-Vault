---
tags: [clase, electiva]
materia: Interfaces Digitales Biomédicas
---
# Interfaces Digitales Biomédicas - Procesamiento Digital de Bioseñales

Materia: [[Interfaces Digitales Biomédicas]]  
Anterior: [[Interfaces Digitales Biomédicas - Microcontroladores y Protocolos de Comunicación]]  
Siguiente: [[Interfaces Digitales Biomédicas - Estándares Clínicos y Seguridad Eléctrica]]

## Contexto y objetivo

Aplicar técnicas de **Procesamiento Digital de Señales (DSP)** a bioseñales adquiridas: diseño y comparación de **filtros digitales FIR e IIR**, análisis espectral mediante la **Transformada Rápida de Fourier (FFT)** y algoritmos clásicos de **detección de picos QRS** (como Pan-Tompkins) para calcular la frecuencia cardíaca y variabilidad (HRV).

## 1. Filtros digitales: FIR vs. IIR

Una vez digitalizada la señal $x[n]$, se procesa mediante ecuaciones en diferencias:

$$y[n] = \sum_{k=0}^{M} b_k\, x[n-k] - \sum_{j=1}^{N} a_j\, y[n-j]$$

- **Filtros FIR (*Finite Impulse Response*)**: solo dependen de entradas presentes y pasadas ($a_j = 0$).
  - *Ventajas*: **siempre estables** y permiten **fase lineal exacta** (no distorsionan la forma de onda del complejo QRS ni del segmento ST en ECG).
  - *Desventaja*: requieren mayor orden $M$ (más costo computacional) para cortes abruptos.
- **Filtros IIR (*Infinite Impulse Response*)**: usan realimentación de salidas pasadas ($a_j \neq 0$, ej. Butterworth, Chebyshev, *notch* biquad).
  - *Ventajas*: orden muy bajo para igual selectividad (ideal en microcontroladores).
  - *Desventaja*: fase no lineal (se puede compensar *offline* con filtrado bidireccional `filtfilt`) y posible inestabilidad por cuantificación de coeficientes.

## 2. Transformada de Fourier (DFT / FFT)

La **FFT** descompone la bioseñal discreta de $N$ muestras en su espectro de frecuencias:
$$X[k] = \sum_{n=0}^{N-1} x[n]\, e^{-j\frac{2\pi}{N}kn}, \qquad \Delta f = \frac{f_s}{N}$$
- **Aplicaciones**: verificar presencia de interferencia de $60\text{ Hz}$, analizar ritmos cerebrales en EEG ($\delta: 0.5\text{–}4\text{ Hz}$, $\theta: 4\text{–}8\text{ Hz}$, $\alpha: 8\text{–}13\text{ Hz}$, $\beta: 13\text{–}30\text{ Hz}$) y detectar fatiga muscular en EMG (desplazamiento hacia bajas frecuencias de la frecuencia mediana).

## 3. Detección de picos QRS (Algoritmo de Pan-Tompkins)

El complejo QRS es el evento de referencia para medir la frecuencia cardíaca (BPM) a partir del ECG. La cadena clásica de Pan-Tompkins consta de:
1. **Filtro pasa-banda** ($5\text{ – }15\text{ Hz}$): atenúa línea base, onda P, onda T e interferencia de $60\text{ Hz}$, resaltando la energía del QRS.
2. **Derivada** ($y[n] = \frac{1}{8T}(-x[n-2] - 2x[n-1] + 2x[n+1] + x[n+2])$): enfatiza las pendientes pronunciadas del QRS.
3. **Elevación al cuadrado** ($y[n]^2$): hace positiva toda la señal y amplifica no linealmente las pendientes altas.
4. **Integración en ventana móvil** (ventana de $\sim 150\text{ ms}$): suaviza los múltiples picos del QRS en un único lóbulo ancho.
5. **Umbralización adaptativa**: detecta los máximos locales que superan el umbral dinámico y respeta un período refractario fisiológico ($\sim 200\text{ ms}$).

La frecuencia cardíaca instantánea en latidos por minuto (BPM) a partir de dos picos consecutivos separados por $N_{RR}$ muestras es:
$$\text{BPM} = \frac{60 \cdot f_s}{N_{RR}}$$

## Errores comunes

- Aplicar un filtro pasa-banda demasiado estrecho para diagnóstico clínico (para medir el segmento ST en isquemia se necesita conservar frecuencias desde $0.05\text{ Hz}$).
- Interpretar el espectro FFT sin aplicar una ventana (Hann/Hamming), generando *spectral leakage* (fuga espectral).

## Ejercicios propuestos

1. Un ECG muestreado a $f_s = 500\text{ Hz}$ presenta dos picos R consecutivos en las muestras $n_1 = 1200$ y $n_2 = 1600$. Calcula el intervalo $RR$ en segundos y la frecuencia cardíaca en BPM.
   - *Respuesta:* $N_{RR} = 400$ muestras $\implies RR = 400 / 500 = 0.8\text{ s}$. $\text{BPM} = 60 / 0.8 = 75\text{ BPM}$.

## Conexiones

- Anterior: [[Interfaces Digitales Biomédicas - Microcontroladores y Protocolos de Comunicación]]
- Siguiente: [[Interfaces Digitales Biomédicas - Estándares Clínicos y Seguridad Eléctrica]]
- Materia: [[Interfaces Digitales Biomédicas]]
- Materias relacionadas: [[Matemática IV]], [[Análisis Numérico]], [[Automatización]]

## Fuente

- Temario de [[Interfaces Digitales Biomédicas]] (Rangayyan, *Biomedical Signal Analysis*; Pan & Tompkins, 1985; PhysioNet).
