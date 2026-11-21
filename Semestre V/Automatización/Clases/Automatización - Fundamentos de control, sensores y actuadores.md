---
tags: [clase, semestre-V]
materia: Automatización
---
# Automatización - Fundamentos de control, sensores y actuadores

Materia: [[Automatización]]
Anterior: —
Siguiente: [[Automatización - PLC, ciclo de scan y lenguaje Ladder]]

## Contexto y objetivo

Esta primera clase introduce los principios básicos de la automatización industrial: qué distingue un sistema de **lazo abierto** de uno de **lazo cerrado**, cómo se clasifican las señales de campo (digitales y analógicas) y cuál es el papel de los **sensores** y **actuadores** como interfaz entre el controlador lógico y el proceso físico.

## 1. Sistemas de lazo abierto vs. lazo cerrado

Todo sistema automatizado busca mantener o llevar una variable física (nivel, temperatura, presión, caudal, posición) a un comportamiento deseado.

### Lazo abierto (*Open-loop*)
La acción de control es independiente de la salida real del proceso. No existe medición ni retroalimentación.

```
Consigna ──▶ [ Controlador ] ──▶ [ Actuador / Planta ] ──▶ Salida
```

- *Ejemplo:* un temporizador de riego que abre la válvula 15 minutos diarios sin medir si el suelo ya está húmedo o si está lloviendo.
- *Ventaja:* simplicidad y bajo costo.
- *Desventaja:* no corrige perturbaciones externas.

### Lazo cerrado (*Closed-loop*)
La salida se mide continuamente mediante un sensor y se compara con la consigna (*setpoint*, $r(t)$) para calcular el error $e(t) = r(t) - y(t)$ y corregir la acción del actuador.

```
Consigna r(t) ──▶ (+) ── e(t) ──▶ [ Controlador ] ──▶ [ Actuador / Planta ] ──▶ Salida y(t)
                   ▲ -                                                               │
                   └──────────────────────── [ Sensor ] ◀────────────────────────────┘
```

- *Ejemplo:* control de nivel en un tanque de bombeo (como en el sistema HIDRA): un sensor ultrasónico o de presión mide el nivel; si baja del umbral mínimo, el controlador enciende la bomba hasta alcanzar el nivel objetivo.

## 2. Señales digitales y analógicas

1. **Señales digitales (discretas / binarias):** adoptan solo dos estados lógicos: `0` (OFF / 0 V) o `1` (ON / típicamente 24 V DC en industria).
   - *Entradas digitales (DI):* pulsadores, interruptores de fin de carrera, sensores inductivos todo/nada, contactos de relé.
   - *Salidas digitales (DO):* luces piloto, bobinas de contactores, electroválvulas ON/OFF, alarmas sonoras.
2. **Señales analógicas (continuas):** varían dentro de un rango continuo para representar magnitudes físicas.
   - *Estándares industriales:* lazo de corriente $4\text{--}20\text{ mA}$ (muy inmune al ruido eléctrico y permite detectar cable roto si cae a $0\text{ mA}$) y tensión $0\text{--}10\text{ V}$.
   - *Conversión:* los módulos de entrada analógica (AI) usan conversores ADC (por ejemplo, de 12 o 16 bits) para transformar la corriente/tensión en un entero digital procesable por el controlador.

## 3. Sensores y actuadores comunes

- **Sensores (captadores de entrada):**
  - *Proximidad inductivos:* detectan metales sin contacto físico.
  - *Proximidad capacitivos:* detectan sólidos, líquidos o plásticos.
  - *Fotoeléctricos / ultrasónicos:* detección de presencia o distancia/nivel.
  - *Temperatura:* termopares (amplio rango) y RTD PT100 (alta precisión).
- **Actuadores (elementos finales de control):**
  - *Eléctricos:* motores AC/DC, contactores, variadores de frecuencia (VFD), servomotores.
  - *Neumáticos e hidráulicos:* cilindros, electroválvulas proporcionales o ON/OFF.

## Errores comunes

- **Usar señales de $0\text{--}10\text{ V}$ en tramos largos de cable:** la caída de tensión por resistencia del cable distorsiona la lectura; en distancias largas se prefiere $4\text{--}20\text{ mA}$.
- **Confundir sensor con transductor:** el sensor capta la magnitud física primaria; el transmisor/transductor la acondiciona a una señal estándar industrial ($4\text{--}20\text{ mA}$ o protocolo digital).

## Ejercicios propuestos

1. **¿Por qué el estándar $4\text{--}20\text{ mA}$ empieza en $4\text{ mA}$ y no en $0\text{ mA}$?**
   - *Respuesta:* Para distinguir el valor mínimo de medición ($4\text{ mA} = 0\%$) de una falla eléctrica o cable desconectado ($0\text{ mA}$), además de poder alimentar sensores a dos hilos.
2. **Clasifica como lazo abierto o cerrado:** (a) tostadora con perilla de tiempo; (b) aire acondicionado con termostato digital.
   - *Respuesta:* (a) Lazo abierto; (b) Lazo cerrado.

## Conexiones

- La retroalimentación y estabilidad de lazo cerrado retoman los conceptos de [[Teoría General de Sistemas]].
- La representación binaria de señales digitales se fundamenta en [[Fundamentos de Lógica Digital]].
- Siguiente: [[Automatización - PLC, ciclo de scan y lenguaje Ladder]].

## Fuente

- Basado en el programa de [[Automatización]] y la bibliografía recomendada (Bolton, Ogata).
