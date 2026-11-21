---
tags: [clase, electiva]
materia: Interfaces Digitales Biomédicas
---
# Interfaces Digitales Biomédicas - Transductores y Acondicionamiento Analógico

Materia: [[Interfaces Digitales Biomédicas]]  
Anterior: [[Interfaces Digitales Biomédicas - Bioseñales y Características Eléctricas]]  
Siguiente: [[Interfaces Digitales Biomédicas - Conversión AD, Muestreo y Cuantificación]]

## Contexto y objetivo

Estudiar cómo los **transductores** convierten variables fisiológicas en señales eléctricas y cómo se acondicionan analógicamente mediante **amplificadores de instrumentación (INA)**, cálculo de **CMRR**, circuito de **pierna derecha (DRL)** y **filtros analógicos** (pasa-banda, *notch* y *antialiasing*).

## 1. Transductores y electrodos biomédicos

- **Electrodos biopotenciales (Ag/AgCl)**: convierten corrientes iónicas del tejido en corrientes electrónicas hacia el cable. El gel electrolítico reduce la impedancia piel-electrodo ($Z_{\text{piel}} \sim 10\text{ – }100\text{ k}\Omega$).
- **Sensores ópticos (SpO₂ / PPG)**: LED rojo ($660\text{ nm}$), LED infrarrojo ($940\text{ nm}$) y fotodiodo con amplificador de transimpedancia (TIA).
- **Sensores de temperatura, presión y flujo**: termistores NTC, galgas extensiométricas en puente de Wheatstone, sensores piezoeléctricos.

## 2. Amplificador de Instrumentación (INA)

Para medir señales diferenciales pequeñas ($V_d = V_+ - V_-$) inmersas en un gran ruido de modo común ($V_{cm}$, ej. $60\text{ Hz}$ inducido en el cuerpo), se usa un **Amplificador de Instrumentación** (clásica topología de 3 operacionales, ej. INA128, AD620):

- **Impedancia de entrada altísima** ($> 10^9\;\Omega$) para no atenuar la señal por el divisor con $Z_{\text{piel}}$.
- **Ganancia ajustable** mediante una sola resistencia externa $R_G$:
  $$G = 1 + \frac{50\text{ k}\Omega}{R_G} \quad \text{(típico en INA128/AD8221)}$$
- **Razón de Rechazo en Modo Común (CMRR)**: mide la capacidad de amplificar $V_d$ y rechazar $V_{cm}$:
  $$\text{CMRR}_{\text{dB}} = 20 \log_{10}\left(\frac{A_d}{A_{cm}}\right)$$
  En biopotenciales se exige $\text{CMRR} \ge 80\text{ – }100\text{ dB}$.

### Circuito de Pierna Derecha (DRL - *Driven Right Leg*)
Invierte y realimenta la señal de modo común promedio hacia un tercer electrodo de referencia en el paciente, reduciendo drásticamente el $V_{cm}$ de $60\text{ Hz}$ y mejorando la seguridad al limitar la corriente con una resistencia de protección.

## 3. Etapas de filtrado analógico

1. **Filtro Pasa-Altos** ($f_c \approx 0.05\text{ – }0.5\text{ Hz}$): elimina el *offset* DC de los electrodos y la deriva basal por respiración.
2. **Filtro Pasa-Bajos (*Antialiasing*)** ($f_c \approx 150\text{ Hz}$ para ECG): atenúa frecuencias por encima de $f_s / 2$ antes del ADC y elimina ruido de alta frecuencia.
3. **Filtro *Notch* (rechazo de banda)** ($50\text{ o }60\text{ Hz}$): atenúa la interferencia residual de la red eléctrica (a menudo se prefiere implementarlo digitalmente para no distorsionar la fase analógica).

## Errores comunes

- Conectar electrodos directamente a un amplificador inversor simple (baja impedancia de entrada y pobre CMRR).
- Aplicar una ganancia total de $1000$ en la primera etapa antes de filtrar el *offset* DC (en lugar de usar ganancia moderada $G_1 \approx 10\text{ – }20$, luego pasa-altos, y luego $G_2 \approx 50$).

## Ejercicios propuestos

1. Un INA tiene ganancia diferencial $A_d = 500$ y ganancia en modo común $A_{cm} = 0.01$. Calcula su $\text{CMRR}_{\text{dB}}$. Si entra una señal ECG de $1\text{ mV}$ con ruido común de $1\text{ V}$, ¿cuál es la amplitud de salida de cada componente?
   - *Respuesta:* $\text{CMRR}_{\text{dB}} = 20\log_{10}(500 / 0.01) = 20\log_{10}(50000) \approx 94\text{ dB}$. Salida ECG $= 500\cdot 1\text{ mV} = 500\text{ mV}$; salida ruido $= 0.01 \cdot 1\text{ V} = 10\text{ mV}$.

## Conexiones

- Anterior: [[Interfaces Digitales Biomédicas - Bioseñales y Características Eléctricas]]
- Siguiente: [[Interfaces Digitales Biomédicas - Conversión AD, Muestreo y Cuantificación]]
- Materia: [[Interfaces Digitales Biomédicas]]
- Materias relacionadas: [[Física II]], [[Laboratorio de Física II]], [[Automatización]]

## Fuente

- Temario de [[Interfaces Digitales Biomédicas]] (Webster, Cap. 3 y 6; Northrop).
