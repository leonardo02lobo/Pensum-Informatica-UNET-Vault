---
tags: [clase, semestre-VIII]
materia: Sistema de Información II
---
# Sistema de Información II - Ciclo de Vida y Tipos de Sistemas Empresariales

Materia: [[Sistema de Información II]]
Anterior: — (primera clase)
Siguiente: [[Sistema de Información II - Arquitectura de Sistemas de Información y APIs]]

## Contexto y objetivo
Ubicar el paso del análisis a la **construcción y gestión de sistemas de información empresariales**, repasando las metodologías del ciclo de vida (SDLC) y clasificando los sistemas según el nivel organizacional y los procesos de negocio que soportan (TPS, MIS, DSS, EIS, ERP, CRM, SCM).

## 1. Definición y dimensiones de un Sistema de Información
Un **Sistema de Información (SI)** no es únicamente software: es un conjunto integrado de **personas, procesos, datos y tecnología** que recolecta, procesa, almacena y distribuye información para apoyar la toma de decisiones, la coordinación y el control en una organización.

## 2. Ciclo de Vida de los Sistemas de Información (SDLC)
1. **Planificación y factibilidad**: alineación estratégica, alcance y viabilidad técnica, operativa y económica.
2. **Análisis de requisitos**: levantamiento con usuarios, reglas de negocio y casos de uso (foco principal de [[Sistema de Información I]]).
3. **Diseño detallado**: arquitectura, base de datos, interfaces y flujos de procesos.
4. **Construcción e integración**: codificación, pruebas unitarias y de integración.
5. **Implantación y capacitación**: migración de datos, puesta en producción y gestión del cambio.
6. **Operación y mantenimiento**: monitoreo, soporte, evolución y retiro.

### Enfoques metodológicos
- **Cascada (secuencial)**: útil cuando los requisitos son estables y regulados, pero rígido ante cambios.
- **Iterativo e incremental**: entrega funcionalidad por incrementos validables.
- **Ágil (Scrum, Kanban)**: ciclos cortos (*sprints*), retroalimentación continua con el usuario y adaptación al cambio; requiere disciplina de trazabilidad y pruebas automatizadas en sistemas empresariales críticos.

## 3. Pirámide de sistemas por nivel organizacional
1. **Nivel operativo — TPS (*Transaction Processing Systems*)**: registran las transacciones diarias rutinarias (facturación, nómina, control de inventario, registro de atenciones). Priorizan integridad ACID, alta disponibilidad y velocidad.
2. **Nivel táctico/gerencial — MIS (*Management Information Systems*)**: generan reportes periódicos y resúmenes agregados a partir de los TPS para supervisar el desempeño.
3. **Nivel táctico/analítico — DSS (*Decision Support Systems*)**: combinan datos históricos, modelos matemáticos o simulación para decisiones semiestructuradas ("¿qué pasa si...?").
4. **Nivel estratégico — EIS (*Executive Information Systems*)**: tableros ejecutivos con **KPIs** y alertas de alto nivel para la alta dirección.

## 4. Sistemas empresariales integrados (aplicaciones transversales)
- **ERP (*Enterprise Resource Planning*)**: integra en una base de datos unificada las áreas de finanzas, contabilidad, inventario, compras, producción y recursos humanos (p. ej., Odoo, SAP). Elimina islas de información.
- **CRM (*Customer Relationship Management*)**: gestiona el ciclo completo de relación con el cliente (mercadeo, ventas, postventa, soporte).
- **SCM (*Supply Chain Management*)**: coordina la cadena de suministro desde proveedores hasta distribución final.

## Errores comunes
- Confundir un **TPS** (orientado a operar y registrar transacciones en tiempo real) con un **MIS/BI** (orientado a consolidar, agregar y analizar tendencias históricas).
- Implantar un **ERP** sin rediseñar ni documentar previamente los procesos de negocio de la empresa, trasladando el desorden manual al software.

## Ejercicios propuestos
1. En una universidad, clasifique en TPS, MIS, DSS o EIS: (a) módulo de inscripción de asignaturas en línea; (b) tablero rectoral con tasa de deserción y rendimiento por facultad; (c) reporte mensual de materias con mayor reprobación.
   - *Respuesta*: (a) TPS; (b) EIS; (c) MIS.
2. ¿Por qué la **trazabilidad** (requisito $\leftrightarrow$ diseño $\leftrightarrow$ código $\leftrightarrow$ prueba) es indispensable en un SI empresarial?
   - *Respuesta*: permite verificar que cada necesidad del negocio fue implementada y probada, facilita auditorías y controla el impacto de futuros cambios.

## Conexiones
- Antecedentes de análisis en [[Sistema de Información I]] y [[Organización]].
- Visión sistémica en [[Teoría General de Sistemas]].
- Evolución hacia ingeniería formal de procesos en [[Ingeniería de Software]].

## Fuente
Basado en el programa orientativo de [[Sistema de Información II]] (Laudon & Laudon, *Sistemas de Información Gerencial*; Kendall & Kendall, *Análisis y Diseño de Sistemas*).
