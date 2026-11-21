---
tags: [materia, semestre-III]
semestre: III
---
# Estructura de Datos

**Semestre:** [[Semestre III]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Programación I]]

## Desbloquea
- [[Programación II]]

## Apuntes

### Descripción general y objetivos

Estructura de Datos (UNET, Semestre III) lleva al estudiante desde la programación básica ([[Programación I]]) hacia el diseño de **tipos abstractos de datos (TAD)** y su implementación eficiente en C/C++. El curso se organiza en cinco temas y se evalúa con un proyecto por cada corte, usando siempre el mismo caso de estudio que va creciendo (en el Material: el servicio de traslados "SpeedCar" de San Cristóbal).

Objetivos:
- Persistir información en **archivos de texto y binarios** y acceder a ella de forma secuencial y directa.
- Aplicar **métodos de ordenamiento y búsqueda**, internos (memoria) y externos (archivos).
- Implementar **pilas, colas y listas** (simples, dobles, circulares) en almacenamiento estático y dinámico.
- Dominar **árboles binarios de búsqueda** y árboles balanceados **AVL**.
- Modelar relaciones con **grafos** (matriz y lista de adyacencia, recorridos, ruta mínima).
- Elegir el paradigma que convenga: estructurado, semi-orientado a objetos, orientado a objetos o programación genérica con `template`.

### Contenido programático (según el Material)

#### Tema 1. Archivos binarios y de texto
Detalle ampliado en [[Estructura de Datos - Archivos Binarios y Acceso Directo en C++]].
- Flujos (`stream`): `fstream`, `ifstream`, `ofstream`; modos `ios::in`, `ios::out`, `ios::app`, `ios::binary`.
- Archivo de texto vs. binario; lectura/escritura con `write` y `read` de registros completos (`struct`/clase).
- Acceso directo con `seekg`/`seekp` y `tellg`; fórmula de posición `i * sizeof(registro)`.
- Operaciones de un CRUD sobre archivo: crear, agregar, consultar, listar, modificar, eliminar.

#### Tema 2. Ordenamiento y búsqueda
Detalle en [[Estructura de Datos - Métodos de Ordenamiento Interno y Externo]].
- Ordenamiento interno: burbuja, selección directa, inserción, Shell, QuickSort, MergeSort, Radix.
- Ordenamiento externo: mezcla directa y mezcla natural sobre archivos (`file1.txt`, `file2.txt`).
- Búsqueda interna: secuencial, binaria, por transformación de claves (hash).
- Búsqueda externa: secuencial, binaria sobre registros, hash por cubetas, registros enlazados (listas/multilistas).

#### Tema 3. Pilas, colas y listas
Detalle en [[Estructura de Datos - Pilas, Colas y Listas Enlazadas]].
- Almacenamiento estático (arreglo) vs. dinámico (nodos con `new`/`delete`).
- Pila (LIFO), cola (FIFO), listas simples, doblemente enlazadas y circulares.

#### Tema 4. Árboles binarios de búsqueda
Detalle en [[Estructura de Datos - Árboles Binarios de Búsqueda y AVL]].
- Terminología: nodo, raíz, hoja, nivel, altura, grado, subárbol.
- Inserción, búsqueda, eliminación y recorridos (preorden, inorden, postorden).
- Balanceo AVL: factor de equilibrio y rotaciones.

#### Tema 5. Grafos
Detalle en [[Estructura de Datos - Grafos, Recorridos y Ruta Mínima]].
- Vértices, aristas, dirigidos/no dirigidos, ponderados.
- Matriz y lista de adyacencia; recorridos en profundidad (DFS) y anchura (BFS); ruta mínima.

### Conceptos clave

- **TAD**: especificación de datos + operaciones, independiente de la implementación.
- **Estructura lineal**: cada elemento tiene un único predecesor y sucesor (arreglo, lista, pila, cola). **No lineal**: árboles y grafos.
- **Nodo**: bloque de memoria dinámica con un campo de información y uno o más punteros.
- **Memoria estática vs. dinámica**: la estática se reserva en compilación (tamaño fijo, posible desperdicio u overflow); la dinámica usa el *free store* y crece/decrece con los datos.
- **Complejidad**: notación O(n), O(log n), O(n log n), O(n²); insertar en cabeza de lista O(1), búsqueda en lista O(n), en ABB balanceado O(log n).
- **Clave**: campo que identifica unívocamente un registro y gobierna la búsqueda y el orden.
- **Plantillas (`template <class T>`)**: permiten estructuras genéricas reutilizables (en el proyecto: `Lista.h`, `Cola.h`).

### Código de ejemplo

Nodo y lista simple dinámica:

```cpp
template <class T>
struct Nodo {
    T info;
    Nodo<T>* sig;
};

template <class T>
void insertarInicio(Nodo<T>*& cab, const T& dato) {
    Nodo<T>* n = new Nodo<T>;
    n->info = dato;
    n->sig  = cab;
    cab = n;
}
```

Escritura y lectura directa en archivo binario:

```cpp
struct Registro { int codigo; char nombre[30]; float precio; };

fstream arc("datos.dat", ios::in | ios::out | ios::binary);
Registro r;
arc.seekg(i * sizeof(Registro), ios::beg);   // salto directo al registro i
arc.read((char*)&r, sizeof(r));
r.precio *= 1.1;
arc.seekp(i * sizeof(Registro), ios::beg);
arc.write((char*)&r, sizeof(r));
```

