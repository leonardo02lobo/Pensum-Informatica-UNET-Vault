---
tags: [clase, semestre-V]
materia: Proyecto Servicio Comunitario
---
# Proyecto Servicio Comunitario - Planificación, Cronograma, Recursos y Matriz de Marco Lógico

Materia: [[Proyecto Servicio Comunitario]]
Anterior: [[Proyecto Servicio Comunitario - Formulación de Objetivos, Alcance y Justificación]]
Siguiente: [[Proyecto Servicio Comunitario - Evaluación, Indicadores y Sostenibilidad del Proyecto]]

## Contexto y objetivo
Un proyecto bien formulado en papel puede fracasar en la práctica si no cuenta con un plan de ejecución realista. La planificación transforma los objetivos específicos en actividades concretas, asigna tiempos compatibles con las **120 horas mínimas** de ley, identifica los recursos necesarios y anticipa riesgos.

Al finalizar esta clase, el estudiante sabrá desglosar objetivos en actividades, elaborar un diagrama de Gantt ajustado a las horas comunitarias, estimar recursos y construir una Matriz de Marco Lógico (MML).

## 1. De los objetivos a las actividades (EDT / WBS)
Cada objetivo específico se descompone en tareas concretas y asignables. Esta estructura jerárquica (análoga a la Estructura de Desglose de Trabajo vista en [[Gerencia de Proyectos]]) garantiza que ninguna actividad quede sin responsable ni tiempo estimado.

Por ejemplo, para el objetivo *"Capacitar a los voluntarios en el uso del sistema"*:
- Actividad 1: Diseñar el manual de usuario ilustrado (6 horas).
- Actividad 2: Preparar la guía práctica y datos de prueba (4 horas).
- Actividad 3: Dictar 2 sesiones presenciales de capacitación (6 horas).
- Actividad 4: Evaluar el desempeño práctico de los participantes (2 horas).

## 2. Cronograma de actividades y Diagrama de Gantt
El **diagrama de Gantt** representa las actividades en función del tiempo (semanas o meses) y permite verificar dos restricciones clave del servicio comunitario:
1. El lapso total debe cubrir el mínimo reglamentario (generalmente **no menor a 3 meses** / 12–16 semanas).
2. La suma de horas planificadas por estudiante debe alcanzar o superar las **120 horas** (conviene planificar entre 125 y 135 horas para tener margen ante imprevistos).

### Ejemplo simplificado de distribución de horas
| Fase | Semanas | Actividades principales | Horas estimadas |
| :--- | :---: | :--- | :---: |
| 1. Inicio y levantamiento | 1–2 | Reuniones iniciales, observación, entrevistas | 18 h |
| 2. Análisis y diseño | 3–5 | Requisitos, modelo de datos, prototipos | 28 h |
| 3. Desarrollo / Implementación | 6–10 | Programación, pruebas, instalación en sitio | 44 h |
| 4. Capacitación y transferencia | 11–13 | Manuales, talleres con la comunidad | 20 h |
| 5. Cierre y sistematización | 14–15 | Evaluación final, entrega, informe | 14 h |
| **Total** | **15 sem** | | **124 h** |

## 3. Presupuesto y gestión de recursos
Aunque el servicio comunitario es gratuito para la comunidad, todo proyecto consume recursos que deben identificarse con claridad:
- **Recursos humanos**: estudiantes prestadores, tutor académico, tutor comunitario, voluntarios locales.
- **Recursos tecnológicos y materiales**: computadoras disponibles en la comunidad, laptops de los estudiantes, papelería, marcadores, impresiones de manuales.
- **Recursos financieros (autogestión)**: costos mínimos de traslado o papelería asumidos por el equipo o gestionados mediante donaciones/software libre (evitando dependencias de licencias costosas).

## 4. Matriz de Marco Lógico (MML)
La **Matriz de Marco Lógico** resume el diseño del proyecto en una tabla de $4 \times 4$ que vincula objetivos, indicadores, fuentes de verificación y factores externos:

| Nivel | Resumen Narrativo | Indicadores Verificables | Medios de Verificación | Supuestos |
| :--- | :--- | :--- | :--- | :--- |
| **Fin** | Contribuir a la eficiencia administrativa del comedor comunitario. | Reducción de errores de entrega en un 80% a los 6 meses. | Informe semestral de la directiva. | La directiva mantiene el uso del sistema. |
| **Propósito (Obj. General)** | Sistema de registro implementado y operando con personal capacitado. | 100% de beneficiarios registrados al finalizar el proyecto. | Base de datos en producción y acta de entrega. | Estabilidad eléctrica en la sede. |
| **Componentes (Obj. Específicos)** | 1. Base de datos y aplicación instalada.<br>2. 5 voluntarios capacitados. | 1 sistema operativo; 5/5 voluntarios aprobados en prueba práctica. | Código fuente, manuales, listas de asistencia. | Disponibilidad horaria de los voluntarios. |
| **Actividades** | Levantamiento, diseño, desarrollo, pruebas, talleres. | 124 horas ejecutadas según cronograma. | Bitácora firmada y fotografías. | Acceso continuo a las instalaciones. |

## 5. Análisis básico de riesgos
Para cada supuesto crítico de la MML conviene definir una acción de mitigación:
- *Riesgo:* Cortes eléctricos durante los talleres. -> *Mitigación:* Llevar laptops con batería cargada y copias impresas de las guías.
- *Riesgo:* Ausencia de internet en la sede. -> *Mitigación:* Diseñar la aplicación para ejecución local (LAN o `localhost`) sin dependencia de servicios en la nube.

## Errores comunes
- **Planificar horas infladas o irrealistas**: asignar 40 horas a "comprar materiales" o "instalar un programa", lo cual será rechazado por el tutor académico.
- **Dejar el desarrollo para la última semana**: no contemplar tiempo para pruebas con usuarios reales ni para imprevistos comunitarios.
- **Olvidar los medios de verificación**: proponer indicadores imposibles de comprobar documentalmente.

## Ejercicios propuestos
1. Si un equipo de 3 estudiantes realiza una jornada de mantenimiento de 4 horas en una escuela, ¿cuántas horas comunitarias acredita cada estudiante?
   - *Respuesta esperada:* Cada estudiante acredita **4 horas** individuales (las horas no se suman entre integrantes; cada prestador debe cumplir sus 120 horas personales).
2. Completa los medios de verificación y un supuesto para el componente: *"Elaborar e instalar un portal informativo estático para el consejo comunal"*.
   - *Respuesta esperada:* Medios de verificación: URL activa o repositorio del código, capturas de pantalla y acta de recepción firmada. Supuesto: el consejo comunal mantiene activo el dominio/alojamiento gratuito o el equipo local donde reside.

## Conexiones
- Materia principal: [[Proyecto Servicio Comunitario]]
- Anterior: [[Proyecto Servicio Comunitario - Formulación de Objetivos, Alcance y Justificación]]
- Siguiente: [[Proyecto Servicio Comunitario - Evaluación, Indicadores y Sostenibilidad del Proyecto]]
- Relación con gestión: [[Gerencia de Proyectos]]

## Fuente
Basado en el programa típico de la asignatura y en la metodología del Marco Lógico aplicada a proyectos sociales.
