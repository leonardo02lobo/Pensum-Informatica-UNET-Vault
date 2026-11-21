---
tags: [clase, semestre-III]
materia: Teoría General de Sistemas
---
# Teoría General de Sistemas - Aplicación de la TGS a sistemas de información y proyecto Scrum

Materia: [[Teoría General de Sistemas]]
Anterior: [[Teoría General de Sistemas - Enfoque de sistemas, información y entropía]]
Siguiente: —

## Contexto y objetivo

Para cerrar el curso, los conceptos de las tres unidades de [[Teoría General de Sistemas]] se integran en el análisis de un **sistema de información real**, definiendo requisitos empresariales, roles de usuario en el ciclo de vida y gestión iterativa mediante **Scrum**. Esta clase sintetiza cómo trasladar la teoría sistémica a la práctica de la ingeniería informática.

## 1. De la TGS al análisis de sistemas de información

Todo sistema de información empresarial es un sistema **abierto, artificial, socio-técnico (Nivel 8 de Boulding)** y orientado a fines (teleológico). Al analizarlo para el proyecto final deben quedar explícitos:

1. **Elementos del Parcial I:** objetivo, entorno, recursos, componentes, administración, entradas, procesos, salidas, retroalimentación y clasificación completa.
2. **Elementos del Parcial II:** qué enfoques de la TGS explican partes del sistema (por ejemplo, teoría de grafos para flujos de navegación o bases de datos relacionales, teoría de colas para atención de solicitudes, cibernética para alertas automáticas).
3. **Elementos del Parcial III:** cómo se combate la entropía organizacional (neguentropía mediante respaldos, bitácoras, capacitación), qué propiedades emergentes surgen y cómo se mide la información útil.

## 2. Requisitos de la empresa y roles de usuario

Antes de construir el sistema, se levantan los requisitos organizacionales:
- **Requisitos funcionales:** qué debe hacer el sistema (registro de usuarios, facturación, generación de reportes, control de inventario).
- **Requisitos no funcionales:** restricciones de calidad (tiempo de respuesta, seguridad, disponibilidad, escalabilidad).

### Roles de usuario según el ciclo de vida del sistema
- **Cliente / Patrocinador:** define la necesidad de negocio y aprueba el presupuesto.
- **Usuario final:** opera el sistema diariamente y aporta retroalimentación sobre usabilidad.
- **Analista de sistemas:** levanta requisitos, modela procesos y traduce necesidades del entorno en especificaciones.
- **Arquitecto / Desarrollador:** diseña e implementa los componentes y sus interfaces.
- **Aseguramiento de Calidad (QA) / Administrador:** verifica el cumplimiento de requisitos y mantiene la operación estable (homeostasis).

## 3. Metodología Scrum como sistema adaptable

**Scrum** es un marco de trabajo ágil que funciona como un sistema abierto con **retroalimentación continua** en ciclos cortos llamados **Sprints** (usualmente de 1 a 4 semanas).

### Roles en Scrum
- **Product Owner (PO):** representa la voz del cliente/entorno, gestiona y prioriza el *Product Backlog* para maximizar el valor.
- **Scrum Master (SM):** facilita el proceso, elimina impedimentos y protege la organización del equipo (función reguladora).
- **Equipo de Desarrollo (Developers):** grupo autoorganizado y multifuncional que construye el incremento del producto.

### Artefactos y eventos principales
```
Product Backlog ──▶ Sprint Planning ──▶ Sprint Backlog
                                              │
                                        [ Sprint (1-4 sem) ]
                                        [ Daily Scrum 15m  ]
                                              │
                                              ▼
     Retroalimentación ◀── Sprint Review ◀── Incremento
            │
            └──▶ Sprint Retrospective (mejora del proceso)
```

- **Sprint Review:** inspección del incremento con los interesados (retroalimentación sobre el producto).
- **Sprint Retrospective:** inspección del funcionamiento interno del equipo (morfogénesis y mejora continua).

## Errores comunes

- **Presentar Scrum solo como una lista de reuniones:** en un informe de TGS debe explicarse *por qué* cada evento actúa como un lazo de retroalimentación que reduce la entropía del proyecto.
- **Confundir roles del ciclo de vida con roles Scrum:** el Product Owner no es necesariamente el usuario final, ni el Scrum Master es un "jefe tradicional"; su rol es facilitador.

## Ejercicios propuestos

1. **Identifica qué evento de Scrum** corresponde a la retroalimentación sobre el producto y cuál a la retroalimentación sobre el proceso interno del equipo.
   - *Respuesta:* Sobre el producto: *Sprint Review*; sobre el proceso interno: *Sprint Retrospective*.
2. **¿Cómo se manifiesta la equifinalidad en el desarrollo ágil?**
   - *Respuesta:* Distintos equipos o iteraciones pueden alcanzar el mismo objetivo de negocio del cliente mediante diferentes soluciones técnicas o prioridades de backlog.

## Conexiones

- Conecta directamente con [[Base de Datos I]] (diseño de datos del sistema propuesto), [[Ingeniería de Software]] y [[Gerencia de Proyectos]].
- Anterior: [[Teoría General de Sistemas - Enfoque de sistemas, información y entropía]].

## Fuente

- Basado en `Material/Proyecto Final de Teoria General de Sistemas.docx` y `Material/Introducción asignatura Teoría General de sistemas (1).pdf`.
