---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: conocimiento general + ~/Documentos/UNET/Compiladores/Parcial 1/31489733.txt + ~/Documentos/UNET/Compiladores/DFA/src/App.java
---
# Compiladores - 02 Análisis Léxico, Expresiones Regulares y Autómatas

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 01 Introducción y Fases del Compilador]]
Siguiente: [[Compiladores - 03 JFlex y el Analizador Léxico de Tiny++]]

## Contexto y objetivo
El analizador léxico lee caracteres y entrega **tokens**. Se especifica con **expresiones regulares** y se implementa con **autómatas finitos**. El material guardado incluye un parcial con ejercicios de DFA, determinización por subconjuntos y por qué preferir un DFA a un NFA, y una implementación en Java de un DFA (`DFA/src/App.java`). Esta nota explica la teoría y resuelve esos ejercicios.

## Teoría
### Tokens, patrones y lexemas
- **Token (testigo)**: par (categoría, valor): `(ID, "x1")`.
- **Patrón**: regla que describe los lexemas de una categoría (una expresión regular).
- **Lexema**: la cadena concreta del fuente.
- Regla de **máxima coincidencia** (*longest match*): se toma el lexema más largo posible; si hay empate entre reglas, gana la primera escrita (por eso las palabras reservadas van antes que `ID` en JFlex).

### Expresiones regulares
Sobre un alfabeto $\Sigma$: $\varepsilon$, un símbolo $a$, unión $r|s$, concatenación $rs$, cerradura de Kleene $r^*$. Azúcar sintáctico: $r^+ = rr^*$, $r? = r|\varepsilon$, clases `[a-z]`. Precedencia: cerradura > concatenación > unión.

Ejemplos: identificador `letra(letra|digito)*`; entero `digito+`; real `digito+ . digito+`.

### Autómatas finitos
Un AF es una 5-tupla $(Q, \Sigma, \delta, q_0, F)$.
- **DFA**: $\delta: Q \times \Sigma \to Q$ (una sola transición por estado y símbolo, sin $\varepsilon$).
- **NFA**: $\delta: Q \times (\Sigma \cup \{\varepsilon\}) \to \mathcal{P}(Q)$.
Ambos reconocen exactamente los lenguajes regulares. Equivalencia: toda ER tiene un NFA, todo NFA un DFA, y todo DFA tiene una ER.

### Pipeline de un generador (Lex/JFlex)
ER $\to$ NFA (Thompson) $\to$ DFA (subconjuntos) $\to$ DFA mínimo $\to$ tabla de transiciones.

### Construcción de Thompson
- Símbolo $a$: dos estados $i \xrightarrow{a} f$.
- Unión $r|s$: nuevo inicio con dos transiciones $\varepsilon$ hacia los NFA de $r$ y $s$, y ambos finales con $\varepsilon$ a un nuevo final.
- Concatenación: el final de $r$ se une (con $\varepsilon$ o fusionándolo) con el inicio de $s$.
- Cerradura $r^*$: nuevo inicio y final; $\varepsilon$ del inicio al final (cero repeticiones), del final de $r$ al inicio de $r$ (repetir) y del inicio al inicio de $r$.
Propiedad: el NFA resultante tiene a lo sumo $2|r|$ estados.

### Construcción de subconjuntos
- $\varepsilon\text{-cerradura}(T)$: estados alcanzables desde $T$ usando solo $\varepsilon$.
- $mover(T, a)$: estados alcanzables desde $T$ con el símbolo $a$.
Algoritmo:
```
D0 = e-cerradura({q0}); estados_sin_marcar = {D0}
mientras haya T sin marcar:
   marcar T
   para cada símbolo a:
       U = e-cerradura(mover(T, a))
       si U no está en Destados: agregarlo sin marcar
       Dtran[T, a] = U
Un estado de D es de aceptación si contiene algún estado de aceptación del NFA.
```
En el peor caso el DFA tiene $2^n$ estados para un NFA de $n$.

### Minimización
Se parten los estados en {aceptación} y {no aceptación} y se refina: dos estados son equivalentes si para todo símbolo van a la misma clase. Se repite hasta que no cambie la partición (algoritmo de Hopcroft/Moore). Se eliminan primero los estados inalcanzables.

## Por qué DFA y no NFA (respuesta del parcial)
El parcial pide justificar que para un analizador léxico conviene un DFA: la simulación es **lineal** ($O(n)$ en la longitud de la entrada, un paso por carácter con una tabla), sin conjuntos de estados activos, sin cerraduras $\varepsilon$ y sin retroceso. Un NFA exige mantener varios estados activos o hacer *backtracking*. No se pierde expresividad porque todo NFA se convierte a DFA por subconjuntos; por eso Lex/JFlex hacen ER $\to$ NFA $\to$ DFA $\to$ DFA mínimo. El costo se paga una sola vez, al generar el scanner.

## Ejemplos resueltos
### 1. DFA para pares de `a` y pares de `b` (ejercicio 5 del parcial)
Alfabeto {a, b}. Estados según la paridad: q0 (par,par), q1 (impar a, par b), q2 (par a, impar b), q3 (impar, impar). Inicial y de aceptación: q0.

