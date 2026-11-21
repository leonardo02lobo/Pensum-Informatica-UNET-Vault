---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 09 - Calidad y métricas de software

Materia: [[Ingeniería de Software]]
Anterior: [[IS 08 - Pruebas de software]]
Siguiente: [[IS 10 - Gestión de proyectos y estimación]]


## Contexto y objetivo
La calidad no se "agrega" al final: se construye y se mide. Esta clase cubre modelos de calidad (ISO/IEC 25010), aseguramiento de calidad (SQA), revisiones e inspecciones, métricas de producto y proceso, y modelos de madurez (CMMI). Complementa [[IS 08 - Pruebas de software]].

## Definiciones
- **Calidad** (ISO 9000): grado en que un conjunto de características inherentes cumple los requisitos. Crosby: "conformidad con los requisitos"; Juran: "aptitud para el uso".
- **Aseguramiento de la calidad (QA/SQA)**: actividades *del proceso* para prevenir defectos (auditorías, estándares, revisiones).
- **Control de calidad (QC)**: actividades *del producto* para detectar defectos (pruebas, inspecciones).
- **Costo de la calidad**: costos de prevención + evaluación + fallas internas + fallas externas. Las fallas externas son las más caras.

## ISO/IEC 25010 (modelo de calidad del producto)
Ocho características:
1. **Adecuación funcional** (completitud, corrección, pertinencia).
2. **Eficiencia de desempeño** (tiempo, recursos, capacidad).
3. **Compatibilidad** (coexistencia, interoperabilidad).
4. **Usabilidad** (reconocibilidad, aprendizaje, operabilidad, protección ante errores, accesibilidad).
5. **Fiabilidad** (madurez, disponibilidad, tolerancia a fallos, recuperabilidad).
6. **Seguridad** (confidencialidad, integridad, no repudio, responsabilidad, autenticidad).
7. **Mantenibilidad** (modularidad, reusabilidad, analizabilidad, modificabilidad, testabilidad).
8. **Portabilidad** (adaptabilidad, instalabilidad, reemplazabilidad).
Existe además el modelo de **calidad en uso** (efectividad, eficiencia, satisfacción, libertad de riesgo, cobertura de contexto). Predecesores: ISO 9126, McCall, Boehm.

## Estándares y modelos de proceso
- **ISO 9001**: sistema de gestión de calidad (organización).
- **ISO/IEC 12207**: ciclo de vida del software. **ISO/IEC 15504 (SPICE)** / 33000: evaluación de procesos.
- **CMMI** (Capability Maturity Model Integration): niveles de madurez: 1 Inicial, 2 Gestionado, 3 Definido, 4 Gestionado cuantitativamente, 5 En optimización.
- **PSP/TSP** (Humphrey): disciplina personal y de equipo.
- **MoProSoft** (México) y **COMPETISOFT** para pymes latinoamericanas.

## Revisiones técnicas
Detectan defectos en artefactos antes de ejecutar nada, muy rentables (pueden hallar una gran parte de los defectos de requisitos y diseño).
- **Walkthrough**: el autor guía a los pares (informal).
- **Revisión por pares / code review** (pull requests): checklist, enfoque en legibilidad, correctitud y pruebas.
- **Inspección de Fagan**: formal, roles (moderador, autor, lector, registrador), entrada/salida con criterios, métricas de defectos.
Checklist de code review: ¿hay pruebas?, ¿nombres claros?, ¿manejo de errores?, ¿seguridad (entrada no validada, secretos)?, ¿duplicación?, ¿complejidad razonable?

## Métricas
Una **métrica** es una medida cuantitativa de un atributo. Principio GQM (Goal-Question-Metric): define el objetivo, las preguntas, luego las métricas.

