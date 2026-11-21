---
tags: [clase, semestre-III]
materia: Estructura de Datos
---
# Estructura de Datos - Métodos de Búsqueda y Tablas Hash

Materia: [[Estructura de Datos]]
Anterior: [[Estructura de Datos - Métodos de Ordenamiento Interno y Externo]]
Siguiente: [[Estructura de Datos - Pilas, Colas y Listas Enlazadas]]

## Contexto y objetivo

La recuperación rápida de información por clave es una operación crítica en sistemas de software y bases de datos. Esta clase cubre la segunda parte del Tema 2 de [[Estructura de Datos]] (ver [[Estructura de Datos - Métodos de Ordenamiento Interno y Externo]]): búsqueda secuencial, búsqueda binaria (interna y sobre archivos binarios), transformación de claves (**hashing**) y resolución de colisiones.

## 1. Búsqueda secuencial y búsqueda binaria

| Método | Precondición | Complejidad | Aplicación |
|---|---|---|---|
| **Secuencial** | Ninguna | $O(n)$ | Listas pequeñas o datos desordenados |
| **Binaria** | Datos **ordenados** por clave | $O(\log n)$ | Arreglos o archivos binarios de acceso directo |

Implementación iterativa de búsqueda binaria:
```cpp
int busquedaBinaria(const int a[], int n, int clave) {
    int ini = 0, fin = n - 1;
    while (ini <= fin) {
        int med = ini + (fin - ini) / 2; // evita overflow de (ini + fin)
        if (a[med] == clave) return med;
        if (clave < a[med]) fin = med - 1;
        else ini = med + 1;
    }
    return -1;
}
```

**Búsqueda binaria externa (en archivo binario):**
Si el archivo binario está ordenado por `codigo`, se reemplaza `a[med]` por `seekg(med * sizeof(Reg), ios::beg)` + `read(...)`. Con $1\,000\,000$ de registros, solo se realizan $\approx 20$ accesos a disco en lugar de $500\,000$ en promedio.

## 2. Tablas Hash (Transformación de claves)

La idea del *hashing* es calcular directamente la posición a partir de la clave mediante una función $h(k)$, logrando tiempo promedio $O(1)$:

- **Aritmética modular**: $h(k) = k \bmod M$ (conviene elegir $M$ primo para distribuir mejor).
- **Mitad del cuadrado**: elevar $k^2$ y tomar los dígitos centrales.
- **Plegamiento**: dividir la clave en partes y sumarlas módulo $M$.

## 3. Manejo de colisiones

Ocurre una **colisión** cuando dos claves distintas producen el mismo índice: $h(k_1) = h(k_2)$. Estrategias principales:

1. **Direccionamiento abierto** (todo en la misma tabla):
   - *Sondeo lineal*: $h_i(k) = (h(k) + i) \bmod M$ para $i = 0, 1, 2, \dots$ (simple, pero genera agrupamiento primario).
   - *Sondeo cuadrático*: $h_i(k) = (h(k) + i^2) \bmod M$.
   - *Doble hashing*: usa una segunda función $h_2(k)$ como paso.
2. **Encadenamiento separado**: cada entrada de la tabla apunta a una lista enlazada con las claves que colisionaron en esa posición.

## 4. Búsqueda externa por cubetas y registros enlazados

- **Hashing por cubetas (buckets)**: cada posición hash en disco almacena un bloque de $b$ registros en lugar de uno solo, reduciendo las colisiones y aprovechando la lectura de bloques.
- **Registros enlazados / multilistas**: en archivos binarios, cada registro guarda un campo entero (`int sigPos`) con el índice del siguiente registro en la misma categoría o cubeta de desborde (`-1` indica fin de cadena).

## Errores comunes

- Aplicar búsqueda binaria sobre un arreglo sin ordenar previamente.
- Calcular `(ini + fin) / 2` cuando `ini + fin` supera `INT_MAX` (usar `ini + (fin - ini) / 2`).
- En direccionamiento abierto, borrar una clave poniendo `VACIO` directamente: esto rompe la cadena de sondeo de claves posteriores (debe marcarse como `BORRADO`).

## Ejercicios propuestos

1. Dada una tabla hash de tamaño $M = 7$ con $h(k) = k \bmod 7$ y sondeo lineal, inserta las claves `15, 22, 8, 10`.
2. ¿Cuántas comparaciones como máximo realiza la búsqueda binaria en un arreglo ordenado de $500$ elementos?

**Respuestas:**
1. `15 % 7 = 1` $\rightarrow$ pos 1; `22 % 7 = 1` (colisión) $\rightarrow$ pos 2; `8 % 7 = 1` (colisión en 1 y 2) $\rightarrow$ pos 3; `10 % 7 = 3` (colisión en 3) $\rightarrow$ pos 4.
2. $\lfloor \log_2(500) \rfloor + 1 = 9$ comparaciones.

## Conexiones

- Amplía [[Estructura de Datos - Métodos de Ordenamiento Interno y Externo]].
- Se aplica en [[Base de Datos I]] (índices hash) y se compara con los árboles de [[Estructura de Datos - Árboles Binarios de Búsqueda y AVL]].

## Fuente

Basado en `Material/Tema 2-Ordenamiento de busqueda/Métodos de Búsqueda.ppsx`, `busquedaBinaria.cpp`, `busquedaSencuencial.cpp` y `HashingInterno.cpp`.
