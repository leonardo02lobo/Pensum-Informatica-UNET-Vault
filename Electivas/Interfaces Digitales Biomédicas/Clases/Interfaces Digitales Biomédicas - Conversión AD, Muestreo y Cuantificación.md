---
tags: [clase, electiva]
materia: Interfaces Digitales Biomédicas
---
# Interfaces Digitales Biomédicas - Conversión AD, Muestreo y Cuantificación

Materia: [[Interfaces Digitales Biomédicas]]  
Anterior: [[Interfaces Digitales Biomédicas - Transductores y Acondicionamiento Analógico]]  
Siguiente: [[Interfaces Digitales Biomédicas - Microcontroladores y Protocolos de Comunicación]]

## Contexto y objetivo

Dominar la transición del dominio analógico al digital mediante el **teorema de muestreo de Nyquist-Shannon**, el cálculo de la **resolución del ADC**, el **error de cuantificación** y la relación señal-ruido de cuantificación (**SQNR**), aplicando valores reales de sistemas de adquisición biomédica.

## 1. Muestreo y Teorema de Nyquist-Shannon

Para reconstruir exactamente una señal analógica continua limitada en banda a una frecuencia máxima $f_{\max}$, la frecuencia de muestreo $f_s$ debe satisfacer:

$$f_s \ge 2 f_{\max}$$

- La frecuencia $f_N = f_s / 2$ se denomina **frecuencia de Nyquist**.
- Si existen componentes espectrales por encima de $f_s/2$, ocurre **aliasing** (solapamiento espectral: frecuencias altas se disfrazan de bajas frecuencias falsas). Por ello es obligatorio colocar un **filtro pasa-bajos *antialiasing*** antes del ADC.
- **En la práctica biomédica** se sobremuestrea ($f_s \approx 4\text{ a }10 \times f_{\max}$) para facilitar el diseño del filtro *antialiasing* y preservar la morfología temporal (ej. picos QRS):
  - ECG ($f_{\max} \approx 150\text{ Hz}$): $f_s \ge 300\text{ Hz}$; típico **$500\text{ Hz}$ o $1000\text{ Hz}$**.
  - EMG ($f_{\max} \approx 500\text{ Hz}$): típico **$1\text{ – }2\text{ kHz}$**.

## 2. Cuantificación y resolución del ADC

Un Conversor Analógico-Digital (ADC) de $n$ bits divide el rango de voltaje de referencia $[0, V_{\text{ref}}]$ (o $[-V_{\text{ref}}, +V_{\text{ref}}]$) en $2^n$ niveles discretos.

$$\text{Resolución (LSB)} = \Delta V = \frac{V_{\text{ref}}}{2^n}$$

**Ejemplo del programa:** con $V_{\text{ref}} = 3.3\text{ V}$ y un ADC de $12\text{ bits}$ (como el del ESP32 o STM32):
$$\Delta V = \frac{3.3\text{ V}}{2^{12}} = \frac{3.3}{4096} \approx 0.806\text{ mV}$$

### Error de cuantificación y SQNR
El error máximo de cuantificación es $\pm \Delta V / 2$. Modelando el error como ruido uniforme en $[-\Delta V/2, \Delta V/2]$, la relación señal-ruido de cuantificación ideal para una senoide de escala completa es:
$$\text{SQNR}_{\text{dB}} \approx 6.02\,n + 1.76\text{ dB}$$
Cada bit adicional de resolución mejora la relación señal-ruido en aproximadamente **$6\text{ dB}$**.

## 3. Referido a la entrada (RTI - *Referred to Input*)

Si la etapa analógica amplifica la bioseñal con ganancia $G$, la mínima variación fisiológica detectable en la entrada es:
$$\Delta V_{\text{RTI}} = \frac{\Delta V_{\text{ADC}}}{G} = \frac{V_{\text{ref}}}{G \cdot 2^n}$$
Con $G = 500$, $V_{\text{ref}} = 3.3\text{ V}$ y $12\text{ bits}$: $\Delta V_{\text{RTI}} = \frac{0.806\text{ mV}}{500} \approx 1.61\;\mu\text{V}$, suficiente para ECG de alta calidad.

## 4. Conversión D/A (DAC)

El **DAC** realiza la operación inversa (ej. generar pulsos de calibración de $1\text{ mV}$, estimulación eléctrica o salida de audio/monitor analógico) a partir de una palabra digital de $n$ bits.

## Errores comunes

- Elegir $f_s = 2 f_{\max}$ exacto sin filtro *antialiasing* ideal (los filtros reales tienen pendiente finita, por lo que $f_s$ debe ser mayor).
- Usar un ADC de $10\text{ bits}$ (Arduino Uno, $\Delta V \approx 4.88\text{ mV}$) con baja ganancia para intentar medir señales de EEG de $50\;\mu\text{V}$.

## Ejercicios propuestos

1. Se desea digitalizar una señal EMG con $f_{\max} = 500\text{ Hz}$ usando un ADC de $16\text{ bits}$ con $V_{\text{ref}} = 5\text{ V}$ y ganancia previa $G = 200$. Calcula: *(a)* $f_s$ mínima teórica y recomendada, *(b)* resolución del ADC y *(c)* resolución referida a la entrada.
   - *Respuesta:* *(a)* $f_s \ge 1000\text{ Hz}$; recomendada $2000\text{ – }2500\text{ Hz}$. *(b)* $\Delta V = 5 / 65536 \approx 76.3\;\mu\text{V}$. *(c)* $\Delta V_{\text{RTI}} = 76.3\;\mu\text{V} / 200 \approx 0.38\;\mu\text{V}$.

## Conexiones

- Anterior: [[Interfaces Digitales Biomédicas - Transductores y Acondicionamiento Analógico]]
- Siguiente: [[Interfaces Digitales Biomédicas - Microcontroladores y Protocolos de Comunicación]]
- Materia: [[Interfaces Digitales Biomédicas]]
- Materias relacionadas: [[Fundamentos de Lógica Digital]], [[Organización del Computador]], [[Introducción a las Telecomunicaciones]]

## Fuente

- Temario de [[Interfaces Digitales Biomédicas]] (Webster; Northrop).
