---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: conocimiento general + gramática de ~/Documentos/UNET/Compiladores/Compilador/src/main/cup/sintactico.cup
---
# Compiladores - 04 Gramáticas Libres de Contexto, BNF y Ambigüedad

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 03 JFlex y el Analizador Léxico de Tiny++]]
Siguiente: [[Compiladores - 05 Análisis Sintáctico Descendente LL(1)]]

## Contexto y objetivo
Las expresiones regulares no pueden describir estructuras anidadas (paréntesis balanceados, bloques `if ... end`). Para eso se usan **gramáticas libres de contexto (GLC)**. Esta nota fija el vocabulario necesario para los analizadores LL y LR.

## Definiciones
Una GLC es $G = (N, T, P, S)$:
- $N$: no terminales (variables sintácticas), $T$: terminales (tokens), $P$: producciones $A \to \alpha$ con $A \in N$ y $\alpha \in (N \cup T)^*$, $S$: símbolo inicial.
- **Derivación**: $\alpha A \beta \Rightarrow \alpha \gamma \beta$ si $A \to \gamma \in P$. **Más a la izquierda** (siempre se expande el no terminal más a la izquierda) y **más a la derecha**.
- **Forma sentencial**: cadena derivable de $S$; **sentencia**: forma sentencial formada solo por terminales.
- **Lenguaje generado**: $L(G) = \{w \in T^* : S \Rightarrow^* w\}$.
- **Árbol de análisis (parse tree)**: raíz $S$, hojas terminales (o $\varepsilon$), cada nodo interno corresponde a una producción.
- **BNF**: `<A> ::= alfa | beta`. **EBNF** añade `[ ]` (opcional), `{ }` (repetición) y `( )` (agrupación).

## Ambigüedad
Una gramática es **ambigua** si existe una sentencia con dos árboles de análisis distintos (o dos derivaciones más a la izquierda). Ejemplo clásico:
$$E \to E + E \mid E * E \mid (E) \mid id$$
La cadena `id + id * id` tiene dos árboles: $(id+id)*id$ y $id+(id*id)$.

### Cómo eliminarla: niveles de precedencia y asociatividad
```
E -> E + T | T          (+ asocia a la izquierda: recursión izquierda)
T -> T * F | F
F -> ( E ) | id
```
Cada nivel de no terminal fija una precedencia (mayor cuanto más profundo) y la dirección de la recursión fija la asociatividad. Otra ambigüedad famosa es el **else colgante**: `if a then if b then s1 else s2`. Se resuelve asociando el `else` al `if` más cercano o usando un delimitador `end`.

**Caso real, Tiny++**: la gramática de `sintactico.cup` evita tablas de precedencia con una jerarquía de no terminales: `exp` (or) → `and_exp` (and) → `not_exp` (not) → `rel_exp` (comparaciones) → `simple_exp` (+, -) → `term` (*, /) → `factor`. Menor a mayor precedencia: `or` < `and` < `not` < comparación < `+ -` < `* /`. Los condicionales usan `end` como terminador, por lo que no hay *else* colgante.

## Transformaciones de gramáticas
### Recursión izquierda
$A \to A\alpha \mid \beta$ no sirve para análisis descendente (bucle infinito). Se elimina:
$$A \to \beta A', \quad A' \to \alpha A' \mid \varepsilon$$
### Factorización izquierda
$A \to \alpha\beta_1 \mid \alpha\beta_2$ se transforma en $A \to \alpha A'$, $A' \to \beta_1 \mid \beta_2$ para decidir con un solo símbolo de adelanto.

## Ejemplo resuelto: derivación y árbol
Gramática: $E \to E+T \mid T$, $T \to T*F \mid F$, $F \to (E) \mid id$. Cadena `id + id * id`.
Derivación más a la izquierda:
$E \Rightarrow E+T \Rightarrow T+T \Rightarrow F+T \Rightarrow id+T \Rightarrow id+T*F \Rightarrow id+F*F \Rightarrow id+id*F \Rightarrow id+id*id$.
El árbol coloca `*` más profundo que `+`: la multiplicación se agrupa primero. Es el único árbol posible, la gramática no es ambigua.

## Gramáticas del lenguaje Tiny++ (resumen)
```
program  ::= top_seq
top_seq  ::= top_seq SEMI top_item | top_item
top_item ::= stmt | proc_decl | func_decl
stmt_seq ::= stmt_seq SEMI stmt | stmt
```
Las sentencias se **separan** (no terminan) con `;`. Las subrutinas solo aparecen en `top_seq`: declararlas dentro de un bloque es un error **sintáctico** por construcción de la gramática, un ejemplo de cómo codificar restricciones en la GLC.

## Errores comunes
- Confundir ambigüedad (propiedad de la gramática) con ambigüedad del lenguaje (inherente).
- Eliminar la recursión izquierda y olvidar $\varepsilon$ en $A'$.
- Cambiar la asociatividad al eliminar recursión izquierda sin ajustar el árbol de atributos (el árbol semántico debe seguir siendo asociativo a izquierda).
- Creer que toda GLC es LL(1) o LR(1).

## Ejercicios propuestos
1. Elimine la recursión izquierda de $E \to E + T \mid T$. *Resp.: $E \to T E'$, $E' \to + T E' \mid \varepsilon$.*
2. Muestre que $S \to S S \mid a$ es ambigua. *Resp.: `aaa` tiene dos árboles ($(aa)a$ y $a(aa)$).*
3. Dé una GLC para paréntesis balanceados. *Resp.: $S \to ( S ) S \mid \varepsilon$.*

## Conexiones
Siguientes pasos: análisis [[Compiladores - 05 Análisis Sintáctico Descendente LL(1)]] y [[Compiladores - 06 Análisis Sintáctico Ascendente LR y CUP]]. Uso de BNF en el parcial: [[Compiladores - 01 Introducción y Fases del Compilador]]. Estructuras de árbol: [[Estructura de Datos]].

## Fuente
Conocimiento general; gramática de Tiny++ en `~/Documentos/UNET/Compiladores/Compilador/src/main/cup/sintactico.cup`.
