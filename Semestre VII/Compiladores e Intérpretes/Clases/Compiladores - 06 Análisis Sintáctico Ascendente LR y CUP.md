---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: conocimiento general + ~/Documentos/UNET/Compiladores/Compilador/src/main/cup/sintactico.cup
---
# Compiladores - 06 Análisis Sintáctico Ascendente LR y CUP

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 05 Análisis Sintáctico Descendente LL(1)]]
Siguiente: [[Compiladores - 07 Traducción Dirigida por la Sintaxis y AST]]

## Contexto y objetivo
El análisis **ascendente** parte de los tokens y *reduce* hasta llegar al símbolo inicial, reconstruyendo una derivación **más a la derecha en orden inverso**. La familia **LR($k$)** es más potente que LL($k$) y es la que usan Yacc, Bison y **CUP** (el generador del proyecto Tiny++). Se explican autómatas LR(0), SLR, LALR, conflictos y el uso de CUP.

## Teoría
### Desplazar-reducir (shift-reduce)
Una **pila** de estados/símbolos y la entrada. Acciones: **desplazar** (shift: mover el token a la pila), **reducir** (reduce $A \to \beta$: sacar $|\beta|$ símbolos y apilar $A$), **aceptar**, **error**. El **mango (handle)** es la subcadena en el tope que corresponde al lado derecho de una producción cuya reducción es un paso de la derivación inversa.

### Elementos LR(0) y autómata
Un **ítem** $A \to \alpha \cdot \beta$ indica cuánto del lado derecho se ha visto. Se aumenta la gramática con $S' \to S$. Operaciones: **cerradura** (si $A \to \alpha \cdot B \beta$, añadir $B \to \cdot \gamma$) e **ir_a(I, X)** (avanzar el punto sobre $X$). Los conjuntos de ítems son los estados del autómata.

### Tablas ACTION y GOTO
- **LR(0)**: reducir en toda la fila si hay ítem completo (genera muchos conflictos).
- **SLR(1)**: reducir $A \to \beta$ solo para $a \in FOLLOW(A)$.
- **LR(1)**: ítems $[A \to \alpha \cdot \beta, a]$ con símbolo de adelanto exacto; tablas enormes.
- **LALR(1)**: fusiona estados LR(1) con el mismo núcleo; tamaño de SLR, casi la potencia de LR(1). Es lo que generan Yacc/Bison/CUP.

### Conflictos
- **shift/reduce**: no se sabe si desplazar o reducir (típico de ambigüedad como *else* colgante o operadores sin precedencia). Los generadores resuelven por defecto en favor de *shift*; se corrige con declaraciones de precedencia/asociatividad o reescribiendo.
- **reduce/reduce**: dos reducciones posibles; suele indicar una gramática mal diseñada.

## Ejemplo resuelto: tabla SLR paso a paso
Gramática: (1) $E \to E + T$, (2) $E \to T$, (3) $T \to id$; aumentada $S' \to E$.
Estados:
- $I_0$: $S' \to \cdot E$, $E \to \cdot E+T$, $E \to \cdot T$, $T \to \cdot id$
- $I_1 = ir\_a(I_0,E)$: $S' \to E \cdot$, $E \to E \cdot +T$
- $I_2 = ir\_a(I_0,T)$: $E \to T \cdot$
- $I_3 = ir\_a(I_0,id)$: $T \to id \cdot$
- $I_4 = ir\_a(I_1,+)$: $E \to E+\cdot T$, $T \to \cdot id$
- $I_5 = ir\_a(I_4,T)$: $E \to E+T \cdot$ (y $ir\_a(I_4,id)=I_3$)

$FOLLOW(E)=FOLLOW(T)=\{+,\$\}$.

| Estado | id | + | $ | E | T |
|---|---|---|---|---|---|
| 0 | s3 | | | 1 | 2 |
| 1 | | s4 | acc | | |
| 2 | | r2 | r2 | | |
| 3 | | r3 | r3 | | |
| 4 | s3 | | | | 5 |
| 5 | | r1 | r1 | | |

