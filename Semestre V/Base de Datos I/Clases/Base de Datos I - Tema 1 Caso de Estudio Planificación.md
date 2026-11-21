---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaI/casoEstudio/ (Caso Estudio Tema 1 2025-1.pdf, casoEstudio1.docx.pdf, Formato Aprobación Proyecto Tema 1 2024-3 .doc.pdf, Formato Trazabilidad Tema 1 2024-3.docx.pdf)
---
# Tema 1 - Caso de estudio: fase de planificación (Gestión de Ventas de Productos de Entretenimiento)

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 1 Metodología DAMA-DMBOK y ciclo de vida]]
Siguiente: [[Base de Datos I - Tema 2 Caso de Estudio Requisitos y DER]]

## Contexto
El caso de estudio de la materia (lapso 2025-1, UNET, Departamento de Ingeniería en Informática) es un proyecto de desarrollo de base de datos que se construye por entregas, una por tema. Esta nota documenta el **enunciado del Tema 1** y los tres documentos de apoyo (formato de aprobación, formato de trazabilidad y un informe de equipo de ejemplo), explicando qué evalúa cada uno y cómo abordarlo.

## 1. Enunciado resumido
Los ejecutivos de una compañía de **Gestión de Ventas de Productos de Entretenimiento** detectan una fuerte caída de ventas por: precios altos, falta de promociones atractivas, retrasos en la entrega y desinformación del estado de los despachos. Se decide **automatizar por Web** pedidos, facturación y despacho. El fin del caso es **desarrollar la base de datos** que soporte esa aplicación, y que permita: (1) mantener los datos operativos, (2) parametrizar y flexibilizar la gestión, (3) alta eficiencia de acceso, (4) robustez, integridad y consistencia, (5) respaldo y recuperación oportuna.

Un Gerente de Proyecto (Ing. Pedro Pérez, personaje del enunciado) acuerda ejecutarlo en fases: objetivos del negocio y de la aplicación; requisitos y entidades; análisis; diseño relacional; implementación.

**Propósitos de la aplicación y de la BD**:
1. Gestionar datos de pedidos, facturación y despacho.
2. Generar automáticamente precios según categorías, promociones, tiendas y ciudades (menos errores manuales).
3. Optimizar tiempos de despacho por zonas y ciudades.
4. Permitir al cliente consultar en tiempo real el estado y ubicación de su pedido.
5. Gestionar informes y estadísticas para decisiones.
6. Administrar parámetros de la aplicación.

**Presupuesto**: 10.000 $: 30 % equipos, 20 % nube, 20 % adiestramiento, 20 % asesorías, 10 % reserva gerencial (3.000 / 2.000 / 2.000 / 2.000 / 1.000).

**Informe del proyecto** (estructura exigida): 1 Introducción; 2 Justificación; 3 Marco funcional DAMA-DMBOK (qué es, por qué y para qué; estructura general); 4 Objetivo general y específicos; 5 Fase de planificación (a: función y actividades del marco DMBOK en planificación; b: documento de aprobación; c: trazabilidad objetivos del negocio vs. objetivos de la aplicación); 6 Definición de requisitos; 7 Diseño conceptual/lógico; 8 Implementación; 9 Requerimientos de consultas y funcionalidades. **En este tema solo se entregan los puntos 1 a 5**; el informe se alimenta en cada fase.

## 2. Cómo resolver cada sección
### Introducción y justificación
Describir el problema (síntomas: precios, promociones, retrasos, desinformación), la solución (BD relacional para una app web), el marco (DAMA-DMBOK) y el alcance del informe. La justificación debe responder: necesidad empresarial, solución, alineación con objetivos estratégicos, viabilidad económica y **consecuencias de no ejecutar** el proyecto. Un recurso útil es una tabla "objetivo del negocio -> cómo lo respalda la BD" (mejorar servicio -> consulta y trazabilidad en tiempo real; reducir costos -> eliminar tareas manuales; agilizar -> automatización integral; aumentar márgenes -> promociones dinámicas).

### Marco DAMA-DMBOK
Explicar qué es (guía de DAMA International con principios, procesos y buenas prácticas), por qué (los datos son un activo; su gestión mejora calidad, innovación y ventaja competitiva) y para qué (roles, políticas, métodos y métricas). Describir la rueda (gobernanza al centro y áreas alrededor) y aplicar cada área al proyecto (p. ej. modelado -> DER y diccionario de datos; calidad -> reglas CHECK y métricas; seguridad -> roles cliente/operador/admin).

