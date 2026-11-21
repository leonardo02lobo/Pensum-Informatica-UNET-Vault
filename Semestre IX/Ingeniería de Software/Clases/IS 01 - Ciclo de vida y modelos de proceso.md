---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 01 - Ciclo de vida y modelos de proceso

Materia: [[Ingeniería de Software]]
Siguiente: [[IS 02 - Ingeniería de requisitos]]

## Contexto y objetivo
El software no se construye "programando y ya": requiere un **proceso** que ordene actividades, roles y artefactos. Esta clase presenta el ciclo de vida del software (SDLC), los modelos de proceso clásicos y cómo elegir uno según el riesgo, la estabilidad de los requisitos y el tamaño del equipo. Objetivo: que puedas justificar la elección de un modelo para un proyecto concreto (por ejemplo, tu [[TAP Tesis]] o [[TAP Pasantía]]).

## Conceptos base
- **Software**: programas + datos + documentación (definición ampliada). Es intangible, no se desgasta pero se **degrada** por los cambios (la curva de fallos tiene "picos" tras cada modificación).
- **Ingeniería de software** (IEEE 610.12): aplicación de un enfoque sistemático, disciplinado y cuantificable al desarrollo, operación y mantenimiento del software.
- **Crisis del software** (1968, conferencia de la OTAN): proyectos tardíos, sobre presupuesto, de baja calidad. Sigue vigente: los informes CHAOS del Standish Group reportan que una fracción significativa de proyectos falla o se desvía (las cifras exactas varían por edición; consultar la fuente).
- **Proceso de software**: conjunto coherente de actividades para producir software. Actividades universales (Sommerville): **especificación, diseño e implementación, validación, evolución**. Pressman las llama *comunicación, planeación, modelado, construcción, despliegue*.
- **Artefacto**: producto de trabajo (documento, modelo, código, caso de prueba). **Baseline (línea base)**: artefacto revisado y aprobado que solo cambia por control formal de cambios.

## Modelos de proceso

### 1. Cascada (waterfall)
Fases secuenciales: requisitos, análisis, diseño, implementación, pruebas, despliegue, mantenimiento. Cada fase termina con un entregable aprobado. 
- Ventajas: simple, documentación abundante, fácil de gestionar contractualmente.
- Desventajas: los errores de requisitos se descubren tarde (costo de corrección crece de forma aproximadamente exponencial con la fase; Boehm); el cliente ve el producto solo al final.
- Úsalo cuando los requisitos son **estables y bien entendidos** (sistemas embebidos con especificación formal, migraciones).

### 2. Modelo en V
Extiende cascada asociando a cada fase de desarrollo una fase de prueba: requisitos con pruebas de aceptación; diseño de arquitectura con pruebas de sistema; diseño detallado con pruebas de integración; codificación con pruebas unitarias. Resalta que **las pruebas se planifican desde el inicio**.

### 3. Incremental
El sistema se entrega en incrementos funcionales. El primero es el núcleo. Reduce el riesgo y permite retroalimentación temprana. Es la base de casi todos los modelos modernos.

### 4. Prototipado
Se construye un prototipo (desechable o evolutivo) para aclarar requisitos. Riesgo: que el prototipo "desechable" termine siendo el producto final sin calidad estructural.

### 5. Espiral (Boehm, 1988)
Ciclos repetidos de cuatro cuadrantes: (1) determinar objetivos, (2) **identificar y resolver riesgos**, (3) desarrollar y verificar, (4) planificar el siguiente ciclo. Es un modelo *dirigido por riesgos*; adecuado para proyectos grandes y costosos con incertidumbre alta. Su coste de gestión es alto.

### 6. Proceso Unificado (RUP)
Iterativo e incremental, dirigido por casos de uso, centrado en la arquitectura. Cuatro fases: Inicio, Elaboración, Construcción, Transición; disciplinas transversales (modelado de negocio, requisitos, análisis y diseño, implementación, pruebas, despliegue, gestión). Detalle en Metodologías ágiles y RUP.

### 7. Métodos ágiles
Scrum, XP, Kanban: iteraciones cortas (1 a 4 semanas), colaboración con el cliente, cambio bienvenido. Ver Metodologías ágiles y RUP.

### 8. Desarrollo basado en componentes / reutilización
Se ensambla software a partir de componentes o servicios existentes (bibliotecas, APIs, microservicios). Riesgos: dependencia de terceros y desajuste de interfaces.

## Cómo elegir un modelo
| Criterio | Inclina hacia |
|---|---|
| Requisitos estables | Cascada / V |
| Requisitos cambiantes | Ágil / incremental |
| Riesgo técnico alto | Espiral / prototipado |
| Cliente disponible | Ágil |
| Contrato a precio fijo | Plan dirigido + incrementos |
| Equipo muy pequeño (1-3) | Kanban/XP ligero |
| Seguridad crítica (médico, aviación) | V con trazabilidad formal |

## Ejemplo resuelto: elegir modelo para un sistema de inventario
Escenario: laboratorio universitario quiere un sistema de inventario; el encargado no sabe exactamente qué reportes necesita; equipo de 2 estudiantes; 4 meses.
1. Estabilidad de requisitos: baja (el usuario no sabe lo que quiere) lo que descarta cascada pura.
2. Riesgo técnico: bajo (aplicación web CRUD).
3. Disponibilidad del cliente: media (reuniones quincenales).
4. Decisión: **incremental con iteraciones de 2 semanas estilo Scrum-lite**; incremento 1 = altas/bajas de equipos; 2 = préstamos; 3 = reportes. Entrega de demo al final de cada iteración y ajuste del *backlog*.
5. Se conserva de cascada: un documento breve de requisitos (ERS) por incremento y un plan de pruebas.

## Mantenimiento y evolución (Leyes de Lehman)
Los sistemas en uso deben cambiar continuamente o se vuelven progresivamente menos útiles; su complejidad crece salvo que se invierta en reducirla. Tipos de mantenimiento: **correctivo** (errores), **adaptativo** (nuevo entorno), **perfectivo** (nuevas funciones/rendimiento), **preventivo** (refactorización). Típicamente el perfectivo y adaptativo dominan el costo total (del orden de la mayor parte del presupuesto de vida del sistema).

## Errores comunes
- Creer que "ágil" significa "sin documentación ni planificación".
- Usar cascada con requisitos que cambian cada semana.
- Confundir *prototipo* con *producto*.
- No definir criterios de salida de cada fase/iteración (definición de "hecho").
- Ignorar el mantenimiento al estimar costos.

## Ejercicios propuestos
1. Clasifica en V, espiral o ágil: (a) software de control de una bomba de infusión; (b) startup que valida una idea de app. *Resp.: (a) V (o cascada con verificación formal); (b) ágil/prototipado.*
2. ¿Qué cuadrante de la espiral aporta la gestión de riesgos? *Resp.: el segundo (identificar y resolver riesgos).*
3. Explica por qué corregir un error de requisitos en producción cuesta más que en la fase de requisitos. *Resp.: porque afecta diseño, código, pruebas, documentación y usuarios ya desplegados; el trabajo derivado se multiplica.*

## Conexiones
[[Sistema de Información II]] (análisis y diseño), [[Gerencia de Proyectos]] (planificación), [[Sistemas Distribuidos]] (arquitecturas), [[Metodología de la Investigación]] (elegir metodología de desarrollo en el marco metodológico).

## Fuente
Conocimiento general. Referencias: Sommerville, *Ingeniería de Software*; Pressman, *Ingeniería del Software*; Boehm (1988), "A Spiral Model of Software Development and Enhancement".
