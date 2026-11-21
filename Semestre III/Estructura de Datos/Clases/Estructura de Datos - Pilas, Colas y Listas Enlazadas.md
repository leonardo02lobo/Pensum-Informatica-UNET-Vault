---
tags: [clase, semestre-III]
materia: Estructura de Datos
---
# Estructura de Datos - Pilas, Colas y Listas Enlazadas

Materia: [[Estructura de Datos]]
Anterior: [[Estructura de Datos - Métodos de Búsqueda y Tablas Hash]]
Siguiente: [[Estructura de Datos - Árboles Binarios de Búsqueda y AVL]]

## Contexto y objetivo

Las estructuras lineales dinámicas permiten crecer y decrecer en tiempo de ejecución sin desperdiciar memoria ni imponer límites fijos. Siguiendo el Tema 3 de [[Estructura de Datos]] (ver Pilas, colas y listas enlazadas), esta clase desarrolla la implementación y aplicaciones de **pilas**, **colas** y **listas enlazadas** (simples, doblemente enlazadas y circulares).

## 1. Pila (*Stack*, LIFO)

Principio **LIFO** (*Last-In, First-Out*): el último elemento en entrar es el primero en salir. Todas las operaciones ocurren por el **tope**:

- `push(x)`: apila en $O(1)$.
- `pop()`: desapila y retorna el tope en $O(1)$.
- `peek()` / `top()`: consulta el tope sin extraerlo.
- `vacia()`: verifica `tope == nullptr`.

```cpp
template <class T>
struct NodoPila { T dato; NodoPila<T>* sig; };

template <class T>
void push(NodoPila<T>*& tope, const T& x) {
    tope = new NodoPila<T>{x, tope};
}

template <class T>
bool pop(NodoPila<T>*& tope, T& x) {
    if (!tope) return false;
    NodoPila<T>* aux = tope;
    x = aux->dato;
    tope = tope->sig;
    delete aux;
    return true;
}
```

**Aplicaciones:** balanceo de paréntesis `({[]})`, evaluación de expresiones posfijas, historial *Undo/Redo*, pila de llamadas recursivas y recorrido DFS.

## 2. Cola (*Queue*, FIFO)

Principio **FIFO** (*First-In, First-Out*): se inserta por el **final** (`encolar`) y se extrae por el **frente** (`desencolar`), ambas en $O(1)$ manteniendo punteros `frente` y `final`.

- **Cola circular estática**: usa aritmética modular `idx = (idx + 1) % MAX` para reutilizar las posiciones liberadas al principio del arreglo.
- **Cola de prioridad**: cada elemento tiene una prioridad y se extrae primero el de mayor prioridad.
- **Bicola (Deque)**: permite insertar y eliminar por ambos extremos.

**Aplicaciones:** colas de impresión, atención de solicitudes (en SpeedCar: cola de traslados pendientes), planificación de CPU en [[Sistemas Operativos]] y recorrido BFS.

## 3. Listas enlazadas: variantes y operaciones

| Variante | Enlaces por nodo | Ventaja principal |
|---|---|---|
| **Simple** | `sig` | Inserción al inicio $O(1)$, mínimo uso de memoria |
| **Doblemente enlazada** | `ant` y `sig` | Recorrido bidireccional; eliminar un nodo conocido en $O(1)$ |
| **Circular** | El último apunta al primero | Ideal para turnos rotativos (*round-robin*) |

**Inserción ordenada en lista simple** (manteniendo las claves ascendentes):
```cpp
void insertarOrdenado(Nodo<int>*& cab, int x) {
    Nodo<int>* nuevo = new Nodo<int>{x, nullptr};
    if (!cab || x < cab->dato) {
        nuevo->sig = cab;
        cab = nuevo;
        return;
    }
    Nodo<int>* act = cab;
    while (act->sig && act->sig->dato < x) {
        act = act->sig;
    }
    nuevo->sig = act->sig;
    act->sig = nuevo;
}
```

## Errores comunes

- Desencolar el último elemento de una cola y olvidar actualizar `final = nullptr` cuando `frente` queda `nullptr`.
- En listas doblemente enlazadas, perder el orden al reenlazar los cuatro punteros (`ant->sig`, `nuevo->ant`, `nuevo->sig`, `sig->ant`).
- Iterar una lista circular con `while (act != nullptr)` en lugar de `do { ... } while (act != cab)` (bucle infinito).

## Ejercicios propuestos

1. Evalúa la expresión en notación posfija `5 1 2 + 4 * + 3 -` usando una pila.
2. En una cola circular de tamaño $5$ con `frente = 3` y `final = 1`, ¿cuántos elementos hay actualmente?

**Respuestas:**
1. `1 + 2 = 3`; `3 * 4 = 12`; `5 + 12 = 17`; `17 - 3 = 14`.
2. Posiciones ocupadas: `3, 4, 0, 1` $\rightarrow$ $4$ elementos.

## Conexiones

- Amplía Pilas, colas y listas enlazadas.
- Se utiliza directamente en [[Estructura de Datos - Grafos, Recorridos y Ruta Mínima]] (BFS/DFS) y en [[Sistemas Operativos]].

## Fuente

Basado en `Material/Tema 3-Pilas, Colas, Listas simples y Doblemente Enlazadas/Colas y Pilas Teoria.ppsx`, `listas.pdf`, `listas-dinamicas.pdf` y `Primer Proyecto Parcial 2/`.
