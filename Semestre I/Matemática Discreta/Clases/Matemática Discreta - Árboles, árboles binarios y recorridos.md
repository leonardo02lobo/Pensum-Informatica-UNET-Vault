---
tags: [clase, semestre-I]
materia: Matemática Discreta
---
# Matemática Discreta - Árboles, árboles binarios y recorridos

Materia: [[Matemática Discreta]]  
Anterior: [[Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton]]

## Contexto y objetivo
Los **árboles** son grafos especiales fundamentales en informática: representan jerarquías de archivos, árboles de decisión, expresiones aritméticas en compiladores y estructuras de búsqueda rápida. En esta clase final se definen los árboles libres y con raíz, las propiedades de los **árboles binarios** y los tres algoritmos clásicos de recorrido: **preorden, inorden y postorden**.

## 1. Definición y propiedades de los árboles
Un **árbol** es un grafo no dirigido, **conexo** y **sin ciclos** (acíclico).
- **Propiedad fundamental**: todo árbol con $n$ vértices tiene exactamente **$n - 1$ aristas**.
- Entre cualquier par de vértices de un árbol existe un **único camino simple**.

### Terminología de árboles con raíz
Al designar un vértice especial como **raíz**:
- **Padre e hijos**: si $u$ está justo encima de $v$ en el camino desde la raíz, $u$ es padre de $v$ y $v$ es hijo de $u$.
- **Hoja (nodo terminal)**: vértice sin hijos. Los demás se llaman *nodos internos*.
- **Nivel / profundidad** de un nodo: longitud del camino desde la raíz (la raíz está en nivel $0$).
- **Altura ($h$)** del árbol: máximo nivel alcanzado por alguna hoja.

## 2. Árboles binarios
Un **árbol binario** es un árbol con raíz donde cada nodo tiene **como máximo 2 hijos**, distinguiéndose entre **hijo izquierdo** e **hijo derecho**.
- Un árbol binario de altura $h$ tiene a lo sumo $2^{h+1} - 1$ nodos (cuando está *lleno* o completo en todos sus niveles).
- En un árbol binario lleno con $n$ nodos, todos los niveles salvo posiblemente el último están completos.

## 3. Recorridos en profundidad de un árbol binario
Recorrer un árbol significa visitar sistemáticamente cada nodo exactamente una vez:

```text
preorden(nodo):   Visitar(nodo) -> preorden(izq)  -> preorden(der)
inorden(nodo):    inorden(izq)  -> Visitar(nodo) -> inorden(der)
postorden(nodo):  postorden(izq)-> postorden(der)-> Visitar(nodo)
```

- **Preorden (Raíz – Izq – Der)**: útil para clonar un árbol o escribir expresiones en notación prefija.
- **Inorden (Izq – Raíz – Der)**: en un árbol binario de búsqueda, devuelve las claves en orden ascendente; en árboles de expresiones produce la notación infija.
- **Postorden (Izq – Der – Raíz)**: útil para evaluar expresiones aritméticas (notación polaca inversa) o liberar memoria de abajo hacia arriba.

## 4. Ejemplo resuelto de recorridos
Considera el árbol binario con raíz `1`, hijo izquierdo `2` (cuyos hijos son `4` a la izquierda y `5` a la derecha) e hijo derecho `3`:
- **Preorden**: `1  2  4  5  3`
- **Inorden**: `4  2  5  1  3`
- **Postorden**: `4  5  2  3  1`

Otro ejemplo (de la nota principal): raíz `R`, hijo izquierdo `I` (con hijos `a`, `b`) e hijo derecho `D`:
- **Preorden**: `R  I  a  b  D`
- **Inorden**: `a  I  b  R  D`
- **Postorden**: `a  b  I  D  R`

## Errores comunes
- Confundir el orden de visita de la raíz en **inorden** (va *entre* el subárbol izquierdo y el derecho, no al principio).
- Olvidar que en un árbol binario un único hijo puede ser izquierdo **o** derecho (la posición importa).
- Contar la altura por número de nodos en vez de número de aristas desde la raíz (si la raíz sola tiene altura $0$, un árbol de altura $h$ tiene hasta $2^{h+1} - 1$ nodos).

## Ejercicios propuestos
1. ¿Cuántas aristas tiene un árbol con $15$ vértices?  
   *Respuesta:* $15 - 1 = 14$ aristas.
2. Dado el árbol de expresión con raíz `+`, hijo izquierdo `*` (hijos `3` y `4`) e hijo derecho `5`, escribe su recorrido en **postorden** y **inorden**.  
   *Respuesta:* Postorden: `3  4  *  5  +` (evalúa $3\cdot 4 + 5 = 17$); Inorden: `3  *  4  +  5`.

## Conexiones
- Materia principal: [[Matemática Discreta]]
- Nota resumen: [[Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton]]
- Anterior: [[Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton]]
- Aplicación directa: [[Estructura de Datos]] (implementación recursiva de árboles binarios de búsqueda, AVL y recorridos).

## Fuente
Material de [[Matemática Discreta]] en `Material/Recorrido del Arbol/Árbol binario y profundidad (recorrido de árbol)..pdf` y `Material/Mapas /MAPA CONCEPTUAL.pdf`.
