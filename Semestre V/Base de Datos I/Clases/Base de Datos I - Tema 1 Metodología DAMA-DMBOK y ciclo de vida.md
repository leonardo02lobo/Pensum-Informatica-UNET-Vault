---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaI/materialApoyo/Metodologia de Base de Datos.pdf
---
# Tema 1 - Marco DAMA-DMBOK y metodología de desarrollo de base de datos

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 1 Fundamentos de Base de Datos]]
Siguiente: [[Base de Datos I - Tema 1 Caso de Estudio Planificación]]

## Contexto y objetivo
Un buen diseño de base de datos no empieza con SQL sino con una **metodología**: saber por qué se hace el proyecto, quién gobierna los datos y en qué fases se construye. El documento "El Marco de Trabajo de Gestión de Datos DAMA-DMBOK y la Metodología de Desarrollo de Base de Datos" (Ing. Silverio Bonilla) presenta (1) el marco internacional DAMA-DMBOK y (2) el ciclo de vida de seis fases que estructura todos los temas de la materia. Se conecta con [[Ingeniería de Software]] (ciclo de vida del software) y con [[Sistema de Información I]].

## 1. Gestión de datos
**Gestión de datos** es el desarrollo, ejecución y supervisión de planes, políticas, programas y prácticas que entregan, controlan, protegen y aumentan el valor de los activos de datos e información durante todo su ciclo de vida. Un **profesional de gestión de datos** es quien trabaja en cualquier faceta (desde la gestión técnica hasta el uso correcto de los datos) para cumplir los objetivos estratégicos de la organización. Premisa: los datos son un **activo empresarial vital**, que permite conocer clientes, productos y servicios, innovar y alcanzar metas.

## 2. El marco DAMA-DMBOK y la Rueda DAMA
DAMA International (Data Management Association) publica la *Guía DAMA del cuerpo de conocimiento de la gestión de datos* (DMBOK). Su ilustración es la **Rueda DAMA**: en el centro la **Gobernanza de Datos** (necesaria para dar coherencia y equilibrio) y alrededor las demás áreas de conocimiento, todas necesarias en una función madura aunque pueden implementarse en momentos distintos según la organización. Áreas (DMBOK 2):
1. Gobernanza de datos (núcleo)
2. Arquitectura de datos
3. Modelado y diseño de datos
4. Almacenamiento y operaciones de datos
5. Seguridad de datos
6. Integración e interoperabilidad
7. Gestión de documentos y contenido
8. Datos maestros y de referencia
9. Data warehousing e inteligencia de negocio
10. Gestión de metadatos
11. Calidad de datos

(El documento de la materia enfatiza gobernanza, arquitectura y modelado; el listado completo corresponde al DMBOK2, verificar con el programa oficial qué áreas se evalúan.)

### Gobernanza de datos
Aplicación de **autoridad y control** (planificación, ejecución, monitoreo) sobre la gestión de los activos de datos. Guía a todas las demás funciones. Se centra en cómo se toman decisiones sobre los datos y cómo se espera que se comporten personas y procesos. Todas las organizaciones toman decisiones sobre datos, tengan o no una función formal; con gobernanza formal capturan más valor. Requisito cultural: la organización debe valorar los datos y gestionar el cambio; sin ello ninguna estrategia funciona. Un programa de gobernanza suele incluir:
- **Estrategia**: definir y comunicar la estrategia de datos y de gobernanza.
- **Política**: establecer y hacer cumplir políticas sobre administración de datos y metadatos, acceso, uso, seguridad y calidad.
- **Estándares y calidad**: fijar y aplicar estándares de calidad y de arquitectura de datos.

