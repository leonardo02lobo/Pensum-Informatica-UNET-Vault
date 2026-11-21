---
tags: [clase, semestre-III]
materia: Teoría General de Sistemas
---
# Teoría General de Sistemas - Concepto de sistema y elementos básicos

Materia: [[Teoría General de Sistemas]]
Anterior: —
Siguiente: [[Teoría General de Sistemas - Carácter dinámico, homeostasis y sinergia]]

## Contexto y objetivo

Esta primera clase introduce la terminología fundamental de la **Unidad I** de [[Teoría General de Sistemas]]. El objetivo es comprender qué es un sistema desde el punto de vista formal, identificar sus elementos constitutivos y analizar los cinco aspectos clave propuestos por C. W. Churchman para estudiar cualquier sistema real o conceptual.

## 1. Definición de sistema

Un **sistema** es un conjunto ordenado de componentes o elementos interrelacionados entre sí —ya sean materiales o conceptuales— que interactúan de forma organizada para cumplir un propósito o función común, dotado de una estructura, una composición y un entorno particulares.

Todo sistema puede entenderse como un segmento de la realidad que se aísla conceptualmente para su estudio, sin perder de vista que sus partes dependen unas de otras: si se modifica un componente, el efecto se propaga al resto del conjunto.

### Elementos estructurales básicos
- **Componentes (partes):** elementos individuales que integran el sistema (pueden ser subsistemas).
- **Relaciones:** vínculos lógicos, físicos o informacionales que conectan a los componentes.
- **Estructura:** patrón estable de organización de las relaciones entre los componentes.
- **Frontera (límite):** línea real o conceptual que separa al sistema de su entorno y define qué pertenece al sistema y qué queda fuera.
- **Entorno (medio ambiente):** conjunto de objetos y condiciones externas que influyen en el sistema y se ven influidos por él, pero que no están bajo su control directo.

## 2. Modelo básico de flujo: Entrada, Proceso, Salida y Retroalimentación

Cualquier sistema dinámico puede representarse mediante el siguiente diagrama funcional:

```
Entradas (Inputs) ──▶ [ Proceso / Transformación ] ──▶ Salidas (Outputs)
        ▲                                                      │
        └─────────────── Retroalimentación (Feedback) ◀────────┘
```

1. **Entradas (Inputs):** materia, energía o información que el sistema importa desde el entorno para operar.
2. **Proceso (Transformación):** actividad interna mediante la cual los componentes convierten las entradas en salidas.
3. **Salidas (Outputs):** resultados (productos, servicios, datos, calor, residuos) que el sistema entrega al entorno.
4. **Retroalimentación (Feedback):** retorno de información sobre el desempeño o resultado de las salidas hacia la entrada, permitiendo ajustar el comportamiento del sistema.

## 3. Los cinco aspectos relevantes en el estudio de un sistema (Churchman)

Para analizar rigurosamente un sistema se consideran cinco dimensiones fundamentales:

| Aspecto | Pregunta clave | Descripción |
| :--- | :--- | :--- |
| **1. Objetivos** | ¿Para qué existe el sistema? | Metas o propósitos que justifican su funcionamiento y permiten medir su desempeño. |
| **2. Medio ambiente** | ¿Qué lo rodea y condiciona? | Factores externos que imponen restricciones o suministran entradas fuera del control del sistema. |
| **3. Recursos** | ¿Con qué cuenta el sistema? | Medios internos (humanos, financieros, tecnológicos, materiales, información) disponibles para operar. |
| **4. Componentes** | ¿Qué partes ejecutan las tareas? | Subsistemas y actividades específicas cuya ejecución contribuye al logro de los objetivos. |
| **5. Administración** | ¿Cómo se planifica y controla? | Función que fija objetivos, asigna recursos, coordina componentes y evalúa resultados mediante retroalimentación. |

## 4. Ejemplo resuelto: Sistema de inscripción universitaria

Analicemos el proceso de inscripción en una universidad como la UNET bajo el enfoque de sistemas:

- **Objetivo:** inscribir a los estudiantes en sus asignaturas correspondientes sin conflictos de horario ni violación de prelaciones.
- **Entradas:** solicitudes de inscripción, notas aprobadas, oferta académica, cupos por sección.
- **Componentes:** módulo de autenticación, validador de prelaciones, gestor de cupos, generador de horarios.
- **Proceso:** verificación de requisitos académicos, reserva de cupo y registro de la carga académica.
- **Salidas:** planilla de inscripción confirmada, listas de clase para docentes, estadísticas de demanda.
- **Entorno:** Dirección de Control de Estudios, estudiantes, docentes, normativa académica y fallas eléctricas o de red.
- **Recursos:** servidores, base de datos, personal de soporte, red universitaria.
- **Administración:** reglas de negocio, fechas de inscripción por índice académico y monitoreo de errores.
- **Retroalimentación:** reportes de choques de horario o secciones saturadas que llevan a abrir nuevos cupos o ajustar reglas.

## Errores comunes

- **Confundir entorno con recursos:** el entorno está fuera del control del sistema (por ejemplo, las leyes o el clima), mientras que los recursos están dentro de la frontera y el sistema los administra.
- **Definir objetivos como actividades:** "procesar datos" es una actividad o proceso; un objetivo debe expresar un propósito medible (por ejemplo, "garantizar la integridad y disponibilidad de los registros académicos").
- **Omitir la frontera:** sin definir la frontera es imposible distinguir qué es entrada, qué es componente interno y qué pertenece al entorno.

## Ejercicios propuestos

1. **Identifica los 5 aspectos de Churchman** para un sistema de biblioteca universitaria.
   - *Respuesta breve:* Objetivo: facilitar el acceso al material bibliográfico; Medio ambiente: editoriales, políticas universitarias, usuarios; Recursos: libros, personal, software, presupuesto; Componentes: catalogación, préstamo, devolución; Administración: dirección de biblioteca y reglamento de préstamos.
2. **Distingue entrada, proceso y salida** en un compilador de C++.
   - *Respuesta breve:* Entrada: código fuente `.cpp`; Proceso: análisis léxico, sintáctico, semántico y generación de código; Salida: ejecutable binario o mensajes de error.

## Conexiones

- Fundamento conceptual para el modelado de datos en [[Base de Datos I]] y el análisis de procesos en [[Ingeniería de Software]].
- Se relaciona con los sistemas de control estudiados en [[Automatización]] y la visión histórica de [[Introducción a la Ingeniería Informática]].
- Continúa en [[Teoría General de Sistemas - Carácter dinámico, homeostasis y sinergia]].

## Fuente

- Basado en `Material/Introducción asignatura Teoría General de sistemas (1).pdf`, `Material/Parcial I de TGS.docx` y `Material/Primer ensayo TGS_ Sistemas. Grupo 4 Sección 3. .docx`.
