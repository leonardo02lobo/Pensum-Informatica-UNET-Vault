---
tags: [clase, semestre-VI]
materia: Comunicaciones I
fuente: conocimiento general
---
# Comunicaciones I - 01 Modelo de comunicación y redes

Materia: [[Comunicaciones I]]
Siguiente: [[Comunicaciones I - 02 Señales y análisis de Fourier]]

## Contexto y objetivo
Se parte del modelo básico de un sistema de comunicaciones y de la terminología de redes. Es la puerta de entrada tras [[Organización del Computador]] y la base de [[Comunicaciones II]]. Programa oficial: verificar con el programa sinóptico UNET.

## Modelo de comunicación (Shannon)
Fuente -> transmisor (codificador/modulador) -> **canal** (+ ruido) -> receptor (demodulador/decodificador) -> destino.
- **Información**: lo que se transmite; **señal**: su representación física; **ruido**: perturbaciones aleatorias.
- El objetivo es la reproducción fiel en el destino con el menor costo de recursos (potencia, ancho de banda, tiempo).

## Tipos de transmisión
- **Analógica** (variación continua) vs **digital** (valores discretos). Datos analógicos o digitales pueden transportarse con señales analógicas o digitales (4 combinaciones): digital->digital (codificación de línea), digital->analógico (modulación), analógico->digital (PCM), analógico->analógico (AM/FM).
- **Modos de operación**: simplex (un sentido: TV), half duplex (alterna: radio walkie-talkie), full duplex (simultáneo: teléfono).
- **Serie vs paralelo**; **síncrona vs asíncrona** (bits de inicio/parada, p. ej. UART 8N1: 10 bits por byte, eficiencia 80 %).

## Parámetros fundamentales
- **Tasa de bits** R (bps), **tasa de símbolos** o baudios D = R / log2(M).
- **Ancho de banda** B (Hz). **Retardo** de propagación $t_p = d / v$ (v ≈ 2·10^8 m/s en cobre/fibra); de transmisión $t_t = L / R$.
- **Rendimiento (throughput)** frente a **capacidad**.
- **Atenuación**, **distorsión**, **ruido** (térmico $N = kTB$, impulsivo, diafonía).

### Ejemplo
Enviar 1 MB (8·10^6 bits) por un enlace de 10 Mbps y 2000 km: $t_t = 0.8$ s, $t_p = 2\times10^6 / 2\times10^8 = 10$ ms. Tiempo total ≈ 0.81 s. Si el enlace fuese de 1 Gbps: $t_t$ = 8 ms; domina ya la propagación.

## Redes: clasificación
- Por alcance: PAN, **LAN**, MAN, **WAN**, Internet.
- Por topología física: bus, anillo, estrella, árbol, malla.
- Por técnica de conmutación:
  - **Conmutación de circuitos** (circuito dedicado; telefonía): retardo constante, recursos reservados.
  - **Conmutación de paquetes** (Internet): multiplexación estadística; retardos variables y posibilidad de pérdida.
  - Datagramas frente a circuitos virtuales.
- **Retardo en conmutación de paquetes**: nodal = procesamiento + cola + transmisión + propagación.

### Ejemplo de conmutación
Mensaje de 7.5 Mbit por 3 enlaces de 1.5 Mbps. Sin segmentar (store-and-forward): 3·(7.5/1.5) = 15 s. Con paquetes de 1.5 Mbit (5 paquetes) en pipeline: (3 + 5 - 1)·1 s = 7 s. Segmentar reduce el retardo total.

## Estándares y organismos
ITU-T, IEEE (802.x), ISO, IETF (RFC), ANSI/TIA/EIA.

## Errores comunes
- Confundir bps con baudios.
- Mezclar retardo de transmisión (depende del tamaño y tasa) con el de propagación (depende de la distancia).
- Decir que la conmutación de paquetes siempre es mejor: para tráfico constante y sensible al retardo, los circuitos son ventajosos.

## Ejercicios propuestos
1. Un canal con 16 niveles transmite 2400 baudios. ¿Tasa? *Resp.: 2400·4 = 9600 bps.*
2. Tiempo de propagación en 3000 km de fibra. *Resp.: 15 ms.*
3. UART 8N1 a 115200 baudios: bytes/s. *Resp.: 11 520.*

## Conexiones
[[Comunicaciones I - 02 Señales y análisis de Fourier]]; capas: [[Comunicaciones I - 11 Modelos de capas y redes LAN]]; [[Introducción a las Telecomunicaciones]].

## Fuente
Conocimiento general (Stallings; Forouzan; Tanenbaum).
