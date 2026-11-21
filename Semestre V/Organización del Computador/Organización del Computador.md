---
tags: [materia, semestre-V]
semestre: V
---
# Organización del Computador

**Semestre:** [[Semestre V]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Programación II]]
- [[Fundamentos de Lógica Digital]]

## Desbloquea
- [[Sistemas Operativos]]
- [[Comunicaciones I]]

## Apuntes

### Descripción general y objetivos
Organización del Computador explica cómo está construido un computador desde el nivel de lenguaje de máquina hasta la microarquitectura: representación de datos, conjunto de instrucciones, CPU (ruta de datos y unidad de control), memoria, entrada/salida y buses. Objetivo: entender qué ocurre cuando un programa de alto nivel se ejecuta, programar en ensamblador y razonar sobre rendimiento. No hay Material del estudiante en esta carpeta; el contenido se basa en el programa típico de la materia (verificar con el programa oficial).

### Contenido programático
1. **Introducción**: modelo de von Neumann, niveles de abstracción, historia y generaciones, medidas de rendimiento.
2. **Representación de la información**: sistemas de numeración (binario, octal, hexadecimal), complemento a 2, punto flotante IEEE 754, códigos (ASCII, Unicode).
3. **Aritmética del computador**: suma/resta con acarreo y desbordamiento, multiplicación (Booth) y división, ALU.
4. **Arquitectura del conjunto de instrucciones (ISA)**: formatos, modos de direccionamiento, tipos de instrucción, CISC vs RISC; programación en ensamblador (por ejemplo x86 o MIPS).
5. **La CPU**: registros, ciclo de instrucción (captar-decodificar-ejecutar), ruta de datos, unidad de control cableada y microprogramada, segmentación (pipeline) y riesgos.
6. **Memoria**: jerarquía, memoria caché (correspondencia directa, asociativa, por conjuntos), memoria virtual y paginación.
7. **Entrada/salida**: E/S programada, por interrupciones y DMA; buses y periféricos.

### Conceptos clave
- **Complemento a 2**: `-x = ~x + 1`; rango de n bits: `-2^(n-1)` a `2^(n-1)-1`.
- **CPI** (ciclos por instrucción) y **tiempo de CPU** = IC × CPI × T_ciclo.
- **Pipeline**: solapamiento de etapas; riesgos estructurales, de datos y de control.
- **Localidad temporal y espacial** justifican la caché.
- **Interrupción**: señal que desvía la ejecución a una rutina de servicio.

### Fórmulas y código
```
Tiempo de CPU = IC * CPI / f
Speedup (Amdahl) = 1 / ((1-f) + f/s)
Tiempo medio de acceso = tasa_acierto*t_cache + (1-tasa_acierto)*t_memoria
IEEE 754 simple: (-1)^s * 1.m * 2^(e-127)
```
Ejemplo en ensamblador MIPS (suma de un arreglo):
```asm
      li   $t0, 0          # i = 0
      li   $t1, 0          # suma = 0
loop: lw   $t2, 0($a0)
      add  $t1, $t1, $t2
      addi $a0, $a0, 4
      addi $t0, $t0, 1
      blt  $t0, $a1, loop
```

### Ejemplos resueltos
- 5 en 8 bits: 00000101; -5 = 11111010 + 1 = 11111011.
- Caché con acierto 95%, t_cache=1 ns, t_mem=100 ns: `0.95·1 + 0.05·100 = 5.95 ns`.

### Relación con otras materias
Se apoya en [[Fundamentos de Lógica Digital]] (compuertas, registros, ALU) y [[Programación II]]. Desbloquea [[Sistemas Operativos]] y [[Comunicaciones I]]; también sirve a [[Compiladores e Intérpretes]], [[Sistemas Distribuidos]] y [[Automatización]].

### Evaluación y consejos
- Parciales teórico-prácticos con conversiones numéricas, ensamblador y cálculos de rendimiento.
- Traza a mano el ciclo de instrucción y dibuja la ruta de datos.
- Practica con un simulador (MARS/SPIM o emu8086).

### Bibliografía recomendada
- Stallings, W. *Organización y Arquitectura de Computadores*. Pearson.
- Patterson y Hennessy. *Estructura y Diseño de Computadores*. Reverté.
- Tanenbaum, A. *Organización de Computadoras: un enfoque estructurado*.

### Recursos del Material/
No hay carpeta `Material/` en esta materia.
