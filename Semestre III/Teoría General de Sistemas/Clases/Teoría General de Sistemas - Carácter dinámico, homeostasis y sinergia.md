---
tags: [clase, semestre-III]
materia: Teoría General de Sistemas
---
# Teoría General de Sistemas - Carácter dinámico, homeostasis y sinergia

Materia: [[Teoría General de Sistemas]]
Anterior: [[Teoría General de Sistemas - Concepto de sistema y elementos básicos]]
Siguiente: [[Teoría General de Sistemas - Clasificación de sistemas y jerarquía de Boulding]]

## Contexto y objetivo

Los sistemas reales no son fotografías estáticas: cambian en el tiempo, responden a perturbaciones del entorno y exhiben propiedades que no existen en sus partes aisladas. Esta clase profundiza en el **carácter dinámico** de los sistemas (Unidad I): regulación, retroalimentación, homeostasis, sinergia, propiedades emergentes y equifinalidad.

## 1. Carácter dinámico y regulación

Un sistema es **dinámico** cuando su estado cambia a lo largo del tiempo como resultado de sus procesos internos y de su interacción con el entorno. Para evitar que el sistema colapse o se desvíe de sus objetivos ante perturbaciones externas, necesita mecanismos de **regulación y control**.

La regulación consiste en medir el estado actual del sistema (salida), compararlo con un valor de referencia o consigna ($r$) y generar una acción correctiva sobre las entradas o el proceso.

$$e(t) = r(t) - y(t)$$

donde $e(t)$ es el error o desviación en el instante $t$, $r(t)$ es el estado deseado y $y(t)$ es la salida observada.

## 2. Retroalimentación positiva y negativa

La **retroalimentación** (*feedback*) es el mecanismo mediante el cual parte de la salida regresa como entrada para influir en el comportamiento futuro del sistema. Existen dos tipos fundamentales:

1. **Retroalimentación negativa (estabilizadora):**
   - Actúa en sentido contrario a la desviación detectada, reduciendo el error $e(t)$.
   - Mantiene el equilibrio y la estabilidad del sistema.
   - *Ejemplos:* termostato de un aire acondicionado, regulación de la temperatura corporal, control de congestión TCP en redes.

2. **Retroalimentación positiva (amplificadora):**
   - Refuerza o amplifica la desviación en la misma dirección en que ocurrió.
   - Conduce a crecimiento exponencial, saturación o colapso si no se limita.
   - *Ejemplos:* efecto avalancha en una red social viral, interés compuesto, acoplamiento acústico (pitido de micrófono cerca del altavoz), pánico financiero.

## 3. Homeostasis y morfogénesis

- **Homeostasis:** capacidad de un sistema abierto para mantener su equilibrio interno dinámico dentro de márgenes viables, a pesar de las fluctuaciones del entorno. Se logra principalmente mediante **retroalimentación negativa**.
  - *Ejemplo informático:* un balanceador de carga que redirige tráfico y escala instancias automáticamente cuando aumenta la demanda para mantener la latencia dentro de un umbral aceptable.
- **Morfogénesis:** capacidad de un sistema para modificar su propia estructura y forma de organización con el fin de adaptarse a cambios profundos del entorno. Se asocia con la **retroalimentación positiva** controlada (aprendizaje y evolución).

## 4. Sinergia y propiedades emergentes

La **sinergia** (del griego *synergía*, cooperación) se expresa en el principio sistémico clásico: *"el todo es mayor que la suma de sus partes"*. Ocurre cuando la interacción coordinada de los componentes produce un resultado cualitativa o cuantitativamente superior al que producirían operando por separado.

De la sinergia surgen las **propiedades emergentes**: atributos que posee el sistema completo, pero que **no existen** en ninguno de sus componentes individuales.

- *Ejemplo:* un microprocesador, una memoria RAM, un disco y un sistema operativo por separado no pueden ejecutar una aplicación web; al integrarse e interactuar, emerge la capacidad de cómputo distribuido.
- *Ejemplo biológico:* ninguna neurona aislada posee consciencia, pero la red neuronal completa genera pensamiento y lenguaje.

## 5. Equifinalidad y multifinalidad

- **Equifinalidad:** propiedad de los sistemas abiertos por la cual un mismo estado final puede alcanzarse partiendo de **condiciones iniciales diferentes** y siguiendo **caminos distintos**. Contrastar con los sistemas cerrados mecánicos, donde el estado final está rígidamente determinado por las condiciones iniciales.
  - *Ejemplo:* dos estudiantes con conocimientos previos distintos y métodos de estudio diferentes aprueban la misma asignatura; dos arquitecturas de software distintas cumplen el mismo requerimiento de negocio.
- **Multifinalidad:** fenómeno inverso en el que condiciones iniciales similares pueden conducir a estados finales muy distintos según las interacciones con el entorno.

## Errores comunes

- **Pensar que la retroalimentación positiva es "buena" y la negativa "mala":** en TGS, "positiva" y "negativa" no son juicios de valor moral. La negativa estabiliza (vital para sobrevivir) y la positiva amplifica (puede destruir el sistema si no tiene freno, como un cáncer o un bucle infinito).
- **Confundir homeostasis con estatismo:** la homeostasis no significa ausencia de cambio, sino ajuste continuo para conservar variables esenciales dentro de límites estables.

## Ejercicios propuestos

1. **Clasifica el tipo de retroalimentación** en: (a) un servidor que reduce la tasa de envío cuando detecta pérdida de paquetes; (b) un rumor que gana más difusión cuanta más gente lo comparte.
   - *Respuesta:* (a) Retroalimentación negativa (estabiliza la red); (b) Retroalimentación positiva (amplifica la difusión).
2. **Da un ejemplo de propiedad emergente** en un equipo de desarrollo de software.
   - *Respuesta:* La velocidad de entrega continua y la calidad arquitectónica emergen de la colaboración, revisión de código y comunicación entre desarrolladores, QA y diseñadores; ningún integrante aislado las posee por sí solo.

## Conexiones

- La regulación y retroalimentación negativa son la base matemática de los lazos de control en [[Automatización]].
- El comportamiento dinámico de sistemas se modela computacionalmente en [[Simulación de Sistemas]].
- Anterior: [[Teoría General de Sistemas - Concepto de sistema y elementos básicos]].
- Siguiente: [[Teoría General de Sistemas - Clasificación de sistemas y jerarquía de Boulding]].

## Fuente

- Basado en `Material/Introducción asignatura Teoría General de sistemas (1).pdf` y `Material/Parcial I de TGS.docx`.
