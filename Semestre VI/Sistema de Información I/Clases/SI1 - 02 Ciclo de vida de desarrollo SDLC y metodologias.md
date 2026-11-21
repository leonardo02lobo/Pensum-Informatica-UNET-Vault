---
tags: [clase, semestre-VI]
materia: Sistema de Información I
fuente: conocimiento general
---
# SI1 - 02 Ciclo de vida de desarrollo (SDLC) y metodologías

Materia: [[Sistema de Información I]]
Anterior: [[SI1 - 01 Conceptos y tipos de sistemas de informacion]]
Siguiente: [[SI1 - 03 Investigacion preliminar y factibilidad]]

## Contexto y objetivo
Desarrollar un SI sin método conduce a sobrecostos y rechazo del usuario. El **ciclo de vida de desarrollo de sistemas (SDLC)** organiza el trabajo en fases. Objetivo: conocer las fases, los modelos (cascada, iterativo, prototipado, espiral, ágil) y criterios para elegir.

## Fases del SDLC
1. **Planificación / identificación del problema**: necesidad, alcance, objetivos.
2. **Análisis**: requisitos, procesos actuales, datos (DFD, casos de uso).
3. **Diseño**: arquitectura, base de datos, interfaces, controles.
4. **Implementación**: codificación, pruebas, conversión de datos, capacitación.
5. **Mantenimiento**: correctivo, adaptativo, perfectivo, preventivo (consume típicamente 60–80 % del costo total del ciclo de vida).
Cada fase produce **entregables** (documentos o artefactos) y termina en un **hito** de revisión.

## Modelos
### Cascada (*waterfall*)
Fases secuenciales sin retorno. Ventajas: orden, documentación, fácil gestión. Desventajas: cambios costosos, el usuario ve el producto al final. Útil con requisitos estables y bien entendidos.

### Prototipado
Se construye una versión inicial para validar requisitos y se refina. *Desechable* (se descarta) o *evolutivo* (se convierte en el sistema). Reduce el riesgo de requisitos malentendidos; riesgo: prototipo "pasa a producción" sin diseño.

### Incremental / iterativo
Entregas parciales funcionales (incrementos); cada iteración repasa análisis-diseño-prueba.

### Espiral (Boehm)
Ciclos con cuatro cuadrantes: determinar objetivos, **analizar riesgos**, desarrollar y verificar, planificar siguiente vuelta. Para proyectos grandes y de alto riesgo.

### Modelo en V
Cada fase de desarrollo tiene su fase de prueba paralela: requisitos↔aceptación, diseño↔integración, codificación↔unitarias.

### Ágil (Scrum, XP, Kanban)
Manifiesto Ágil: individuos e interacciones, software funcionando, colaboración con el cliente, respuesta al cambio. **Scrum**: sprints de 1–4 semanas, roles (Product Owner, Scrum Master, equipo), artefactos (backlog de producto, backlog de sprint, incremento), eventos (planificación, daily, revisión, retrospectiva). **Kanban**: tablero con límite de trabajo en curso. Ver [[Ingeniería de Software]].

## Desarrollo estructurado vs orientado a objetos
Estructurado: DFD, diccionario de datos, ER, enfoque en procesos y datos ([[SI1 - 05 Diagramas de flujo de datos y diccionario de datos]]). Orientado a objetos: UML, casos de uso, clases ([[SI1 - 06 UML casos de uso y diagramas de actividad]]).

## Criterios de selección
| Situación | Modelo recomendado |
|---|---|
| Requisitos estables, contrato fijo | Cascada / V |
| Usuario no sabe lo que quiere | Prototipado / ágil |
| Alto riesgo técnico | Espiral |
| Entrega rápida de valor | Incremental / ágil |

## Ejemplo resuelto
Sistema de control de inventario para una ferretería (3 desarrolladores). Requisitos poco claros: se opta por **prototipado + incrementos**: incremento 1 (catálogo y existencias, 3 semanas), 2 (compras y proveedores), 3 (reportes). Tras cada incremento el dueño valida. Costo de un cambio de requisito: bajo en el incremento 1; en cascada el mismo cambio descubierto en pruebas costaría órdenes de magnitud más (regla clásica de Boehm: el costo crece exponencialmente con la fase en que se detecta).

## Errores comunes
- Saltar el análisis "porque ya sé qué hacer".
- Documentar de más en ágil o nada en absoluto: ágil no significa "sin documentación".
- Confundir prototipo con producto.
- Subestimar el mantenimiento.

## Ejercicios propuestos
1. ¿Qué modelo usaría para un sistema de control de vuelo? *Resp.: V o espiral (seguridad crítica, riesgo alto).*
2. Diferencie mantenimiento correctivo y perfectivo. *Resp.: corrige errores / mejora funcionalidad o rendimiento.*
3. ¿Qué es un incremento? *Resp.: porción funcional entregable del sistema.*

## Conexiones
[[Ingeniería de Software]], [[Gerencia de Proyectos]], [[SI2 - 07 Pruebas implantacion y gestion del cambio]].

## Fuente
Conocimiento general (Kendall y Kendall; Pressman; Sommerville).
