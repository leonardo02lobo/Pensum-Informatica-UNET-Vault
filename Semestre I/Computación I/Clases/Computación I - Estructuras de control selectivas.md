---
tags: [clase, semestre-I]
materia: Computación I
---
# Computación I - Estructuras de control selectivas

Materia: [[Computación I]]  
Anterior: [[Computación I - Elementos del lenguaje C, tipos y operadores]] · Siguiente: [[Computación I - Estructuras de control repetitivas y validación]]

## Contexto y objetivo
Un programa secuencial ejecuta siempre las mismas instrucciones en el mismo orden. Para tomar decisiones según los datos de entrada, C ofrece las **estructuras de control selectivas** (`if`, `if-else`, `if-else if` encadenado y `switch`). El objetivo de esta clase es dominar la construcción de condiciones lógicas correctas y elegir la estructura selectiva más limpia para cada problema.

## 1. Selección simple y doble: `if` e `if-else`
- **Simple (`if`)**: ejecuta un bloque solo si la condición es verdadera (distinta de `0` en C).
- **Doble (`if-else`)**: ejecuta un bloque si la condición es verdadera y otro alternativo si es falsa.

```c
if (nota >= 10) {
    printf("Aprobado\n");
} else {
    printf("Reprobado\n");
}
```

> [!note] Llaves `{}`
> Aunque C permite omitir las llaves cuando el bloque tiene una sola instrucción, usarlas siempre previene errores difíciles de detectar al agregar nuevas líneas dentro de una rama.

## 2. Selección múltiple anidada y encadenada (`if - else if - else`)
Cuando existen varias condiciones mutuamente excluyentes por rangos (por ejemplo, escalas de notas o tarifas por tramo), se encadenan bloques `else if`:

```c
if (promedio >= 18) {
    printf("Sobresaliente\n");
} else if (promedio >= 15) {
    printf("Distinguido\n");
} else if (promedio >= 10) {
    printf("Aprobado\n");
} else {
    printf("Reprobado\n");
}
```
La evaluación es descendente: al cumplirse la primera condición verdadera, se ejecuta su bloque y se omiten las demás ramas.

## 3. Selección múltiple discreta: `switch`
La sentencia `switch` compara una **expresión entera o carácter** (`int` o `char`) contra valores constantes (`case`). No sirve para rangos (`x > 10`) ni para cadenas de texto (`"hola"`).

```c
switch (opcion) {
    case 'A':
    case 'a':
        printf("Alta de registro\n");
        break;
    case 'B':
    case 'b':
        printf("Baja de registro\n");
        break;
    default:
        printf("Opción no válida\n");
}
```

- **`break`**: detiene la ejecución del `switch`. Si se omite, ocurre *fall-through* (continúa ejecutando el siguiente `case`), lo cual solo es útil cuando varios casos comparten la misma acción (como `'A'` y `'a'`).
- **`default`**: rama opcional que se ejecuta si ningún `case` coincide.

## 4. Operador ternario `?:`
Para asignaciones condicionales breves existe el operador ternario:
```c
int mayor = (a > b) ? a : b;
```
Equivale a un `if-else` que asigna `a` si `a > b` es verdadero, o `b` en caso contrario.

## 5. Ejemplo resuelto: calculadora de tarifa de envío
En el tercer parcial de Computación I suele evaluarse la combinación de validación, funciones y `switch`. Veamos un ejemplo de `switch` para calcular un recargo según zona (`'Z'`, `'D'`, `'A'`):

```c
#include <stdio.h>

int main(void) {
    char zona;
    float peso, costo_base = 10.0f, total;

    printf("Zona (Z, D, A) y peso (kg): ");
    scanf(" %c %f", &zona, &peso);

    switch (zona) {
        case 'Z':
            total = costo_base + peso * 1.5f;
            break;
        case 'D':
            total = costo_base + peso * 2.2f;
            break;
        case 'A':
            total = costo_base + peso * 3.0f;
            break;
        default:
            printf("Zona inválida.\n");
            return 1;
    }

    printf("Total del envío: %.2f\n", total);
    return 0;
}
```

## Errores comunes
- **Escribir `if (x = 5)` en lugar de `if (x == 5)`**: asigna `5` a `x` y la condición siempre resulta verdadera.
- **Colocar punto y coma tras el `if`**: `if (x > 0); { ... }` termina el `if` vacío y el bloque se ejecuta siempre.
- **Olvidar `break` en un `switch`**: provoca que se ejecuten las instrucciones de los casos siguientes.
- **Escribir condiciones matemáticas encadenadas**: en C `if (10 <= x <= 20)` es un error lógico (se evalúa `(10 <= x)` que da `0` o `1`, y luego `0 <= 20` o `1 <= 20`, siempre verdadero). Debe escribirse `if (x >= 10 && x <= 20)`.

## Ejercicios propuestos
1. Escribe un programa que lea un año y determine si es bisiesto (divisible entre 4 y no entre 100, o divisible entre 400).  
   *Respuesta:* `if ((anio % 4 == 0 && anio % 100 != 0) || (anio % 400 == 0))`.
2. Convierte el siguiente `switch` a `if-else if`: `switch(n){ case 1: x=10; break; case 2: x=20; break; default: x=0; }`.  
   *Respuesta:* `if (n == 1) x = 10; else if (n == 2) x = 20; else x = 0;`.

## Conexiones
- Materia principal: [[Computación I]]
- Anterior: [[Computación I - Elementos del lenguaje C, tipos y operadores]]
- Siguiente: [[Computación I - Estructuras de control repetitivas y validación]]
- Relación con lógica: [[Matemática Discreta - Lógica proposicional y cuantificadores]] (tablas de verdad y conectivos lógicos).

## Fuente
Programa oficial de [[Computación I]]; `Material/tercer parcial seccion 15_a39104ee41eb4a5a6b4e097327931475.pdf` (patrón de selección con `switch`).
