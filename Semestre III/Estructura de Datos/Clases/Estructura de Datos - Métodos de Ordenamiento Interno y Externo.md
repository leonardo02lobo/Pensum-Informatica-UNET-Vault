---
tags: [clase, semestre-III]
materia: Estructura de Datos
---
# Estructura de Datos - Métodos de Ordenamiento Interno y Externo

Materia: [[Estructura de Datos]]
Anterior: [[Estructura de Datos - Archivos Binarios y Acceso Directo en C++]]
Siguiente: [[Estructura de Datos - Métodos de Búsqueda y Tablas Hash]]

## Contexto y objetivo

Ordenar colecciones de datos es requisito previo para algoritmos eficientes como la búsqueda binaria y para la generación de reportes. Siguiendo el Tema 2 de [[Estructura de Datos]] (y Ordenamiento y búsqueda), esta clase estudia los algoritmos de **ordenamiento interno** (en memoria RAM) y **ordenamiento externo** (sobre archivos en disco).

## 1. Clasificación de algoritmos de ordenamiento

- **Internos**: todo el conjunto de datos cabe en memoria principal; el costo se mide en comparaciones e intercambios.
- **Externos**: los datos residen en almacenamiento secundario; se minimizan las lecturas y escrituras secuenciales de disco.
- **Estabilidad**: un método es *estable* si conserva el orden relativo de elementos con claves iguales.

## 2. Ordenamiento interno elemental: $O(n^2)$

| Método | Mecanismo | Mejor caso | Peor caso | Estable |
|---|---|---|---|---|
| **Burbuja** | Compara adyacentes e intercambia si están invertidos | $O(n)$ (con bandera) | $O(n^2)$ | Sí |
| **Selección directa** | Busca el mínimo del resto y lo intercambia con la posición $i$ | $O(n^2)$ | $O(n^2)$ | No |
| **Inserción directa** | Inserta cada elemento en la sublista izquierda ya ordenada | $O(n)$ | $O(n^2)$ | Sí |

```cpp
void insercion(int a[], int n) {
    for (int i = 1; i < n; i++) {
        int clave = a[i];
        int j = i - 1;
        while (j >= 0 && a[j] > clave) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = clave;
    }
}
```

## 3. Ordenamiento interno eficiente

- **ShellSort**: generalización de inserción con incrementos decrecientes $h$ (p. ej. $n/2, n/4, \dots, 1$). Complejidad aproximada $O(n^{1.3})$ a $O(n^{1.5})$.
- **QuickSort**: elige un pivote, particiona el arreglo en menores y mayores, y ordena recursivamente. Promedio $O(n \log n)$, peor caso $O(n^2)$ (si el arreglo ya está ordenado y se elige mal el pivote).
- **MergeSort**: divide el arreglo en mitades y las mezcla ordenadas. Siempre $O(n \log n)$ y estable, pero requiere $O(n)$ de memoria auxiliar.
- **RadixSort**: ordena por dígitos/caracteres sin comparaciones; complejidad $O(d \cdot (n + k))$ donde $d$ es el número de dígitos y $k$ la base (10 para decimales).

## 4. Ordenamiento externo: Mezcla directa y Mezcla natural

Cuando el archivo es mayor que la memoria disponible, se usan dos archivos auxiliares (`file1.txt`, `file2.txt`):

1. **Mezcla directa**:
   - **Partición**: distribuye alternadamente bloques (*runs*) de longitud $L = 1, 2, 4, 8, \dots$ entre `file1` y `file2`.
   - **Fusión**: mezcla pares de bloques de tamaño $L$ de ambos auxiliares hacia el archivo principal en bloques ordenados de tamaño $2L$.
   - Número de pasadas: $\lceil \log_2 n \rceil$.

2. **Mezcla natural**:
   - En lugar de bloques de tamaño fijo $L$, detecta las **secuencias ya ordenadas** (*runs* naturales) presentes en el archivo original (cuando $x_{k+1} < x_k$ termina un tramo y se cambia de archivo auxiliar).
   - Si el archivo está parcialmente ordenado, reduce drásticamente el número de pasadas.

## Ejemplo resuelto (RadixSort paso a paso)

Ordenar `[170, 45, 75, 90, 802, 24, 2, 66]`:
1. Por unidades: `[170, 90, 802, 2, 24, 45, 75, 66]`.
2. Por decenas: `[802, 2, 24, 45, 66, 170, 75, 90]`.
3. Por centenas: `[2, 24, 45, 66, 75, 90, 170, 802]`.

## Errores comunes

- Elegir burbuja para arreglos grandes cuando QuickSort o MergeSort son órdenes de magnitud más rápidos.
- En QuickSort, olvidar la condición de parada `if (izq < der)` provocando desbordamiento de pila (*stack overflow*).
- En mezcla externa, no vaciar los elementos restantes de `file1` o `file2` cuando uno de los dos termina primero.

## Ejercicios propuestos

1. ¿Qué algoritmo $O(n^2)$ conviene si el arreglo ya está casi ordenado? ¿Por qué?
2. ¿Cuántas pasadas requiere la mezcla directa para ordenar un archivo de $1024$ registros?

**Respuestas:**
1. Inserción directa, porque en un arreglo casi ordenado su ciclo interno apenas se ejecuta y se aproxima a $O(n)$.
2. $\log_2(1024) = 10$ pasadas.

## Conexiones

- Amplía Ordenamiento y búsqueda.
- Prepara los datos para [[Estructura de Datos - Métodos de Búsqueda y Tablas Hash]].

## Fuente

Basado en `Material/Tema 2-Ordenamiento de busqueda/metodos de ordenamiento.pdf`, `OrdenamientoBurbuja.cpp`, `Ordenamiento-mezcla-directa.cpp` y `Ordenamiento-mezcla-natural.cpp`.
