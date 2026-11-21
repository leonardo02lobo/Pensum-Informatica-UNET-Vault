---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 02 - Ingeniería de requisitos

Materia: [[Ingeniería de Software]]
Anterior: [[IS 01 - Ciclo de vida y modelos de proceso]]
Siguiente: [[IS 03 - Casos de uso e historias de usuario]]

## Contexto y objetivo
Un requisito mal entendido es el origen más caro de defectos. La ingeniería de requisitos (IR) es el proceso de descubrir, analizar, documentar, validar y gestionar lo que el sistema debe hacer y las restricciones bajo las que debe operar. Al terminar sabrás clasificar requisitos, aplicar técnicas de elicitación, redactar una ERS y verificar la calidad de cada requisito.

## Definiciones
- **Requisito** (IEEE 610.12): condición o capacidad que necesita un usuario para resolver un problema o lograr un objetivo; o que debe cumplir el sistema para satisfacer un contrato, estándar o especificación.
- **Requisito funcional (RF)**: servicio o comportamiento que el sistema ofrece ("El sistema permitirá registrar un préstamo de equipo").
- **Requisito no funcional (RNF)**: propiedad o restricción sobre cómo se presta el servicio. Categorías (ISO/IEC 25010): rendimiento, seguridad, usabilidad, fiabilidad, mantenibilidad, portabilidad, compatibilidad, adecuación funcional. Además, restricciones de diseño/legales/de negocio.
- **Requisito de dominio**: derivado de reglas del dominio (p.ej. reglas contables).
- **Stakeholder**: persona u organización afectada por el sistema (usuarios, clientes, operadores, reguladores).

## El proceso de IR
1. **Estudio de viabilidad**: ¿es técnica, económica y operativamente factible?
2. **Elicitación (descubrimiento)**.
3. **Análisis y negociación**: detectar conflictos, priorizar.
4. **Especificación**: documento ERS y/o modelos.
5. **Validación**: revisiones, prototipos, casos de prueba.
6. **Gestión**: control de cambios y trazabilidad durante toda la vida.

Es **iterativo**: en métodos ágiles el ciclo ocurre en cada iteración sobre el backlog.

## Técnicas de elicitación
| Técnica | Cuándo | Riesgo |
|---|---|---|
| Entrevistas (estructuradas, abiertas) | Conocer necesidades y contexto | Sesgo del entrevistado; conocimiento tácito no dicho |
| Cuestionarios | Muchos usuarios | Preguntas mal formuladas, baja respuesta |
| Observación / etnografía | Procesos reales vs declarados | Efecto del observador |
| Talleres JAD | Resolver conflictos entre stakeholders | Logística |
| Análisis de documentos y sistemas existentes | Sistemas heredados | Información obsoleta |
| Prototipos | Interfaces y requisitos difusos | Expectativas infladas |
| Casos de uso e historias de usuario | Comportamiento | Detalle insuficiente |
| Lluvia de ideas | Innovación | Poca estructura |

Buenas preguntas de entrevista: "Cuéntame cómo haces X hoy", "¿qué pasa cuando falla Y?", "¿quién más interviene?", "¿cómo sabrás que el sistema ayudó?".

## Calidad de un requisito (IEEE 830 / ISO 29148)
Debe ser **necesario, no ambiguo, completo, consistente, verificable, factible, trazable y atómico**.

Ejemplo malo: "El sistema debe ser rápido y fácil de usar." 
Ejemplo bueno: "RNF-03: el 95% de las consultas de inventario deberán responder en menos de 2 s con 50 usuarios concurrentes." 
Palabras sospechosas: *rápido, amigable, flexible, adecuado, etc., y/o, normalmente*.

Plantilla EARS (Easy Approach to Requirements Syntax): 
- Ubicuo: "El <sistema> deberá <respuesta>."
- Dirigido por evento: "Cuando <evento>, el <sistema> deberá <respuesta>."
- Estado: "Mientras <estado>, el <sistema> deberá ..."
- No deseado: "Si <condición>, entonces el <sistema> deberá ..."

