---
tags: [clase, semestre-III]
materia: Estructura de Datos
---
# Estructura de Datos - Árboles Binarios de Búsqueda y AVL

Materia: [[Estructura de Datos]]
Anterior: [[Estructura de Datos - Pilas, Colas y Listas Enlazadas]]
Siguiente: [[Estructura de Datos - Grafos, Recorridos y Ruta Mínima]]

## Contexto y objetivo

Las listas enlazadas requieren $O(n)$ para buscar una clave. Los **árboles binarios de búsqueda (ABB)** organizan los datos jerárquicamente para buscar en $O(\log n)$, y los **árboles AVL** garantizan ese desempeño mediante autobalanceo. Esta clase desarrolla el Tema 4 de [[Estructura de Datos]] (ver Árboles binarios de búsqueda y AVL).

## 1. Terminología y recorridos de árboles binarios

- **Raíz**: nodo superior sin padre. **Hoja**: nodo sin hijos.
- **Nivel**: distancia en aristas desde la raíz (raíz = nivel 0). **Altura**: máxima longitud de camino hasta una hoja (en implementaciones AVL suele definirse hoja con altura 1 y `nullptr` con altura 0).
- **Recorridos recursivos**:
  - **Preorden** (Raíz, Izq, Der): útil para clonar o serializar el árbol.
  - **Inorden** (Izq, Raíz, Der): en un ABB produce todas las claves en **orden ascendente**.
  - **Postorden** (Izq, Der, Raíz): útil para liberar la memoria de todo el árbol (`delete` después de liberar hijos).

## 2. Árbol Binario de Búsqueda (ABB)

**Invariante:** para todo nodo $x$, las claves de su subárbol izquierdo son menores que $x$ y las del subárbol derecho son mayores.

**Eliminación de un nodo en ABB (3 casos):**
1. **Es hoja**: se libera directamente y el puntero del padre pasa a `nullptr`.
2. **Tiene un solo hijo**: el padre apunta directamente al único hijo y se libera el nodo.
3. **Tiene dos hijos**: se sustituye la clave del nodo por su **sucesor inorden** (el mínimo del subárbol derecho) o su predecesor inorden, y luego se elimina ese sucesor (que a lo sumo tendrá un hijo derecho).

## 3. Árboles AVL y rotaciones

Si se insertan claves ordenadas (`10, 20, 30, 40`) en un ABB simple, el árbol degenera en una lista de altura $n$ y la búsqueda cae a $O(n)$. Un **AVL** mantiene para cada nodo un **factor de equilibrio**:
$$FE(nodo) = \text{altura}(izq) - \text{altura}(der) \in \{-1, 0, 1\}$$

Cuando una inserción o eliminación produce $|FE| = 2$, se restablece el equilibrio con una de cuatro rotaciones:

| Desbalance | Condición | Acción |
|---|---|---|
| **Izquierda-Izquierda (LL)** | $FE > 1$ y $FE(izq) \ge 0$ | Rotación simple a la derecha |
| **Derecha-Derecha (RR)** | $FE < -1$ y $FE(der) \le 0$ | Rotación simple a la izquierda |
| **Izquierda-Derecha (LR)** | $FE > 1$ y $FE(izq) < 0$ | Rotación izquierda en hijo izq. + derecha en nodo |
| **Derecha-Izquierda (RL)** | $FE < -1$ y $FE(der) > 0$ | Rotación derecha en hijo der. + izquierda en nodo |

```cpp
int altura(NodoAVL* n) { return n ? n->altura : 0; }

NodoAVL* rotarIzquierda(NodoAVL* x) {
    NodoAVL* y = x->der;
    NodoAVL* T2 = y->izq;
    y->izq = x;
    x->der = T2;
    x->altura = 1 + max(altura(x->izq), altura(x->der));
    y->altura = 1 + max(altura(y->izq), altura(y->der));
    return y;
}
```

Con un AVL, la altura máxima es $O(\log n)$, garantizando inserción, búsqueda y eliminación en $O(\log n)$ en el peor caso.

## Errores comunes

- En rotaciones AVL, actualizar primero la altura del nuevo padre (`y`) antes que la del hijo (`x`), obteniendo alturas incorrectas.
- Olvidar reasignar el puntero retornado por `insertar` o `rotar` al padre en la recursión (`r->izq = insertar(r->izq, x)`).
- En la eliminación de dos hijos, olvidar eliminar el nodo sucesor tras copiar su dato, duplicando el registro.

## Ejercicios propuestos

1. Inserta la secuencia `30, 10, 20` en un AVL inicialmente vacío e indica qué rotación ocurre.
2. Si un ABB tiene claves `{15, 10, 20, 8, 12, 25}`, ¿qué devuelve su recorrido inorden y su recorrido postorden?

**Respuestas:**
1. Al insertar `20`, `30` queda con $FE = +2$ y su hijo `10` con $FE = -1$ (caso LR): rotación izquierda en `10`, luego derecha en `30`. Raíz final: `20`, hijos `10` y `30`.
2. Inorden: `8, 10, 12, 15, 20, 25`. Postorden: `8, 12, 10, 25, 20, 15`.

## Conexiones

- Amplía Árboles binarios de búsqueda y AVL.
- Base para los árboles B/B+ de [[Base de Datos I]] y para [[Estructura de Datos - Grafos, Recorridos y Ruta Mínima]].

## Fuente

Basado en `Material/Tema 4-ÁRBOLES BINARIOS DE BÚSQUEDA/Presentacion de Arboles binarios.ppsx`, `Arbol.cpp` y `Proyecto Arbol AVL/`.
