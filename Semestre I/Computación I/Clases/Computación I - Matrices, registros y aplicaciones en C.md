---
tags: [clase, semestre-I]
materia: Computación I
---
# Computación I - Matrices, registros y aplicaciones en C

Materia: [[Computación I]]  
Anterior: [[Computación I - Arreglos unidimensionales y cadenas de caracteres]]

## Contexto y objetivo
Los proyectos integradores de Computación I (como la gestión de asistencia por estados en `Embajada.c` o el tablero $10 \times 10$ del *Juego de los Barquitos*) requieren estructuras bidimensionales y agrupación de datos heterogéneos. En esta última clase se estudian las **matrices**, las **estructuras (`struct`)** y nociones introductorias de **archivos** y **punteros**, consolidando el puente hacia [[Programación I]].

## 1. Arreglos bidimensionales (matrices)
Una matriz es una tabla de `FILAS` $\times$ `COLUMNAS` del mismo tipo:
```c
int tablero[10][10]; /* 10 filas (0..9), 10 columnas (0..9) */
```
Su recorrido estándar utiliza **dos ciclos `for` anidados**: el externo para las filas (`i`) y el interno para las columnas (`j`).

### Ejemplo: promedio por fila (patrón de `Embajada.c`)
Dada una matriz `asistencia[24][20]` (24 estados $\times$ 20 días), el promedio de cada estado se calcula reiniciando el acumulador en cada fila:
```c
for (int i = 0; i < 24; i++) {
    int acumulador = 0;
    for (int j = 0; j < 20; j++) {
        acumulador += asistencia[i][j];
    }
    promedio[i] = (float)acumulador / 20.0f;
}
```
Al pasar una matriz a una función en C, es obligatorio especificar al menos la segunda dimensión:
```c
void mostrar_tablero(char tab[][10], int filas);
```

## 2. Registros (`struct`)
Mientras un arreglo agrupa datos del mismo tipo, un `struct` agrupa campos de **distintos tipos** pertenecientes a una misma entidad (por ejemplo, un empleado o un estudiante), evitando mantener múltiples arreglos paralelos dispersos:

```c
#include <stdio.h>

struct Empleado {
    char nombre[30];
    char cedula[12];
    float salario;
};

int main(void) {
    struct Empleado emp = {"María Arias", "E30567345", 1500.70f};
    printf("%s (%s): %.2f\n", emp.nombre, emp.cedula, emp.salario);
    return 0;
}
```
También pueden declararse arreglos de estructuras: `struct Empleado nomina[40];`, accediendo al salario del empleado `i` mediante `nomina[i].salario`.

## 3. Nociones complementarias: punteros básicos y archivos
Según el alcance del lapso, se introducen dos herramientas clave para la persistencia y el manejo de memoria:
- **Punteros**: variables que almacenan la dirección de memoria de otra variable (`int *p = &x;`). Permiten modificar variables externas desde una función (*paso por referencia simulado*).
- **Archivos de texto (`FILE *`)**: permiten guardar datos en disco para no perderlos al cerrar el programa:
  ```c
  FILE *f = fopen("datos.txt", "w");
  if (f != NULL) {
      fprintf(f, "Resultado: %d\n", 42);
      fclose(f);
  }
  ```

## 4. Integración en un proyecto de consola
Un proyecto completo en C (como el *Juego de los Barquitos* o un sistema de nómina) combina:
1. Matrices para tableros o tablas de datos.
2. Funciones especializadas (`inicializar_tablero`, `mostrar_tablero`, `validar_coordenada`).
3. Menú principal con `do-while` y `switch`.
4. Validaciones estrictas de límites (`fila >= 0 && fila < 10`) y estado de casillas antes de realizar cambios.

## Errores comunes
- **Invertir filas y columnas** al indexar `m[j][i]` cuando la matriz es `m[FILAS][COLS]`.
- **No reiniciar el acumulador** antes del ciclo interno al sumar por filas o columnas.
- **Omitir el número de columnas** en el parámetro de una función que recibe una matriz (`int m[][]` no compila).
- **No cerrar un archivo con `fclose`** o usar el puntero `FILE *` sin verificar `f != NULL`.

## Ejercicios propuestos
1. Escribe un fragmento en C que sume los elementos de la diagonal principal de una matriz cuadrada `int m[4][4]`.  
   *Respuesta:* `int suma = 0; for (int i = 0; i < 4; i++) suma += m[i][i];`.
2. Define un `struct Producto` con `codigo` (`int`), `nombre` (`char[25]`) y `precio` (`float`).  
   *Respuesta:* `struct Producto { int codigo; char nombre[25]; float precio; };`.

## Conexiones
- Materia principal: [[Computación I]]
- Anterior: [[Computación I - Arreglos unidimensionales y cadenas de caracteres]]
- Desbloquea: [[Programación I]] (orientación a objetos, clases a partir de `struct`) y [[Estructura de Datos]] (listas, punteros y matrices).

## Fuente
Programa oficial de [[Computación I]]; `Material/Embajada.c`, `Material/Recursos Humanos.c` y `Material/Juego de barcos_f97b4d5c2041efdc7686d838672c9346.pdf`.
