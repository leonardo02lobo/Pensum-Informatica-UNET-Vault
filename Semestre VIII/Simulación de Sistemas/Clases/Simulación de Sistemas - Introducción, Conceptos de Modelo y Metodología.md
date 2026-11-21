---
tags: [clase, semestre-VIII]
materia: Simulación de Sistemas
---
# Simulación de Sistemas - Introducción, Conceptos de Modelo y Metodología

Materia: [[Simulación de Sistemas]]
Anterior: — (primera clase)
Siguiente: [[Simulación de Sistemas - Generación de Números Pseudoaleatorios y Pruebas Estadísticas]]

## Contexto y objetivo
Establecer los fundamentos conceptuales de la **simulación de sistemas** (definición de R. E. Shannon), clasificar los tipos de modelos y dominar las etapas metodológicas de un estudio completo de simulación, desde la formulación del problema hasta el análisis e implementación de resultados.

## 1. Sistema, modelo y simulación
- **Sistema**: conjunto de entidades (personas, máquinas, servidores, imperios) que interactúan entre sí y con su entorno hacia un objetivo común. Se describe mediante **variables de estado**, **parámetros** y **relaciones**.
- **Modelo**: representación simplificada de un sistema real que captura únicamente los aspectos relevantes para el problema estudiado.
- **Simulación** (R. E. Shannon): *proceso de diseñar un modelo de un sistema real y llevar a término experiencias con él, con la finalidad de comprender el comportamiento del sistema o evaluar nuevas estrategias para su funcionamiento*.

## 2. ¿Cuándo simular frente a soluciones analíticas?
La simulación no sustituye a las matemáticas analíticas (p. ej., fórmulas exactas de colas $M/M/1$), sino que las complementa cuando:
1. No existe una formulación matemática analítica cerrada.
2. Las hipótesis simplificadoras requeridas por el modelo analítico (estacionariedad, llegadas Markovianas) son inaceptables.
3. Los procedimientos numéricos disponibles son inviables computacionalmente.
4. Se desea observar la **historia animada o traza temporal** del sistema y no solo promedios en estado estable.
5. Experimentar sobre el sistema real es costoso, peligroso, lento o imposible (p. ej., saturación de red o estrategia militar).

### Ventajas y desventajas
- **Ventajas**: flexibilidad para modelar sistemas complejos, compresión/expansión del tiempo, experimentación controlada sin riesgo, identificación de cuellos de botella.
- **Desventajas**: no es una técnica de optimización exacta por sí sola (solo evalúa escenarios), requiere datos de entrada confiables, puede ser costosa en tiempo de desarrollo y cómputo.

## 3. Clasificación de los modelos de simulación
- **Estáticos vs. Dinámicos**: los estáticos representan el sistema en un instante dado (Montecarlo); los dinámicos evolucionan en el tiempo.
- **Deterministas vs. Estocásticos**: los deterministas no tienen variables aleatorias; los estocásticos incorporan incertidumbre probabilística.
- **Continuos vs. Discretos**:
  - *Continuos*: las variables de estado cambian de forma suave en el tiempo (ecuaciones diferenciales).
  - *Discretos*: las variables de estado cambian únicamente en instantes puntuales llamados **eventos** (p. ej., llegada de un cliente, fin de un turno).

## 4. Metodología de un estudio de simulación
1. **Formulación del problema y definición de objetivos**: preguntas a responder, métricas de desempeño, alcance.
2. **Recolección y análisis de datos**: ajuste de distribuciones de probabilidad a datos históricos.
3. **Modelo conceptual**: definición de entidades, atributos, eventos, variables de estado y supuestos (enfoque del Parcial I).
4. **Modelo formal**: ecuaciones de transición de estado, diccionario de variables y algoritmos de eventos (enfoque del Parcial II).
5. **Traducción / Programación**: implementación en Python, SimPy, Arena, GPSS o AnyLogic.
6. **Verificación y validación**: comprobar que el código implementa el modelo (*verificación*) y que el modelo representa la realidad (*validación*).
7. **Diseño experimental y corridas**: réplicas, longitud de corrida, período de calentamiento.
8. **Análisis de salida y documentación**: intervalos de confianza, sensibilidad y recomendaciones.

## Errores comunes
- Comenzar a programar antes de definir claramente el modelo conceptual y las métricas de salida.
- Simular un problema que tiene solución analítica simple (como una cola $M/M/1$ estándar en régimen permanente) sin justificar qué detalle adicional se necesita.
- Confundir simulación determinista con ausencia de complejidad: un modelo determinista con muchas interacciones no lineales puede requerir simulación igualmente.

## Ejercicios propuestos
1. Clasifique los siguientes sistemas según sean discretos/continuos, estáticos/dinámicos y deterministas/estocásticos: (a) integración de $\pi$ lanzando dardos al azar; (b) cola de atención en una taquilla bancaria con llegadas aleatorias; (c) enfriamiento de un servidor modelado por la ley de Newton.
   - *Respuesta*: (a) estático, estocástico; (b) dinámico, discreto, estocástico; (c) dinámico, continuo, determinista.
2. En el proyecto [[Age of Conquest Simulación de Eventos Discretos]], ¿por qué el modelo es discreto y dinámico?
   - *Respuesta*: el estado del mapa, tesoros y ejércitos evoluciona a lo largo del tiempo (dinámico), pero solo cambia en instantes discretos definidos por `turno.fase` (eventos).

## Conexiones
- Base sistémica en [[Teoría General de Sistemas]].
- Soluciones analíticas previas en [[Investigación de Operaciones II]].
- Aplicación práctica en [[Age of Conquest Simulación de Eventos Discretos]].

## Fuente
Basado en [[Simulación de Sistemas]] (Shannon, *Simulación de sistemas*; Law & Kelton, *Simulation Modeling and Analysis*; Banks et al., *Discrete-Event System Simulation*).
