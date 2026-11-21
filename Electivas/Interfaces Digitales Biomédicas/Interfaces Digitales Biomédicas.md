---
tags: [electiva]
---
# Interfaces Digitales Biomédicas

Opción de [[Electivas]].

## Descripción
Estudia cómo conectar sensores y dispositivos biomédicos con sistemas digitales: adquisición de bioseñales, acondicionamiento, conversión analógico-digital, procesamiento y comunicación. Objetivo: diseñar interfaces básicas entre un equipo biomédico y una computadora o microcontrolador.

## Temario típico (verificar con el programa oficial)
1. Bioseñales (ECG, EEG, EMG, SpO2) y sus características.
2. Transductores y sensores, amplificadores de instrumentación y filtros.
3. Conversión A/D y D/A, muestreo y cuantificación.
4. Microcontroladores (Arduino, ESP32) y comunicación serial, SPI, I2C, Bluetooth.
5. Procesamiento digital: filtrado FIR/IIR, detección de picos QRS, transformada de Fourier.
6. Estándares y seguridad: HL7, DICOM, normas de seguridad eléctrica del paciente (IEC 60601).

## Fórmulas y ejemplos
```
Teorema de muestreo: fs >= 2 * fmax        # ECG: fmax ~ 150 Hz -> fs >= 300 Hz (típico 500 Hz)
Resolución ADC = Vref / 2^n                # 3.3 V, 12 bits -> 0.8 mV
```

## Relación con el pensum
[[Fundamentos de Lógica Digital]], [[Organización del Computador]], [[Física II]], [[Laboratorio de Física II]], [[Automatización]], [[Matemática IV]]. Complementa [[Introducción a las Telecomunicaciones]].

## Recursos y bibliografía
- Webster, J. *Medical Instrumentation: Application and Design*.
- Northrop, R. *Introduction to Instrumentation and Measurements*.
- Rangayyan, R. *Biomedical Signal Analysis*.
- PhysioNet (bases de datos abiertas de bioseñales), BITalino, Arduino.
