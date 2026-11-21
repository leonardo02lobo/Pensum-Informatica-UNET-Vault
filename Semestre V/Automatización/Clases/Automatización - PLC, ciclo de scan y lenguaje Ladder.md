---
tags: [clase, semestre-V]
materia: Automatización
---
# Automatización - PLC, ciclo de scan y lenguaje Ladder

Materia: [[Automatización]]
Anterior: [[Automatización - Fundamentos de control, sensores y actuadores]]
Siguiente: [[Automatización - Lógica secuencial con temporizadores y contadores]]

## Contexto y objetivo

El **Controlador Lógico Programable (PLC)** es el corazón del control industrial moderno. Esta clase explica su arquitectura interna, su mecanismo determinista de ejecución (**ciclo de scan**) y los elementos básicos del lenguaje gráfico **Ladder** (diagrama de contactos): contactos normalmente abiertos/cerrados, bobinas, marcas internas y enclavamiento *Set/Reset*.

## 1. Arquitectura de un PLC

Un PLC es una computadora industrial robusta diseñada para operar en ambientes con ruido eléctrico, vibración y temperatura variable. Sus bloques principales son:
- **Fuente de alimentación:** convierte tensión de red (110/220 V AC) a 24 V DC o 5 V DC internos.
- **CPU y memoria:** ejecuta el programa de usuario y almacena la tabla de imagen de entradas/salidas y variables internas.
- **Módulos de E/S (I/O):** interfaces aisladas ópticamente (optoacopladores) hacia sensores (`X` o `I`) y actuadores (`Y` o `Q`).
- **Interfaces de comunicación:** puertos Ethernet, RS-485, USB para programación, HMI y redes industriales.

## 2. El ciclo de scan determinista

A diferencia de un programa de propósito general orientado a eventos impredecibles, un PLC ejecuta un bucle infinito y determinista llamado **ciclo de scan** (típicamente de 1 a 20 ms):

```
┌──────────────────────────────────────────────────────────┐
│  1. Leer entradas físicas ──▶ Tabla de imagen de entradas │
│                          │                               │
│  2. Ejecutar programa de usuario (Rung 1, Rung 2, ...)   │
│                          │                               │
│  3. Tareas de diagnóstico y comunicación                 │
│                          │                               │
│  4. Escribir tabla de imagen de salidas ──▶ Salidas físicas │
└──────────────────────────────────────────────────────────┘
```

> **Consecuencia clave:** durante la ejecución de los *rungs* en el paso 2, el PLC trabaja contra la *tabla de imagen* en memoria, no directamente contra los bornes físicos. Si una entrada cambia a mitad de ciclo, su nuevo estado se verá en el **siguiente** scan.

## 3. Lenguaje Ladder (Diagrama de Escalera, IEC 61131-3)

El lenguaje Ladder imita los antiguos esquemas eléctricos de relés. Consta de dos rieles verticales (alimentación lógica izquierda y retorno derecho) y líneas horizontales llamadas **rungs** (peldaños), que se evalúan de izquierda a derecha y de arriba hacia abajo.

### Elementos fundamentales
- **Contacto Normalmente Abierto (NA / `| |`):** deja pasar continuidad lógica cuando el bit asociado vale `1`.
- **Contacto Normalmente Cerrado (NC / `|/|`)**: deja pasar continuidad lógica cuando el bit asociado vale `0`.
- **Bobina simple (`( )`):** asigna `1` al bit si el rung es verdadero y `0` si es falso.
- **Bobina Set (`(S)`) y Reset (`(R)`):** `SET` enclava un bit en `1` de forma permanente hasta que una instrucción `RESET` lo devuelva a `0`.
- **Marcas internas (`M`):** bits auxiliares en memoria (no tienen salida física asociada) útiles para guardar estados o banderas.

### Ejemplo: Arranque y parada con enclavamiento (memoria)
```
RUNG 1 (Marcha/Paro con autorretención):
|---[ X0 (Start) ]---+---[/ X1 (Stop_NC) ]---( Y0 (Motor) )---|
|                    |                                        |
|---[ Y0 (Motor) ]---+                                        |
```
Al pulsar `X0`, se energiza `Y0`; el contacto paralelo de `Y0` mantiene la corriente lógica aunque se suelte `X0`, hasta que se active `X1` (parada).

## Errores comunes

- **Doble bobina sobre la misma salida (`Y0`):** si dos *rungs* distintos usan bobinas simples `( )` sobre `Y0`, prevalecerá el último *rung* evaluado antes de actualizar las salidas físicas, anulando al primero. Para controlar una salida desde múltiples condiciones se usan ramas en paralelo o bobinas `SET`/`RESET`.
- **Confundir contacto físico NC con instrucción NC en Ladder:** si un botón de parada de emergencia está cableado físicamente como NC (cerrado en reposo, envía `1` al PLC), en el programa Ladder se debe usar un contacto **NA (`| |`)** para permitir el paso mientras no se presione.

## Ejercicios propuestos

1. **¿Qué ocurre si un programa Ladder entra en un bucle infinito dentro de un rung?**
   - *Respuesta:* El tiempo de scan excede el límite del *Watchdog Timer* del PLC, provocando una falla crítica (*CPU Fault*) y pasando las salidas a estado seguro (apagadas).
2. **Escribe la expresión booleana equivalente** al *rung* de marcha/paro anterior.
   - *Respuesta:* $Y_0 = (X_0 + Y_0) \cdot \overline{X_1}$.

## Conexiones

- La lógica de contactos es aplicación directa del álgebra booleana de [[Fundamentos de Lógica Digital]].
- El ciclo de scan y el *watchdog* se relacionan con sistemas de tiempo real en [[Sistemas Operativos]] y [[Organización del Computador]].
- Anterior: [[Automatización - Fundamentos de control, sensores y actuadores]].
- Siguiente: [[Automatización - Lógica secuencial con temporizadores y contadores]].

## Fuente

- Basado en el programa de [[Automatización]] y [[Practica 1]].
