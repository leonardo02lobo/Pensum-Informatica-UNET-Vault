---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 10 - Gestión de proyectos y estimación

Materia: [[Ingeniería de Software]]
Anterior: [[IS 09 - Calidad y métricas de software]]
Siguiente: [[IS 11 - Gestión de configuración y DevOps]]

## Contexto y objetivo
Un **proyecto** es un esfuerzo temporal para crear un producto o servicio único. Gestionarlo exige planificar alcance, tiempo, costo, calidad, riesgos y personas. En software, la dificultad central es la **estimación** bajo incertidumbre. Objetivo: aprender WBS, cronograma (CPM), estimación (COCOMO, puntos de función, historias), gestión de riesgos y seguimiento (valor ganado). Para una visión más general, ver la electiva [[Gerencia de Proyectos]].

## Triángulo de hierro y planificación
Alcance, tiempo y costo (con la calidad en el centro) están interrelacionados: cambiar uno afecta los otros. **Ley de Brooks**: añadir personas a un proyecto atrasado lo atrasa más (costos de comunicación $n(n-1)/2$ canales).
Entregables de la planificación: acta de constitución, plan de alcance, WBS, cronograma, presupuesto, plan de riesgos, plan de comunicaciones, plan de calidad.

## WBS (EDT) y estimación de tareas
La **Estructura de Desglose del Trabajo** descompone el alcance en paquetes de trabajo (regla 8/80: entre 8 y 80 horas) orientada a entregables. Ejemplo: 1 Gestión; 2 Requisitos; 3 Diseño; 4 Construcción (4.1 módulo equipos, 4.2 módulo préstamos); 5 Pruebas; 6 Despliegue y documentación.

Técnicas de estimación:
- **Juicio de expertos / Delphi**.
- **Analogía**: comparar con proyectos similares.
- **Tres puntos (PERT)**: $E = (O + 4M + P)/6$, desviación $\sigma = (P-O)/6$.
- **Planning Poker** y puntos de historia (ver [[IS 03 - Casos de uso e historias de usuario]]).
- **Paramétricas**: COCOMO, puntos de función.

## COCOMO
**COCOMO básico (Boehm, 1981)**: $E = a\,(KLOC)^b$ persona-mes, $D = c\,E^d$ meses, personal medio $N = E/D$.
| Modo | a | b | c | d |
|---|---|---|---|---|
| Orgánico | 2.4 | 1.05 | 2.5 | 0.38 |
| Semiacoplado | 3.0 | 1.12 | 2.5 | 0.35 |
| Empotrado | 3.6 | 1.20 | 2.5 | 0.32 |

**Ejemplo.** Proyecto orgánico de 20 KLOC:
1. $E = 2.4 \times 20^{1.05}$. $20^{1.05} = e^{1.05 \ln 20} = e^{1.05 \times 2.9957} = e^{3.1455} = 23.2$. $E = 55.7$ persona-mes.
2. $D = 2.5 \times 55.7^{0.38}$. $55.7^{0.38} = e^{0.38 \times 4.0197} = e^{1.5275} = 4.61$. $D = 11.5$ meses.
3. $N = 55.7/11.5 = 4.8$ personas.
**COCOMO II** (2000): $E = A \cdot \text{Size}^{B} \cdot \prod EM_i$ con $B = 1.01 + 0.01 \sum SF_j$ (factores de escala) y multiplicadores de esfuerzo (producto, plataforma, personal, proyecto). Modelos: composición de aplicaciones, diseño temprano, post-arquitectura.

## Ruta crítica (CPM) y PERT
Red de actividades con precedencias. Para cada una: ES, EF, LS, LF, holgura = LS - ES. La **ruta crítica** es la más larga; holgura 0.

**Ejemplo resuelto.** 
| Act | Dur (días) | Pred |
|---|---|---|
| A Requisitos | 5 | - |
| B Diseño | 8 | A |
| C BD | 6 | B |
| D Backend | 12 | B |
| E Frontend | 10 | B |
| F Pruebas | 7 | C, D, E |
1. Hacia adelante: A: 0-5; B: 5-13; C: 13-19; D: 13-25; E: 13-23; F: ES = max(19,25,23) = 25, EF = 32.
2. Hacia atrás: F: LF 32, LS 25; D: LF 25, LS 13; C: LF 25, LS 19 (holgura 6); E: LF 25, LS 15 (holgura 2); B: LS 5; A: LS 0.
3. Ruta crítica: A-B-D-F = 5+8+12+7 = **32 días**. Holguras: C = 6, E = 2.
4. Acción: acelerar D (crash) o paralelizar parte de F; atrasar E hasta 2 días no afecta.

