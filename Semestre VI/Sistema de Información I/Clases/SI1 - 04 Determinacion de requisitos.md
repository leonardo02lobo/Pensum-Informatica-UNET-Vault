---
tags: [clase, semestre-VI]
materia: Sistema de Información I
fuente: conocimiento general
---
# SI1 - 04 Determinación de requisitos

Materia: [[Sistema de Información I]]
Anterior: [[SI1 - 03 Investigacion preliminar y factibilidad]]
Siguiente: [[SI1 - 05 Diagramas de flujo de datos y diccionario de datos]]

## Contexto y objetivo
Los errores de requisitos son los más caros del desarrollo. **Determinar requisitos** es descubrir, documentar y validar qué necesitan los usuarios del sistema. Objetivo: dominar las técnicas de levantamiento, redactar requisitos de calidad y gestionarlos.

## Tipos de requisitos
- **Funcionales (RF)**: servicios que el sistema debe ofrecer. "El sistema permitirá registrar una venta".
- **No funcionales (RNF)**: restricciones y calidades: rendimiento, seguridad, usabilidad, disponibilidad, portabilidad, mantenibilidad. "El 95 % de las consultas responderá en menos de 2 s".
- **De dominio / reglas de negocio**: "un préstamo no excede 3 libros".
- **De usuario** (lenguaje natural) vs **de sistema** (detallados y técnicos).

## Técnicas de levantamiento
| Técnica | Cuándo | Ventaja | Riesgo |
|---|---|---|---|
| Entrevista (estructurada, abierta) | pocos usuarios clave | profundidad | sesgo, tiempo |
| Cuestionario | muchos usuarios | alcance | preguntas mal formuladas, baja tasa de respuesta |
| Observación | procesos reales | revela lo no dicho | efecto Hawthorne (cambian al ser observados) |
| Revisión de documentos | formularios, reportes, manuales | objetivo | desactualizados |
| JAD / talleres | consenso rápido | colaboración | requiere facilitador |
| Prototipos | UI incierta | validación visual | expectativas |
| Historias de usuario | ágil | cercano al usuario | falta de detalle |
Buenas prácticas de entrevista: preparar guion, preguntas abiertas y cerradas, no sugerir respuestas, resumir y confirmar, documentar de inmediato.

## Calidad de un requisito
Debe ser **necesario, no ambiguo, medible/verificable, consistente, completo, factible, trazable e identificado** (RF-012). Evitar palabras vagas: "rápido", "amigable", "etc.".

Plantilla: *"El sistema [deberá] [verbo] [objeto] [condición/criterio]"*. Ejemplo: "El sistema deberá calcular el total de la factura incluyendo IVA en menos de 1 segundo".

Historia de usuario: *Como [rol] quiero [acción] para [beneficio]*, con **criterios de aceptación** (Dado/Cuando/Entonces).

## Documento de especificación (ERS / SRS)
Introducción, descripción general, requisitos funcionales, no funcionales, interfaces externas, restricciones, apéndices. Norma de referencia: IEEE 830 (sustituida por ISO/IEC/IEEE 29148).

## Gestión de requisitos
- **Priorización**: MoSCoW (Must, Should, Could, Won't) o matriz valor/esfuerzo.
- **Trazabilidad**: matriz requisito → caso de uso → diseño → prueba.
- **Control de cambios**: solicitud, análisis de impacto, aprobación, versión.
- **Validación**: revisiones, prototipos, pruebas de aceptación.

## Ejemplo resuelto: biblioteca universitaria
Entrevista con la bibliotecaria revela:
- RF-01 Registrar préstamo (cédula, código de libro).
- RF-02 Calcular multa: 0,5 USD por día de retraso.
- RN-01 Máximo 3 libros por estudiante.
- RNF-01 Búsqueda de catálogo en menos de 2 s con 50 000 títulos.
- RNF-02 Solo el personal autenticado modifica el catálogo.
Matriz de trazabilidad: RF-02 → CU "Devolver libro" → tabla `multa` → prueba P-07. Priorización MoSCoW: RF-01 Must, reportes estadísticos Could.
Requisito mal redactado: "El sistema debe ser rápido". Reescritura verificable: "El sistema responderá a la búsqueda en menos de 2 s en el 95 % de las consultas".

## Errores comunes
- Confundir solución con requisito ("usar un combo desplegable").
- No distinguir quién es el usuario real.
- Requisitos contradictorios entre departamentos sin arbitraje.
- Congelar requisitos sin proceso de cambio.
- No incluir RNF.

## Ejercicios propuestos
1. Clasifique: "los datos personales se cifrarán". *Resp.: no funcional (seguridad).*
2. Reescriba "interfaz amigable". *Resp.: "un usuario nuevo completa una venta en menos de 3 min sin capacitación (prueba con 5 usuarios)".*
3. ¿Qué técnica usaría para 500 estudiantes? *Resp.: cuestionario.*

## Conexiones
[[SI1 - 05 Diagramas de flujo de datos y diccionario de datos]], [[SI1 - 06 UML casos de uso y diagramas de actividad]], [[Ingeniería de Software]].

## Fuente
Conocimiento general (Kendall y Kendall; Sommerville; IEEE 830).