### Objetivos
Un **objetivo general** (el "qué" integral) y **objetivos específicos** medibles (SMART: específicos, con indicador y fecha). El informe de ejemplo del equipo define 8 objetivos específicos (elicitación de requisitos, diseño lógico 3FN, implementación física, lógica de negocio en BD, seguridad y respaldo con RPO/RTO, calidad de datos, rendimiento y transferencia de conocimiento) con metas y fechas, y criterios de éxito (cobertura funcional, disponibilidad, reducción de reclamos, ROI, madurez de gobernanza). Nota: ese ejemplo supone PostgreSQL 16, mientras el curso trabaja en Oracle; las cifras (ROI, plazos, porcentajes) son supuestos del equipo, no datos del enunciado.

### Fase de planificación (5a): función y actividades DMBOK
Se pide justificar qué hace el marco en esta fase. El ejemplo del equipo lo organiza por dominio:
| Dominio | Función en planificación | Actividades | Entregable |
|---|---|---|---|
| Gobernanza | definir autoridad, control, políticas | asignar roles (sponsor, data steward), políticas de nomenclatura y control de cambios | matriz RACI, política v1.0 |
| Arquitectura | trazar el marco tecnológico | elegir motor, topología de 3 capas (Web, API, BD) | diagrama de arquitectura |
| Modelado y diseño | lenguaje común | glosario, convención de nombres PK/FK | estándares de modelado |
| Calidad | prevenir defectos | métricas (nulos, duplicados, rangos) | checklist de calidad |
| Seguridad | proteger desde la concepción | clasificar datos, roles mínimos | política preliminar |

### Documento de aprobación (5b)
El formato proporcionado ("Aprobación Desarrollo de Base de Datos") contiene: control de versiones (0.1 borrador, 1.0 aprobación formal); nombre y siglas del proyecto (en el ejemplo, BDGVPE); situación actual con limitaciones; descripción del proyecto respondiendo qué/para qué/quién/cómo/cuándo/dónde; descripción de la BD (repositorio normalizado a 3FN); necesidad del negocio; presupuesto preliminar; y **entidades de datos** relevantes. Entidades listadas en el ejemplo: Producto, Categoría, Tienda, Ciudad, Promoción, Cliente, Pedido, Detalle Pedido, Factura, Despacho. Estas diez entidades son el germen del DER del Tema 2.

### Trazabilidad (5c)
La matriz cruza **objetivos del software** (filas, ObjSof1..ObjSofn) con **objetivos del negocio** (columnas, ObjNeg1..ObjNegm). Cada celda con una marca justifica *cómo* el objetivo de la aplicación contribuye al del negocio; una fila vacía revela una funcionalidad sin valor de negocio, y una columna vacía un objetivo de negocio no cubierto. Ejemplos del formato: "seguimiento en tiempo real de pedidos" apoya "mejorar calidad de servicio"; "automatización del cálculo de precios" apoya "reducir costos operativos" y "aumentar márgenes". El formato incluye 10 objetivos de software (seguimiento, notificaciones, precios automáticos, facturas y guías, optimización de rutas, GPS, promociones dinámicas, dashboard, parámetros configurables, módulo de calidad) frente a 4 objetivos de negocio. Los números del formato (ahorros, porcentajes) son ilustrativos.

## 3. Qué evalúa este entregable
- Comprensión del ciclo de vida y de la fase de planificación.
- Capacidad de redactar objetivos medibles y alinearlos con el negocio (trazabilidad).
- Uso adecuado del marco DAMA-DMBOK como referencia, no como lista memorizada.

## Errores comunes
- Objetivos vagos ("mejorar el sistema") sin indicador.
- Copiar tecnologías que no corresponden al entorno de la asignatura sin justificarlo.
- Matriz de trazabilidad con todas las celdas marcadas sin explicación (pierde valor).
- Mezclar contenido de fases posteriores (requisitos, DER) en esta entrega.

## Ejercicios propuestos
1. Redacte un objetivo específico medible sobre calidad de datos. (Ej.: "Reducir a menos de 1 % los registros de cliente duplicados al cierre de la fase de implementación, medido con una consulta de conteo por cédula".)
2. Construya una matriz de trazabilidad 3x3 con "notificar despacho", "calcular precios", "dashboard" frente a "servicio", "costos", "decisiones".
3. Reparta un presupuesto de 12.000 $ con los mismos porcentajes. (3.600 / 2.400 / 2.400 / 2.400 / 1.200.)

## Conexiones
Metodología: [[Base de Datos I - Tema 1 Metodología DAMA-DMBOK y ciclo de vida]]. Gestión de proyectos de software: [[Ingeniería de Software]]. Siguiente entrega: [[Base de Datos I - Tema 2 Caso de Estudio Requisitos y DER]].

## Fuente
Archivos de `Material/baseDatosI/temaI/casoEstudio/`: enunciado "Caso Estudio Tema 1 2025-1.pdf"; informe de equipo `casoEstudio1.docx.pdf` (mayo 2025); formatos de aprobación y de trazabilidad. Los nombres de autores del informe de ejemplo no se reproducen aquí.
