---
tags: [materia, semestre-I]
semestre: I
---
# Computación I

**Semestre:** [[Semestre I]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- _Ninguna_

## Desbloquea
- [[Programación I]]

## Apuntes

### Descripción general y objetivos
Computación I (código 0415102T según los documentos del Material) es la materia de entrada a la programación: se aprende a **resolver problemas con algoritmos** y a codificarlos en **lenguaje C** de forma estructurada. Es prelación directa de [[Programación I]] (junto con [[Matemática Discreta]]). Objetivos: pensar de forma algorítmica, dominar variables, estructuras de control, funciones, arreglos, cadenas y (según el lapso) estructuras y archivos, y depurar programas de consola.

Nota hija: [[Computación I - Elementos del lenguaje C, tipos y operadores]].

### Contenido programático (verificar con el programa oficial)
1. **Introducción a la computación**: hardware/software, sistema binario, lenguajes de programación, compilador vs. intérprete, ciclo edición-compilación-ejecución.
2. **Algoritmos**: definición y propiedades (finito, preciso, definido), pseudocódigo, diagramas de flujo, análisis de problemas (entrada-proceso-salida).
3. **Elementos de C**: estructura de un programa, tipos de datos (`int`, `float`, `double`, `char`), constantes (`#define`, `const`), operadores aritméticos, relacionales y lógicos, `printf`/`scanf`, precedencia.
4. **Estructuras de control**: selección (`if`, `if-else`, `switch`), repetición (`while`, `do-while`, `for`), acumuladores, contadores, banderas, validación de entrada.
5. **Funciones**: prototipos, parámetros por valor, retorno, ámbito (local/global), modularización.
6. **Arreglos**: vectores y matrices, recorridos, búsqueda, ordenamiento simple, cadenas de caracteres (`string.h`).
7. **Temas complementarios**: estructuras (`struct`), punteros básicos y archivos (según el docente).

### Conceptos clave
- **Algoritmo**: secuencia finita de pasos que resuelve un problema.
- **Variable**: espacio de memoria con nombre y tipo. **Acumulador**: variable que suma valores; **contador**: cuenta ocurrencias.
- **Paso por valor**: la función recibe una copia del argumento.
- **Validación**: repetir la lectura hasta que el dato cumpla la condición.
- **Matriz**: arreglo bidimensional `tipo a[filas][cols]`.

### Código de ejemplo
```c
#include <stdio.h>

float promedio(int v[], int n) {
    int suma = 0;
    for (int i = 0; i < n; i++) suma += v[i];
    return (float)suma / n;
}

int main(void) {
    int datos[5], i;
    char opc;
    do {                       /* validación de entrada */
        printf("Ingrese Z, D o A: ");
        scanf(" %c", &opc);
    } while (opc != 'Z' && opc != 'D' && opc != 'A');
    for (i = 0; i < 5; i++) scanf("%d", &datos[i]);
    printf("Promedio: %.2f\n", promedio(datos, 5));
    return 0;
}
```

### Ejemplo resuelto: promedio por fila de una matriz
Dada `asistencia[24][20]` (como en `Embajada.c`: 24 estados x 20 días), el promedio de cada estado se calcula con un acumulador por fila:
```c
for (i = 0; i < 24; i++) {
    acumulador = 0;
    for (j = 0; j < 20; j++) acumulador += asistencia[i][j];
    promedio[i] = (float)acumulador / 20;
}
```

### Relación con otras materias
- [[Programación I]]: continúa con programación orientada a objetos (Java y C++); C++ hereda la sintaxis de C.
- [[Matemática Discreta]]: lógica y conjuntos respaldan el pensamiento algorítmico.
- Más adelante: [[Estructura de Datos]], [[Fundamentos de Lógica Digital]].

### Evaluación y consejos
- Según el Material, hubo exámenes parciales (el tercer parcial 2023-1 valía 50 puntos y pedía un programa con validación, función secundaria y `switch`) y un proyecto (Juego de los Barquitos, 50 puntos). Verificar ponderaciones con el programa del lapso.
- Practica a diario: compila, prueba casos límite, usa nombres claros, comenta el código y separa en funciones.
- Errores comunes: olvidar `&` en `scanf`, `=` vs `==`, desbordar índices de arreglos, división entera.

### Bibliografía recomendada
- Kernighan y Ritchie, *El lenguaje de programación C*.
- Deitel y Deitel, *Cómo programar en C/C++*.
- Joyanes Aguilar, *Fundamentos de programación*.

### Recursos del Material/
- [Embajada.c](Material/Embajada.c): programa de proyecto con matrices de asistencia por estado y menú (Embajada del Reino Unido).
- [Recursos Humanos.c](Material/Recursos%20Humanos.c): gestión de empleados con arreglos paralelos, `struct`-like, salarios y búsquedas.
- [Enunciado Juego de barcos](Material/Juego%20de%20barcos_f97b4d5c2041efdc7686d838672c9346.pdf): especificación del juego Batalla Naval en C (tablero 10x10, validaciones).
- [Tercer parcial sección 15](Material/tercer%20parcial%20seccion%2015_a39104ee41eb4a5a6b4e097327931475.pdf): examen con función y `switch`.
- [integrantes](Material/intregrantes.txt): lista del equipo del proyecto.
- Archivos comprimidos: `2 parcial computacion.rar` y `JUEGO DE LOS BARQUITOS.rar` (código del segundo parcial y del juego).
