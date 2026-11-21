---
tags: [clase, semestre-III]
materia: Teoría General de Sistemas
---
# Teoría General de Sistemas - Origen, evolución y enfoques de la TGS

Materia: [[Teoría General de Sistemas]]
Anterior: [[Teoría General de Sistemas - Clasificación de sistemas y jerarquía de Boulding]]
Siguiente: [[Teoría General de Sistemas - Enfoque de sistemas, información y entropía]]

## Contexto y objetivo

Esta clase desarrolla la **Unidad II** de [[Teoría General de Sistemas]]. Se estudia el surgimiento histórico de la TGS en el siglo XX, las vías para organizar sus teorías y el mapa de los principales **enfoques y disciplinas matemáticas y conceptuales** que la integran.

## 1. Origen y evolución histórica

A mediados del siglo XX, la ciencia tradicional había alcanzado un alto grado de especialización, pero cada disciplina hablaba un idioma propio y estudiaba los fenómenos de forma aislada. En la década de 1950, el biólogo austriaco **Ludwig von Bertalanffy** formuló la **Teoría General de Sistemas (TGS)** buscando principios y modelos válidos para sistemas de cualquier naturaleza (biológicos, físicos, sociales o tecnológicos).

En 1954 se fundó la *Society for General Systems Research* (con von Bertalanffy, Kenneth Boulding, Anatol Rapoport y Ralph Gerard), consolidando la TGS como un marco interdisciplinario orientado a descubrir **isomorfismos**: leyes estructuralmente idénticas que aparecen en campos distintos (por ejemplo, ecuaciones exponenciales en crecimiento poblacional, desintegración radiactiva e interés compuesto).

## 2. Enfoques para organizar las teorías de sistemas

Para estructurar el conocimiento sistémico existen dos grandes caminos:

1. **Enfoque empírico (inductivo):** parte de la observación de múltiples sistemas reales en distintas disciplinas, identifica regularidades y formula modelos comunes (por ejemplo, la jerarquía de Boulding).
2. **Enfoque epistemológico (deductivo / axiomático):** parte de definiciones formales, axiomas y estructuras matemáticas generales (como conjuntos, relaciones y funciones) para derivar propiedades aplicables a cualquier sistema posible.

## 3. Principales enfoques y herramientas de la TGS

La TGS integra un conjunto amplio de teorías formales y aplicadas:

| Enfoque | Idea central | Aplicación típica |
| :--- | :--- | :--- |
| **Teoría clásica de sistemas** | Usa cálculo diferencial y ecuaciones dinámicas (Bertalanffy) para describir crecimiento, competencia y equilibrio. | Dinámica de poblaciones, sistemas físicos continuos. |
| **Teoría de las gráficas (grafos)** | Modela elementos como vértices ($V$) y relaciones como aristas ($E$): $G=(V,E)$. | Redes de computadores, rutas, dependencias de tareas. |
| **Teoría de redes y de juegos** | Redes de flujo y toma de decisiones estratégicas entre agentes racionales con intereses en conflicto o cooperación. | Economía, seguridad informática, asignación de recursos. |
| **Cibernética y Teoría de la Información** | Control y comunicación en animales y máquinas (Wiener); medición cuantitativa de la información (Shannon). | Control automático, telecomunicaciones, compresión de datos. |
| **Teoría de la decisión** | Selección óptima de alternativas bajo certeza, riesgo o incertidumbre. | Inteligencia de negocios, sistemas expertos. |
| **Teoría de colas** | Estudio matemático de líneas de espera, tasas de llegada ($\lambda$) y tasas de servicio ($\mu$). | Servidores web, atención al cliente, tráfico de paquetes. |
| **Enfoque axiomático de Mesarovic** | Define un sistema formalmente como una relación sobre conjuntos de entradas y salidas: $S \subseteq X \times Y$. | Especificación formal de software y sistemas abstractos. |
| **Teoría entrelazada de Wymore** | Modelo matemático riguroso (sistemas T3D) que unifica sistemas discretos y continuos para ingeniería de sistemas. | Diseño de ingeniería de sistemas complejos. |
| **Enfoque de Churchman** | Aborda los sistemas desde la filosofía de la gestión y la ética, evaluando objetivos, entorno, recursos, componentes y administración. | Gestión organizacional y proyectos de TI. |
| **Teorías inductivas e isomorfismos** | Extracción de patrones comunes mediante analogías estructurales rigurosas entre disciplinas distintas. | Transferencia de modelos biológicos a computación (redes neuronales, algoritmos genéticos). |

## 4. Ejemplo de isomorfismo: Teoría de grafos en dos dominios

Un mismo grafo dirigido $G = (V, E)$ puede representar:
- **En redes de computadoras:** enrutadores ($V$) y enlaces de comunicación ($E$) para hallar la ruta más corta.
- **En gestión de proyectos:** tareas ($V$) y prelaciones ($E$) para calcular la ruta crítica.

Aunque la materia física es distinta, la estructura matemática y los algoritmos (como Dijkstra o Bellman-Ford) son exactamente los mismos.

## Errores comunes

- **Confundir isomorfismo con metáfora superficial:** un isomorfismo exige una correspondencia estructural o matemática exacta entre relaciones de dos sistemas, no una simple comparación poética.
- **Creer que la TGS reemplaza a las disciplinas particulares:** la TGS no sustituye a la física, la biología o la informática, sino que proporciona un lenguaje puente entre ellas.

## Ejercicios propuestos

1. **¿Qué enfoque de la TGS usarías** para dimensionar cuántos cajeros o servidores necesita un sistema de atención con llegadas aleatorias?
   - *Respuesta:* Teoría de colas.
2. **¿Qué diferencia al enfoque empírico del enfoque axiomático de Mesarovic?**
   - *Respuesta:* El empírico parte de observar sistemas reales para generalizar patrones; el axiomático parte de definiciones matemáticas formales ($S \subseteq X \times Y$) para deducir propiedades universales.

## Conexiones

- La teoría de grafos y relaciones conecta directamente con [[Estructura de Datos]] y [[Estructuras Discretas]].
- La teoría de colas y la teoría de juegos se profundizan en [[Investigación de Operaciones I]].
- La cibernética se aplica en [[Automatización]].
- Anterior: [[Teoría General de Sistemas - Clasificación de sistemas y jerarquía de Boulding]].
- Siguiente: [[Teoría General de Sistemas - Enfoque de sistemas, información y entropía]].

## Fuente

- Basado en `Material/Trabajo II Unidad 2.docx`, `Material/Trabajo II Unidad 2.pdf`, `Material/tgs 2 parcial borrador.docx` y `Material/Introducción asignatura Teoría General de sistemas (1).pdf`.
