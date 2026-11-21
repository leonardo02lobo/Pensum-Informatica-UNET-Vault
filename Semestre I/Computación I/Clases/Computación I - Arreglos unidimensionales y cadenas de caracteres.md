---
tags: [clase, semestre-I]
materia: Computación I
---
# Computación I - Arreglos unidimensionales y cadenas de caracteres

Materia: [[Computación I]]  
Anterior: [[Computación I - Funciones y modularización en C]] · Siguiente: [[Computación I - Matrices, registros y aplicaciones en C]]

## Contexto y objetivo
Hasta ahora cada variable almacenaba un único dato. Cuando necesitamos manejar decenas de notas, salarios o nombres, necesitamos estructuras indexadas. Esta clase cubre los **arreglos unidimensionales (vectores)**, los algoritmos clásicos sobre vectores (recorrido, búsqueda secuencial, ordenamiento burbuja) y el manejo de **cadenas de caracteres** (`char[]` y `<string.h>`).

## 1. Declaración e indexación de vectores
Un **vector** es una colección contigua de elementos del **mismo tipo** bajo un único nombre. En C, los índices comienzan en **`0`** y terminan en **`N - 1`**.

```c
int notas[5];                      /* 5 enteros: notas[0] .. notas[4] */
float precios[3] = {10.5f, 20.0f, 5.25f};
int ceros[10] = {0};               /* Inicializa los 10 elementos en 0 */
```

Para pasar un vector a una función, se pasa el nombre del arreglo (en realidad su dirección base, por lo que **sí puede modificarse** dentro de la función) junto con su tamaño `n`:
```c
float promedio(int v[], int n) {
    int suma = 0;
    for (int i = 0; i < n; i++) {
        suma += v[i];
    }
    return (float)suma / n;
}
```

## 2. Búsqueda y ordenamiento simple
### Búsqueda secuencial
Recorre el vector desde `0` hasta `n - 1` buscando un `objetivo`. Retorna el índice si lo encuentra, o `-1` si no existe:
```c
int buscar(int v[], int n, int objetivo) {
    for (int i = 0; i < n; i++) {
        if (v[i] == objetivo) return i;
    }
    return -1;
}
```

### Ordenamiento por burbuja (*Bubble Sort*)
Compara pares adyacentes y los intercambia si están en orden incorrecto, repitiendo pasadas hasta ordenar el vector:
```c
void ordenar_burbuja(int v[], int n) {
    int aux;
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            if (v[j] > v[j + 1]) {
                aux = v[j];
                v[j] = v[j + 1];
                v[j + 1] = aux;
            }
        }
    }
}
```

## 3. Cadenas de caracteres y `<string.h>`
En C no existe un tipo `string` nativo: una cadena es un **arreglo de `char` terminado en el carácter nulo `'\0'`**. Por ello, para guardar una palabra de hasta 19 letras se necesita un arreglo de tamaño `20`.

```c
char nombre[20] = "UNET"; /* Contiene 'U','N','E','T','\0' */
```

Funciones esenciales de `<string.h>`:
- `strlen(s)`: devuelve la longitud de `s` (sin contar `'\0'`).
- `strcpy(dest, orig)`: copia `orig` dentro de `dest` (no se puede hacer `dest = orig;`).
- `strcmp(a, b)`: compara alfabéticamente; devuelve **`0` si son iguales**, `< 0` si `a < b` y `> 0` si `a > b`.
- `strcat(dest, orig)`: concatena `orig` al final de `dest`.

> [!warning] Lectura segura de cadenas
> `scanf("%s", nombre);` (sin `&`, porque el nombre del arreglo ya es una dirección) lee solo hasta el primer espacio. Para leer líneas completas con espacios se prefiere `fgets(nombre, sizeof(nombre), stdin);`.

## 4. Ejemplo resuelto: búsqueda de un estudiante en arreglos paralelos
En `Recursos Humanos.c` se usan arreglos paralelos para asociar datos de la misma entidad en el mismo índice `i`:
```c
char nombres[3][15] = {"José", "Pedro", "María"};
float salarios[3]   = {3700.30f, 2800.00f, 1500.70f};
```
Si buscamos `"Pedro"` con `strcmp(nombres[i], "Pedro") == 0`, obtenemos el índice `i = 1` y consultamos su salario en `salarios[1]`.

## Errores comunes
- **Desbordamiento de índice (*out-of-bounds*)**: acceder a `v[n]` cuando los índices válidos son `0 .. n-1`. C no detiene el programa automáticamente y corrompe memoria vecina.
- **Comparar cadenas con `==`**: `if (a == b)` compara direcciones de memoria, no el contenido; debe usarse `strcmp(a, b) == 0`.
- **Asignar cadenas con `=`**: `nombre = "Ana";` es inválido fuera de la declaración; usar `strcpy(nombre, "Ana");`.
- **Olvidar espacio para `'\0'`**: declarar `char s[4] = "Hola";` trunca o omite el terminador nulo.

## Ejercicios propuestos
1. Escribe una función `int contar_mayores(float v[], int n, float limite)` que cuente cuántos elementos superan `limite`.  
   *Respuesta:* Recorrer con `for`, incrementar `c++` cuando `v[i] > limite`, retornar `c`.
2. ¿Qué imprime `printf("%d", strcmp("Ana", "Ana"));`?  
   *Respuesta:* `0`, porque ambas cadenas son idénticas.

## Conexiones
- Materia principal: [[Computación I]]
- Anterior: [[Computación I - Funciones y modularización en C]]
- Siguiente: [[Computación I - Matrices, registros y aplicaciones en C]]
- Continuidad: [[Estructura de Datos]] (arreglos dinámicos, búsqueda binaria y ordenamientos avanzados).

## Fuente
Programa oficial de [[Computación I]]; [[Computación I - Elementos del lenguaje C, tipos y operadores]]; `Material/Recursos Humanos.c` (arreglos paralelos y uso de `strcpy`/`strcasecmp`).
