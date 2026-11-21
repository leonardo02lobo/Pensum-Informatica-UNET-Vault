---
tags: [clase, electiva]
materia: Gerencia de Proyectos
fuente: "conocimiento general"
---
# GP 02 - Alcance y WBS

Materia: [[Gerencia de Proyectos]]
Anterior: [[GP 01 - Ciclo de vida, interesados y acta de constitución]]
Siguiente: [[GP 03 - Cronograma y ruta crítica CPM]]

## Contexto y objetivo
El mayor generador de retrasos y sobrecostos es el alcance mal definido ("scope creep"). Esta clase cubre la recopilación de requisitos, el enunciado del alcance, la **Estructura de Desglose del Trabajo (WBS/EDT)** y su diccionario, la verificación y el control del alcance. El objetivo es construir una WBS correcta (regla del 100 %) para un proyecto de software.

## Teoría

### Producto vs. proyecto
- **Alcance del producto**: características y funciones del resultado.
- **Alcance del proyecto**: trabajo necesario para entregarlo.

### Requisitos
Recopilación: entrevistas, talleres, encuestas, observación, prototipos, historias de usuario. Documentación: requisitos funcionales y no funcionales, **matriz de trazabilidad** (requisito, origen, entregable, prueba). Ver [[Ingeniería de Software]].

### Enunciado del alcance
Descripción del alcance, entregables, criterios de aceptación, **exclusiones** (lo que no se hará), restricciones y supuestos.

### WBS (EDT)
Descomposición jerárquica orientada a **entregables** del trabajo total del proyecto.
- **Regla del 100 %**: la WBS incluye todo el trabajo (y solo ese) definido en el alcance; los hijos suman el 100 % del padre.
- **Paquete de trabajo**: nivel más bajo; se puede estimar, asignar y controlar. Regla práctica: entre 8 y 80 horas (regla 8/80) o entre uno y diez días de esfuerzo; en software, tareas de 1 a 2 semanas máximo.
- Los nodos se redactan como **sustantivos** (entregables), no como verbos (actividades); las actividades salen después, en la definición de actividades.
- **Diccionario de la WBS**: por cada paquete, descripción, entregable, criterios de aceptación, responsable, estimaciones y dependencias.
- Estilos: por **entregables** o por **fases**.
- Numeración jerárquica 1.1, 1.2, 1.2.1...
- **Matriz de asignación de responsabilidades**: RACI.

### Control del alcance
- **Validar el alcance**: aceptación formal de entregables por el cliente.
- **Control de cambios**: solicitud de cambio, evaluación de impacto (tiempo, costo, riesgo), aprobación por el comité de control de cambios (CCB), actualización de línea base.
- **Línea base del alcance**: enunciado + WBS + diccionario.
- Medidas: porcentaje de cambios aceptados; densidad de cambios.
- **Técnicas de estimación basadas en la WBS**: ascendente (suma de paquetes), análoga, paramétrica (puntos de función, COCOMO).

### Estimación paramétrica simple: COCOMO básico (modo orgánico)
$$E=2{,}4\,(KLOC)^{1{,}05}\ \text{persona-mes},\qquad T=2{,}5\,E^{0{,}38}\ \text{meses}$$
Es un modelo histórico; úselo solo como ilustración y calibre con datos propios.

## Ejemplo resuelto 1: WBS del sistema de inscripción en línea
```
1 Sistema de inscripción en línea
 1.1 Gestión del proyecto
   1.1.1 Plan del proyecto
   1.1.2 Informes de avance
 1.2 Requisitos y diseño
   1.2.1 Documento de requisitos
   1.2.2 Prototipo de interfaz
   1.2.3 Modelo de datos
 1.3 Desarrollo
   1.3.1 Módulo de registro de estudiantes
   1.3.2 Módulo de pagos
   1.3.3 Módulo de reportes
 1.4 Pruebas
   1.4.1 Plan y casos de prueba
   1.4.2 Informe de pruebas
 1.5 Despliegue y capacitación
   1.5.1 Entorno de producción
   1.5.2 Manual y capacitación
```
Verificación 100 %: ¿la integración con el proveedor de pagos aparece? Sí, en 1.3.2; ¿el análisis de seguridad? No: se añade **1.4.3 Pruebas de seguridad**, hallazgo típico al revisar la regla del 100 %.

## Ejemplo resuelto 2: estimación ascendente y COCOMO
Estimación ascendente con paquetes en horas-persona (hipotética): requisitos 80, prototipo 60, modelo de datos 40, registro 160, pagos 120, reportes 80, pruebas 110, seguridad 30, despliegue 40, capacitación 30, gestión 80. 
Suma: $80+60+40+160+120+80+110+30+40+30+80=830$ h. Con 6 horas productivas diarias por persona: $830/6=138{,}3$ persona-días; con 2 desarrolladores en paralelo (sin considerar dependencias) $\approx69$ días hábiles. Se añade una reserva de contingencia de 15 % (riesgos identificados): $830\times1{,}15=954{,}5$ h.

Comparación con COCOMO para 10 KLOC: $E=2{,}4\cdot10^{1{,}05}=2{,}4\cdot11{,}22=26{,}9$ persona-mes (aprox. 4 300 h a 160 h/mes). Es mucho mayor: eso indica que el sistema estimado en 830 h es muy pequeño frente a los 10 KLOC; o bien el tamaño real es de pocos KLOC, o la estimación ascendente es optimista. La discrepancia obliga a revisar. Para 2 KLOC: $E=2{,}4\cdot2^{1{,}05}=2{,}4\cdot2{,}07=4{,}97$ persona-mes (aprox. 795 h), coherente con la suma ascendente. (Cálculos aproximados.)

## Ejemplo resuelto 3: solicitud de cambio
Solicitud: añadir pagos con billetera móvil. Impacto: +60 h de desarrollo, +20 h de pruebas, costo +1 800 USD (a 22,5 USD/h), +1 semana en la ruta crítica. Decisión del CCB: aprobar con ajuste de cronograma y presupuesto, o diferir a una segunda versión. Se registra en la bitácora de cambios y se actualiza la línea base.

## Errores comunes
- WBS por actividades (verbos) o por departamentos en lugar de entregables.
- Paquetes de trabajo demasiado grandes (no estimables) o demasiado pequeños (microgestión).
- Olvidar la gestión del proyecto, las pruebas, la documentación y el despliegue.
- No registrar exclusiones del alcance.
- Aceptar cambios "pequeños" sin evaluar el impacto acumulado.

## Ejercicios propuestos
1. Descomponga "Sitio web de tienda" a tres niveles. *Respuesta: libre; debe incluir gestión, diseño, desarrollo (catálogo, carrito, pagos), pruebas y despliegue.*
2. Suma de paquetes 400 h con 10 % de contingencia: total. *Respuesta: 440 h.*
3. ¿Por qué "Programar" no debe ser un nodo de la WBS? *Respuesta: es una actividad, no un entregable; los nodos deben ser sustantivos que representen resultados.*

## Conexiones con otras materias
[[Ingeniería de Software]], [[IS 01 - Ciclo de vida y modelos de proceso]], [[IS 08 - Pruebas de software]], [[Investigación de Operaciones I]].

## Fuente
PMI, *PMBOK* y *Practice Standard for Work Breakdown Structures*; Boehm (COCOMO); Kerzner. Cálculos aproximados e ilustrativos.