Traza de `id + id $`:
| Pila | Entrada | Acción |
|---|---|---|
| 0 | id + id $ | s3 |
| 0 id 3 | + id $ | r3 (T → id), ir_a(0,T)=2 |
| 0 T 2 | + id $ | r2 (E → T), ir_a(0,E)=1 |
| 0 E 1 | + id $ | s4 |
| 0 E 1 + 4 | id $ | s3 |
| 0 E 1 + 4 id 3 | $ | r3, ir_a(4,T)=5 |
| 0 E 1 + 4 T 5 | $ | r1 (E → E+T; se sacan 3), ir_a(0,E)=1 |
| 0 E 1 | $ | aceptar |

## CUP en el proyecto Tiny++
Un `.cup` tiene: bloque `parser code {: ... :}` (métodos del parser, aquí `syntax_error` que guarda diagnósticos), `action code {: ... :}` (variables y auxiliares para las acciones, aquí `enlazar`, `enLinea`), declaración de `terminal` y `non terminal` con tipo de valor, y reglas con acciones entre `{: ... :}`:
```
func_decl ::= FUNCTION:fu ID:nombre LPAREN params:ps RPAREN COLON tipo:t stmt_seq:cuerpo END
   {: RESULT = enLinea(new NodoFuncion(nombre.toString(), (java.util.List<NodoParametro>) ps, t, cuerpo), fuleft); :}
   ;
```
`RESULT` es el valor sintetizado del no terminal; `etiqueta:nombre` da acceso al valor del símbolo y `nombreleft`/`nombreright` a su posición (línea y columna que el lexer almacenó). Las secuencias de sentencias se enlazan como lista de hermanos (`enlazar`), y las listas de parámetros/argumentos usan `java.util.List`.
Generación: `make generate` ejecuta JFlex y CUP y produce `Lexico.java`, `parser.java`, `sym.java` en `build/gen/`.

**Recuperación de errores**: `syntax_error` no imprime, sino que añade un diagnóstico `Sintáctico` (con "símbolo inesperado 'x'" o "fin de archivo inesperado") y suprime errores derivados de un error léxico en la misma línea. `unrecovered_syntax_error` termina el análisis.

## Comparación LL vs LR
| | LL(1) | LALR(1) |
|---|---|---|
| Dirección | descendente | ascendente |
| Recursión izquierda | prohibida | permitida (y preferida) |
| Potencia | menor | mayor |
| Facilidad manual | alta (descenso recursivo) | solo con generador |
| Herramientas | ANTLR (LL(*)) | Yacc, Bison, CUP |

## Errores comunes
- Intentar escribir a mano tablas LR grandes: usar generador.
- Ignorar los conflictos reportados por CUP (el warning indica ambigüedad).
- Confundir `ir_a` (GOTO) con ACTION.
- Declarar tipos de terminales incorrectos y obtener `ClassCastException` en las acciones.

## Ejercicios propuestos
1. Reduzca por el método ascendente `id + id` en la gramática del ejemplo y numere las reducciones. *Resp.: T→id, E→T, T→id, E→E+T (reglas 3, 2, 3, 1).*
2. ¿Qué conflicto produce $E \to E+E \mid id$ con `id + id + id`? *Resp.: shift/reduce, se resuelve con asociatividad izquierda.*
3. ¿Por qué `RESULT` puede asignarse en una acción de CUP? *Resp.: es el atributo sintetizado del lado izquierdo.*

## Conexiones
El semántico se apoya en el AST construido aquí ([[Compiladores - 07 Traducción Dirigida por la Sintaxis y AST]], [[Compiladores - 08 Análisis Semántico y Tabla de Símbolos]]). El lexer que entrega tokens: [[Compiladores - 03 JFlex y el Analizador Léxico de Tiny++]].

## Fuente
`~/Documentos/UNET/Compiladores/Compilador/src/main/cup/sintactico.cup` y conocimiento general.
