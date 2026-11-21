---
tags: [tema, semestre-VII]
semestre: VII
---
# Tiny++ Compilador e IDE

Nota hija de [[Compiladores e Intérpretes]]. Resume el proyecto final (fuente: `~/Documentos/UNET/Compiladores`, fuera del vault).

## Enunciado
Ampliar el lenguaje **Tiny** (de las clases de laboratorio) a **Tiny++**, generando código para la máquina virtual **TM (Tiny Machine)**, y construir un **IDE** con editor y **depurador visual** acoplado a la TM.

## Características del lenguaje Tiny++
1. **Tipado estricto**: `int`, `bool`, `string`; declaración obligatoria antes de usar.
2. **Arreglos unidimensionales** con índices compuestos (`A[i*2+1] := 10;`).
3. **Procedimientos y funciones** con parámetros formales y recursión.
4. **Ámbitos**: variables locales al bloque o función; globales solo las del cuerpo principal.
5. **Verificaciones semánticas**: variable no declarada; compatibilidad de tipos en operaciones, asignaciones y paso de parámetros.

## Arquitectura del compilador (Java 17, JFlex, CUP)
```
programa.tny -> Lexer(JFlex) -> Parser(CUP) -> AST -> Analizador semántico -> Generador (UtGen) -> programa.tm
                 errores léxicos   errores sintácticos      errores semánticos
```
| Pieza | Rol |
|---|---|
| Lexer (`lexico.flex`) | tokens con línea y columna |
| Parser (`sintactico.cup`) | gramática y construcción del AST |
| Tabla de símbolos / Ámbito | pila de ámbitos, tipo y dirección de memoria |
| AnalizadorSemantico | pase aparte sobre el AST |
| Generador | código TM con pila dinámica y marcos de activación, anotaciones para el IDE |
| ListaDiagnosticos | acumula errores de todas las fases con formato de contrato |

Comandos: `make` (compila `tinypp.jar`), `make tm` (simulador de referencia en C), `make test` (pruebas del contrato y casos golden).

## IDE
Editor con resaltado, compilación (Ctrl+F9), ejecución con pestaña de entrada/salida (Ctrl+F5) y depuración paso a paso (F5) que visualiza registros, memoria y pila de la TM. Consume el compilador como proceso externo.

## Conceptos aplicados
Autómatas y expresiones regulares (léxico), gramáticas LALR (CUP), gramáticas de atributos y tabla de símbolos (semántica), registros de activación y convenciones de llamada (generación). Relación con [[Sistemas Operativos]] (pila, procesos) y [[Organización del Computador]] (ISA).
