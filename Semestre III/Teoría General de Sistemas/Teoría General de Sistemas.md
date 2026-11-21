---
tags: [materia, semestre-III]
semestre: III
---
# Teoría General de Sistemas

**Semestre:** [[Semestre III]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Introducción a la Ingeniería Informática]]

## Desbloquea
- [[Base de Datos I]]

## Apuntes

### Descripción general y objetivos

Teoría General de Sistemas (TGS) forma el **pensamiento sistémico**: dotar al estudiante de conceptos para percibir, identificar, clasificar, estudiar, analizar y caracterizar situaciones reales como sistemas, mediante la filosofía, el enfoque, las metodologías y técnicas de la TGS. Prelación: [[Introducción a la Ingeniería Informática]]. Desbloquea [[Base de Datos I]] y es fundamento de análisis y diseño de sistemas de información, [[Simulación de Sistemas]] y gestión de proyectos.

### Contenido programático (según la presentación de la asignatura)

#### Unidad I. Terminología básica de sistemas (Parcial I, 35 %)
1. Concepto de sistema.
2. Aspectos relevantes en su estudio: **objetivos, medio ambiente, recursos, componentes y administración**.
3. Carácter dinámico: regulación, **retroalimentación**, comportamiento.
4. Jerarquía de los sistemas según **Boulding**; análisis de disgregación y agregación.
5. Clasificación: físicos/abstractos, abiertos/cerrados, discretos/continuos/híbridos, neutrales/controlados, determinísticos/probabilísticos.

#### Unidad II. Teoría General de Sistemas (Parcial II, 40 %)
1. Origen y evolución histórica de la TGS (von Bertalanffy, años 1950).
2. Enfoques para organizar teorías de sistemas: empírico, epistemológico.
3. Enfoques de la TGS: teoría clásica, teoría de las gráficas, teoría de redes y de juegos, cibernética y teoría de la información, teoría de la decisión, teoría de colas, enfoque axiomático de Mesarovic, teoría entrelazada de Wymore, enfoque axiomático de Churchman, teorías inductivas e isomorfismos.

#### Unidad III. El enfoque de sistemas (Parcial III, 25 %)
1. Carencias de los enfoques analíticos-mecánicos.
2. Metas de la TGS.
3. Conceptos importantes: **información y entropía**, causalidad y teleología, organización, unidad de la ciencia.

### Conceptos clave y definiciones

- **Sistema**: conjunto ordenado de componentes relacionados entre sí (materiales o conceptuales) con estructura, composición y entorno propios.
- **Entorno (medio ambiente)**: lo que rodea al sistema e influye en él; la **frontera** lo separa.
- **Sistema abierto**: intercambia materia, energía o información con el entorno; **cerrado**: no.
- **Entrada, proceso, salida y retroalimentación** (positiva amplifica, negativa estabiliza).
- **Homeostasis**: tendencia a mantener el equilibrio interno.
- **Sinergia y propiedades emergentes**: el todo es más que la suma de las partes.
- **Entropía**: medida del desorden; los sistemas abiertos pueden importar neguentropía.
- **Equifinalidad**: un mismo estado final se alcanza por caminos distintos.
- **Isomorfismo**: semejanza estructural entre sistemas de distinta naturaleza.
- **Cibernética** (Wiener): control y comunicación en sistemas.
- **Escalas de Boulding**: estructuras estáticas, relojería, termostato, célula, planta, animal, ser humano, organización social, sistemas trascendentales.

### Fórmulas y representaciones

```
Modelo básico:   Entradas ──▶ [ Procesos / Componentes ] ──▶ Salidas
                      ▲                                        │
                      └────────── Retroalimentación ◀──────────┘

Entropía de Shannon:  H = - Σ p_i · log2(p_i)    (bits)
```

### Ejemplo resuelto

**Sistema de inscripción universitaria**: Objetivo: inscribir estudiantes sin errores. Entradas: solicitudes y cupos. Procesos: validación de prelaciones, asignación de sección. Salidas: planilla de inscripción. Entorno: Control de Estudios, estudiantes. Retroalimentación: errores reportados que corrigen reglas. Es un sistema abierto, artificial, discreto y determinístico.

### Proyecto final (Material)

Las pautas piden presentar y defender el análisis del sistema propuesto: componentes (Parcial 1), dónde se explican los conceptos del 2.º y 3.er parcial, requisitos de la empresa, roles de usuario según el ciclo de vida y la metodología **Scrum** bien detallada.

### Relación con otras materias

- Parte de [[Introducción a la Ingeniería Informática]].
- Desbloquea [[Base de Datos I]] (modelado de datos como sistema de información).
- Se vincula con [[Simulación de Sistemas]], [[Automatización]] (control y retroalimentación) y [[Investigación de Operaciones I]] (modelos y teoría de colas).

### Evaluación y consejos de estudio

- Cronograma según la presentación: Unidad I = trabajo individual (20), dos trabajos en grupo (15 + 15) y parcial escrito (50); Unidad II = dos trabajos en grupo (25 + 25) y parcial escrito (50); Unidad III = trabajo en grupo (100). Verificar con el programa oficial.
- Entregas por correo y avisos por Telegram/Google; la puntualidad es estricta.
- Preparar ejemplos propios de cada concepto (clasificar sistemas reales).
- Redactar con citas y bibliografía; los trabajos incluyen introducción, desarrollo, conclusión y referencias.

### Bibliografía recomendada

- von Bertalanffy, L. *Teoría general de los sistemas*, Fondo de Cultura Económica.
- Johansen, O. *Introducción a la teoría general de sistemas*, Limusa.
- Churchman, C. W. *El enfoque de sistemas*.
- Boulding, K. "General Systems Theory: The Skeleton of Science" (1956).

### Recursos del Material/

- [Introducción asignatura Teoría General de sistemas (1).pdf](Material/Introducci%C3%B3n%20asignatura%20Teor%C3%ADa%20General%20de%20sistemas%20(1).pdf): objetivos, contenido por unidad, cronograma y puntos importantes.
- [Parcial I de TGS.docx](Material/Parcial%20I%20de%20TGS.docx): desarrollo de la Unidad I (concepto de sistema y aspectos relevantes).
- [Primer ensayo TGS: Sistemas](Material/Primer%20ensayo%20TGS_%20Sistemas.%20Grupo%204%20Secci%C3%B3n%203.%20.docx): ensayo grupal sobre sistemas.
- [Trabajo II Unidad 2.docx](Material/Trabajo%20II%20Unidad%202.docx) y [PDF](Material/Trabajo%20II%20Unidad%202.pdf), [tgs 2 parcial borrador.docx](Material/tgs%202%20parcial%20borrador.docx): enfoques de la TGS (clásica, gráficas, redes y juegos, cibernética, etc.).
- [tgs 3 parcial.docx](Material/tgs%203%20parcial.docx): carencias de enfoques analíticos, metas de la TGS, información y entropía, causalidad y teleología.
- [Proyecto Final de Teoria General de Sistemas.docx](Material/Proyecto%20Final%20de%20Teoria%20General%20de%20Sistemas.docx): pautas del proyecto final (Scrum, roles, requisitos).
