---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: conocimiento general (Aho et al., Louden)
---
# Compiladores - 05 Análisis Sintáctico Descendente LL(1)

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 04 Gramáticas Libres de Contexto, BNF y Ambigüedad]]
Siguiente: [[Compiladores - 06 Análisis Sintáctico Ascendente LR y CUP]]

## Contexto y objetivo
El análisis **descendente** construye el árbol desde la raíz (símbolo inicial) hacia las hojas, simulando una derivación **más a la izquierda**. El método **LL(1)** lee la entrada de izquierda a derecha (L), produce derivación más a la izquierda (L) y usa **1** símbolo de adelanto. Se presentan FIRST, FOLLOW, la tabla predictiva, el descenso recursivo y ejemplos resueltos.

## Teoría
### FIRST
$FIRST(\alpha)$ = conjunto de terminales que pueden iniciar una cadena derivada de $\alpha$; contiene $\varepsilon$ si $\alpha \Rightarrow^* \varepsilon$.
Reglas:
1. $FIRST(a) = \{a\}$ para terminal $a$.
2. Si $A \to \varepsilon$, $\varepsilon \in FIRST(A)$.
3. Si $A \to Y_1 Y_2 \dots Y_k$: se añade $FIRST(Y_1) \setminus \{\varepsilon\}$; si $\varepsilon \in FIRST(Y_1)$ se sigue con $Y_2$, etc.; si todos derivan $\varepsilon$, se añade $\varepsilon$.

### FOLLOW
$FOLLOW(A)$ = terminales que pueden aparecer inmediatamente a la derecha de $A$ en alguna forma sentencial ($\$$ marca fin de entrada).
1. $\$ \in FOLLOW(S)$.
2. Si $A \to \alpha B \beta$: $FIRST(\beta) \setminus \{\varepsilon\} \subseteq FOLLOW(B)$.
3. Si $A \to \alpha B$ o $A \to \alpha B \beta$ con $\varepsilon \in FIRST(\beta)$: $FOLLOW(A) \subseteq FOLLOW(B)$.
Se itera hasta un **punto fijo**.

### Tabla predictiva y condición LL(1)
Para cada producción $A \to \alpha$: para todo $a \in FIRST(\alpha)$, $M[A,a] = A \to \alpha$; si $\varepsilon \in FIRST(\alpha)$, para todo $b \in FOLLOW(A)$, $M[A,b] = A \to \alpha$. Una gramática es **LL(1)** si ninguna celda tiene más de una producción. Equivalente: para $A \to \alpha \mid \beta$, $FIRST(\alpha) \cap FIRST(\beta) = \emptyset$ y, si $\beta \Rightarrow^* \varepsilon$, $FIRST(\alpha) \cap FOLLOW(A) = \emptyset$. No es LL(1) ninguna gramática ambigua, con recursión izquierda o sin factorizar.

### Algoritmo con pila
```
push $, push S
mientras tope != $:
    X = tope, a = token actual
    si X es terminal: si X == a: pop, avanzar; sino error
    sino si M[X,a] = X -> Y1..Yk: pop; push Yk..Y1 (Y1 queda arriba)
    sino error
aceptar si token actual == $
```

### Descenso recursivo
Un procedimiento por no terminal; el cuerpo refleja el lado derecho de la producción y se decide con el token de adelanto. Es el método usado a mano en muchos compiladores (el Tiny original de Louden). Ejemplo para `factor`:
```java
void factor() {
    if (tok == ID)      match(ID);
    else if (tok == NUM) match(NUM);
    else if (tok == LPAREN) { match(LPAREN); exp(); match(RPAREN); }
    else error("factor inesperado");
}
```

## Ejemplo resuelto completo
Gramática (ya sin recursión izquierda):
$E \to T E'$; $E' \to + T E' \mid \varepsilon$; $T \to F T'$; $T' \to * F T' \mid \varepsilon$; $F \to (E) \mid id$.

**FIRST**: $FIRST(F)=FIRST(T)=FIRST(E)=\{(, id\}$; $FIRST(E')=\{+,\varepsilon\}$; $FIRST(T')=\{*,\varepsilon\}$.
**FOLLOW**: $FOLLOW(E)=FOLLOW(E')=\{ ), \$\}$; $FOLLOW(T)=FOLLOW(T')=\{+, ), \$\}$; $FOLLOW(F)=\{*, +, ), \$\}$.

**Tabla M**:

| | id | + | * | ( | ) | $ |
|---|---|---|---|---|---|---|
| E | TE' | | | TE' | | |
| E' | | +TE' | | | ε | ε |
| T | FT' | | | FT' | | |
| T' | | ε | *FT' | | ε | ε |
| F | id | | | (E) | | |

**Traza** de `id + id $`:
| Pila (tope a la izquierda) | Entrada | Acción |
|---|---|---|
| E $ | id + id $ | E → T E' |
| T E' $ | id + id $ | T → F T' |
| F T' E' $ | id + id $ | F → id |
| id T' E' $ | id + id $ | match id |
| T' E' $ | + id $ | T' → ε |
| E' $ | + id $ | E' → + T E' |
| + T E' $ | + id $ | match + |
| T E' $ | id $ | T → F T' |
| F T' E' $ | id $ | F → id |
| id T' E' $ | id $ | match id |
| T' E' $ | $ | T' → ε |
| E' $ | $ | E' → ε |
| $ | $ | aceptar |

## Recuperación de errores (modo pánico)
Al fallar `M[X,a]`, se descartan tokens hasta hallar uno de $FOLLOW(X)$ (o de un conjunto de sincronización) y se saca $X$ de la pila.

## Errores comunes
- Calcular FOLLOW con $\varepsilon$ en lugar de omitirlo (nunca es parte de FOLLOW).
- Olvidar propagar $FOLLOW(A)$ a $B$ cuando $B$ es el último símbolo.
- Dejar recursión izquierda: el descenso recursivo cicla.
- Apilar el lado derecho en el orden incorrecto (el primer símbolo debe quedar en el tope).

## Ejercicios propuestos
1. Calcule FIRST y FOLLOW de $S \to aSb \mid \varepsilon$. *Resp.: $FIRST(S)=\{a,\varepsilon\}$; $FOLLOW(S)=\{b,\$\}$; es LL(1).*
2. ¿Es LL(1) $S \to a \mid ab$? *Resp.: no; $FIRST$ coinciden; factorizar: $S \to aS'$, $S' \to b \mid \varepsilon$.*
3. Trace `(id)` con la tabla anterior. *Resp.: E→TE', T→FT', F→(E), match (, E→TE'..., F→id, T'→ε, E'→ε, match ), T'→ε, E'→ε; aceptada.*

## Conexiones
La alternativa que usa Tiny++ (CUP) es ascendente: [[Compiladores - 06 Análisis Sintáctico Ascendente LR y CUP]]. Gramáticas: [[Compiladores - 04 Gramáticas Libres de Contexto, BNF y Ambigüedad]]. Estructuras de pila: [[Estructura de Datos]].

## Fuente
Conocimiento general; el temario de la materia (ver [[Compiladores e Intérpretes]]) incluye LL(1), FIRST/FOLLOW y descenso recursivo.
