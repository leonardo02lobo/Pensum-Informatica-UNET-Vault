---
tags: [clase, electiva]
materia: Organización
fuente: "conocimiento general"
---
# ORG 05 - Gestión del cambio y mejora continua

Materia: [[Organización]]
Anterior: [[ORG 04 - Cultura, liderazgo y comunicación]]
Siguiente: [[ORG 06 - Organización del área de TI, ITIL y COBIT]]

## Contexto y objetivo
Implantar un sistema nuevo, reorganizar un área o adoptar un método ágil exigen que las personas cambien su forma de trabajar. Con frecuencia los proyectos técnicamente correctos fracasan por la resistencia al cambio. Esta clase presenta modelos de cambio, estrategias para gestionarlo y las herramientas de mejora continua (PDCA, Kaizen, Six Sigma, 5S) con cálculos de capacidad y de defectos.

## Teoría

### Tipos de cambio
Planificado vs. emergente; incremental vs. transformacional; estructural, tecnológico, cultural, de procesos.

### Modelo de Lewin
Tres fases: **descongelar** (crear necesidad), **cambiar** (moverse a la nueva situación) y **recongelar** (institucionalizar). Análisis de **campo de fuerzas**: fuerzas impulsoras vs. restrictivas; el cambio se logra aumentando las primeras o reduciendo las segundas (reducir las restrictivas suele generar menos tensión).

### Modelo de Kotter (8 pasos)
1. Crear sentido de urgencia. 2. Formar una coalición guía. 3. Desarrollar visión y estrategia. 4. Comunicar la visión. 5. Facilitar la acción (quitar obstáculos). 6. Generar victorias a corto plazo. 7. Consolidar logros y seguir cambiando. 8. Anclar el cambio en la cultura.

### Otros modelos
**ADKAR** (Prosci): Conciencia, Deseo, Conocimiento, Habilidad, Refuerzo. Curva del cambio (Kübler-Ross adaptada): negación, resistencia, exploración, compromiso.

### Resistencia al cambio
Causas: miedo a perder estatus o empleo, falta de información, hábito, desconfianza, costo personal. Tácticas (Kotter y Schlesinger): educación y comunicación, participación, facilitación y apoyo, negociación, manipulación y cooptación (no recomendable), coerción (último recurso).

### Mejora continua
- **Ciclo PDCA (Deming)**: Planificar, Hacer, Verificar (Check), Actuar.
- **Kaizen**: mejoras pequeñas y constantes con participación de todos.
- **Herramientas de calidad**: diagrama de Pareto, diagrama causa-efecto (Ishikawa), histograma, hoja de verificación, diagrama de dispersión, gráficos de control, diagrama de flujo.
- **5S**: Clasificar, Ordenar, Limpiar, Estandarizar, Disciplina.
- **Lean**: eliminar desperdicios (muda).
- **Six Sigma**: reducir variación; metodología DMAIC (Definir, Medir, Analizar, Mejorar, Controlar).
- **Métricas**: DPMO $=\dfrac{\text{defectos}}{\text{unidades}\times\text{oportunidades}}\times10^{6}$; rendimiento $Y=1-\dfrac{\text{defectos}}{\text{oportunidades totales}}$.
- **Índice de capacidad del proceso**: $C_p=\dfrac{LSE-LIE}{6\sigma}$; $C_{pk}=\min\left(\dfrac{LSE-\mu}{3\sigma},\dfrac{\mu-LIE}{3\sigma}\right)$. Proceso capaz si $C_{pk}\ge1{,}33$ (referencia).

Para procesos y manuales vea [[ORG 03 - Procesos y BPM]]; para estadística básica, [[Estadística I]].

## Ejemplo resuelto 1: Pareto de incidencias de soporte
Mes de incidencias (hipotético): 100 total.

| Causa | Cantidad | % | % acumulado |
|---|---|---|---|
| Contraseñas olvidadas | 38 | 38 | 38 |
| Fallas de red local | 24 | 24 | 62 |
| Errores del ERP | 18 | 18 | 80 |
| Impresoras | 12 | 12 | 92 |
| Otros | 8 | 8 | 100 |

Con tres causas se explica el 80 %. Acción PDCA: **Plan** (autoservicio de restablecimiento de contraseñas, meta: reducir de 38 a 10 casos/mes), **Do** (piloto en un departamento), **Check** (medir casos tras 4 semanas), **Act** (extender o ajustar). Si el piloto da 12 casos, ahorro de 26 incidencias al mes; con 15 min por caso son 6,5 horas/mes.

## Ejemplo resuelto 2: capacidad de proceso
Tiempo de respuesta de soporte: especificación entre 0 y 60 min (LIE=0, LSE=60). Muestra: $\mu=35$ min, $\sigma=6$ min.
- $C_p=\dfrac{60-0}{36}=1{,}67$.
- $C_{pk}=\min\left(\dfrac{60-35}{18},\dfrac{35-0}{18}\right)=\min(1{,}39;1{,}94)=1{,}39$.
El proceso es capaz (1,39 mayor que 1,33), pero está descentrado hacia el límite superior; reducir la media a 30 min daría $C_{pk}=\dfrac{30}{18}=1{,}67$.

## Ejemplo resuelto 3: DPMO
Formulario de alta de clientes: 500 formularios, 5 oportunidades de error cada uno, 40 defectos encontrados. $\text{DPMO}=\dfrac{40}{500\cdot5}\cdot10^6=16\,000$. Rendimiento $=1-0{,}016=98{,}4\,\%$; corresponde aproximadamente a un nivel sigma de 3,6 (con el desplazamiento convencional de 1,5; valor aproximado a verificar en tablas).

## Plan de gestión del cambio (resumen)
Para introducir un sistema nuevo: análisis de interesados, mensaje clave, plan de comunicación, capacitación, usuarios clave ("campeones"), medición de adopción (porcentaje de usuarios activos), soporte post-implantación y refuerzo. Se conecta con [[Gerencia de Proyectos]].

## Errores comunes
- Comunicar tarde y solo por correo.
- Declarar victoria demasiado pronto (Kotter, paso 7).
- Mejorar lo que no es crítico: sin datos (Pareto) se ataca lo equivocado.
- Cambiar sin medir la línea base.
- Usar PDCA como formalidad sin cerrar el ciclo con la acción de estandarizar.

## Ejercicios propuestos
1. 300 unidades, 4 oportunidades, 18 defectos: DPMO. *Respuesta: $18/1200\cdot10^6=15\,000$.*
2. $LSE=10$, $LIE=4$, $\mu=7$, $\sigma=0{,}5$: $C_p$ y $C_{pk}$. *Respuesta: $C_p=2$; $C_{pk}=\min(2;2)=2$.*
3. Identifique dos fuerzas impulsoras y dos restrictivas para adoptar Scrum. *Respuesta: impulsoras: retrasos y cambios de requisitos; restrictivas: costumbre del control jerárquico y falta de capacitación.*

## Conexiones con otras materias
[[Estadística I]], [[Gerencia de Proyectos]], [[Ingeniería de Software]], [[IS 08 - Pruebas de software]], [[Efectividad Personal]].

## Fuente
Lewin; Kotter; Deming; Chiavenato; Robbins. Cifras ilustrativas; niveles sigma aproximados.
