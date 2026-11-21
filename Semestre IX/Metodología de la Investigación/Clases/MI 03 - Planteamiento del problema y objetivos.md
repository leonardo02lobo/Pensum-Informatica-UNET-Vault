---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 03 - Planteamiento del problema y objetivos

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 02 - Enfoques y tipos de investigación]]
Siguiente: [[MI 04 - Marco teórico y revisión bibliográfica]]

## Contexto y objetivo
Un buen planteamiento del problema es la mitad de la investigación: define qué se hará, por qué importa y hasta dónde llega. Este capítulo suele ser el primero del anteproyecto ([[Estructura del anteproyecto de investigación]]). Objetivo: redactar el planteamiento, la formulación, el objetivo general y los específicos, la justificación, el alcance y las limitaciones, con calidad verificable.

## Selección y delimitación del tema
Criterios de un buen tema: **relevante** (resuelve una necesidad real), **viable** (tiempo, recursos, datos, tutor), **original o útil**, **delimitado** (en tiempo, espacio, población, tecnología), **interesante** para ti.
Delimitar: de "seguridad informática" a "detección de intrusiones en la red WiFi de la facultad usando aprendizaje automático (2026)". Fuentes de ideas: problemas en organizaciones, líneas del departamento, trabajos futuros de artículos, convocatorias. La brecha de investigación (*research gap*) se halla revisando el estado del arte ([[MI 04 - Marco teórico y revisión bibliográfica]]).

## El planteamiento del problema
Estructura clásica (embudo de lo general a lo particular):
1. **Contexto general**: situación mundial/nacional/local del tema (con datos y citas).
2. **Situación actual (diagnóstico)**: cómo se hace hoy en el ámbito específico.
3. **Problema y causas**: qué falla y por qué (se puede apoyar en diagrama de Ishikawa o árbol de problemas).
4. **Consecuencias (pronóstico)**: qué ocurre si no se resuelve.
5. **Control del pronóstico** (qué se propone): la solución en términos generales.
6. **Formulación**: pregunta de investigación.

**Árbol de problemas**: problema central, causas (raíces) y efectos (ramas). Se convierte en **árbol de objetivos**: el problema central pasa a ser objetivo; las causas a medios; los efectos a fines.

### Formulación como pregunta
Debe ser clara, concreta, medible, con variable(s) y unidad de análisis. 
- Mala: "¿Cómo mejorar la seguridad?" 
- Buena: "¿En qué medida un sistema automatizado de control de préstamos reduce el tiempo de atención y las pérdidas de equipos en el Laboratorio X durante el período 2026?"
Para proyectos de desarrollo: "¿Cómo diseñar e implementar un sistema ... que permita ...?"

## Objetivos
### Objetivo general
Expresa el **propósito global**. Un solo verbo en infinitivo, un solo resultado, coherente con el título y la pregunta. Debe poder alcanzarse en el tiempo disponible.
### Objetivos específicos
Pasos concretos y medibles para alcanzar el general, ordenados lógicamente; típicamente 3-5; cada uno con un verbo distinto; cubren cada fase de la metodología (diagnosticar, diseñar, implementar, evaluar).

### Taxonomía de Bloom para elegir el verbo
- Conocer/comprender: identificar, describir, explicar, caracterizar.
- Aplicar/analizar: determinar, comparar, clasificar, relacionar, diagnosticar.
- Sintetizar/evaluar: diseñar, desarrollar, proponer, implementar, evaluar, validar.
Evita verbos ambiguos: *conocer, entender, mejorar* sin métrica, *estudiar*.

### Ejemplo coherente
- Título: Sistema web para el control de préstamos de equipos del Laboratorio X.
- **General**: Desarrollar un sistema web para el control de préstamos de equipos del Laboratorio X que reduzca el tiempo de atención.
- **Específicos**:
  1. Diagnosticar el proceso actual de préstamo, identificando tiempos y puntos críticos.
  2. Definir los requisitos funcionales y no funcionales del sistema.
  3. Diseñar la arquitectura y la base de datos del sistema.
  4. Implementar el sistema aplicando la metodología seleccionada.
  5. Evaluar el desempeño y la usabilidad mediante pruebas y encuesta a usuarios.
Observa: cada específico produce un entregable que se reconoce en el informe (un capítulo o etapa).

### Criterios SMART
Específicos, Medibles, Alcanzables, Relevantes, con Tiempo.

## Justificación
Responde **por qué** vale la pena: importancia **teórica** (aporta conocimiento), **práctica** (resuelve una necesidad), **metodológica** (nuevo instrumento/método), **social/institucional**, **económica**. Incluye beneficiarios y, si procede, relación con las líneas de investigación o con planes nacionales (verificar). Evita frases vacías ("es muy importante porque ayuda"): usa datos.

## Alcance, delimitación y limitaciones
- **Alcance**: hasta dónde llega el trabajo (qué módulos, qué población, qué entregables; qué **no** incluye).
- **Delimitación**: espacial, temporal, temática.
- **Limitaciones**: obstáculos fuera de tu control (acceso a datos, tiempo, recursos, disponibilidad de usuarios).
Sé explícito: "El sistema no incluye facturación ni integración con el sistema académico".

## Viabilidad
Técnica (¿hay tecnología y conocimiento?), operativa (¿lo usarán?), económica (¿costo asumible?), de tiempo, legal/ética. Una viabilidad débil es causa común de abandono de tesis.

## Ejemplo resuelto: de la idea al planteamiento (párrafos guía)
1. Contexto: "La gestión de inventarios mediante registros en papel genera errores y retrasos en organizaciones educativas (citar fuente)".
2. Situación: "En el Laboratorio X los préstamos se anotan en un cuaderno; cada gestión toma en promedio ___ minutos (medir en la fase diagnóstica)".
3. Causas: falta de registro unificado, búsqueda manual, falta de alertas.
4. Consecuencias: pérdida de equipos, imposibilidad de saber disponibilidad, conflictos entre usuarios.
5. Pregunta y objetivos como arriba.
Nota honesta: los datos específicos deben provenir de tu diagnóstico real; no los inventes.

## Errores comunes
- Objetivo general idéntico a un específico, o con dos verbos ("analizar y diseñar").
- Objetivos que describen actividades de trabajo ("reunirse con el tutor").
- Planteamiento que describe la solución antes del problema ("Se necesita una app").
- Pregunta de sí/no cuando se quiere medir un efecto.
- Alcance exagerado (querer resolver todo).
- Justificación sin datos ni beneficiarios.

## Ejercicios propuestos
1. Corrige: "Estudiar el uso de IA y mejorar la educación". *Resp.: delimita población, verbo medible y variable: "Determinar el efecto del uso de ... sobre el rendimiento de estudiantes de ... en ...".*
2. Escribe 4 objetivos específicos para un sistema de reservas de aulas. *Resp. ejemplo: diagnosticar el proceso actual; especificar requisitos; diseñar e implementar el sistema; evaluar con usuarios.*
3. Distingue limitación de delimitación. *Resp.: la delimitación es una decisión del investigador; la limitación es un obstáculo externo.*

## Conexiones
[[Seminario]], [[IS 02 - Ingeniería de requisitos]], [[Gerencia de Proyectos]], [[TAP Tesis]], [[TAP Pasantía]].

## Fuente
Conocimiento general. Hernández Sampieri, caps. de planteamiento; Arias, *El Proyecto de Investigación*; Bloom (taxonomía revisada, Anderson y Krathwohl).
