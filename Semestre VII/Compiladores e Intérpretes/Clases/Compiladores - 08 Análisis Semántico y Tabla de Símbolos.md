---
tags: [clase, semestre-VII]
materia: Compiladores e Intérpretes
fuente: ~/Documentos/UNET/Compiladores/Compilador/src/main/java/ve/edu/unet/ (AnalizadorSemantico, TablaSimbolos, Ambito) + Presentacion/ejemplos
---
# Compiladores - 08 Análisis Semántico y Tabla de Símbolos

Materia: [[Compiladores e Intérpretes]]
Anterior: [[Compiladores - 07 Traducción Dirigida por la Sintaxis y AST]]
Siguiente: [[Compiladores - 09 Código Intermedio y la Tiny Machine]]

## Contexto y objetivo
La gramática libre de contexto no puede expresar "toda variable debe declararse antes de usarse" ni "no se suma un `bool` con un `int`". El **análisis semántico** comprueba estas reglas contextuales usando una **tabla de símbolos** y un **sistema de tipos**. En Tiny++ es una pasada separada sobre el AST (`AnalizadorSemantico.java`, 404 líneas) y es la parte de la especificación que exige "no permitir variables no declaradas" y "verificar compatibilidad de tipos en operaciones, asignaciones y paso de parámetros".

## Teoría
### Tabla de símbolos
Estructura que asocia cada identificador con sus atributos: nombre, **tipo**, **ámbito**, línea de declaración, **dirección** de memoria, y para subrutinas la firma (tipos de parámetros) y tipo de retorno. Operaciones: *insertar*, *buscar*, *abrir ámbito*, *cerrar ámbito*. Implementaciones: tabla hash por ámbito, apiladas.

### Ámbitos (scopes)
- **Estático (léxico)**: la visibilidad se decide por la estructura del texto del programa. Lo usan casi todos los lenguajes modernos y Tiny++.
- Regla: una declaración es visible desde su punto de declaración hasta el final de su bloque, incluidos los bloques anidados; se puede **sombrear** un nombre exterior, pero no declarar dos veces el mismo nombre en el mismo ámbito.
- Búsqueda: de dentro hacia fuera por la cadena de padres.

### Sistema de tipos
**Tipado estático y fuerte**: cada expresión tiene un tipo determinado en compilación y no hay conversiones implícitas. **Equivalencia de tipos por nombre/estructura**; aquí los tipos son `int`, `bool`, `string` y arreglos unidimensionales de `int` o `bool` (y `string`).

Reglas de tipado (Tiny++):
| Construcción | Regla |
|---|---|
| `x := e` | tipo(e) = tipo(x) |
| `a + b`, `a - b`, `a * b`, `a / b` | ambos `int` → `int` |
| `<`, `<=`, `>`, `>=` | ambos `int` → `bool` |
| `=`, `<>` | dos `int` o dos `bool` → `bool` |
| `and`, `or`, `not` | `bool` → `bool` |
| `if c`, `until c` | c es `bool` |
| `read x` | x es `int` |
| `A[e]` | A es arreglo y e es `int`; tipo = tipo del elemento |
| llamada `f(a1..an)` | n coincide y tipo(ai) = tipo del parámetro i |
| `return e` | tipo(e) = tipo de retorno de la función |

Los `string` solo se pueden asignar, pasar, devolver, guardar en arreglos y escribir; `+`, `=`, `<` con cadenas son errores.

### Atributos
Se pueden evaluar como atributos **sintetizados** (el tipo de una expresión sube desde sus hijos) y **heredados** (el ámbito actual baja por el recorrido). Se ve cuando el analizador mantiene `ambitoActual` mientras visita el árbol (ver [[Compiladores - 07 Traducción Dirigida por la Sintaxis y AST]]).

