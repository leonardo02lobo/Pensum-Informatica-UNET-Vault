---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: conocimiento general + ~/Documentos/UNET/Compiladores/Parcial 1/31489733.txt (pregunta 7) + nodosAST del Compilador
---
# Compiladores - 07 Traducción Dirigida por la Sintaxis y AST

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 06 Análisis Sintáctico Ascendente LR y CUP]]
Siguiente: [[Compiladores - 08 Análisis Semántico y Tabla de Símbolos]]

## Contexto y objetivo
La **traducción dirigida por la sintaxis (TDS)** asocia significado a la estructura sintáctica: se aprovecha el análisis del parser para calcular valores, tipos o código. El parcial pregunta explícitamente cómo aplicarla; aquí se desarrolla esa respuesta y se muestra cómo Tiny++ construye su **árbol de sintaxis abstracta (AST)**.

## Teoría
### Gramática con atributos
A cada símbolo $X$ se le asocian **atributos** $X.a$ (valor, tipo, código...). Cada producción lleva **reglas semánticas** que los calculan.
- **Sintetizado**: el atributo de un nodo se calcula a partir de sus hijos (flujo hacia arriba). Ejemplo: $E.val = E_1.val + T.val$.
- **Heredado**: el atributo viene del padre o de los hermanos (flujo hacia abajo o lateral). Ejemplo: en `int a, b, c` el tipo de la declaración se hereda a la lista de identificadores.
- Gramática **S-atribuida**: solo sintetizados; se evalúa durante un análisis ascendente en una sola pasada. **L-atribuida**: heredados que solo dependen de padre y hermanos a la izquierda; se evalúa en un recorrido de izquierda a derecha.

### Procedimiento (respuesta del parcial)
1. Definir la GLC (BNF).
2. Convertirla en gramática con atributos.
3. Asociar acciones semánticas a cada regla.
4. Usar un parser que ejecute la acción al reconocer (reducir) la regla.
Ejemplo: `E ::= E:e1 MAS T:t {: RESULT = e1 + t; :}` en CUP (aquí `e1` y `t` son valores ya calculados).

### Esquema de traducción
Las acciones se intercalan en las producciones: `E -> E1 + T { print('+') }` produce notación postfija si la acción va al final.

## AST: árbol de sintaxis abstracta
El árbol de análisis contiene detalle superfluo (paréntesis, símbolos auxiliares). El **AST** conserva solo la estructura esencial. Ejemplo de `2 * (3 + 4)`:
```
   *
  / \
 2   +
    / \
   3   4
```
En Tiny++ el AST se arma con clases del paquete `ve.edu.unet.nodosAST`: `NodoBase` (con hermano derecho y línea), `NodoIf`, `NodoRepeat`, `NodoAsignacion`, `NodoLeer`/`NodoEscribir`, `NodoOperacion`, `NodoNot`, `NodoValor`, `NodoIdentificador`, `NodoIndexado`, `NodoArreglo`, `NodoCadena`, `NodoDeclaracion`, `NodoProcedimiento`, `NodoFuncion`, `NodoParametro`, `NodoLlamada`, `NodoReturn`, y las enumeraciones `Tipo` y `tipoOp`. Las sentencias consecutivas se enlazan como **hermanos** (lista enlazada), no como una lista dentro de un nodo; ésto es heredado del Tiny original (`NodoBase.getHermanoDerecha`). La línea de origen de cada sentencia se guarda con `enLinea(nodo, linea)` para reportar errores y generar las anotaciones `@line` del código objeto.

Ejemplo de acción en `sintactico.cup`:
```
return_stmt ::= RETURN:r exp:e {: RESULT = enLinea(new NodoReturn(e), rleft); :}
```
`rleft` es la línea del token `RETURN`, fijada por el lexer.

## Ejemplo resuelto: evaluación dirigida por la sintaxis
Gramática de atributos:
```
E -> E1 + T     E.val = E1.val + T.val
E -> T          E.val = T.val
T -> T1 * F     T.val = T1.val * F.val
T -> F          T.val = F.val
F -> ( E )      F.val = E.val
F -> num        F.val = num.lexval
```
Entrada `3 + 2 * 4`: el parser reduce `F→3`, `T→3`, `E→3`; luego `F→2`, `T→2`; `F→4`, `T→T*F` con val = 8; `E→E+T` con val = 11. El valor 11 queda en el atributo de la raíz.

## Errores comunes
- Intentar usar atributos heredados en un parser LR sin trucos (marcadores): son naturales en LL.
- Mutar el AST durante el parseo en producciones que luego se descartan por error.
- Olvidar guardar la posición en el nodo: los mensajes semánticos pierden la línea.
- Confundir árbol de análisis con AST.

## Ejercicios propuestos
1. Escriba la regla semántica para `D -> T L` con `L.tipo = T.tipo` (heredado). *Resp.: ver heredados; cada identificador de L registra su tipo en la tabla de símbolos.*
2. Dé las acciones CUP para $E \to E - T$. *Resp.: `E ::= E:a MENOS T:b {: RESULT = a - b; :}`.*
3. Dibuje el AST de `x := y + 1`. *Resp.: asignación con hijo identificador x y operación + con hijos y y 1.*

## Conexiones
Fundamento del análisis semántico ([[Compiladores - 08 Análisis Semántico y Tabla de Símbolos]]) y del generador ([[Compiladores - 10 Generación de Código Tiny++ y Marcos de Activación]]). El parser: [[Compiladores - 06 Análisis Sintáctico Ascendente LR y CUP]].

## Fuente
Pregunta 7 de `~/Documentos/UNET/Compiladores/Parcial 1/31489733.txt`; `Compilador/src/main/cup/sintactico.cup`; lista de clases de `Compilador/src/main/java/ve/edu/unet/nodosAST/`.