## 3. Ciclo de vida de desarrollo de una base de datos (seis fases)
| Fase | Qué se hace | Entregables típicos |
|---|---|---|
| 1. Planificación preliminar | Planificación estratégica de datos; **modelo de datos de alto nivel** con las entidades críticas para la empresa. | Visión de entidades estratégicas, documento de aprobación. |
| 2. Estudio de viabilidad | Viabilidad **técnica**, **económica** y **operativa**. | Informe de viabilidad. |
| 3. Definición de requisitos | Alcance de la BD; requisitos de información de las unidades funcionales (documento de requisitos); necesidades de hardware/software; plan de desarrollo. | Documento de requisitos de datos. |
| 4. Diseño conceptual o lógico | Identificar entidades, **matriz de relaciones**, diagrama Entidad-Relación. | DER, diccionario de datos. |
| 5. Implementación | Transformar el diseño lógico en físico (diagrama de tablas), escribir y ejecutar el script **DDL**, pruebas. | Scripts, base creada, casos de prueba. |
| 6. Evaluación y perfeccionamiento | Medir eficiencia (tiempos de respuesta), optimizar sentencias DML, **entonación** (tuning) de la BD. | Informe de rendimiento. |

La estructura de los temas del curso sigue este ciclo: Tema I (planificación), Tema II (requisitos y modelo conceptual), Tema III (modelo relacional y físico), Tema IV (implementación DDL/DML), Tema V (consultas avanzadas) y Tema VI (PL/SQL).

## 4. Ejemplo resuelto: aplicar el ciclo a "Ventas de entretenimiento"
1. *Planificación*: la junta quiere automatizar pedidos, facturación y despacho; entidades estratégicas: cliente, producto, pedido, factura, despacho.
2. *Viabilidad*: técnica (¿Oracle XE o PostgreSQL en nube?), económica (presupuesto de 10.000 $ repartido por porcentajes), operativa (¿el personal puede operarla? hay capacitación prevista).
3. *Requisitos*: entrevistas con ventas, logística y facturación; se listan "requisitos de datos" (tema II).
4. *Diseño lógico*: matriz de relaciones cliente-pedido (1:N), pedido-producto (M:N resuelta con detalle_pedido).
5. *Implementación*: DDL con claves y restricciones, pruebas con casos de prueba.
6. *Evaluación*: índices sobre columnas de búsqueda frecuente, revisar planes de ejecución.
Ver [[Base de Datos I - Tema 1 Caso de Estudio Planificación]].

## 5. Aprobación del proyecto y trazabilidad (conceptos)
- **Documento de aprobación**: control de versiones (versión, hecho por, revisado por, aprobado por, fecha, motivo); situación actual; descripción del proyecto (qué, para qué, quién, cómo, cuándo, dónde); descripción de la BD; necesidad del negocio; presupuesto; entidades de datos relevantes.
- **Matriz de trazabilidad**: cruza los objetivos de la aplicación (ObjSoft) con los del negocio (ObjNeg) para justificar que cada funcionalidad aporta a una meta.

## Errores comunes
- Saltar directamente a crear tablas sin fase de requisitos: genera rediseños costosos.
- Tratar la gobernanza como un "documento" en vez de roles, políticas y procesos activos.
- Confundir viabilidad económica con presupuesto: la viabilidad compara costos con beneficios.
- Olvidar la fase 6: una base que "funciona" pero lenta incumple el objetivo de eficiencia.

## Ejercicios propuestos
1. ¿En qué fase se elabora el DER? (Diseño conceptual o lógico.)
2. Dé un ejemplo de política de datos de seguridad y una de calidad. (Roles con mínimo privilegio; reglas CHECK/validaciones de rango.)
3. ¿Qué distingue el centro de la Rueda DAMA? (La gobernanza de datos, que coordina el resto.)
4. Enumere las tres viabilidades. (Técnica, económica, operativa.)

## Conexiones
[[Administración de Base de Datos]] (seguridad, respaldo, tuning), [[Base de Datos II]], [[Ingeniería de Software]].

## Fuente
`Material/baseDatosI/temaI/materialApoyo/Metodologia de Base de Datos.pdf` (12 diapositivas). El listado completo de áreas DMBOK2 se añade desde conocimiento general.
