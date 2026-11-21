---
tags: [clase, semestre-VI]
materia: Servicio Comunitario
---
# Servicio Comunitario - Ejecución de Actividades y Gestión en Campo

Materia: [[Servicio Comunitario]]
Anterior: [[Servicio Comunitario - Inicio, Formalización y Aceptación Comunitaria]]
Siguiente: [[Servicio Comunitario - Seguimiento, Bitácora y Control de Horas]]

## Contexto y objetivo
Una vez formalizado el inicio, comienza la fase medular de [[Servicio Comunitario]]: ejecutar las actividades planificadas para alcanzar las **120 horas mínimas** y entregar valor real a la comunidad. En proyectos de Ingeniería en Informática, esta etapa combina trabajo técnico (desarrollo, bases de datos, soporte, redes) con trabajo humano (capacitación, pruebas con usuarios, gestión de imprevistos).

Al finalizar esta clase, el estudiante sabrá cómo organizar las jornadas de trabajo en campo y remoto, aplicar buenas prácticas técnicas adaptadas a entornos comunitarios y manejar desviaciones respecto al cronograma original.

## 1. Modalidades de ejecución: trabajo en sitio y trabajo técnico
Dependiendo de la naturaleza del proyecto aprobado, las actividades se distribuyen en dos frentes complementarios:
- **Actividades presenciales en la comunidad**: levantamiento detallado de datos, instalación de equipos o software, pruebas piloto con usuarios finales, talleres de capacitación y soporte en sitio.
- **Actividades técnicas de desarrollo/preparación** (según lo permitido en el plan aprobado y validado por el tutor): diseño de esquemas en [[Base de Datos I]], programación de módulos de [[Desarrollo de Aplicaciones Web]] o [[Ingeniería de Software]], redacción de manuales y preparación de material didáctico.

*Regla práctica:* Todo trabajo técnico realizado fuera de la sede debe reflejarse en entregables verificables (commits, prototipos mostrados en reuniones, manuales) y contar con el visto bueno del tutor académico.

## 2. Buenas prácticas técnicas en entornos de bajos recursos
Las comunidades suelen tener restricciones muy distintas a las de una empresa tecnológica:
- **Hardware heterogéneo o limitado**: probar las aplicaciones en equipos reales de la comunidad (a menudo con poca RAM o procesadores antiguos), evitando dependencias pesadas innecesarias.
- **Operación offline / local**: si la conectividad a internet es intermitente, priorizar arquitecturas locales (`localhost` o red de área local) con sincronización opcional o exportación sencilla a CSV/PDF.
- **Software libre y gratuito**: emplear sistemas operativos Linux ligeros, LibreOffice, PostgreSQL/SQLite, Python, PHP o herramientas web abiertas para garantizar cero costos de licenciamiento.
- **Interfaces simples y tolerantes a errores**: formularios claros, mensajes de error en español comprensible, validaciones robustas y botones de respaldo accesibles.

## 3. Conducción de talleres y capacitaciones comunitarias
Cuando el proyecto incluye alfabetización digital o capacitación de usuarios:
1. **Preparar el ambiente con antelación**: llegar 30 minutos antes para verificar electricidad, proyector, equipos encendidos y archivos copiados.
2. **Enfoque práctico ("aprender haciendo")**: dedicar menos del 30% del tiempo a diapositivas teóricas y más del 70% a ejercicios guiados por los asistentes.
3. **Material de apoyo impreso o visual**: entregar guías resumidas de una o dos páginas que los participantes puedan consultar después.
4. **Control de asistencia**: pasar lista en cada sesión con nombre, cédula/teléfono y firma.

## 4. Gestión de imprevistos y control de cambios
En campo ocurren retrasos (suspensiones de clases, fallas eléctricas, enfermedad de un vocero). Ante un imprevisto:
- Documentar la causa en el diario de campo o bitácora.
- Reprogramar la actividad en acuerdo con el tutor comunitario.
- Si el cambio altera objetivos o cronograma sustancialmente, notificar inmediatamente al tutor académico aplicando control de cambios de [[Gerencia de Proyectos]].

## Errores comunes
- **Desarrollar todo el semestre "a puerta cerrada"**: desaparecer de la comunidad durante 8 semanas y llegar al final con un sistema que no se adapta a la realidad de los usuarios.
- **No hacer pruebas piloto**: instalar la versión final el último día sin haberla validado con datos reales.

## Ejercicios propuestos
1. Una escuela te pide un sistema de control de notas, pero solo tiene dos PC con 2 GB de RAM, Windows 7 y sin internet permanente. ¿Qué decisiones técnicas tomarías?
   - *Respuesta esperada:* Diseñar una aplicación web ligera ejecutada localmente (o aplicación de escritorio sencilla) con base de datos SQLite o MariaDB local, interfaz HTML/CSS sin frameworks pesados, sin dependencia de CDN externos y con exportación directa a PDF/hojas de cálculo.
2. Si una jornada de taller se suspende por falla eléctrica general en la zona, ¿cómo debes proceder?
   - *Respuesta esperada:* Registrar la incidencia en la bitácora sin computar las horas no ejecutadas, reprogramar la fecha con el tutor comunitario y aprovechar el tiempo para revisar guías o coordinar ajustes con el equipo.

## Conexiones
- Materia principal: [[Servicio Comunitario]]
- Anterior: [[Servicio Comunitario - Inicio, Formalización y Aceptación Comunitaria]]
- Siguiente: [[Servicio Comunitario - Seguimiento, Bitácora y Control de Horas]]
- Materias técnicas aplicadas: [[Ingeniería de Software]], [[Base de Datos I]], [[Desarrollo de Aplicaciones Web]], [[Gerencia de Proyectos]]

## Fuente
Basado en el programa típico de la asignatura y en buenas prácticas de ejecución de proyectos informáticos comunitarios.
