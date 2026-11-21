---
tags: [clase, semestre-V]
materia: Automatización
---
# Automatización - Lógica secuencial con temporizadores y contadores

Materia: [[Automatización]]
Anterior: [[Automatización - PLC, ciclo de scan y lenguaje Ladder]]
Siguiente: [[Automatización - Protocolos industriales e IoT: Modbus, OPC-UA, MQTT y HTTP]]

## Contexto y objetivo

La mayoría de los procesos industriales no dependen solo de combinaciones instantáneas de entradas, sino de **secuencias en el tiempo** y **conteo de eventos**. Esta clase explica el funcionamiento de los **temporizadores** (`TON`, `TOF`) y **contadores** (`CTU`, `CTD`) en PLC, y desarrolla paso a paso la lógica de la **Práctica 1** de [[Automatización]].

## 1. Temporizadores en PLC

Un temporizador mide intervalos de tiempo respecto a un valor preestablecido (**Preset**, `PT`).

- **TON (*Timer On-Delay*, retardo a la conexión):**
  - Cuando la entrada `IN` pasa a `1`, el temporizador comienza a contar el tiempo transcurrido `ET`.
  - Cuando `ET >= PT`, su salida `Q` pasa a `1`.
  - Si `IN` vuelve a `0` en cualquier momento, `ET` se reinicia a `0` y `Q` pasa a `0`.
- **TOF (*Timer Off-Delay*, retardo a la desconexión):**
  - Cuando `IN` pasa a `1`, la salida `Q` se activa inmediatamente.
  - Cuando `IN` vuelve a `0`, `Q` permanece activa durante el tiempo `PT` y luego se apaga.

## 2. Contadores en PLC

- **CTU (*Count Up*, contador ascendente):** incrementa su valor acumulado (`CV`) en cada **flanco ascendente** (`0 -> 1`) de la entrada de conteo `CU`. Cuando `CV >= PV` (*Preset Value*), activa su salida `Q`. Se reinicia con la entrada `R` (*Reset*).
- **CTD (*Count Down*, contador descendente):** decrementa `CV` desde `PV` hasta `0` en cada flanco ascendente de `CD`.

> **Importante:** los contadores responden a *flancos*, no a niveles continuos, por lo que mantener un pulsador presionado solo cuenta **una vez** hasta que se suelta y se vuelve a presionar.

## 3. Caso práctico desarrollado: Práctica 1

**Enunciado:**
Se dispone de un pulsador de entrada `X0`, un pulsador de parada `STOP`, una luz piloto `Y0` y un ventilador `Y1`.
- Al **primer pulso** en `X0`, se enciende la luz `Y0`.
- Al **segundo pulso**, el sistema ignora el cambio (la luz sigue encendida, el ventilador apagado).
- Al **tercer pulso**, tras un retardo de **10 segundos**, arranca el ventilador `Y1`.
- Al presionar `STOP`, se inicia un retardo de **10 segundos** tras el cual se apagan `Y0`, `Y1` y se reinicia el contador `C1`.

### Estructura de la lógica Ladder (en pseudocódigo de rungs)

```text
RUNG 1: Conteo de pulsos de entrada
  X0 (flanco ascendente) ──▶ [ CTU C1, PV = 3 ]

RUNG 2: Primer pulso -> Encender luz Y0 mediante marca M1
  [ C1.CV == 1 ] ──▶ (SET M1)
  [ M1 ]         ──▶ ( Y0 )

RUNG 3: Tercer pulso -> Retardo de 10 s para arrancar ventilador Y1
  [ C1.CV >= 3 ] ──▶ [ TON T1, PT = 10s ]
  [ T1.Q ]       ──▶ (SET Y1)

RUNG 4: Secuencia de parada con retardo de 10 s
  [ STOP ]       ──▶ (SET M_STOP)
  [ M_STOP ]     ──▶ [ TON T2, PT = 10s ]
  [ T2.Q ]       ──▶ (RESET M1)
                 ──▶ (RESET Y1)
                 ──▶ (RESET C1)
                 ──▶ (RESET M_STOP)
```

### Variante con luz intermitente
Si se requiere que `Y0` parpadee (por ejemplo, 1 s ON / 1 s OFF) durante el retardo de parada `M_STOP`, se encadenan dos temporizadores `TON` en oscilador astable (donde la salida negada de `T_OFF` habilita a `T_ON` y `T_ON.Q` habilita a `T_OFF`) y se condiciona `Y0` con la señal pulsante mientras `M_STOP` esté activo.

## Errores comunes

- **No usar flanco o enclavamiento en la señal de `STOP`:** si `STOP` es un pulsador momentáneo y alimenta directamente al `TON T2`, al soltar el botón el temporizador se reinicia antes de cumplir los 10 segundos. Por eso se enclava con `M_STOP`.
- **Olvidar reiniciar el contador `C1`:** si al finalizar la parada no se aplica `RESET C1`, en el siguiente ciclo `C1.CV` seguirá valiendo `3` y el ventilador arrancará inmediatamente.

## Ejercicios propuestos

1. **¿Qué sucede en la Práctica 1 si el usuario presiona `X0` una cuarta vez antes de presionar `STOP`?**
   - *Respuesta:* Si no se bloquea el conteo de `C1` cuando `C1.CV >= 3`, `CV` pasará a 4, pero como la condición del Rung 3 es `>= 3`, `Y1` seguirá encendido. Es buena práctica poner `[/ T1.Q]` en serie con `X0` para evitar conteos innecesarios.
2. **Dibuja la lógica de un oscilador de 1 Hz (0.5 s ON, 0.5 s OFF)** usando dos temporizadores `TON`.
   - *Respuesta:* `[/ T2.Q] -> TON T1 (0.5s)` y `[T1.Q] -> TON T2 (0.5s)`; la salida intermitente es `[T1.Q]`.

## Conexiones

- Implementa directamente los requerimientos de [[Practica 1]].
- Se apoya en máquinas de estado finitas vistas en [[Fundamentos de Lógica Digital]].
- Anterior: [[Automatización - PLC, ciclo de scan y lenguaje Ladder]].
- Siguiente: [[Automatización - Protocolos industriales e IoT: Modbus, OPC-UA, MQTT y HTTP]].

## Fuente

- Basado en [[Automatización]] y [[Practica 1]].
