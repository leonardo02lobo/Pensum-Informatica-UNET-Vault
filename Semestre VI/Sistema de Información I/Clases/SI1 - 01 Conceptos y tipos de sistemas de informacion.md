---
tags: [clase, semestre-VI]
materia: Sistema de Información I
fuente: conocimiento general
---
# SI1 - 01 Conceptos y tipos de sistemas de información

Materia: [[Sistema de Información I]]
Siguiente: [[SI1 - 02 Ciclo de vida de desarrollo SDLC y metodologias]]

## Contexto y objetivo
Todo análisis de sistemas parte de una pregunta: ¿qué es un sistema de información (SI) y qué papel cumple en una organización? Esta nota fija el vocabulario base (dato, información, conocimiento, sistema), los componentes de un SI y su clasificación. El temario sigue el programa típico de la materia; verificar con el programa oficial de la UNET.

## Dato, información y conocimiento
- **Dato**: hecho crudo sin contexto (`"27"`).
- **Información**: datos procesados con significado para una decisión ("27 pedidos pendientes hoy").
- **Conocimiento**: información interpretada y contrastada con la experiencia ("si pendientes > 25 se necesita refuerzo").
Un buen indicador de calidad de la información: **exactitud, oportunidad, relevancia, completitud, consistencia, accesibilidad** (cada una puede medirse; p.ej. exactitud = registros correctos / registros auditados).

## Sistema y sistema de información
**Sistema**: conjunto de elementos interrelacionados que cumplen un objetivo, con entradas, proceso, salidas, retroalimentación y entorno (ver [[Teoría General de Sistemas]]).
**Sistema de información**: conjunto organizado de personas, procesos, datos, hardware, software y redes que recolecta, procesa, almacena y distribuye información para apoyar operación, decisión y control.

Componentes (modelo clásico): 1) personas, 2) procedimientos, 3) datos, 4) software, 5) hardware, 6) comunicaciones. Un SI **no es sinónimo de computadora**: un archivo manual con procedimientos es un SI, aunque no automatizado.

Actividades: **entrada → procesamiento → almacenamiento → salida → control/retroalimentación**.

## Clasificación por nivel organizacional (pirámide)
| Nivel | Tipo | Función | Ejemplo |
|---|---|---|---|
| Operativo | **TPS** (procesamiento de transacciones) | registrar eventos del día a día | punto de venta, nómina |
| Conocimiento | KWS / OAS | apoyo a profesionales y oficinas | diseño CAD, ofimática |
| Táctico | **MIS** (información gerencial) | informes periódicos de resumen | ventas por mes |
| Táctico | **DSS** (apoyo a decisiones) | análisis "qué pasa si" | simulación de precios |
| Estratégico | **EIS/ESS** | tableros ejecutivos | indicadores globales |
Los sistemas integrales: **ERP**, **CRM**, **SCM** (ver [[SI2 - 01 ERP CRM SCM y sistemas de apoyo a decisiones]]).

## Clasificación por la relación con las decisiones
Estructuradas (reglas claras, TPS), semiestructuradas (DSS), no estructuradas (EIS).

## Roles
Analista de sistemas (puente usuario-técnico), usuario, patrocinador, programador, administrador de BD ([[Administración de Base de Datos]]), líder de proyecto.

## Ejemplo resuelto: clasificar sistemas
1. Registro de matrícula de una universidad: **TPS** (captura transacciones).
2. Reporte semestral de deserción por carrera: **MIS**.
3. Modelo que estima cuántas secciones abrir bajo distintos supuestos de inscripción: **DSS**.
4. Tablero del rector con indicadores clave: **EIS**.
Cada uno alimenta al siguiente: el TPS genera los datos que el almacén de datos consolida para MIS/DSS (ver [[BD2 - 06 Data Warehouse OLAP y modelado dimensional]]).

## Errores comunes
- Confundir dato con información.
- Pensar que un SI es solo software.
- Automatizar un proceso defectuoso: se obtiene "un mal proceso, más rápido".
- Ignorar al usuario final en el diseño.

## Ejercicios propuestos
1. Diga si un reporte de ventas del mes pasado es dato o información. *Resp.: información (datos procesados en contexto).*
2. Dé un ejemplo de retroalimentación en un SI de inventario. *Resp.: alerta de reorden cuando el stock baja del mínimo.*
3. ¿Qué tipo de SI es un cajero automático? *Resp.: TPS.*

## Conexiones
[[Base de Datos I]], [[Teoría General de Sistemas]], [[SI1 - 02 Ciclo de vida de desarrollo SDLC y metodologias]].

## Fuente
Conocimiento general (Kendall y Kendall; Laudon y Laudon; Senn). Sin material propio de la materia.
