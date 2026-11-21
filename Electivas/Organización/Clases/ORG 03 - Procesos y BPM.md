---
tags: [clase, electiva]
materia: Organización
fuente: "conocimiento general"
---
# ORG 03 - Procesos y BPM

Materia: [[Organización]]
Anterior: [[ORG 02 - Estructura organizacional]]
Siguiente: [[ORG 04 - Cultura, liderazgo y comunicación]]

## Contexto y objetivo
Una organización crea valor mediante **procesos**, no mediante departamentos. Esta clase presenta la gestión por procesos (BPM), el mapa de procesos, la notación BPMN, los manuales de procedimientos y los indicadores de desempeño. El objetivo es modelar un proceso, calcular métricas de tiempo y capacidad y detectar cuellos de botella.

## Teoría

### Definiciones
- **Proceso**: conjunto de actividades interrelacionadas que transforman entradas en salidas de valor para un cliente.
- **Proceso estratégico, misional (clave) y de apoyo** (clasificación del mapa de procesos).
- **Procedimiento**: forma específica de ejecutar un proceso o actividad (documentado).
- **BPM** (Business Process Management): disciplina para identificar, modelar, ejecutar, monitorear y optimizar procesos. Ciclo: Diseño, Modelado, Ejecución, Monitoreo, Optimización.
- **Cadena de valor** (Porter): actividades primarias y de apoyo.

### Mapa de procesos
Muestra procesos estratégicos (planificación), misionales (desde el requerimiento del cliente hasta su satisfacción) y de apoyo (RR. HH., TI, finanzas). Relaciona con [[Sistema de Información I]] porque los sistemas soportan procesos.

### Modelado: BPMN 2.0 (elementos básicos)
- **Eventos**: inicio (círculo fino), intermedios, fin (círculo grueso).
- **Actividades**: tareas y subprocesos (rectángulos redondeados).
- **Compuertas**: exclusiva (XOR), paralela (AND), inclusiva (OR).
- **Flujos**: de secuencia, de mensaje; **carriles (swimlanes)** por rol.
- Otras notaciones: diagrama de flujo, SIPOC, diagrama de actividad UML (ver [[IS 04 - Modelado con UML]]).

### Documentación
**Manual de procedimientos**: objetivo, alcance, responsables, definiciones, descripción paso a paso, formatos, diagrama, indicadores, control de versiones.

### Indicadores y análisis cuantitativo
- **Tiempo de ciclo** $TC$: tiempo total desde el inicio hasta el fin (incluye esperas).
- **Tiempo de proceso (valor agregado)**.
- **Eficiencia del ciclo**: $EC=\dfrac{T_{valor}}{T_{ciclo}}$.
- **Capacidad** de una etapa: $C_i=\dfrac{n_i}{t_i}$ (servidores / tiempo de servicio). Capacidad del proceso: $\min_i C_i$ (**cuello de botella**).
- **Ley de Little**: $WIP = \lambda \cdot T$ (trabajo en proceso = tasa de llegada × tiempo en el sistema).
- **Utilización** $\rho=\dfrac{\lambda}{C}$.
- **Calidad**: tasa de errores y retrabajo.
- Mejoras: eliminar, simplificar, automatizar, paralelizar, reordenar (principios de reingeniería, Hammer y Champy).

## Ejemplo resuelto: proceso de atención de solicitudes de soporte
Proceso con 4 etapas, con tiempos de servicio y personal (hipotéticos):

| Etapa | Servidores | Tiempo por caso (min) | Capacidad (casos/h) |
|---|---|---|---|
| 1. Registro | 1 | 5 | $60/5=12$ |
| 2. Clasificación | 2 | 10 | $2\cdot 60/10=12$ |
| 3. Resolución | 4 | 40 | $4\cdot60/40=6$ |
| 4. Cierre y encuesta | 1 | 6 | $60/6=10$ |

**Cuello de botella**: resolución con 6 casos/h. Capacidad del proceso: 6 casos/h.
Si llegan $\lambda = 5$ casos/h: utilización $\rho=5/6=83\%$; ok. Si llegan 7: la cola crece sin límite.

**Tiempo de proceso**: $5+10+40+6=61$ min de trabajo. Supongamos esperas medias de 15, 20, 60 y 5 min en las colas respectivas. Tiempo de ciclo $=61+100=161$ min. Eficiencia del ciclo: $\dfrac{61}{161}=38\%$.

**Ley de Little**: con $\lambda=5$ casos/h y $T=161/60=2{,}68$ h: $WIP=5\times2{,}68=13{,}4$ casos en curso en promedio.

**Mejora**: capacitar a una persona para resolución (5 servidores): capacidad $=5\cdot 60/40=7{,}5$ casos/h; el nuevo cuello es la etapa 2 o la 4 (10 y 12 casos/h; el menor es 7,5 en resolución... aún cuello); se ve también que la utilización baja a $5/7{,}5=67\%$, con lo que las esperas se reducen. Una mejora adicional: automatizar el registro con formulario web (etapa 1 pasa a 0 min).

### Diagrama textual (BPMN simplificado)
```
(Inicio) -> [Registrar solicitud] -> [Clasificar] -> <¿Crítica?>
   si -> [Resolver nivel 2] -> [Cerrar]
   no -> [Resolver nivel 1] -> [Cerrar] -> (Fin)
```

## Errores comunes
- Modelar "como debería ser" sin validar con quienes ejecutan el proceso (el modelo AS-IS debe ser real).
- Optimizar una etapa que no es el cuello de botella.
- Procesos documentados que no se usan (manual en un estante).
- Medir solo costos, sin tiempo de ciclo ni calidad.
- Automatizar un proceso malo: se obtiene un mal proceso más rápido.

## Ejercicios propuestos
1. Dos servidores, 15 min por caso: capacidad horaria. *Respuesta: 8 casos/h.*
2. $T_{valor}=30$ min, $T_{ciclo}=120$ min: eficiencia. *Respuesta: 25 %.*
3. Llegan 8 casos/h con $T=1{,}5$ h: WIP por Little. *Respuesta: 12 casos.*

## Conexiones con otras materias
[[Sistema de Información I]], [[Sistema de Información II]], [[Ingeniería de Software]], [[IS 04 - Modelado con UML]], [[Investigación de Operaciones I]].

## Fuente
Chiavenato; Hammer y Champy; especificación BPMN 2.0 (OMG); conocimiento general. Cifras ilustrativas.
