---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 03 - Casos de uso e historias de usuario

Materia: [[Ingeniería de Software]]
Anterior: [[IS 02 - Ingeniería de requisitos]]
Siguiente: [[IS 04 - Modelado con UML]]

## Contexto y objetivo
Los requisitos funcionales se suelen capturar como **casos de uso** (enfoques dirigidos por plan, RUP) o como **historias de usuario** (enfoques ágiles). Ambos describen valor para un actor, pero con diferente nivel de detalle y formalidad. Objetivo: escribir ambos con calidad, derivar criterios de aceptación y saber cuándo usar cada uno.

## Casos de uso

### Definiciones
- **Actor**: rol externo que interactúa con el sistema (persona, sistema externo, temporizador). No es un usuario concreto sino un rol.
- **Caso de uso (CU)**: secuencia de interacciones entre uno o más actores y el sistema que produce un resultado observable de valor para un actor (Jacobson).
- **Escenario**: una ruta concreta a través de un CU (curso básico o alternos).
- **Diagrama de casos de uso (UML)**: óvalos (CU), figuras (actores), caja (frontera del sistema), asociaciones.
- Relaciones: **include** (el CU base siempre invoca al incluido, p.ej. "Registrar préstamo" incluye "Autenticar"), **extend** (comportamiento opcional bajo condición, p.ej. "Aplicar descuento" extiende "Registrar venta"), **generalización** entre actores o CU.

### Niveles de objetivo (Cockburn)
Nube (estratégico), **nivel de usuario/mar** (un objetivo de un actor en una sesión: el que modelamos), pez (subfunción). Un CU bien dimensionado cumple la "prueba del jefe": ¿el actor se iría contento tras completarlo?

### Plantilla de caso de uso completo
```
CU-02: Registrar préstamo de equipo
Actor principal: Técnico de laboratorio
Actores secundarios: Sistema de correo
Precondiciones: El técnico está autenticado; el equipo existe.
Garantía de éxito (postcondición): Préstamo registrado y equipo en estado "prestado".
Disparador: El solicitante pide un equipo.
Curso básico:
 1. El técnico selecciona "Nuevo préstamo".
 2. El sistema solicita equipo y solicitante.
 3. El técnico ingresa los datos.
 4. El sistema valida disponibilidad y estado del equipo.
 5. El sistema registra el préstamo con fecha prevista de devolución.
 6. El sistema muestra el comprobante.
Cursos alternos:
 4a. El equipo no está disponible: el sistema informa y ofrece lista de espera (fin).
 4b. El equipo está dañado: se rechaza el préstamo.
 3a. Solicitante no registrado: incluir CU-05 Registrar solicitante.
Requisitos especiales: respuesta menor a 2 s.
Frecuencia: ~50 veces/día (estimar con el cliente).
```

### Cómo identificarlos
1. Lista los actores. 2. Para cada actor, pregunta "¿qué quiere lograr con el sistema?". 3. Nombra el CU con **verbo + objeto** ("Consultar saldo"). 4. Elimina CU que son meros CRUD triviales si el cliente no los percibe como objetivo (agrúpalos en "Gestionar X"). 5. Valida el modelo con los stakeholders.

## Historias de usuario

### Formato
"**Como** <rol>, **quiero** <acción/capacidad>, **para** <beneficio>."
Ejemplo: "Como técnico, quiero ver los equipos vencidos, para reclamarlos a tiempo."

### Las 3 C (Ron Jeffries)
- **Card**: la tarjeta (recordatorio breve).
- **Conversation**: la conversación que detalla.
- **Confirmation**: criterios de aceptación.

### Criterio INVEST (Bill Wake)
Independent, Negotiable, Valuable, Estimable, Small, Testable.

### Criterios de aceptación en Gherkin (BDD)
```gherkin
Escenario: Rechazar préstamo de equipo dañado
  Dado que el equipo "Osciloscopio-03" tiene estado "dañado"
  Cuando el técnico intenta registrar su préstamo
  Entonces el sistema muestra "Equipo no disponible"
  Y no se crea ningún registro de préstamo
```
Estructura Dado (contexto) / Cuando (acción) / Entonces (resultado). Se puede automatizar con Cucumber/Behave.

### Épicas, historias y tareas
Una **épica** es una historia grande que se parte en historias; cada historia se descompone en **tareas** técnicas dentro de la iteración. Se mantienen en el *product backlog* ordenado por valor.

### Estimación: puntos de historia
Unidad relativa (secuencia Fibonacci: 1, 2, 3, 5, 8, 13). **Planning Poker**: cada miembro vota en secreto, se discuten extremos y se re-vota. La **velocidad** del equipo (puntos completados por sprint) permite proyectar. Ver [[IS 10 - Gestión de proyectos y estimación]].

## Comparación
| Aspecto | Caso de uso | Historia de usuario |
|---|---|---|
| Detalle | Alto, flujos y alternos | Bajo, se detalla en conversación |
| Documentación | Formal | Ligera |
| Trazabilidad | Fácil | Requiere herramienta |
| Contexto | RUP, contratos | Scrum, XP |
| Riesgo | Burocracia | Pérdida de conocimiento si no se registra |

Se pueden combinar: casos de uso para el modelo global y historias para planificar iteraciones.

## Ejemplo resuelto: de caso de uso a historias y pruebas
Para CU-02 (arriba):
1. Historias: H1 "Como técnico, quiero registrar un préstamo para controlar el inventario" (5 pts); H2 "Como técnico, quiero que el sistema rechace equipos dañados para evitar entregarlos" (2 pts); H3 "Como solicitante, quiero un comprobante para tener evidencia" (3 pts).
2. Criterios de aceptación para H2: escenario Gherkin anterior.
3. Casos de prueba derivados de los flujos: básico (OK), 4a (no disponible), 4b (dañado), 3a (solicitante nuevo): **4 casos mínimos**, uno por camino.

## Errores comunes
- CU que describen la interfaz ("el usuario pulsa el botón azul") en lugar del objetivo.
- Historias gigantes ("Como usuario quiero un sistema completo").
- Historias sin beneficio (no se puede priorizar por valor).
- Criterios de aceptación vagos ("debe funcionar bien").
- Un CU por cada tabla de la BD.

## Ejercicios propuestos
1. Escribe el diagrama (texto) de CU para una biblioteca: actores y 4 CU. *Resp. posible: Actores Socio, Bibliotecario; CU: Buscar libro, Prestar libro, Devolver libro, Renovar préstamo (extend de Prestar o separado).*
2. ¿"Autenticar" debería ser include o extend de "Consultar notas"? *Resp.: include si siempre se exige.*
3. Aplica INVEST a "Como usuario quiero reportes". *Resp.: no es Small/Estimable/Testable; dividir por tipo de reporte con criterios.*

## Conexiones
[[Sistema de Información II]] (diagramas de casos de uso), [[Base de Datos I]], [[IS 01 - Ciclo de vida y modelos de proceso]].

## Fuente
Conocimiento general. Cockburn, *Writing Effective Use Cases*; Cohn, *User Stories Applied*; Larman, *UML y Patrones*.
