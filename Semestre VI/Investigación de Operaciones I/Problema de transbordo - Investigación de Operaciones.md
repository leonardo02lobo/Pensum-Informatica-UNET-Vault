---
tags: [tema, semestre-VI]
---
# Problema de transbordo - Investigación de Operaciones

Nota hija de [[Investigación de Operaciones I]] (modelos de redes).

## Enunciado (del Material)
Dos plantas (A: 100 u, B: 150 u) abastecen tres supermercados (SM1: 80, SM2: 90, SM3: 80) pasando obligatoriamente por un centro de transbordo (X o Y). Los centros tienen oferta y demanda 0. Total ofertado = demandado = 250.

| Planta -> centro | X | Y |
|---|---|---|
| A | 4 | 6 |
| B | 5 | 3 |

| Centro -> super | SM1 | SM2 | SM3 |
|---|---|---|---|
| X | 3 | 4 | 2 |
| Y | 6 | 3 | 5 |

## Truco del modelo de transbordo
Todos los nodos (orígenes, transbordos y destinos) se tratan como orígenes y destinos a la vez. A cada nodo se le suma un **buffer** igual al total (250): oferta de los transbordos = 0 + 250 y su demanda = 0 + 250; el buffer representa lo que "no" pasa. Así el problema se vuelve un transporte equilibrado de nodos (A, B, X, Y) a (X, Y, SM1, SM2, SM3), con costo 0 en la diagonal (X a X, Y a Y).

## Formulación PL directa
Variables: `a_x, a_y, b_x, b_y` (planta a centro) y `x1,x2,x3,y1,y2,y3` (centro a super).
```
Min Z = 4a_x + 6a_y + 5b_x + 3b_y + 3x1 + 4x2 + 2x3 + 6y1 + 3y2 + 5y3
a_x + a_y <= 100            (oferta A)
b_x + b_y <= 150            (oferta B)
a_x + b_x = x1 + x2 + x3    (balance en X)
a_y + b_y = y1 + y2 + y3    (balance en Y)
x1 + y1 = 80 ; x2 + y2 = 90 ; x3 + y3 = 80
todas las variables >= 0
```
Interpretación: es una red de flujo de costo mínimo; la solución óptima es entera por la estructura unimodular de la matriz.
