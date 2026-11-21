---
tags: [materia, semestre-VII]
semestre: VII
---
# Compiladores e Intérpretes

**Semestre:** [[Semestre VII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Sistemas Operativos]]

## Desbloquea
- _Ninguna_

## Material pesado (fuera del vault)
- `~/Documentos/UNET/Compiladores`

## Apuntes

### Descripción general y objetivos
Compiladores e Intérpretes estudia cómo se traduce un lenguaje fuente a código ejecutable o se interpreta directamente. El estudiante aprende teoría de lenguajes formales (autómatas y gramáticas) y la aplica construyendo las fases de un compilador: análisis léxico, sintáctico, semántico, generación de código y, en la práctica de la UNET, un proyecto sobre el lenguaje **Tiny** evolucionado a **Tiny++** con máquina virtual **TM (Tiny Machine)**. Prerrequisito: [[Sistemas Operativos]] (más [[Estructura de Datos]] y [[Matemática Discreta]] como base). Detalle del proyecto en [[Tiny++ Compilador e IDE]].

### Contenido programático
1. **Introducción**: compilador vs intérprete vs traductor híbrido; fases (frontend/backend); herramientas (*bootstrapping*, ensambladores, cargadores).
2. **Análisis léxico**: tokens, patrones, lexemas; expresiones regulares; AFN/AFD; construcción de Thompson, subconjuntos, minimización; generadores (JFlex, Lex).
3. **Análisis sintáctico**: gramáticas libres de contexto, derivaciones, árboles de análisis, ambigüedad; BNF/EBNF.
   - **Descendente**: LL(1), conjuntos FIRST/FOLLOW, descenso recursivo.
   - **Ascendente**: LR(0), SLR, LALR, LR(1); generadores (CUP, Yacc/Bison).
4. **Análisis semántico**: tabla de símbolos, ámbitos, verificación de tipos, gramáticas de atributos (sintetizados/heredados), traducción dirigida por la sintaxis.
5. **Código intermedio y generación de código**: AST, código de tres direcciones, registros de activación (pila), paso de parámetros, generación para máquina de pila/registros.
6. **Optimización** (introducción): eliminación de subexpresiones comunes, plegado de constantes, optimización de bucles.
7. **Manejo de errores** y recuperación (modo pánico).

### Conceptos clave
- **Lexema / token / patrón**: texto concreto, categoría y regla que lo describe.
- **Gramática libre de contexto**: G = (N, T, P, S).
- **FIRST(α)**: terminales que pueden iniciar derivaciones de α. **FOLLOW(A)**: terminales que pueden seguir a A.
- **Conflicto shift/reduce y reduce/reduce**: indican ambigüedad o gramática no apta para el método.
- **AST**: árbol de sintaxis abstracta, sin detalles superfluos.
- **Tabla de símbolos**: nombre, tipo, ámbito, dirección; implementada como pila de tablas hash.
- **Marco de activación**: bloque en la pila con parámetros, retorno y locales de cada llamada.

### Algoritmos y código de ejemplo
Cálculo de FIRST/FOLLOW (idea): repetir hasta punto fijo aplicando las reglas de cada producción.

```
Gramática LL(1):  E -> T E'     E' -> + T E' | ε
                  T -> F T'     T' -> * F T' | ε     F -> ( E ) | id
FIRST(E)=FIRST(T)=FIRST(F)={ (, id }   FIRST(E')={+,ε}   FIRST(T')={*,ε}
FOLLOW(E)=FOLLOW(E')={ ), $ }   FOLLOW(T)=FOLLOW(T')={+, ), $}
```

Especificación JFlex mínima (estructura de tres secciones separadas por `%%`):

```java
import java.io.*;
%%
%class Calculadora
%standalone
%unicode
%line
%%
[0-9]+      { System.out.println("NUM " + yytext()); }
[a-zA-Z_]\w* { System.out.println("ID  " + yytext()); }
[ \t\r\n]   { /* ignorar */ }
.           { System.err.println("Error léxico línea " + (yyline+1)); }
```

Gramática CUP (fragmento):
```
expr ::= expr PLUS term | term ;
term ::= term TIMES factor | factor ;
factor ::= LPAREN expr RPAREN | NUM | ID ;
```

### Ejemplo resuelto breve
AFD para identificadores `letra (letra|dígito)*`: estados q0 (inicio), q1 (aceptación). q0 --letra--> q1; q1 --letra,dígito--> q1. Cualquier otro símbolo en q0 es error. La cadena `x1` pasa q0->q1->q1 y se acepta; `1x` falla en q0.

### Cómo se relaciona con otras materias
- [[Sistemas Operativos]] (pila, procesos, cargador), [[Organización del Computador]] (ISA, ensamblador), [[Estructura de Datos]] (árboles, hash), [[Matemática Discreta]] (lenguajes, grafos), [[Programación II]] (Java/POO).
- Aporta fundamentos útiles para [[Ingeniería de Software]] (herramientas, análisis estático).

### Evaluación y consejos
- El material guardado muestra: parcial teórico (definiciones tipo palabra/cadena, BNF, intérprete, testigos, lenguajes de bajo nivel; selección múltiple; programa en JFlex) y un **proyecto final** (compilador Tiny++ + IDE con depurador visual) con defensa. Verificar ponderaciones con el programa oficial.
- Practique construir AFD/AFN a mano y tablas LL(1)/LR.
- Escriba pruebas por cada fase (casos "golden" con salida esperada).

### Bibliografía
- Aho, Lam, Sethi, Ullman. *Compiladores: principios, técnicas y herramientas* (libro del dragón).
- Louden, K. *Construcción de compiladores: principios y práctica* (origen de Tiny y TM).
- Appel, A. *Modern Compiler Implementation*.
- Manuales de JFlex y CUP.

### Recursos (fuera del vault)
`~/Documentos/UNET/Compiladores`: `Proyecto/` (especificación Tiny++ en .md y .pdf, `TM.C`, simulador web), `Compilador/` (repositorio Java+JFlex+CUP con `make`, pruebas), `IDE for Tiny/` (IDE web/escritorio), `DFA/`, `Presentacion/` (guía de defensa, 12 ejemplos `.tny` con `verificar.sh`), `Parcial 1/`. No hay `Material/` en el vault.
