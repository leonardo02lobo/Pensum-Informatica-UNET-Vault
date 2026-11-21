---
tags: [clase, electiva]
materia: Organización
fuente: "conocimiento general"
---
# ORG 06 - Organización del área de TI, ITIL y COBIT

Materia: [[Organización]]
Anterior: [[ORG 05 - Gestión del cambio y mejora continua]]
Siguiente: —

## Contexto y objetivo
Las tecnologías de información (TI) son un habilitador del negocio y también una fuente de riesgo y costo. Esta clase estudia cómo se organiza el área de TI (roles, estructura), qué es el gobierno de TI y los marcos ITIL y COBIT, con cálculos de disponibilidad, SLA y priorización de incidentes. El objetivo es entender el vocabulario y aplicarlo en un caso sencillo. (Versiones y contenidos de los marcos: verificar con la documentación oficial vigente.)

## Teoría

### Estructura típica del área de TI
- **CIO/Gerente de TI**, **CTO**, **CISO** (seguridad).
- Funciones: desarrollo y mantenimiento de aplicaciones, infraestructura y operaciones, redes, base de datos, seguridad, soporte (mesa de ayuda), arquitectura, gestión de proyectos (PMO), calidad.
- Modelos de organización: **centralizado**, **descentralizado** (TI en cada unidad), **federado** (núcleo + equipos en unidades), **tercerización (outsourcing)** total o parcial.
- Roles en equipos de desarrollo: analista, arquitecto, desarrollador, tester, DevOps/SRE, DBA, scrum master, product owner.
- Alineación estratégica TI-negocio: el negocio define objetivos; TI los habilita y propone oportunidades. Ver [[Sistema de Información II]].

### Gobierno y gestión de TI
- **Gobierno de TI**: asegura que TI cree valor, gestione riesgos y use recursos de forma responsable (dirección y evaluación por el órgano de gobierno).
- **Gestión de TI**: planificar, construir, ejecutar y monitorear. COBIT distingue ambas (EDM para gobierno; APO, BAI, DSS, MEA para gestión).
- Áreas de enfoque: alineación estratégica, entrega de valor, gestión de riesgos, gestión de recursos, medición del desempeño.

### ITIL (Information Technology Infrastructure Library)
Marco de buenas prácticas para la gestión de servicios de TI. **ITIL 4** (referencia): 
- **Sistema de valor de servicio (SVS)**: principios rectores, gobernanza, cadena de valor del servicio, mejora continua y prácticas.
- **Cadena de valor**: planificar, mejorar, involucrar, diseñar y hacer la transición, obtener/construir, entregar y dar soporte.
- **Principios rectores**: enfocarse en el valor, empezar donde se está, avanzar iterando con retroalimentación, colaborar, pensar y trabajar de forma holística, mantenerlo simple y práctico, optimizar y automatizar.
- **Prácticas** (34 en ITIL 4): gestión de incidentes, de problemas, de cambios, de niveles de servicio, mesa de servicio, gestión de configuración, etc.
- Antes (ITIL v3): ciclo de vida con estrategia, diseño, transición, operación y mejora continua del servicio.
- Conceptos: **servicio**, **SLA** (acuerdo de nivel de servicio), **OLA**, **incidente** (interrupción), **problema** (causa de incidentes), **cambio**, **CMDB**.

### COBIT
Marco de gobierno y gestión de TI empresariales de ISACA. **COBIT 2019**: 6 principios del sistema de gobierno, 40 objetivos de gobierno y gestión, factores de diseño, niveles de capacidad de procesos (0 a 5). Dominios: EDM (Evaluar, Dirigir y Monitorear), APO (Alinear, Planificar y Organizar), BAI (Construir, Adquirir e Implementar), DSS (Entregar, dar Servicio y Soporte), MEA (Monitorear, Evaluar y Valorar). Verificar versión y número de objetivos con la fuente oficial.

### Otros estándares
ISO/IEC 20000 (gestión de servicios), ISO/IEC 27001 (seguridad de la información), ISO/IEC 38500 (gobierno de TI), PMBOK (proyectos, ver [[Gerencia de Proyectos]]), CMMI (madurez de procesos de software, ver [[Ingeniería de Software]]).

