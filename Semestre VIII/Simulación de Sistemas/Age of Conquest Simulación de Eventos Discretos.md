---
tags: [tema, semestre-VIII]
semestre: VIII
---
# Age of Conquest Simulación de Eventos Discretos

Nota hija de [[Simulación de Sistemas]]. Proyecto práctico (junio 2026) sobre el juego de estrategia por turnos *Age of Conquest*; fuente en `~/Documentos/UNET/Simulacio  de Sistemas`.

## Sistema
Varios imperios compiten por el control de un mapa dividido en provincias. En cada turno un imperio recauda oro, recluta y mueve ejércitos, combate y conquista. El juego termina al alcanzar un umbral de provincias o eliminar a los rivales.

## Parcial I: modelo conceptual
Simulación de **eventos discretos**: el estado es constante entre eventos; el reloj salta de evento en evento extraído de la **LEF**. El reloj se expresa como `turno.fase` (recaudación, planificación, movimiento, combate, fin), de modo que la LEF ordena eventos dentro del turno y programa eventos de turnos futuros.

## Parcial II: modelo formal
- Ecuación de estado general: S(τ⁺) = Ψₑ(S(τ⁻), Θ, U).
- Renta provincial Iₚ(t) con tasa impositiva y descontento; recaudación Rᵢ = Σ Iₚ; coste de mantenimiento Cᵢ = c_adm·nᵢ + c_up·Mᵢ.
- Tesoro: Gᵢ(t+1) = máx(0, Gᵢ + Rᵢ − Cᵢ − Xᵢ).
- Descontento provincial con clamp en [0, 100].
- Diccionario de variables (estado, flujo, auxiliares), parámetros fijos y algoritmos de cada evento.

## Parcial III: implementación
Código en Python (`sim/`: reloj, azar, economía, militar, diplomacia, eventos, recolector, lote), escenarios JSON, pruebas (`test_traza_dorada.py`, `test_fronteras.py`), corridas por lote y salidas CSV (base, crecimiento, desgaste, fortificación, revueltas, sensibilidad fiscal).

## Lecciones
Separar semilla y parámetros, probar casos de borde, comparar contra una **traza dorada**, y hacer análisis de sensibilidad (p. ej. política fiscal). Ver [[Investigación de Operaciones II]] para validación analítica.
