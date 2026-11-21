---
tags: [clase, semestre-III]
materia: Laboratorio de Física II
---
# Laboratorio de Física II - Instrumentos de Medición y Análisis de Errores

Materia: [[Laboratorio de Física II]]
Anterior: —
Siguiente: [[Laboratorio de Física II - Electrostática y Líneas Equipotenciales]]

## Contexto y objetivo

Toda práctica experimental de [[Laboratorio de Física II]] requiere medir magnitudes eléctricas con precisión y cuantificar la incertidumbre de los resultados. Esta primera clase introduce el manejo seguro del **multímetro digital**, la **fuente de poder DC**, el **protoboard**, el **generador de funciones** y el **osciloscopio**, junto con el tratamiento estadístico de errores y la propagación de incertidumbres.

## 1. Instrumentos del puesto de laboratorio

| Instrumento | Magnitudes que mide / genera | Conexión correcta en el circuito |
|---|---|---|
| **Voltímetro** (multímetro en V) | Diferencia de potencial ($\text{V}$) | En **paralelo** con el elemento (alta impedancia). |
| **Amperímetro** (multímetro en A/mA) | Corriente eléctrica ($\text{I}$) | En **serie** abriendo la rama (baja impedancia). |
| **Óhmetro** (multímetro en $\Omega$) | Resistencia eléctrica ($\text{R}$) | Con el componente **desconectado y sin energía**. |
| **Fuente de poder DC** | Tensión continua regulable | Ajustar límite de corriente antes de energizar. |
| **Protoboard** | Montaje sin soldadura | Buses laterales horizontales; pistas internas verticales por columnas de 5 puntos. |
| **Osciloscopio** | Señales variables en el tiempo $V(t)$ | Permite medir amplitud pico, período $T$, frecuencia $f = 1/T$ y desfase. |

## 2. Cifras significativas, errores e incertidumbre

- **Error absoluto**: $\varepsilon_a = |x_{\text{medido}} - x_{\text{referencia}}|$.
- **Error relativo porcentual**:
  $$\varepsilon_r(\%) = \frac{|x_{\text{medido}} - x_{\text{referencia}}|}{|x_{\text{referencia}}|} \times 100\%$$
- **Media aritmética y desviación estándar muestral** (para $n$ mediciones repetidas $x_i$):
  $$\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i, \qquad s = \sqrt{\frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n - 1}}$$
- **Incertidumbre instrumental** ($\Delta x_{\text{inst}}$): en instrumentos analógicos suele tomarse como la mitad de la apreciación ($\frac{A}{2}$); en multímetros digitales depende de la resolución del último dígito y el porcentaje especificado por el fabricante.

## 3. Propagación de incertidumbres

Si una magnitud $z$ se calcula a partir de variables medidas $x \pm \Delta x$ e $y \pm \Delta y$:
- **Suma o resta** ($z = x \pm y$):
  $$\Delta z = \Delta x + \Delta y$$
- **Producto o cociente** ($z = x \cdot y$ o $z = x / y$):
  $$\frac{\Delta z}{|z|} = \frac{\Delta x}{|x|} + \frac{\Delta y}{|y|}$$
- **Potencia** ($z = x^n$):
  $$\frac{\Delta z}{|z|} = |n| \frac{\Delta x}{|x|}$$

**Ejemplo resuelto:** Se mide $V = (5{,}0 \pm 0{,}1)\,\text{V}$ e $I = (0{,}25 \pm 0{,}01)\,\text{A}$. Calcular $R = V/I$ con su incertidumbre:
- $R = 5{,}0 / 0{,}25 = 20{,}0\,\Omega$.
- $\frac{\Delta R}{R} = \frac{0{,}1}{5{,}0} + \frac{0{,}01}{0{,}25} = 0{,}02 + 0{,}04 = 0{,}06 \implies \Delta R = 0{,}06 \times 20{,}0 = 1{,}2\,\Omega$.
- Resultado reportado: $R = (20{,}0 \pm 1{,}2)\,\Omega$.

## Errores comunes

- Conectar el amperímetro en **paralelo** con la fuente: provoca un cortocircuito y quema el fusible del multímetro.
- Medir resistencia con el circuito encendido (daña el óhmetro y arroja lecturas falsas).
- Reportar un resultado con más cifras significativas de las que justifica la incertidumbre.

## Ejercicios propuestos

1. Una resistencia nominal de $100\,\Omega$ se mide en $97{,}5\,\Omega$. Calcula el error absoluto y el error relativo porcentual.
2. Si $P = V \cdot I$ con $V = (10{,}0 \pm 0{,}2)\,\text{V}$ e $I = (2{,}0 \pm 0{,}1)\,\text{A}$, calcula $P \pm \Delta P$.

**Respuestas:**
1. $\varepsilon_a = 2{,}5\,\Omega$; $\varepsilon_r = 2{,}5\%$.
2. $P = 20{,}0\,\text{W}$; $\Delta P/P = 0{,}02 + 0{,}05 = 0{,}07 \implies \Delta P = 1{,}4\,\text{W}$. Resultado: $(20{,}0 \pm 1{,}4)\,\text{W}$.

## Conexiones

- Retoma el análisis de errores de [[Laboratorio de Física I]] y [[Física I]].
- Sus destrezas con protoboard y multímetro se aplican en todas las prácticas siguientes y en [[Fundamentos de Lógica Digital]].

## Fuente

Elaborado siguiendo el programa referencial de [[Laboratorio de Física II]] (Práctica 1: Instrumentos de medición e incertidumbre).
