---
tags: [clase, electiva]
materia: Interfaces Digitales Biomédicas
---
# Interfaces Digitales Biomédicas - Microcontroladores y Protocolos de Comunicación

Materia: [[Interfaces Digitales Biomédicas]]  
Anterior: [[Interfaces Digitales Biomédicas - Conversión AD, Muestreo y Cuantificación]]  
Siguiente: [[Interfaces Digitales Biomédicas - Procesamiento Digital de Bioseñales]]

## Contexto y objetivo

Diseñar la etapa digital de adquisición en tiempo real usando **microcontroladores** (Arduino, ESP32) mediante interrupciones de temporizador (*timers*) para muestreo determinístico, y comparar los protocolos de comunicación **UART (Serial), SPI, I²C y Bluetooth/BLE** empleados en sensores y monitores biomédicos.

## 1. Muestreo determinístico en microcontroladores

En adquisición biomédica **no se debe usar `delay()`** para controlar $f_s$, porque el tiempo de ejecución del procesamiento y transmisión introduce *jitter* (variación irregular del período $T_s = 1/f_s$), distorsionando el análisis espectral (FFT) y los filtros digitales.

**Buenas prácticas:**
- Configurar un **Timer por hardware** con interrupción periódica exacta (ej. cada $2\text{ ms}$ para $f_s = 500\text{ Hz}$).
- Usar un **buffer circular (ring buffer)** o **DMA** (*Direct Memory Access*) para almacenar muestras en la ISR y transmitirlas en el bucle principal.

```cpp
// Pseudocódigo de muestreo determinístico en ESP32 / Arduino (fs = 500 Hz)
volatile bool newSample = false;
volatile uint16_t adcVal = 0;

void IRAM_ATTR onTimer() {
    adcVal = analogRead(34);   // Lectura rápida en ISR
    newSample = true;
}
```

## 2. Protocolos de comunicación en sistemas biomédicos

| Protocolo | Tipo / Líneas | Velocidad típica | Uso típico en biomédica |
|---|---|---|---|
| **UART / Serial (USB)** | Asíncrono, 2 líneas (TX, RX) | $9600\text{ – }921600\text{ bps}$ | Envío de tramas del microcontrolador hacia la PC (Python/MATLAB) o módulos Bluetooth HC-05. |
| **SPI** | Síncrono, 4 líneas (MOSI, MISO, SCLK, CS) | $1\text{ – }20+\text{ MHz}$ | ADCs biomédicos multicanal de alta resolución (ej. **ADS1298** / ADS1292 de 24 bits para ECG/EEG). |
| **I²C** | Síncrono, 2 líneas (SDA, SCL), direccionamiento | $100\text{ – }400\text{ kHz}$ | Sensores integrados compactos (ej. **MAX30102** para SpO₂ y pulso, acelerómetros, sensores de temperatura). |
| **Bluetooth / BLE** | Inalámbrico ($2.4\text{ GHz}$) | $1\text{ – }2\text{ Mbps}$ (BLE) | Wearables y telemetría ambulatoria sin cables (aislamiento galvánico natural del paciente). |

## 3. Cálculo de ancho de banda de transmisión

Si muestreamos 3 canales de ECG a $f_s = 500\text{ Hz}$ con resolución de $16\text{ bits}$ ($2\text{ bytes}$) más $2\text{ bytes}$ de cabecera/checksum por paquete:
- Tamaño de trama $= 3 \times 2 + 2 = 8\text{ bytes} = 64\text{ bits}$.
- Tasa de datos $= 500 \times 64 = 32\,000\text{ bps}$.
- Con UART a $115\,200\text{ bps}$ (considerando 10 bits por byte con start/stop: $11\,520\text{ bytes/s}$), $500 \times 8 = 4000\text{ bytes/s}$ cabe cómodamente sin pérdida de muestras.

## Errores comunes

- Enviar datos en texto ASCII (`Serial.println(valor)`) a altas frecuencias de muestreo en lugar de tramas binarias compactas, saturando el puerto serial.
- Olvidar resistencias *pull-up* en el bus I²C o compartir el bus SPI sin gestionar correctamente el pin **CS (Chip Select)**.

## Ejercicios propuestos

1. Un sistema EEG de 8 canales muestrea a $f_s = 250\text{ Hz}$ con $24\text{ bits}$ por muestra (sin cabecera). ¿Cuál es la tasa de bits neta? ¿Alcanza un enlace UART a $57\,600\text{ bps}$?
   - *Respuesta:* $8 \times 250 \times 24 = 48\,000\text{ bps}$ netos. Con 1 bit start + 1 stop por byte ($10/8 = 1.25$), requiere $48\,000 \times 1.25 = 60\,000\text{ bps}$, por lo que $57\,600\text{ bps}$ **no alcanza** (se necesita $115\,200\text{ bps}$).

## Conexiones

- Anterior: [[Interfaces Digitales Biomédicas - Conversión AD, Muestreo y Cuantificación]]
- Siguiente: [[Interfaces Digitales Biomédicas - Procesamiento Digital de Bioseñales]]
- Materia: [[Interfaces Digitales Biomédicas]]
- Materias relacionadas: [[Organización del Computador]], [[Fundamentos de Lógica Digital]], [[Introducción a las Telecomunicaciones]]

## Fuente

- Temario de [[Interfaces Digitales Biomédicas]] (Arduino, ESP32, BITalino, hojas de datos ADS1298 / MAX30102).