## Ejemplo resuelto 1: disponibilidad y SLA
Un servicio acuerda **99,9 %** de disponibilidad mensual (30 días).
- Minutos del mes: $30\cdot24\cdot60=43\,200$.
- Indisponibilidad permitida: $0{,}001\cdot43\,200=43{,}2$ min.
Con 99,99 %: $4{,}32$ min. Con 99 %: $432$ min (7,2 horas).

**Sistemas en serie**: aplicación (99,9 %), base de datos (99,95 %), red (99,9 %). Disponibilidad total $=0{,}999\cdot0{,}9995\cdot0{,}999=0{,}99750\approx99{,}75\,\%$, o sea unos $108$ minutos de indisponibilidad al mes: menor que cada componente, por lo que no cumple un SLA de 99,9 %. **Redundancia en paralelo** de dos servidores de aplicación idénticos de 99,9 %: $1-(0{,}001)^2=99{,}9999\,\%$; el total pasa a $0{,}999999\cdot0{,}9995\cdot0{,}999\approx99{,}85\,\%$ (ahora el cuello es la base de datos y la red).
MTBF y MTTR: $A=\dfrac{MTBF}{MTBF+MTTR}$. Con MTBF = 720 h y MTTR = 2 h: $A=\dfrac{720}{722}=99{,}72\,\%$.

## Ejemplo resuelto 2: priorización de incidentes (matriz impacto-urgencia)
Prioridad $=$ impacto × urgencia (escala 1 a 3, donde 3 es el más alto). 

| Incidente | Impacto | Urgencia | Prioridad (producto) | Tiempo objetivo (ejemplo) |
|---|---|---|---|---|
| Caída del sistema de facturación | 3 | 3 | 9 (crítica) | respuesta 15 min, resolución 2 h |
| Un usuario sin acceso a correo | 1 | 2 | 2 (baja) | resolución 1 día hábil |
| Lentitud en la intranet | 2 | 2 | 4 (media) | resolución 8 h |

Un cumplimiento de SLA: si de 80 incidentes críticos y altos se resolvieron a tiempo 72: $\dfrac{72}{80}=90\,\%$. Si la meta es 95 %, se analiza (gestión de problemas) la causa raíz de los 8 incumplimientos.

## Ejemplo resuelto 3: gestión de cambios
Cambio estándar (parche programado) frente a normal (nueva versión de ERP) y de emergencia. El normal pasa por: solicitud, evaluación de riesgo, aprobación del comité de cambios (CAB), plan de reversión, ventana de mantenimiento, revisión posterior. Beneficio: menos incidentes provocados por cambios no controlados.

## Errores comunes
- Creer que ITIL es una norma certificable para la empresa (se certifican personas; la certificación de organización es ISO/IEC 20000).
- Implantar todos los procesos a la vez; ITIL 4 recomienda adaptar y avanzar iterando.
- Confundir incidente (restaurar el servicio) con problema (eliminar la causa raíz).
- Fijar SLA sin medir la capacidad real ni considerar los componentes en serie.
- Gobierno de TI sin participación del negocio.

## Ejercicios propuestos
1. Indisponibilidad permitida mensual (30 días) con 99,5 %. *Respuesta: $0{,}005\cdot43\,200=216$ min (3,6 h).*
2. Dos componentes en serie de 99,8 % y 99,9 %: disponibilidad total. *Respuesta: $\approx99{,}70\,\%$.*
3. Diferencie ITIL y COBIT. *Respuesta: ITIL se centra en la gestión de servicios de TI; COBIT en gobierno y gestión de TI empresariales y control.*

## Conexiones con otras materias
[[Sistema de Información I]], [[Sistema de Información II]], [[Ingeniería de Software]], [[Gerencia de Proyectos]], [[Administración de Redes]], [[Teoría General de Sistemas]].

## Fuente
Chiavenato; documentación pública de AXELOS/PeopleCert (ITIL 4) e ISACA (COBIT); conocimiento general. Versiones y estructuras a verificar con la fuente oficial. Cifras ilustrativas.
