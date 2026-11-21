---
tags: [clase, semestre-III]
materia: Teoría General de Sistemas
---
# Teoría General de Sistemas - Enfoque de sistemas, información y entropía

Materia: [[Teoría General de Sistemas]]
Anterior: [[Teoría General de Sistemas - Origen, evolución y enfoques de la TGS]]
Siguiente: [[Teoría General de Sistemas - Aplicación de la TGS a sistemas de información y proyecto Scrum]]

## Contexto y objetivo

Esta clase cubre la **Unidad III** de [[Teoría General de Sistemas]]: las limitaciones del pensamiento reduccionista clásico, las metas de la TGS y los conceptos integradores de **información, entropía, causalidad, teleología, organización y unidad de la ciencia**.

## 1. Carencias de los enfoques analíticos-mecánicos

El método científico clásico (heredado de Descartes y Newton) se basa en el **reduccionismo** y el **mecanicismo**:
1. Descomponer el objeto de estudio en sus partes más pequeñas.
2. Estudiar cada parte de forma aislada.
3. Sumar los resultados para explicar el todo.

Este enfoque funciona muy bien en sistemas simples o de relojería (Nivel 2 de Boulding), pero **falla ante sistemas complejos** (biológicos, sociales, informáticos distribuidos) porque:
- **Ignora las interacciones:** al aislar las partes se destruyen las relaciones que producen la sinergia y las propiedades emergentes.
- **No explica la finalidad:** el mecanicismo solo busca causas pasadas (causa-efecto lineal), pero no explica cómo un sistema se orienta hacia metas futuras.
- **Pierde la visión del entorno:** descontextualiza al sistema de las fuerzas externas que lo condicionan.

El **enfoque de sistemas** supera estas carencias integrando el análisis (ver las partes) con la síntesis (ver el todo y su entorno).

## 2. Metas de la TGS y unidad de la ciencia

Las principales metas de la Teoría General de Sistemas son:
1. Promover la integración entre ciencias naturales y sociales.
2. Desarrollar principios unificadores que atraviesen horizontalmente las distintas disciplinas (**unidad de la ciencia**).
3. Eliminar la duplicación de esfuerzos teóricos mediante el descubrimiento de isomorfismos.
4. Proveer una base metodológica para resolver problemas complejos de organización, diseño y control.

## 3. Información y entropía

### Entropía termodinámica vs. Neguentropía
La **entropía** es la medida del desorden, desgaste o pérdida de diferenciación dentro de un sistema. Según la segunda ley de la termodinámica, todo sistema cerrado tiende irreversiblemente hacia un estado de máxima entropía (desorden y muerte térmica).

Los **sistemas abiertos**, en cambio, pueden sobrevivir y mantener su estructura importando energía, materia e información del entorno. A esta capacidad de importar orden se le llama **neguentropía** (entropía negativa). En una empresa u organización informática, la capacitación, el mantenimiento preventivo, la documentación y los respaldos son formas de neguentropía que evitan la degradación del sistema.

### Entropía de la información (Shannon)
En teoría de la información, Claude Shannon definió la entropía $H$ como la medida promedio de incertidumbre (o cantidad de información) asociada a una fuente de mensajes con probabilidades $p_1, p_2, \dots, p_n$:

$$H = -\sum_{i=1}^{n} p_i \log_2(p_i) \quad \text{[bits]}$$

- Si un evento es totalmente seguro ($p_1 = 1$), $H = 0$ bits (no aporta información nueva).
- Si todos los $n$ resultados son equiprobables ($p_i = 1/n$), la entropía alcanza su valor máximo: $H = \log_2(n)$ bits.

## 4. Causalidad, teleología y organización

- **Causalidad lineal:** una causa $A$ produce un efecto $B$ ($A \rightarrow B$). Propia de sistemas mecánicos cerrados.
- **Causalidad circular:** $A$ influye en $B$ y $B$ retroalimenta a $A$ ($A \leftrightarrow B$). Propia de sistemas con retroalimentación.
- **Teleología:** estudio de los fines, propósitos o metas que guían el comportamiento de un sistema. Un sistema teleológico (como un misil guiado, un algoritmo de optimización o una organización) ajusta sus acciones en función del objetivo que desea alcanzar.
- **Organización:** grado de ordenamiento y diferenciación funcional entre las partes de un sistema que le permite sostenerse frente a la entropía.

## Ejemplo numérico de entropía de Shannon

Supongamos un sensor industrial que envía dos posibles estados: `OK` con probabilidad $p_1 = 0.75$ y `ERROR` con probabilidad $p_2 = 0.25$.

$$H = -\left(0.75 \log_2(0.75) + 0.25 \log_2(0.25)\right)$$
$$H = -\left(0.75 \cdot (-0.415) + 0.25 \cdot (-2)\right) = 0.311 + 0.500 = 0.811 \text{ bits}$$

Si ambos estados fueran igualmente probables ($p_1 = p_2 = 0.5$), la incertidumbre sería máxima: $H = 1$ bit.

## Errores comunes

- **Confundir entropía con "caos absoluto":** en informática, mayor entropía de una fuente significa mayor imprevisibilidad y, por tanto, mayor contenido de información por símbolo (útil en criptografía y compresión).
- **Aplicar reduccionismo puro a fallas de software:** depurar un módulo aislado sin revisar su interacción con la base de datos o la concurrencia suele ocultar el verdadero origen sistémico del error.

## Ejercicios propuestos

1. **Calcula la entropía de Shannon** para una moneda justa ($p_{\text{cara}} = 0.5, p_{\text{sello}} = 0.5$).
   - *Respuesta:* $H = -(0.5 \log_2 0.5 + 0.5 \log_2 0.5) = 1$ bit.
2. **Explica por qué la documentación técnica actúa como neguentropía** en un proyecto de software.
   - *Respuesta:* Reduce la pérdida de conocimiento cuando cambian los integrantes del equipo, preservando el orden y la mantenibilidad del sistema frente al desgaste del tiempo.

## Conexiones

- La entropía de Shannon se vincula con compresión y transmisión en [[Comunicaciones I]] y cálculo probabilístico en [[Estadística I]].
- La visión integral de organización y teleología fundamenta [[Ingeniería de Software]] y [[Gerencia de Proyectos]].
- Anterior: [[Teoría General de Sistemas - Origen, evolución y enfoques de la TGS]].
- Siguiente: [[Teoría General de Sistemas - Aplicación de la TGS a sistemas de información y proyecto Scrum]].

## Fuente

- Basado en `Material/tgs 3 parcial.docx` y `Material/Introducción asignatura Teoría General de sistemas (1).pdf`.
