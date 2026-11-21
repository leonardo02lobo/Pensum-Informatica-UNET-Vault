---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: conocimiento general + ~/Documentos/UNET/Compiladores/Compilador/README.md
---
# Compiladores - 01 Introducción y Fases del Compilador

Materia: [[Compiladores e Intérpretes]]
Siguiente: [[Compiladores - 02 Análisis Léxico, Expresiones Regulares y Autómatas]]

## Contexto y objetivo
Un programa escrito en un lenguaje de alto nivel no lo entiende el procesador; necesita ser **traducido**. Esta nota define qué es un compilador, un intérprete y un traductor híbrido, y recorre las **fases** que se estudian durante el curso. Es el mapa general: cada fase tiene su propia nota. Las preguntas del primer parcial guardado en el material (definiciones de *palabra/cadena*, *BNF*, *intérprete*, *testigos* —tokens—, lenguajes de bajo nivel) parten de estos conceptos.

## Definiciones precisas
- **Traductor**: programa que convierte texto escrito en un lenguaje fuente a otro lenguaje destino.
- **Compilador**: traductor que lee **todo** el programa fuente y produce un programa equivalente en un lenguaje objeto (ensamblador, código de máquina, bytecode) que se ejecuta después, de forma independiente. Ejemplo: `gcc`, `javac`, y el compilador **Tiny++** del proyecto (genera código para la Tiny Machine).
- **Intérprete**: ejecuta el programa fuente (o una representación intermedia) instrucción por instrucción, sin producir un ejecutable independiente. Ejemplo clásico: el intérprete de Python en modo script, un shell.
- **Híbrido**: compila a una representación intermedia (bytecode) que una máquina virtual interpreta o compila en caliente (JIT). Java: `javac` produce `.class`, la JVM los interpreta/compila.
- **Ensamblador**: traductor de lenguaje simbólico de bajo nivel (mnemónicos) a código de máquina.
- **Lenguaje de bajo nivel**: cercano a la arquitectura (ensamblador, código máquina); de alto nivel: abstrae el hardware (C, Java, Tiny++).
- **Palabra o cadena**: secuencia finita de símbolos de un alfabeto $\Sigma$. La cadena vacía se denota $\varepsilon$. $\Sigma^*$ es el conjunto de todas las cadenas posibles.
- **Lenguaje**: cualquier subconjunto $L \subseteq \Sigma^*$.
- **BNF (Backus-Naur Form)**: notación para describir gramáticas libres de contexto: `<expr> ::= <expr> + <term> | <term>`.

### Compilador vs intérprete
| Aspecto | Compilador | Intérprete |
|---|---|---|
| Traducción | Una vez, antes de ejecutar | Durante la ejecución |
| Velocidad de ejecución | Alta | Menor |
| Detección de errores | Antes de ejecutar (todos los léxicos/sintácticos/semánticos) | A medida que se llega a la instrucción |
| Depuración | Necesita información de depuración | Más simple, hay acceso al fuente |
| Portabilidad | Un binario por plataforma | El fuente corre donde esté el intérprete |

## Las fases de un compilador
```
 fuente --> [Análisis léxico] --> tokens --> [Sintáctico] --> árbol --> [Semántico] --> árbol decorado
        --> [Código intermedio] --> [Optimización] --> [Generación de código] --> objeto
        (tabla de símbolos y manejo de errores acompañan a todas las fases)
```
1. **Análisis léxico (scanner)**: agrupa caracteres en *tokens* (testigos). Ver [[Compiladores - 02 Análisis Léxico, Expresiones Regulares y Autómatas]] y [[Compiladores - 03 JFlex y el Analizador Léxico de Tiny++]].
2. **Análisis sintáctico (parser)**: verifica que la secuencia de tokens cumpla la gramática y construye el árbol. Ver notas 04, 05 y 06.
3. **Análisis semántico**: comprueba lo que la gramática libre de contexto no puede (declaración antes de uso, tipos). Ver [[Compiladores - 08 Análisis Semántico y Tabla de Símbolos]].
4. **Código intermedio**: representación independiente de la máquina (AST, código de tres direcciones).
5. **Optimización**: mejora tiempo/espacio sin cambiar el significado ([[Compiladores - 11 Optimización y Manejo de Errores]]).
6. **Generación de código**: produce el código objeto ([[Compiladores - 10 Generación de Código Tiny++ y Marcos de Activación]]).

