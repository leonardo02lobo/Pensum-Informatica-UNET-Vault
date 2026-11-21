---
tags: [clase, semestre-I]
materia: Computación I
---
# Computación I - Funciones y modularización en C

Materia: [[Computación I]]  
Anterior: [[Computación I - Estructuras de control repetitivas y validación]] · Siguiente: [[Computación I - Arreglos unidimensionales y cadenas de caracteres]]

## Contexto y objetivo
A medida que un programa crece, concentrar toda la lógica en `main` lo vuelve ilegible y difícil de depurar. La **modularización** consiste en dividir un problema grande en subproblemas independientes implementados como **funciones**. En esta clase aprenderás a declarar prototipos, definir funciones con y sin retorno, comprender el paso de parámetros por valor y gestionar el ámbito de las variables.

## 1. Anatomía de una función en C
Una función tiene:
1. **Prototipo (declaración)**: se coloca antes de `main` para informar al compilador el nombre, tipo de retorno y tipos de parámetros.
2. **Definición**: contiene el bloque de código que ejecuta la tarea.
3. **Llamada (invocación)**: punto donde se transfiere el control a la función.

```c
#include <stdio.h>

/* Prototipo */
float calcular_area_triangulo(float base, float altura);
void imprimir_linea(int n);

int main(void) {
    float b = 5.0f, h = 3.0f;
    imprimir_linea(20);
    printf("Área: %.2f\n", calcular_area_triangulo(b, h));
    imprimir_linea(20);
    return 0;
}

/* Definiciones */
float calcular_area_triangulo(float base, float altura) {
    return (base * altura) / 2.0f;
}

void imprimir_linea(int n) {
    for (int i = 0; i < n; i++) printf("-");
    printf("\n");
}
```
- Una función `void` no devuelve valor (ejecuta una acción, como imprimir un menú o dibujar un tablero).
- La instrucción `return expr;` finaliza inmediatamente la función y entrega `expr` al punto de llamada.

## 2. Paso de parámetros por valor
En C, los parámetros escalares (`int`, `float`, `char`, `double`) se pasan **por valor**: la función recibe una **copia** del argumento original. Modificar el parámetro dentro de la función **no altera** la variable original en `main`.

```c
void intentar_duplicar(int x) {
    x = x * 2; /* Solo modifica la copia local x */
}
```
Si `a = 5` y llamamos `intentar_duplicar(a);`, `a` sigue valiendo `5`. Para que `main` obtenga el nuevo valor, la función debe retornarlo (`a = duplicar(a);`) o recibir un puntero/arreglo.

## 3. Ámbito (*scope*) de las variables
- **Variables locales**: declaradas dentro de una función o bloque `{}`. Solo existen mientras esa función se ejecuta y no son visibles fuera de ella.
- **Variables globales**: declaradas fuera de todas las funciones. Son accesibles desde cualquier función, pero su uso excesivo dificulta el mantenimiento porque cualquier función puede modificarlas inesperadamente. En lo posible, pasa los datos mediante parámetros y retorna resultados.

## 4. Ejemplo resuelto: menú modular de conversiones
Un programa bien modularizado separa la lectura validada de las funciones de cálculo:

```c
#include <stdio.h>

float celsius_a_fahrenheit(float c);
int leer_opcion(void);

int main(void) {
    int opc;
    float temp;

    do {
        opc = leer_opcion();
        if (opc == 1) {
            printf("Grados Celsius: ");
            scanf("%f", &temp);
            printf("Fahrenheit: %.2f\n", celsius_a_fahrenheit(temp));
        }
    } while (opc != 2);

    return 0;
}

int leer_opcion(void) {
    int op;
    do {
        printf("\n1. Convertir C -> F\n2. Salir\nOpción: ");
        scanf("%d", &op);
    } while (op < 1 || op > 2);
    return op;
}

float celsius_a_fahrenheit(float c) {
    return c * 9.0f / 5.0f + 32.0f;
}
```

## Errores comunes
- **Olvidar el prototipo** cuando la función se define después de `main`: el compilador puede asumir un retorno `int` implícito y generar errores de tipos.
- **Imprimir dentro de una función de cálculo en vez de usar `return`**: limita la reutilización de la función en otras expresiones.
- **Poner `;` al final de la cabecera de la definición**: `int suma(int a, int b); { ... }` produce error de sintaxis.
- **Esperar que el paso por valor modifique una variable de `main`**.

## Ejercicios propuestos
1. Escribe una función `int es_par(int n)` que retorne `1` si `n` es par y `0` si es impar.  
   *Respuesta:* `int es_par(int n) { return n % 2 == 0; }`.
2. Escribe una función `int maximo3(int a, int b, int c)` que devuelva el mayor de tres enteros.  
   *Respuesta:* Comparar `int m = a; if (b > m) m = b; if (c > m) m = c; return m;`.

## Conexiones
- Materia principal: [[Computación I]]
- Anterior: [[Computación I - Estructuras de control repetitivas y validación]]
- Siguiente: [[Computación I - Arreglos unidimensionales y cadenas de caracteres]]
- Continuidad: [[Programación I]] (métodos y encapsulamiento en C++/Java).

## Fuente
Programa oficial de [[Computación I]]; `Material/tercer parcial seccion 15_a39104ee41eb4a5a6b4e097327931475.pdf` (uso de función secundaria con validación).
