---
tags: [clase, electiva]
materia: Interfaces Digitales Biomédicas
---
# Interfaces Digitales Biomédicas - Bioseñales y Características Eléctricas

Materia: [[Interfaces Digitales Biomédicas]]  
Anterior: —  
Siguiente: [[Interfaces Digitales Biomédicas - Transductores y Acondicionamiento Analógico]]

## Contexto y objetivo

Comprender el origen fisiológico y los parámetros eléctricos fundamentales (rango de amplitud en mV/$\mu$V y ancho de banda en Hz) de las principales **bioseñales** (**ECG, EEG, EMG, SpO₂**), así como las fuentes de ruido e interferencia que condicionan el diseño de cualquier interfaz biomédica.

## 1. Cadena de adquisición biomédica

Una interfaz digital biomédica conecta un organismo vivo con un sistema de cómputo siguiendo la cadena:
$$\text{Paciente} \to \text{Transductor/Electrodo} \to \text{Acondicionamiento (Amplificación + Filtrado)} \to \text{ADC} \to \text{Microcontrolador/PC}$$

## 2. Principales bioseñales y sus parámetros

| Bioseñal | Origen fisiológico | Amplitud típica | Ancho de banda | Sensor típico |
|---|---|---|---|---|
| **ECG** (Electrocardiograma) | Actividad eléctrica del miocardio (ondas P, complejo QRS, onda T) | $0.5\text{ – }5\text{ mV}$ | $0.05\text{ – }150\text{ Hz}$ (diagnóstico); $0.5\text{ – }40\text{ Hz}$ (monitoreo) | Electrodos superficiales Ag/AgCl |
| **EEG** (Electroencefalograma) | Potenciales sinápticos corticales (ritmos $\delta, \theta, \alpha, \beta, \gamma$) | $10\text{ – }100\;\mu\text{V}$ | $0.5\text{ – }100\text{ Hz}$ | Electrodos en cuero cabelludo (sistema 10-20) |
| **EMG** (Electromiograma) | Potenciales de acción de unidades motoras musculares | $0.05\text{ – }10\text{ mV}$ | $10\text{ – }500\text{ Hz}$ (superficial); hasta $2\text{ kHz}$ (aguja) | Electrodos superficiales o de aguja |
| **PPG / SpO₂** (Pulsioximetría) | Absorción diferencial de luz roja ($660\text{ nm}$) e IR ($940\text{ nm}$) por oxihemoglobina | Señal pulsátil (AC/DC) | $0.5\text{ – }10\text{ Hz}$ | Fotodiodo + LEDs rojo/IR |

## 3. Fuentes de ruido e interferencia

Debido a que las bioseñales tienen amplitudes muy bajas ($\mu$V a pocos mV), son altamente vulnerables a:
1. **Interferencia de la red eléctrica ($50/60\text{ Hz}$)**: acoplamiento capacitivo e inductivo en los cables de electrodos (se atenúa con amplificadores diferenciales de alto CMRR y filtros *notch*).
2. **Potencial de media celda (DC offset) de electrodo**: diferencia de potencial electroquímico piel-electrodo (hasta $\pm 300\text{ mV}$), mucho mayor que la señal ECG/EEG; requiere acoplamiento AC o filtros pasa-altos.
3. **Artefactos de movimiento y respiración**: variaciones en la impedancia piel-electrodo de baja frecuencia ($< 0.5\text{ Hz}$).
4. **Diafonía muscular (artefacto EMG sobre ECG/EEG)** y **ruido térmico** de la electrónica.

## Errores comunes

- Diseñar la ganancia del amplificador pensando solo en la amplitud de la bioseñal (ej. $G = 1000$ para ECG de $1\text{ mV}$), olvidando que un *offset* DC de $200\text{ mV}$ saturaría inmediatamente la etapa de entrada si no se filtra antes de la máxima ganancia.
- Subestimar el ancho de banda del ECG: aunque la frecuencia cardíaca es $\sim 1\text{ – }3\text{ Hz}$, el complejo **QRS** tiene pendientes rápidas con energía significativa hasta $40\text{ – }100\text{ Hz}$.

## Ejercicios propuestos

1. ¿Por qué el EEG es mucho más difícil de adquirir que el ECG?
   - *Respuesta:* Su amplitud es de $10\text{ – }100\;\mu\text{V}$ (unas $50$ a $100$ veces menor que el ECG), por lo que la relación señal-ruido (SNR) frente a interferencias de $60\text{ Hz}$ y artefactos EMG oculares/musculares es mucho más crítica.

## Conexiones

- Siguiente: [[Interfaces Digitales Biomédicas - Transductores y Acondicionamiento Analógico]]
- Materia: [[Interfaces Digitales Biomédicas]]
- Materias relacionadas: [[Física II]], [[Laboratorio de Física II]]

## Fuente

- Temario de [[Interfaces Digitales Biomédicas]] (Webster, *Medical Instrumentation*; Rangayyan, *Biomedical Signal Analysis*).