### Frontend y backend
El **frontend** (léxico, sintáctico, semántico, intermedio) depende del lenguaje fuente; el **backend** (optimización final y generación) depende de la máquina destino. Con esta separación, $n$ lenguajes y $m$ máquinas requieren $n + m$ módulos en vez de $n \cdot m$ compiladores completos.

### Pasadas
Una **pasada** es un recorrido completo del programa o su representación. Tiny++ usa varias: el lexer y el parser trabajan acoplados (el parser pide tokens), luego una pasada semántica separada sobre el AST y luego una pasada de generación.

## Herramientas y bootstrapping
- **Generadores de analizadores**: Lex/Flex/JFlex (léxico), Yacc/Bison/CUP (sintáctico).
- **Bootstrapping**: escribir el compilador de un lenguaje en ese mismo lenguaje, apoyándose en una versión previa mínima.
- **Compilación cruzada**: compilador que corre en una plataforma y genera código para otra.
- **Preprocesador, ensamblador, enlazador y cargador** completan la cadena: fuente → preprocesado → ensamblador → objeto reubicable → ejecutable → carga en memoria (relación con [[Sistemas Operativos]] y [[Organización del Computador]]).

## Ejemplo resuelto: de `x := a + 2 * 3` a código
1. **Léxico**: `ID(x) ASSIGN ID(a) PLUS NUM(2) TIMES NUM(3)`.
2. **Sintáctico**: árbol con `+` en la raíz; el hijo derecho es `2 * 3` porque `*` tiene mayor precedencia.
3. **Semántico**: `x` y `a` declaradas como `int`; la expresión es `int`; asignación válida.
4. **Intermedio (tres direcciones)**: `t1 = 2 * 3; t2 = a + t1; x = t2`.
5. **Optimización**: plegado de constantes: `t1 = 6`; queda `x = a + 6`.
6. **Generación (TM)**: `LD 0,addr_a(5)`, `LDC 1,6`, `ADD 0,0,1`, `ST 0,addr_x(5)` (el compilador real genera instrucciones equivalentes con una pila de temporales, ver nota 10).

## Errores comunes
- Confundir **lexema** (texto `contador`), **token** (categoría `ID`) y **patrón** (regla `letra(letra|digito)*`).
- Creer que un error semántico puede detectarse con la gramática libre de contexto: "variable no declarada" requiere una tabla de símbolos.
- Pensar que "compilado" implica siempre código de máquina nativo.
- Decir que el intérprete "no traduce": traduce, pero en tiempo de ejecución.

## Ejercicios propuestos
1. Clasifique como compilador, intérprete o híbrido: `gcc`, `bash`, `javac + JVM`, `node`. *Resp.: compilador, intérprete, híbrido, híbrido (JIT).*
2. ¿Cuántos módulos se necesitan para 4 lenguajes y 3 máquinas con IR común? *Resp.: 4 frontends + 3 backends = 7, en lugar de 12 compiladores.*
3. ¿En qué fase se detecta `int x; x := "hola"`? *Resp.: semántica (incompatibilidad de tipos).*
4. Defina BNF y dé un ejemplo. *Resp.: ver arriba.*

## Conexiones
Parte de la cadena de [[Organización del Computador]] (ISA), [[Estructura de Datos]] (árboles, hash para la tabla de símbolos), [[Matemática Discreta]] (lenguajes y autómatas). Proyecto aplicado: [[Tiny++ Compilador e IDE]] y [[Compiladores - 12 Proyecto Tiny++ Arquitectura, Contrato con el IDE y Defensa]].

## Fuente
Conocimiento general (Aho et al.; Louden) y arquitectura documentada en `~/Documentos/UNET/Compiladores/Compilador/README.md`.