| Estado | a | b |
|---|---|---|
| ->* q0 | q1 | q2 |
| q1 | q0 | q3 |
| q2 | q3 | q0 |
| q3 | q2 | q1 |

Traza de `abba`: q0 -a-> q1 -b-> q3 -b-> q1 -a-> q0: aceptada. `aab`: q0,q1,q0,q2: rechazada.

### 2. Determinización por subconjuntos (ejercicio 8)
El resultado del parcial es una tabla con estados como conjuntos; el estado inicial $\{q0,q1,q2\}$ es de aceptación y de él se llega con `a` a $\{q3,q4\}$ y con `b` al vacío. El método: para cada subconjunto calcular `mover` y cerradura por símbolo, y declarar de aceptación todo subconjunto que contenga un estado final del NFA. Resultado completo (10 filas, incluyendo el estado trampa $\emptyset$):

| Subconjunto | a | b | Acepta |
|---|---|---|---|
| ->* {q0,q1,q2} | {q3,q4} | vacío | sí |
| {q3,q4} | vacío | {q1,q3,q5} | no |
| * {q1,q3,q5} | {q2,q3} | {q1,q3} | sí |
| * {q2,q3} | {q4} | {q1,q3} | sí |
| * {q1,q3} | {q3} | {q1,q3} | sí |
| {q4} | vacío | {q5} | no |
| {q3} | vacío | {q1,q3} | no |
| {q5} | {q2} | vacío | no |
| * {q2} | {q4} | vacío | sí |
| vacío | vacío | vacío | no |
(El NFA original no se conserva en el material; la tabla es la respuesta del estudiante al parcial.)

### 3. Implementación Java de un DFA (`DFA/src/App.java`)
```java
public static boolean DFA(String palabra, Set<Character> alfabeto, String estado_inicial,
        Set<String> estado_aceptacion, Map<String, Map<Character, String>> funcion_transitoria) {
    String estado_actual = estado_inicial;
    for (int i = 0; i < palabra.length(); i++) {
        char simbolo = palabra.charAt(i);
        if (!alfabeto.contains(simbolo)) return false;       // símbolo fuera del alfabeto
        Map<Character, String> transicion = funcion_transitoria.get(estado_actual);
        if (transicion == null) return false;
        estado_actual = transicion.get(simbolo);              // un único destino: determinismo
        if (estado_actual == null) return false;              // transición no definida
    }
    return estado_aceptacion.contains(estado_actual);        // acepta si termina en F
}
```
La función de transición es un `Map` de mapas. En `main` el autómata tiene estados A..E sobre {a,b}, con A, B y C de aceptación: A -a-> B, A -b-> D, B -a-> B, B -b-> C, C absorbente de aceptación, D/E alternan. Analizando la tabla: D y E no pueden volver a A, B ni C, así que cualquier cadena que empiece con `b` se rechaza; si empieza con `a` se queda en B o C y se acepta. El lenguaje es, pues, la cadena vacía más las cadenas sobre {a,b} que empiezan con `a`. Trazas: `"aab"` termina en C (aceptada); `"cabc"` se rechaza por `c` fuera del alfabeto.

### 4. Aplicación que acepta una ER y una cadena (pregunta 7.a del parcial)
Plan en cuatro pasos: (1) *tokenizar* la ER (símbolos, `| * + ?`, paréntesis, clases) y expandir el azúcar ( `[abc]` a `a|b|c`, `r+` a `rr*`) para obtener un árbol por precedencia o notación postfija; (2) NFA con Thompson; (3) DFA con subconjuntos (opcionalmente minimizar); (4) simular la cadena con la tabla y aceptar si se termina en estado final.

## Errores comunes
- Olvidar el **estado trampa** al completar un DFA.
- Marcar de aceptación un subconjunto solo si *todos* sus estados lo son (basta *uno*).
- Aplicar `mover` sin la $\varepsilon$-cerradura posterior.
- Ordenar mal las reglas del scanner (`ID` antes de `if` convierte las reservadas en identificadores).

## Ejercicios propuestos
1. Dé un DFA para cadenas sobre {0,1} que terminan en `01`. *Resp.: 3 estados (sin progreso, vio 0, vio 01), inicial sin progreso, aceptación el tercero.*
2. ER de los enteros con signo opcional. *Resp.: `(+|-)? [0-9]+`.*
3. ¿Cuántos estados como máximo tiene el DFA de un NFA de 4 estados? *Resp.: $2^4 = 16$.*
4. Minimice un DFA con estados indistinguibles q1 y q2 (ambos van a q3 con a y q0 con b, ambos de aceptación). *Resp.: se fusionan.*

## Conexiones
La implementación práctica con JFlex está en [[Compiladores - 03 JFlex y el Analizador Léxico de Tiny++]]. Teoría de lenguajes en [[Matemática Discreta]]; el parcial se discute además en [[Compiladores - 07 Traducción Dirigida por la Sintaxis y AST]].

## Fuente
`~/Documentos/UNET/Compiladores/Parcial 1/31489733.txt` (respuestas del estudiante a los ejercicios 4, 5, 7.a y 8), `~/Documentos/UNET/Compiladores/DFA/src/App.java`. Las imágenes del parcial (`31489733_6.png`, `_9.jpeg`) no se leyeron.
