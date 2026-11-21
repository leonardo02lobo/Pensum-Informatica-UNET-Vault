---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: conocimiento general + Compilador/UtGen.java + Proyecto/TM.C (simulador, no leído completo)
---
# Compiladores - 09 Código Intermedio y la Tiny Machine

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 08 Análisis Semántico y Tabla de Símbolos]]
Siguiente: [[Compiladores - 10 Generación de Código Tiny++ y Marcos de Activación]]

## Contexto y objetivo
Antes de emitir código de máquina, los compiladores suelen usar una **representación intermedia (IR)**. Tiny++ usa directamente el AST y genera código para la **Tiny Machine (TM)**, una máquina de registros didáctica de Kenneth Louden. Esta nota explica la IR (con foco en el **código de tres direcciones**) y el juego de instrucciones de la TM, imprescindible para leer cualquier archivo `.tm`.

## Representaciones intermedias
- **AST**: estructura jerárquica; permite recorridos para análisis y generación.
- **Código de tres direcciones (TAC)**: cada instrucción tiene a lo sumo un operador y tres direcciones: `x = y op z`. Se usan temporales `t1, t2...`.
- **Cuádruplas** `(op, arg1, arg2, resultado)`, **triplas** (referencias por posición), **notación postfija**, **código de máquina de pila**.
- Ventajas: independencia de la máquina, base de optimizaciones, retargeting.

### Ejemplos de TAC
`a := b * c + d` →
```
t1 = b * c
t2 = t1 + d
a  = t2
```
`if x < 10 then y := 1 else y := 2 end` →
```
      t1 = x < 10
      if_false t1 goto L1
      y = 1
      goto L2
L1:   y = 2
L2:
```
`repeat s until c` →
```
L1:   s
      t = c
      if_false t goto L1
```
Arreglos: `x := A[i]` →  `t1 = i * 1; t2 = base_A + t1; x = *t2` (con elementos de 1 celda como en la TM).

## La Tiny Machine (TM)
Arquitectura (Louden): memoria de instrucciones `iMem` y de datos `dMem` separadas, **8 registros** `reg[0..7]`; el registro 7 es el **PC**. La instrucción se ejecuta en un ciclo búsqueda-ejecución; `HALT` detiene.

### Formatos de instrucción
- **RO (registro solamente)**: `opcode r,s,t`.
  - `HALT` detiene; `IN r` lee un entero a `reg[r]`; `OUT r` imprime `reg[r]`; `ADD r,s,t`: $reg[r] = reg[s] + reg[t]$; `SUB`, `MUL`, `DIV` análogas (división entera).
- **RM (registro-memoria)**: `opcode r,d(s)` con dirección efectiva $a = d + reg[s]$.
  - `LD r,d(s)`: $reg[r] = dMem[a]$; `ST r,d(s)`: $dMem[a] = reg[r]$.
  - `LDA r,d(s)`: $reg[r] = a$ (carga la dirección, sirve para sumar constantes y como "mover").
  - `LDC r,d`: $reg[r] = d$ (constante).
  - Saltos condicionales `JLT, JLE, JGT, JGE, JEQ, JNE r,d(s)`: si $reg[r]$ cumple la condición contra 0, entonces $PC = a$.
  - Salto incondicional: `LDA 7,d(s)` o `LDC 7,d` (se escribe en el PC).

### Convención de registros en el compilador Tiny++
| Reg | Nombre | Uso |
|---|---|---|
| 0 | AC | acumulador de expresiones |
| 1 | AC1 | segundo operando |
| 2, 3 | auxiliares | dirección de elemento de arreglo; contador de bucles |
| 4 | FP | puntero de marco (frame pointer) |
| 5 | GP | base de globales (siempre 0) |
| 6 | MP | tope de pila (siguiente celda libre; la pila crece hacia abajo) |
| 7 | PC | contador de programa |
(En la TM original de Louden 5 = GP y 6 = MP; el proyecto agrega FP en 4.)

La TM no tiene comparaciones directas: se resta y se salta según el signo. No tiene `CALL`/`RET` ni pila: el compilador las construye con `LD`, `ST`, `LDA`, `LDC`.

### Ejemplos de código
Comparación `x < y` (resultado 1/0 en AC):
```
LD  0,dx(5)      * AC = x
LD  1,dy(5)      * AC1 = y
SUB 0,0,1        * AC = x - y
JLT 0,2(7)       * si AC<0 salta 2 (PC relativo con reg 7)
LDC 0,0(0)       * falso
LDA 7,1(7)       * salta el LDC siguiente
LDC 0,1(0)       * verdadero
```
`write 5`: `LDC 0,5(0)` y `OUT 0,0,0`. `read x`: `IN 0,0,0` y `ST 0,dx(5)`.

## Ejemplo resuelto: traducir `x := (a + b) * 2`
Con un esquema de pila de temporales (`push`: `ST r,0(6)` y `LDA 6,-1(6)`; `pop`: `LDA 6,1(6)` y `LD r,0(6)`):
```
LD  0,da(5)      * AC = a
ST  0,0(6)       * apilar
LDA 6,-1(6)
LD  0,db(5)      * AC = b
LDA 6,1(6)       * desapilar a AC1
LD  1,0(6)
ADD 0,1,0        * AC = a + b
ST  0,0(6)       * apilar
LDA 6,-1(6)
LDC 0,2(0)       * AC = 2
LDA 6,1(6)
LD  1,0(6)
MUL 0,1,0        * AC = (a+b)*2
ST  0,dx(5)      * x = AC
```
Es el patrón general del generador por recorrido: evaluar el operando izquierdo, apilarlo, evaluar el derecho, desapilar, operar.

## Backpatching (parcheo)
Para saltos hacia adelante (`if`, `repeat`, return) se **reserva** el hueco con `emitirSalto(1)`, se genera el cuerpo y luego se vuelve con `cargarRespaldo(hueco)` para escribir la dirección correcta y `restaurarRespaldo()` para continuar. `UtGen` guarda las instrucciones en un `TreeMap` por dirección precisamente para permitir el parcheo y entregar el programa ordenado con `volcar()`.

## Errores comunes
- Olvidar que `JEQ`/`JLT` comparan el registro contra 0, no dos registros.
- Saltar con `LDA 7,d(7)` esperando dirección absoluta (es relativo al PC ya incrementado).
- Desbalancear push/pop: la pila crece o se corrompe.
- Confundir `LDA` (carga una dirección) con `LD` (carga el contenido).

## Ejercicios propuestos
1. ¿Qué hace `LDA 0,5(0)` cuando `reg[0]=10`? *Resp.: $reg[0] = 5 + 10 = 15$.*
2. Escriba TM para `if x = 0 then write 1 end`. *Resp.: LD 0,dx(5); JNE 0,2(7); LDC 0,1(0); OUT 0,0,0.*
3. Dé el TAC de `x := a - b / c`. *Resp.: t1 = b / c; t2 = a - t1; x = t2.*

## Conexiones
La generación de código completa: [[Compiladores - 10 Generación de Código Tiny++ y Marcos de Activación]]. Arquitectura y ensamblador: [[Organización del Computador]]. El simulador depurable: [[Compiladores - 12 Proyecto Tiny++ Arquitectura, Contrato con el IDE y Defensa]].

## Fuente
`~/Documentos/UNET/Compiladores/Compilador/src/main/java/ve/edu/unet/UtGen.java` (comentarios sobre RO/RM/registros) y `Compilador/README.md`; el simulador `Proyecto/TM.C` y `tmsimv1.html` no se leyeron en detalle (la semántica de instrucciones sigue la TM estándar de Louden).
