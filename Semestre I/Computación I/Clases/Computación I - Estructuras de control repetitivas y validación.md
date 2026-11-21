---
tags: [clase, semestre-I]
materia: Computación I
---
# Computación I - Estructuras de control repetitivas y validación

Materia: [[Computación I]]  
Anterior: [[Computación I - Estructuras de control selectivas]] · Siguiente: [[Computación I - Funciones y modularización en C]]

## Contexto y objetivo
Muchas tareas en programación exigen repetir un conjunto de instrucciones un número conocido o desconocido de veces: procesar listas de datos, calcular sumatorias o exigir al usuario que ingrese un dato válido. En esta clase se estudian los tres ciclos de C (`while`, `do-while` y `for`), junto con los patrones esenciales de **contadores**, **acumuladores**, **banderas** y **validación de entrada**.

## 1. Los tres ciclos en C
### `while` (cero o más repeticiones)
Evalúa la condición *antes* de entrar al cuerpo. Si inicialmente es falsa, el bloque no se ejecuta ni una vez.
```c
int i = 1;
while (i <= 5) {
    printf("%d ", i);
    i++;
}
```

### `do-while` (al menos una repetición)
Ejecuta el bloque *primero* y evalúa la condición al final (lleva `;` obligatorio). Es el ciclo estándar para **menús interactivos** y **validación de entrada**, como se observa en `Recursos Humanos.c`.
```c
int opcion;
do {
    printf("1. Consultar  2. Salir\nOpción: ");
    scanf("%d", &opcion);
} while (opcion < 1 || opcion > 2);
```

### `for` (número conocido de iteraciones)
Compacta inicialización, condición y actualización en una sola línea:
```c
for (int i = 0; i < n; i++) {
    /* cuerpo del ciclo */
}
```
Orden de ejecución: (1) inicialización una sola vez; (2) condición; (3) cuerpo; (4) incremento; vuelta a (2).

## 2. Contadores, acumuladores y banderas
- **Contador**: variable entera que incrementa (o decrementa) en una cantidad fija (normalmente `1`) cada vez que ocurre un evento. Debe inicializarse en `0`: `cont++;`.
- **Acumulador**: variable que va sumando (o multiplicando) valores variables en cada iteración. Debe inicializarse en el elemento neutro (`0` para suma, `1` para producto): `suma += nota;`.
- **Bandera (*flag*)**: variable entera o booleana (`0`/`1` o `bool` de `<stdbool.h>`) que indica si ocurrió un estado o condición (por ejemplo, si se encontró un elemento).

## 3. Validación de entrada y control con centinela
- **Validación**: repetir la lectura con `do-while` mientras el dato esté *fuera* del rango permitido.
- **Ciclo controlado por centinela**: leer datos hasta que el usuario introduzca un valor especial de parada (por ejemplo, `-1` para terminar una serie de notas).

## 4. Ejemplo resuelto: promedio de notas válidas con centinela
Leer calificaciones entre `0` y `20` hasta ingresar `-1`. Mostrar cuántas se ingresaron, el promedio y la nota máxima.

```c
#include <stdio.h>

int main(void) {
    float nota, suma = 0.0f, max = -1.0f;
    int cont = 0;

    printf("Ingrese notas (0-20), o -1 para terminar:\n");
    scanf("%f", &nota);

    while (nota != -1) {
        if (nota >= 0.0f && nota <= 20.0f) {
            suma += nota;
            cont++;
            if (nota > max) {
                max = nota;
            }
        } else {
            printf("Nota fuera de rango, ignorada.\n");
        }
        scanf("%f", &nota);
    }

    if (cont > 0) {
        printf("Cantidad: %d | Promedio: %.2f | Máxima: %.2f\n",
               cont, suma / cont, max);
    } else {
        printf("No se ingresaron notas válidas.\n");
    }
    return 0;
}
```

## Errores comunes
- **No inicializar contadores o acumuladores**: usar `suma += x;` sin `suma = 0;` suma sobre basura de memoria.
- **Ciclo infinito**: olvidar actualizar la variable de control dentro de un `while` o escribir `while (i = 10)` en lugar de `while (i < 10)`.
- **Error de condición en validación**: escribir `while (opc >= 1 && opc <= 4)` para validar un menú (el ciclo repite *cuando el dato es válido* en vez de cuando es *inválido*). La condición de repetición debe ser la negación: `while (opc < 1 || opc > 4)`.
- **Dividir por cero** al calcular un promedio si el usuario ingresa el centinela de inmediato (`cont == 0`).

## Ejercicios propuestos
1. Escribe un ciclo `for` que imprima los múltiplos de `3` entre `1` y `30`.  
   *Respuesta:* `for (int i = 3; i <= 30; i += 3) printf("%d ", i);`.
2. Valida con `do-while` que el usuario ingrese únicamente `'S'` o `'N'`.  
   *Respuesta:* `do { scanf(" %c", &r); } while (r != 'S' && r != 'N');`.
3. Calcula el factorial $n! = 1 \cdot 2 \cdots n$ para un entero $n \ge 0$ usando un acumulador multiplicativo.  
   *Respuesta:* Inicializar `long fact = 1;` y multiplicar `fact *= i;` de `1` a `n`.

## Conexiones
- Materia principal: [[Computación I]]
- Anterior: [[Computación I - Estructuras de control selectivas]]
- Siguiente: [[Computación I - Funciones y modularización en C]]

## Fuente
Programa oficial de [[Computación I]]; `Material/Recursos Humanos.c` (validación de menú con `do-while`, contadores, acumuladores y banderas).