### Métricas de producto
- **Tamaño**: LOC/KLOC, **puntos de función** (FP) independientes del lenguaje.
- **Complejidad ciclomática** $V(G) = E - N + 2P$ (valores: 1-10 simple; 11-20 moderada; 21-50 alta; más de 50 inestable; umbrales orientativos).
- **Acoplamiento y cohesión** de Chidamber y Kemerer (CK) para OO: WMC (métodos ponderados por clase), DIT (profundidad de herencia), NOC (hijos), CBO (acoplamiento entre objetos), RFC (respuesta), LCOM (falta de cohesión).
- **Índice de mantenibilidad**: $MI = 171 - 5.2\ln(HV) - 0.23\,V(G) - 16.2\ln(LOC)$ (HV = volumen de Halstead). Se suele reescalar a 0-100.
- **Halstead**: usa operadores y operandos: volumen $V = N \log_2 n$.
- **Cobertura de pruebas**, **densidad de defectos** (defectos/KLOC), **deuda técnica** (SonarQube: ratio de deuda).
- **Estabilidad** (Martin): $I = Ce/(Ca + Ce)$ (inestabilidad por acoplamiento eferente y aferente).

### Métricas de proceso y proyecto
- Velocidad (puntos por sprint), *lead time* y *cycle time*, tasa de fugas de defectos, eficiencia de remoción de defectos $DRE = E/(E+D)$ (E defectos hallados antes de entrega; D hallados después).
- **Métricas DORA** (DevOps): frecuencia de despliegue, tiempo de entrega de cambios, tasa de fallo de cambios, tiempo de recuperación (MTTR). Ver [[IS 11 - Gestión de configuración y DevOps]].

### Fiabilidad
$$\text{Disponibilidad} = \frac{MTBF}{MTBF + MTTR}$$
Ejemplo: MTBF = 500 h, MTTR = 2 h: $A = 500/502 = 0.996$ (99.6%). "Cuatro nueves" (99.99%) permiten unos 52 min de caída al año.

## Ejemplo resuelto: DRE y decisión de calidad
Un equipo detecta 90 defectos durante desarrollo y pruebas y 10 tras la entrega.
1. $DRE = 90/(90+10) = 0.90$ (90%).
2. Meta de la organización: 95%. Hay brecha.
3. Acciones: añadir inspección de requisitos y revisión de código obligatoria; subir cobertura mínima en CI al 80%; análisis estático en cada commit.
4. Se vuelve a medir en el siguiente release (ej. 95 y 5: DRE 95%).

## Ejemplo resuelto: puntos de función simplificados
Conteo no ajustado (pesos medios): entradas externas 5 x 4 = 20; salidas 4 x 5 = 20; consultas 3 x 4 = 12; archivos lógicos internos 3 x 10 = 30; interfaces externas 1 x 7 = 7. UFP = 89. Con factor de ajuste de valor VAF = 0.65 + 0.01 x (suma de 14 características, supón 35) = 1.00 y FP = 89. Esfuerzo: si la productividad de la organización es 10 FP/persona-mes, entonces 8.9 persona-meses. (Los pesos exactos dependen de la complejidad baja/media/alta según IFPUG: verificar tablas.)

## Mejora continua
Ciclo PDCA (Planificar, Hacer, Verificar, Actuar), retrospectivas ágiles, análisis de causa raíz (diagrama de Ishikawa, 5 porqués), diagrama de Pareto (20% de causas generan 80% de defectos).

## Errores comunes
- Medir lo que es fácil y no lo que importa (LOC como productividad).
- Usar métricas para evaluar personas (efecto Goodhart: cuando una métrica se vuelve objetivo deja de ser buena métrica).
- Quality gates que bloquean por detalles menores sin priorizar el riesgo.
- Confundir QA con "el equipo de pruebas".

## Ejercicios propuestos
1. Una función tiene 3 `if` y un `while`: ¿$V(G)$? *Resp.: 5 (4 decisiones + 1).*
2. MTBF = 1000 h y MTTR = 10 h: disponibilidad. *Resp.: 1000/1010 = 99.01%.*
3. ¿Qué característica ISO 25010 cubre "se puede modificar sin romper otras partes"? *Resp.: mantenibilidad (modificabilidad/modularidad).*

## Conexiones
[[IS 08 - Pruebas de software]], [[IS 08 - Pruebas de software]], [[Estadística I]] (métricas, distribución de defectos), [[Gerencia de Proyectos]].

## Fuente
Conocimiento general. ISO/IEC 25010; Pressman; Sommerville; Humphrey; CMMI Institute.