Verbos normativos: **deberá** (obligatorio), **debería** (recomendado), **podrá** (opcional).

## Documento de Especificación de Requisitos (ERS, IEEE 830)
Estructura clásica:
1. Introducción (propósito, alcance, definiciones, referencias, visión general).
2. Descripción general (perspectiva del producto, funciones, características de usuarios, restricciones, supuestos y dependencias).
3. Requisitos específicos (interfaces externas, funciones, rendimiento, restricciones de diseño, atributos de calidad).
4. Apéndices e índice.
La norma ISO/IEC/IEEE 29148 sustituyó a la 830; conserva el espíritu.

## Priorización
- **MoSCoW**: Must, Should, Could, Won't (this time).
- **Kano**: básicos, de desempeño, de deleite.
- **Valor/Esfuerzo**: matriz 2x2.
- **100 puntos**: cada stakeholder reparte 100 puntos.

## Trazabilidad
Matriz que vincula requisito, caso de uso, componente de diseño, código y caso de prueba. Permite análisis de impacto: "si cambia RF-12, ¿qué pruebas y módulos se afectan?".

Ejemplo (fragmento):
| Requisito | Caso de uso | Componente | Prueba |
|---|---|---|---|
| RF-01 Registrar préstamo | CU-02 | PrestamoService | CP-010, CP-011 |
| RNF-03 Respuesta menor a 2 s | - | Capa de consulta + índice | CP-050 (carga) |

## Ejemplo resuelto: de la necesidad a requisitos verificables
Necesidad declarada: "Queremos controlar quién se lleva los equipos del laboratorio."
1. Preguntas: ¿quién autoriza? ¿cuánto tiempo puede estar prestado? ¿qué pasa si no devuelve?
2. RF derivados:
   - RF-01: Cuando un técnico registre un préstamo, el sistema deberá guardar equipo, solicitante, fecha y fecha de devolución prevista.
   - RF-02: Si un equipo supera la fecha de devolución, el sistema deberá marcarlo "vencido" y listarlo en el reporte diario.
   - RF-03: El sistema no permitirá prestar un equipo con estado "dañado".
3. RNF: RNF-01 autenticación obligatoria con roles (técnico/administrador); RNF-02 respaldo diario; RNF-03 respuesta menor a 2 s.
4. Restricción: debe funcionar en navegadores de los laboratorios (verificar versiones).
5. Validación: se muestra un prototipo de pantalla y se contrastan RF con el encargado, firmando la ERS.

## Errores comunes
- Mezclar requisitos con diseño ("usar MySQL" no es requisito salvo restricción real).
- Omitir los RNF hasta que el sistema es lento o inseguro.
- No identificar a todos los stakeholders.
- Documentar y no validar con quienes usarán el sistema.
- *Gold plating*: agregar funciones no pedidas.
- Congelar requisitos sin gestión de cambios.

## Ejercicios propuestos
1. Reescribe de forma verificable: "La aplicación debe soportar muchos usuarios." *Resp.: "El sistema deberá soportar 500 usuarios concurrentes con tiempo medio de respuesta menor a 3 s."*
2. Clasifica: "El sistema cifrará las contraseñas con bcrypt." *Resp.: RNF de seguridad (o restricción de diseño).*
3. Prioriza con MoSCoW: login, exportar a PDF, modo oscuro, registrar venta. *Resp.: Must: login y registrar venta; Could: exportar PDF; Won't/Could: modo oscuro.*

## Conexiones
[[Sistema de Información II]] (levantamiento de información), [[Base de Datos I]] (requisitos de datos), [[Metodología de la Investigación]] (instrumentos de recolección: entrevista, cuestionario), [[Estadística I]] (tamaño de muestra de encuestas).

## Fuente
Conocimiento general. Sommerville, *Ingeniería de Software* (cap. de ingeniería de requisitos); IEEE 830-1998; ISO/IEC/IEEE 29148:2018.