## Implementación en Tiny++
- `Ambito`: clase con `clase` (GLOBAL, BLOQUE, SUBRUTINA), `padre`, `linea`, `profundidad` y un `LinkedHashMap<String, RegistroSimbolo>` con sus símbolos.
- `TablaSimbolos`: `abrirAmbito`, `abrirSubrutina`, `cerrarAmbito`, `InsertarSimbolo`, `InsertarArreglo`, `InsertarParametro`, `InsertarProcedimiento`, `InsertarFuncion`, `BuscarSimbolo` (sube por la cadena), `BuscarEnAmbitoActual` (solo el ámbito actual, para detectar redeclaración). Cada declaración recibe su **propia celda** de memoria (no se reutilizan entre bloques); el límite global es `MAX_CELDAS_GLOBALES = 512`, y también guarda el *pool* de literales de cadena.
- `RegistroSimbolo`: tipo, línea, dirección, `esFuncion`, firma, celdas locales.
- **Sin errores en cascada**: una expresión con error recibe un tipo especial `ERROR` que las reglas aceptan sin generar más mensajes. Así `b := x + 1` con `x` mal declarada produce un solo error.

### Mensajes reales (extraídos del analizador)
- "la variable 'y' no está declarada"
- "la variable 'x' ya está declarada en este ámbito (línea N)"
- "asignación incompatible a 'x': se esperaba int ..."
- "la condición del if debe ser bool, se encontró int"
- "read sólo acepta variables int"
- "'x' espera 2 argumento(s) y se recibieron 1"
- "argumento 1 de 'mostrar': se esperaba int ..."
- "el procedimiento 'p' no devuelve valor y no puede usarse en una expresión"
- "la función 'f' debe contener al menos un return"
- "return sólo se permite dentro de una subrutina"
- "se excede el área de memoria global (512 celdas)"

## Ejemplo resuelto
Programa `11_error_semantico.tny` del material de la presentación:
```
int x;
bool b;
x := true;      { int := bool }
y := 5;         { variable no declarada }
if x then       { condición no bool }
  write x
end;
b := x + 1      { int asignado a bool }
```
Pasada semántica: tabla global = {x:int, b:bool}.
1. `x := true`: tipo(true)=bool ≠ int, error de asignación.
2. `y := 5`: `BuscarSimbolo("y")` falla, error de variable no declarada.
3. `if x`: x es int, la condición debe ser bool.
4. `b := x + 1`: `x + 1` es int, b es bool, error.
Cuatro errores en una sola pasada, ordenados por línea; el compilador sale con código 1 y no crea el `.tm`.

Ejemplo de ámbito:
```
int x; x := 1;
if true then int x; x := 9; write x end;   { escribe 9: x del bloque sombrea }
write x                                     { escribe 1 }
```

## Errores comunes
- No cerrar el ámbito al salir de un bloque (símbolos "filtrados").
- Buscar redeclaraciones en toda la cadena en vez de solo en el ámbito actual (impediría el sombreado).
- Generar errores en cascada con tipos desconocidos.
- Olvidar chequear tipos de parámetros formales vs. argumentos.
- Permitir `return` en el programa principal.

## Ejercicios propuestos
1. ¿Es válido `int x; if true then int x; x := 1 end`? *Resp.: sí, `x` del bloque sombrea a la global.*
2. ¿Y `int x; int x;`? *Resp.: no: redeclaración en el mismo ámbito.*
3. ¿Qué tipo tiene `A[i*2+1]` si `int A[8]` y `i:int`? *Resp.: int.*
4. ¿Por qué la comprobación de tipos se hace en una pasada aparte? *Resp.: separa responsabilidades, permite reportar todos los errores semánticos ordenados y deja el parser sin lógica de tipos.*

## Conexiones
Los símbolos aportan direcciones al generador: [[Compiladores - 10 Generación de Código Tiny++ y Marcos de Activación]]. Estructuras de hash y pilas: [[Estructura de Datos]]. Reglas de diagnóstico: [[Compiladores - 11 Optimización y Manejo de Errores]].

## Fuente
`~/Documentos/UNET/Compiladores/Compilador/src/main/java/ve/edu/unet/{AnalizadorSemantico,TablaSimbolos,Ambito,RegistroSimbolo}.java`, `Compilador/README.md` y `Presentacion/ejemplos/11_error_semantico.tny`, `12_error_parametros.tny`.
