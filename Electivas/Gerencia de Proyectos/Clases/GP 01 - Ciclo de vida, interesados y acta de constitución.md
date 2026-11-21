---
tags: [clase, electiva]
materia: Gerencia de Proyectos
fuente: "conocimiento general"
---
# GP 01 - Ciclo de vida, interesados y acta de constitución

Materia: [[Gerencia de Proyectos]]
Anterior: —
Siguiente: [[GP 02 - Alcance y WBS]]

## Contexto y objetivo
Todo proyecto comienza con una pregunta: ¿qué es exactamente un proyecto y quién tiene interés en él? Esta clase define proyecto, programa y portafolio, describe el ciclo de vida y los grupos de procesos del PMBOK, y construye el **acta de constitución** y el **registro de interesados**. (Temario a verificar con el programa oficial; el PMBOK tiene ediciones con estructuras distintas, aquí se usa la clásica de grupos de procesos y se mencionan los dominios de la 7.ª edición.)

## Teoría

### Definiciones
- **Proyecto**: esfuerzo temporal para crear un producto, servicio o resultado único. Tiene inicio y fin definidos, es progresivamente elaborado y está sujeto a restricciones.
- **Programa**: grupo de proyectos relacionados gestionados de forma coordinada. **Portafolio**: conjunto de proyectos y programas alineados a objetivos estratégicos.
- **Operaciones** son repetitivas y continuas; los proyectos son únicos y temporales.
- **Restricciones (triple restricción ampliada)**: alcance, tiempo, costo, calidad, recursos y riesgo. Cambiar una afecta a las demás.
- **Gerente de proyecto**: responsable de lograr los objetivos; integra, comunica y negocia.

### Ciclo de vida del proyecto y del producto
Fases genéricas: **inicio, organización y preparación, ejecución, cierre**. Curvas típicas: el costo y el personal crecen y luego decrecen; el riesgo y la incertidumbre son máximos al inicio; el costo de los cambios crece con el tiempo.
Tipos de ciclo de vida:
- **Predictivo (cascada)**: alcance definido al inicio.
- **Iterativo/incremental**: se refina por entregas.
- **Ágil**: iteraciones cortas con alcance adaptable (ver [[GP 07 - Enfoques ágiles y gestión híbrida]]).
- **Híbrido**.
Ciclo de vida de software: ver [[Ingeniería de Software]] y [[IS 01 - Ciclo de vida y modelos de proceso]].

### Grupos de procesos (PMBOK clásico)
**Iniciación, Planificación, Ejecución, Seguimiento y Control, Cierre**; y áreas de conocimiento: integración, alcance, cronograma, costos, calidad, recursos, comunicaciones, riesgos, adquisiciones e interesados.

### Acta de constitución del proyecto (project charter)
Documento que autoriza formalmente el proyecto y da autoridad al gerente. Contenido típico:
1. Justificación (necesidad de negocio, caso de negocio).
2. Objetivos medibles (SMART) y criterios de éxito.
3. Requisitos de alto nivel y descripción del alcance preliminar.
4. Entregables principales y cronograma de hitos.
5. Presupuesto resumido.
6. Riesgos y supuestos de alto nivel; restricciones.
7. Interesados clave; patrocinador y gerente asignado, con su nivel de autoridad.

### Interesados (stakeholders)
- **Identificación**: patrocinador, cliente, usuarios, equipo, proveedores, reguladores, comunidad.
- **Matriz poder-interés (Mendelow)**: alto poder y alto interés: **gestionar de cerca**; alto poder, bajo interés: **mantener satisfecho**; bajo poder, alto interés: **mantener informado**; bajo poder, bajo interés: **monitorear**.
- **Compromiso**: desconocedor, resistente, neutral, partidario, líder; se compara el nivel actual con el deseado.

### Caso de negocio: evaluación de selección de proyectos
Métodos: payback, VAN, TIR, razón beneficio/costo, modelos de puntuación. Fundamentos en [[Ingeniería Económica]].

## Ejemplo resuelto 1: acta de constitución resumida
Proyecto: "Sistema de inscripción en línea de una academia".
- **Justificación**: la inscripción manual toma 3 días por estudiante y genera errores del 6 %.
- **Objetivo SMART**: reducir en 6 meses el tiempo de inscripción a menos de 15 minutos y los errores a menos del 1 %, con un presupuesto máximo de 24 000 USD (cifra ilustrativa).
- **Entregables**: aplicación web, módulo de pagos, manual y capacitación.
- **Hitos**: requisitos aprobados (mes 1), prototipo (mes 2), piloto (mes 4), producción (mes 6).
- **Supuestos**: la academia aporta datos históricos; la pasarela de pago aprueba el comercio a tiempo.
- **Riesgos iniciales**: resistencia del personal administrativo, cambios en precios.
- **Autoridad**: la directora aprueba cambios menores a 1 000 USD; los mayores pasan al comité.

## Ejemplo resuelto 2: matriz poder-interés
| Interesado | Poder | Interés | Estrategia |
|---|---|---|---|
| Directora (patrocinadora) | Alto | Alto | Gestionar de cerca; reunión semanal |
| Personal administrativo | Medio | Alto | Mantener informado, involucrar en pruebas |
| Padres de estudiantes | Bajo | Medio | Mantener informado (comunicados) |
| Proveedor de pagos | Medio | Bajo | Mantener satisfecho (cumplir requisitos) |
| Ministerio/regulador | Alto | Bajo | Mantener satisfecho; verificar requisitos |

### Selección de proyectos por puntuación
Dos candidatos, criterios con pesos: alineación estratégica 0,4; beneficio financiero 0,35; riesgo (5 = bajo) 0,25.
- Proyecto P: 4, 3, 2 $\Rightarrow 1{,}6+1{,}05+0{,}5=3{,}15$.
- Proyecto Q: 3, 4, 4 $\Rightarrow 1{,}2+1{,}4+1{,}0=3{,}60$.
Se prioriza Q.

## Errores comunes
- Iniciar sin acta y sin patrocinador con autoridad.
- Objetivos no medibles ("mejorar la experiencia").
- Identificar interesados solo al inicio; la lista debe revisarse en cada fase.
- Confundir proyecto con operación o con producto.
- Planificar la ejecución sin criterios de éxito acordados.

## Ejercicios propuestos
1. Clasifique: (a) el mantenimiento mensual de servidores; (b) migración de un datacenter. *Respuesta: (a) operación; (b) proyecto.*
2. Un interesado tiene alto poder y bajo interés: estrategia. *Respuesta: mantener satisfecho.*
3. Puntaje de un proyecto con calificaciones (5, 2, 3) y pesos (0,4; 0,35; 0,25). *Respuesta: 2+0,7+0,75 = 3,45.*

## Conexiones con otras materias
[[Ingeniería de Software]], [[Ingeniería Económica]], [[Organización]] (estructuras matriciales), [[Efectividad Personal]], [[TAP Pasantía]].

## Fuente
PMI, *Guía de los Fundamentos para la Dirección de Proyectos (PMBOK)*; Kerzner. Cifras ilustrativas.