## Gestión de riesgos
Proceso: identificar, analizar (probabilidad x impacto), planificar respuesta, monitorear. Estrategias: **evitar, mitigar, transferir (seguro, contrato), aceptar**.
Registro de riesgos (ejemplo):
| Riesgo | Prob. | Impacto | Exposición | Respuesta |
|---|---|---|---|---|
| Rotación del desarrollador clave | 0.3 | 8 | 2.4 | Documentar, programación en pares |
| Requisitos cambian | 0.6 | 5 | 3.0 | Entregas incrementales, control de cambios |
| Servidor de pruebas no disponible | 0.2 | 4 | 0.8 | Entorno en contenedores |
Exposición = probabilidad x impacto. Riesgos clásicos (Boehm): déficit de personal, plazos irreales, funciones erróneas, interfaz de usuario errónea, *gold plating*, flujo constante de cambios, componentes externos, rendimiento.

## Seguimiento: valor ganado (EVM)
Variables: **PV** (valor planificado), **EV** (valor ganado = % completado x presupuesto), **AC** (costo real).
- Variación de cronograma $SV = EV - PV$; índice $SPI = EV/PV$.
- Variación de costo $CV = EV - AC$; índice $CPI = EV/AC$.
- Estimación al concluir $EAC = BAC/CPI$.
**Ejemplo.** BAC = 100 000; a mitad del plan PV = 50 000; trabajo completado 40%: EV = 40 000; AC = 45 000. $SPI = 0.8$ (atrasado); $CPI = 0.89$ (sobrecosto); $EAC = 100000/0.889 = 112500$.

## Seguimiento ágil
Burndown/burnup, velocidad, tablero Kanban con límites WIP, métricas de flujo (lead time, cycle time). Retrospectivas y revisiones de sprint (ver [[IS 01 - Ciclo de vida y modelos de proceso]]).

## Equipo y comunicación
Roles típicos: gerente de proyecto, analista, arquitecto, desarrolladores, QA, DevOps, *Product Owner*. Herramientas: Jira, Trello, GitHub Projects, Redmine. Principios: reuniones cortas y con propósito, decisiones documentadas, acuerdos de trabajo (*working agreements*).

## Ejemplo: plan para tu TAP
Aplica a [[TAP Tesis]] o [[TAP Pasantía]]: WBS con entregables (anteproyecto, prototipo v1, v2, informe), cronograma con hitos de revisión del tutor, 3 riesgos principales (acceso a datos, disponibilidad del tutor, alcance excesivo) y plan de mitigación. Evita planificar al 100% de capacidad: deja colchón (10-20%).

## Errores comunes
- Estimar solo el tiempo de programar y olvidar pruebas, reuniones, documentación.
- Estimación como compromiso: una estimación es un rango (cono de incertidumbre: al inicio puede variar entre 0.25x y 4x).
- Plan que nadie actualiza.
- Ignorar la ruta crítica en la gestión diaria.
- No registrar lecciones aprendidas.

## Ejercicios propuestos
1. PERT: O = 4, M = 6, P = 14 días. *Resp.: E = (4 + 24 + 14)/6 = 7 días; $\sigma$ = 1.67.*
2. Con EV = 30, AC = 36, PV = 36: SPI y CPI. *Resp.: SPI = 0.83; CPI = 0.83.*
3. Equipo de 6 personas: cantidad de canales de comunicación. *Resp.: 6x5/2 = 15.*

## Conexiones
[[Gerencia de Proyectos]], [[Estadística I]] (distribución beta/normal en PERT), [[Investigación de Operaciones II]] (redes y programación de proyectos, si disponible en el pensum), [[IS 01 - Ciclo de vida y modelos de proceso]].

## Fuente
Conocimiento general. PMI, *Guía del PMBOK*; Boehm, *Software Engineering Economics*; McConnell, *Software Estimation*; Brooks, *The Mythical Man-Month*.
