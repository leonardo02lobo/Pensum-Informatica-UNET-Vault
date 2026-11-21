---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: ~/Documentos/UNET/Compiladores/Compilador/src/main/jflex/lexico.flex y Parcial 1/31489733.txt
---
# Compiladores - 03 JFlex y el Analizador Léxico de Tiny++

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 02 Análisis Léxico, Expresiones Regulares y Autómatas]]
Siguiente: [[Compiladores - 04 Gramáticas Libres de Contexto, BNF y Ambigüedad]]

## Contexto y objetivo
**JFlex** genera en Java un analizador léxico (DFA) a partir de una especificación. Aquí se explica la estructura de un archivo `.flex`, se resuelve el programa del parcial (una "calculadora" de filas `S 5`/`R 3`) y se analiza el lexer real de Tiny++ (`lexico.flex`).

## Estructura de un archivo JFlex
Tres secciones separadas por `%%`:
1. **Código de usuario**: `package`, `import`, copiados tal cual.
2. **Opciones y declaraciones**: `%class`, `%unicode`, `%line`, `%column`, `%standalone`, `%type`, `%function`, `%state`; bloque `%{ ... %}` (código dentro de la clase); `%eof{ ... %eof}`; macros `nombre = regex`.
3. **Reglas léxicas**: `regex { acción }` con estados léxicos `<ESTADO>`.

Opciones habituales: `%line` y `%column` dan `yyline`, `yycolumn` (base 0); `yytext()` es el lexema, `yycharat(i)` un carácter, `yylength()`, `yybegin(ESTADO)` cambia de estado. Resolución de conflictos: **máximo lexema; empate: regla más arriba**.

## Ejemplo del parcial: la Calculadora
Entrada: filas con una letra y un número (`S 10`, `R 3`). `S` suma, `R` resta, otra letra se ignora; al final imprime el resultado.
```java
%class Calculadora
%standalone
%unicode
%line
%{
  private int resultado = 0;
  private void operar(char letra, int numero) {
    switch (letra) { case 'S': resultado += numero; break;
                     case 'R': resultado -= numero; break;
                     default: break; }
  }
%}
%eof{  System.out.println("Resultado final: " + resultado);  %eof}
LETRA = [a-zA-Z]   NUMERO = [0-9]+   BLANCO = [ \t]   FIN = \r|\n|\r\n
%%
{LETRA}{BLANCO}*{NUMERO} {
    char letra = Character.toUpperCase(yycharat(0));
    int numero = Integer.parseInt(yytext().substring(1).trim());
    operar(letra, numero);
}
{FIN}      { }
{BLANCO}+  { }
[^]        { }
```
Puntos clave: `%standalone` crea un `main` y evita definir tokens; `%eof{...%eof}` imprime al terminar; la regla principal reconoce toda la fila como *un solo lexema*; `yytext().substring(1).trim()` quita la letra y los blancos; la última regla `[^]` (cualquier carácter) absorbe lo inválido. Traza para `S 10\nR 3\nS 5`: 10, 7, 12 y se imprime `Resultado final: 12`. Con `s 4` funciona porque `toUpperCase`.

## El lexer de Tiny++ (`lexico.flex`)
Configuración: `%class Lexico`, `%implements java_cup.runtime.Scanner`, `%function next_token`, `%type java_cup.runtime.Symbol`, `%unicode`, `%line`, `%column`, y un estado exclusivo `%state COMENTARIO`.

**Macros**:
```
letra         = [a-zA-Z_]
digito        = [0-9]
numero        = {digito}+
identificador = {letra}({letra}|{digito})*
nuevalinea    = \r\n | [\r\n\u000B\u0085  ]
espacio       = [ \t\f]+
```
**Reglas**: primero las palabras reservadas (`if then else end repeat until read write int bool string true false and or not procedure function return`), luego los operadores (`:=` antes de `:`, `<=`, `>=`, `<>` antes de `<`, `>`), delimitadores `( ) [ ] ; ,`, cadenas, número, identificador, saltos de línea, espacios y comentarios.

Dos decisiones de diseño importantes:
- **Orden**: `"if"` aparece antes de `{identificador}`; aunque ambas reconocen `if` con igual longitud, gana la primera. En cambio `iffy` produce `ID` por máximo lexema.
- **Prefijos de operadores**: `:=` (longitud 2) vence a `:` (longitud 1) por máximo lexema.

**Posición de los tokens**: cada token se entrega como `new Symbol(tipo, yyline+1, yycolumn+1, yytext())`; `left` = línea y `right` = columna (base 1), que CUP usa luego para reportar errores.

**Cadenas**: `\"([^\"\\\r\n]|\\[^\r\n])*\"` acepta comillas dobles con escapes; el método `decodificarCadena` resuelve `\"`, `\\`, `\n` y valida que cada carácter sea ASCII imprimible (32 a 126), reportando errores con columna y siguiendo con el análisis. Hay una segunda regla para cadena sin cerrar (error "cadena sin cerrar").

**Comentarios** `{ ... }`: `{` guarda la posición y cambia al estado `COMENTARIO`; allí `[^}]+` se ignora, `}` vuelve a `YYINITIAL`, y `<<EOF>>` reporta "comentario sin cerrar" con la posición de apertura y devuelve `EOF`. Esto muestra cómo los **estados léxicos** reemplazan a expresiones regulares complejas para estructuras anidadas o con delimitadores.

**Errores**: ningún error se imprime; se agregan a `ListaDiagnosticos` con fase `LEXICO` (regla `.` = "carácter inválido 'x'"). El lexer continúa para reportar varios errores en una pasada.

**Modo `verbose`**: cada acción llama `symbol("NOMBRE", sym.NOMBRE)` que imprime `token NOMBRE` cuando se pide `--verbose`.

## Ejemplo resuelto
Fuente: `int x; x := 3 { suma }`
Tokens: `T_INT, ID(x), SEMI, ID(x), ASSIGN, NUM(3)`, el comentario no genera token, `EOF`. Con `x := 3 @` se agrega un diagnóstico `Léxico error en línea 1:..: carácter inválido '@'` y el análisis sigue.

## Errores comunes
- Poner `identificador` antes de las reservadas.
- Olvidar que `yyline`/`yycolumn` son base 0.
- En comentarios con `[^}]+` olvidar la regla `<<EOF>>`: un comentario abierto se come todo el archivo en silencio.
- Reglas sin cubrir todos los caracteres: sin `.` final, un carácter inesperado lanza excepción.

## Ejercicios propuestos
1. Añada al lexer de Tiny++ un token para `%` (módulo). *Resp.: regla `"%" { return symbol("MOD", sym.MOD); }` y declarar el terminal en el `.cup`.*
2. Escriba la macro de un real `12.5`. *Resp.: `real = {digito}+ "." {digito}+` antes de `numero` o con regla más larga.*
3. ¿Qué token produce `<>=`? *Resp.: `NE` y luego `EQ` (máximo lexema de dos caracteres `<>`).*

## Conexiones
Los tokens alimentan al parser CUP ([[Compiladores - 06 Análisis Sintáctico Ascendente LR y CUP]]); los diagnósticos se explican en [[Compiladores - 11 Optimización y Manejo de Errores]] y en [[Tiny++ Compilador e IDE]].

## Fuente
`~/Documentos/UNET/Compiladores/Compilador/src/main/jflex/lexico.flex`; programa 3 de `Parcial 1/31489733.txt`.