Búsqueda binaria (arreglo ordenado):

```cpp
int busquedaBinaria(int a[], int n, int x) {
    int ini = 0, fin = n - 1;
    while (ini <= fin) {
        int med = (ini + fin) / 2;
        if (a[med] == x) return med;
        if (x < a[med]) fin = med - 1; else ini = med + 1;
    }
    return -1;
}
```

### Ejemplos resueltos breves

1. **Pila**: evaluar si `( [ { } ] )` está balanceado. Se apila cada apertura; al leer un cierre se desapila y se compara. Si la pila queda vacía al final, la expresión es válida.
2. **Cola**: simular clientes en un banco; `encolar` al llegar, `desencolar` al atender; el tiempo de espera es la diferencia entre atención y llegada.
3. **ABB**: insertar 11, 5, 8, 20, 22, 6. Raíz 11; 5 a la izquierda; 8 a la derecha de 5; 20 a la derecha de 11; 22 a la derecha de 20; 6 a la izquierda de 8. Inorden: 5, 6, 8, 11, 20, 22 (ordenado).

### Relación con otras materias

- Prelación directa: [[Programación I]] (punteros, funciones, arreglos, archivos básicos).
- Desbloquea [[Programación II]], donde se retoman recursividad, grafos y árboles en problemas de lógica matemática.
- Fundamento para [[Base de Datos I]] (índices, árboles B, hashing), [[Sistemas Operativos]] (colas de planificación, listas de procesos) y [[Matemática Discreta]] (teoría de grafos y árboles).
- Los algoritmos de grafos conectan con [[Investigación de Operaciones I]] (rutas mínimas, flujos).

### Evaluación y consejos de estudio

- Cada corte tiene un proyecto grande (ejemplo del Material: Proyecto 1 de 40 pts, entrega 31/10/2024) más prácticas; los parciales integran teoría y programación. Verificar con el programa oficial la ponderación vigente.
- Dibuja siempre los punteros en papel antes de codificar; la mayoría de los errores son de enlaces perdidos (`memory leak`, `segmentation fault`).
- Prueba casos borde: estructura vacía, un solo elemento, eliminar cabeza/cola/raíz.
- Reutiliza `Lista.h`/`Cola.h` genéricas entre proyectos para ahorrar tiempo.
- Usa `valgrind` o al menos revisa cada `new` con su `delete`.

### Bibliografía recomendada

- Cairó, O. y Guardati, S. *Estructuras de Datos*, 3.ª ed., McGraw-Hill, 2006 (citada en las presentaciones del profesor).
- Luna, C. A. *Estructura de Datos*, Red Tercer Milenio, 2012.
- Miller, B. y Ranum, D. *Solución de problemas con algoritmos y estructuras de datos usando Python* (runestone.academy).
- Weiss, M. A. *Estructuras de datos en C++*; Cormen et al., *Introduction to Algorithms* (complementarias).

### Recursos del Material/

Presentaciones del Prof. David Ortiz y proyectos del estudiante:
- [Presentación Archivos binarios](Material/Tema%201-Archivos%20Binarios%20y%20de%20Texto/Presentacion%20Archivos%20binarios.ppsx): flujos, `seekg`, práctica de CRUD.
- [Proyecto 1 (enunciado PDF)](Material/Tema%201-Archivos%20Binarios%20y%20de%20Texto/primer%20proyecto-parcial%201.pdf): sistema de traslados SpeedCar con archivos.
- [Métodos de Búsqueda](Material/Tema%202-Ordenamiento%20de%20busqueda/Métodos%20de%20Búsqueda.ppsx): búsqueda interna y externa.
- [Métodos de ordenamiento (guía)](Material/Tema%202-Ordenamiento%20de%20busqueda/metodos%20de%20ordenamiento.pdf): guía teórica de algoritmos de ordenamiento.
- Carpetas `Metodos de Ordenamiento Interno`, `Metodos de Ordenamiento Externa` y `Metodos de Busqueda` con código `.cpp` (burbuja, mezcla directa/natural, secuencial, binaria, hashing).
- [Colas y Pilas Teoría](Material/Tema%203-Pilas,%20Colas,%20Listas%20simples%20y%20Doblemente%20Enlazadas/Colas%20y%20Pilas%20Teoria.ppsx), [listas](Material/Tema%203-Pilas,%20Colas,%20Listas%20simples%20y%20Doblemente%20Enlazadas/listas.pdf) y [listas dinámicas](Material/Tema%203-Pilas,%20Colas,%20Listas%20simples%20y%20Doblemente%20Enlazadas/listas-dinamicas.pdf): teoría; código en subcarpetas `Pilas`, `Colas`, `listas`.
- [Presentación de Árboles binarios](Material/Tema%204-ÁRBOLES%20BINARIOS%20DE%20BÚSQUEDA/Presentacion%20de%20Arboles%20binarios.ppsx) y carpeta `Proyecto Arbol AVL` (inventario con AVL, `enunciado.txt`).
- [Presentación Grafos](Material/Tema%205-Grafos/Presentacion%20Grafos.ppsx) y proyecto final con `Grafo.h` (Proyecto Parcial 3).
