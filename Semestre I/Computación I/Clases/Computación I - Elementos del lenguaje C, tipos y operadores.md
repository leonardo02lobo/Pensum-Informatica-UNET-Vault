---
tags: [clase, semestre-I]
materia: Computación I
---
# Computación I - Elementos del lenguaje C, tipos y operadores

Materia: [[Computación I]]  
Anterior: [[Computación I - Introducción a la computación y algoritmos]] · Siguiente: [[Computación I - Estructuras de control selectivas]]

## Contexto y objetivo
Una vez formulado el algoritmo, el siguiente paso es traducirlo a **lenguaje C**. En esta clase se estudia la anatomía mínima de un programa en C, la declaración de variables y constantes, los tipos de datos primitivos, la entrada y salida formateada con `scanf` y `printf`, y las reglas de precedencia de operadores (incluyendo la temida división entera).

## 1. Estructura básica de un programa en C
Todo programa ejecutable en C parte de la función `main`:

```c
#include <stdio.h>      /* Biblioteca estándar de entrada/salida */
#define IVA 0.16f       /* Constante simbólica mediante macro */

int main(void) {
    const float DESCUENTO = 0.10f; /* Constante tipada */
    float precio, total;

    printf("Ingrese el precio base: ");
    scanf("%f", &precio);

    total = precio * (1.0f - DESCUENTO) * (1.0f + IVA);
    printf("Total a pagar: %.2f\n", total);

    return 0;           /* 0 indica terminación exitosa */
}
```

- `#include <stdio.h>`: incorpora las declaraciones de `printf` y `scanf`.
- `#define NOMBRE valor`: sustituye texto antes de compilar (no ocupa memoria ni lleva `;`).
- `const tipo NOMBRE = valor;`: crea una constante con tipo verificable por el compilador.

## 2. Tipos de datos y especificadores de formato
Las variables son espacios de memoria identificados por un nombre válido (letras, dígitos y `_`, sin empezar por dígito ni usar palabras reservadas).

| Tipo en C | Uso habitual | Tamaño típico | Especificador `printf`/`scanf` |
|---|---|---|---|
| `int` | Enteros con signo | 4 bytes | `%d` |
| `float` | Reales de precisión simple | 4 bytes | `%f` |
| `double` | Reales de doble precisión | 8 bytes | `%f` (printf) / `%lf` (scanf) |
| `char` | Un carácter ASCII | 1 byte | `%c` |

> [!tip] Lectura de caracteres con `scanf`
> Al leer un `char` después de un número, el salto de línea `\n` previo queda en el búfer de entrada. Coloca un espacio antes de `%c` (`scanf(" %c", &opc);`) para descartar espacios y saltos de línea residuales, tal como se hace en programas interactivos.

## 3. Operadores y precedencia
### Operadores aritméticos
`+`, `-`, `*`, `/`, `%` (módulo o residuo, **solo aplicable a enteros**).
- **División entera vs. real**: en C, si ambos operandos de `/` son `int`, el resultado se trunca a entero: `5 / 2` evalúa a `2`. Para obtener `2.5`, al menos un operando debe ser real o usar conversión explícita (*casting*): `(float)5 / 2`.

### Operadores relacionales y lógicos
- **Relacionales**: `==` (igual), `!=` (distinto), `<`, `<=`, `>`, `>=`. Devuelven `1` (verdadero) o `0` (falso).
- **Lógicos**: `&&` (Y lógico), `||` (O lógico), `!` (negación).
- **Asignación compuesta e incremento**: `+=`, `-=`, `*=`, `/=`, `++`, `--`.

### Precedencia (de mayor a menor)
1. Paréntesis `()`
2. Unarios: `!`, `++`, `--`, `-` (signo), `(tipo)` (cast)
3. Multiplicativos: `*`, `/`, `%`
4. Aditivos: `+`, `-`
5. Relacionales: `<`, `<=`, `>`, `>=`
6. Igualdad: `==`, `!=`
7. Lógicos: `&&` luego `||`
8. Asignación: `=`, `+=`, etc.

## 4. Ejemplo resuelto: conversión de segundos a horas, minutos y segundos
Dado un total entero de segundos `seg`, descomponerlo en `hh:mm:ss`:

```c
#include <stdio.h>

int main(void) {
    int total_seg, horas, minutos, segundos;

    printf("Ingrese cantidad de segundos: ");
    scanf("%d", &total_seg);

    horas = total_seg / 3600;
    minutos = (total_seg % 3600) / 60;
    segundos = total_seg % 60;

    printf("Equivalente: %02d:%02d:%02d\n", horas, minutos, segundos);
    return 0;
}
```
Si `total_seg = 3725`: `horas = 1`, `3725 % 3600 = 125`, `minutos = 125 / 60 = 2`, `segundos = 125 % 60 = 5`, imprimiendo `01:02:05`.

## Errores comunes
- **Olvidar el operador `&` en `scanf`**: `scanf("%d", x);` provoca un fallo de segmentación porque `scanf` necesita la dirección de memoria (`&x`).
- **División entera accidental**: escribir `float prom = suma / n;` cuando `suma` y `n` son `int`. Debe escribirse `(float)suma / n`.
- **Confundir `=` con `==`**: `=` asigna un valor; `==` compara dos valores.
- **Usar `%` con `float` o `double`**: el operador módulo solo funciona con tipos enteros.

## Ejercicios propuestos
1. ¿Qué valor toma `r` en `int a = 7, b = 2; float r = a / b + 0.5;`?  
   *Respuesta:* `3.5`, porque `a / b` es división entera (`3`) y luego `3 + 0.5` da `3.5`.
2. Escribe una expresión lógica en C que sea verdadera si `edad` está entre `18` y `65` inclusive.  
   *Respuesta:* `(edad >= 18 && edad <= 65)`.
3. Escribe un programa que lea el radio de un círculo y muestre su área ($A = \pi r^2$) con 3 decimales.  
   *Respuesta:* Usar `#define PI 3.14159265` y `printf("%.3f\n", PI * r * r);`.

## Conexiones
- Materia principal: [[Computación I]]
- Nota de referencia rápida: Lenguaje C - fundamentos y ejemplos
- Anterior: [[Computación I - Introducción a la computación y algoritmos]]
- Siguiente: [[Computación I - Estructuras de control selectivas]]

## Fuente
Programa oficial de [[Computación I]] y notas de sintaxis en Lenguaje C - fundamentos y ejemplos; Kernighan y Ritchie, *El lenguaje de programación C*.
