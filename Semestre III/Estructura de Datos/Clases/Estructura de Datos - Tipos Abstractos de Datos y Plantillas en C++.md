---
tags: [clase, semestre-III]
materia: Estructura de Datos
---
# Estructura de Datos - Tipos Abstractos de Datos y Plantillas en C++

Materia: [[Estructura de Datos]]
Anterior: —
Siguiente: [[Estructura de Datos - Archivos Binarios y Acceso Directo en C++]]

## Contexto y objetivo

Al pasar de [[Programación I]] a [[Estructura de Datos]], el foco cambia de escribir algoritmos aislados a diseñar **Tipos Abstractos de Datos (TAD)** reutilizables, independientes de su representación en memoria. Esta clase introduce el concepto de TAD, el análisis asintótico básico ($O(n)$), la gestión de memoria estática frente a dinámica en C++ y el uso de plantillas (`template`) para construir contenedores genéricos como `Lista.h` y `Cola.h`.

## 1. Tipos Abstractos de Datos (TAD)

Un **TAD** se define mediante dos componentes:
1. **Especificación lógica (interfaz)**: qué datos almacena y qué operaciones ofrece (precondiciones y postcondiciones), sin importar cómo se implementen.
2. **Implementación (estructura de datos)**: la representación concreta en memoria (arreglo, nodos enlazados, archivo) y los algoritmos de cada operación.

Ventajas del enfoque por TAD:
- **Encapsulamiento**: el programa cliente (`main.cpp`) no depende de los detalles internos del contenedor.
- **Intercambiabilidad**: se puede cambiar una lista estática por una dinámica sin reescribir la lógica de negocio (por ejemplo, en el proyecto SpeedCar).

## 2. Memoria estática vs. memoria dinámica y punteros

| Criterio | Memoria estática / automática | Memoria dinámica (*heap* / *free store*) |
|---|---|---|
| Reserva | En compilación o al entrar al bloque | En ejecución con `new` / `new[]` |
| Tamaño | Fijo (`int v[100]`) | Variable según la demanda |
| Liberación | Automática al salir del ámbito | Manual con `delete` / `delete[]` |
| Riesgos | Desperdicio o desbordamiento (*overflow*) | Fugas de memoria (*memory leaks*) o punteros colgantes |

**Regla de oro en C++:** cada `new` debe tener su `delete` correspondiente, y tras liberar un puntero conviene asignarle `nullptr` (o `NULL` en código legado del curso).

## 3. Complejidad algorítmica (Notación Big-$O$)

Para comparar estructuras y algoritmos independientemente del hardware, se mide el crecimiento del tiempo $T(n)$ o espacio respecto al tamaño de entrada $n$:

- $O(1)$: tiempo constante (acceso a un índice de arreglo, inserción en cabeza de lista).
- $O(\log n)$: logarítmico (búsqueda binaria, operaciones en árbol AVL).
- $O(n)$: lineal (recorrido de un arreglo o lista enlazada).
- $O(n \log n)$: casi lineal (QuickSort promedio, MergeSort).
- $O(n^2)$: cuadrático (burbuja, inserción, selección en peor caso).

## 4. Programación genérica con `template`

Las plantillas permiten escribir una única clase o función parametrizada por un tipo `T`:

```cpp
template <class T>
struct Nodo {
    T info;
    Nodo<T>* sig;
};

template <class T>
class Contenedor {
private:
    Nodo<T>* cab;
public:
    Contenedor() : cab(nullptr) {}
    bool vacia() const { return cab == nullptr; }
    void insertarInicio(const T& dato) {
        Nodo<T>* nuevo = new Nodo<T>{dato, cab};
        cab = nuevo;
    }
    ~Contenedor() {
        while (cab) {
            Nodo<T>* aux = cab;
            cab = cab->sig;
            delete aux;
        }
    }
};
```

> [!note] En C++, la implementación de una clase `template` debe estar en el mismo archivo de cabecera (`.h`) para que el compilador pueda instanciarla con cada tipo concreto (`Lista<Usuario>`, `Cola<Traslado>`).

## Errores comunes

- Separar la definición de métodos `template` en un `.cpp` sin instanciación explícita (produce errores de enlazado *undefined reference*).
- Pasar punteros por valor cuando la función debe modificar hacia dónde apunta la cabeza (en C++ debe usarse referencia a puntero `Nodo<T>*& cab`).
- Olvidar el destructor `~Contenedor()`, causando fugas de memoria al destruir objetos temporales.

## Ejercicios propuestos

1. ¿Cuál es la complejidad temporal de acceder al $k$-ésimo elemento en un arreglo vs. en una lista simplemente enlazada?
2. Escribe una función `template <class T>` llamada `intercambiar` que reciba dos variables por referencia y permute sus valores.

**Respuestas:**
1. En un arreglo es $O(1)$ (aritmética de direcciones); en una lista enlazada es $O(n)$ (hay que recorrer desde la cabeza).
2. `template <class T> void intercambiar(T& a, T& b) { T aux = a; a = b; b = aux; }`.

## Conexiones

- Retoma punteros, funciones y `struct` de [[Programación I]].
- Se aplica directamente en [[Estructura de Datos - Pilas, Colas y Listas Enlazadas]] y [[Programación II]].

## Fuente

Elaborado según los objetivos introductorios de [[Estructura de Datos]] y las cabeceras genéricas (`Lista.h`, `Cola.h`) del `Material/`.
