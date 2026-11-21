---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 1-Introducción a la Matemática Financiera/Ingeniería Económica.pdf y Tema 1-Tarea.docx
---
# Ingeniería Económica - Tema 1: Enfoque sistémico de la empresa y flujos monetarios

Materia: [[Ingeniería Económica]]
Siguiente: [[Ingeniería Económica - Tema 2 Interés, tasas y equivalencia]]

## Contexto y objetivo
El Tema 1 (presentación del Núcleo de Técnicas Cuantitativas, Departamento de Ingeniería Industrial, UNET) define qué es la Ingeniería Económica y construye el vocabulario necesario antes de las fórmulas: la empresa como sistema, las decisiones financieras, qué es un proyecto de inversión, qué estudios lo componen, los seis pasos de un estudio económico y los **flujos monetarios** que se dibujan en un diagrama de tiempo. Prepara el terreno para la matemática financiera ([[Ingeniería Económica - Tema 2 Interés, tasas y equivalencia]]) y para los criterios de decisión ([[Ingeniería Económica - Tema 3 Criterios VA, EA y TIR]]).

**Definición central.** La Ingeniería Económica es la disciplina cuyo objetivo es *medir por anticipado la rentabilidad de los proyectos de inversión* para recomendar la selección de inversiones con un criterio económico, dado que las empresas tienen entre sus objetivos fundamentales la obtención de beneficios.

## 1. La empresa como sistema
La empresa se modela como un sistema de transformación:

- **Entradas (recursos):** mano de obra, materia prima, maquinaria, energía y capital.
- **Proceso:** transformación.
- **Salidas:** bienes (alimentos, vestido, vivienda, automóviles) y servicios (transporte, electricidad, agua, comunicaciones).
- **Políticas internas** que gobiernan el sistema: de mercado (tamaños de producto, distribución, promoción), de investigación y desarrollo (mejoras, nuevos diseños), de producción y suministros (tamaño de planta, grado de automatización, reposición de inventarios, número de suplidores), de personal (reclutamiento, selección, entrenamiento, incentivos) y **financieras** (adquisición de equipos, capital de deuda o propio, beneficios a repartir, cuentas por cobrar).

Las políticas financieras se desglosan en: utilización de capital de deuda/propio, forma de suplir necesidades a corto plazo, capacidad de endeudamiento (límites), liquidez, tamaño de inventarios, beneficios a repartir (dividendos) y áreas de inversión (rendimiento, riesgo, criterios para seleccionar alternativas, aspectos legales).

## 2. Decisiones de financiamiento
Permiten establecer la mejor **estructura de capital**: la cantidad y calidad del aporte de capital de cada fuente.

| Capital propio | Capital de deuda |
|---|---|
| Venta de acciones | Préstamos hipotecarios |
| Utilidades retenidas | Bonos |
| Venta de activos | Pagarés |
| Reservas por depreciación | Créditos de suplidores |

## 3. El proyecto y su desarrollo
**Proyecto:** oportunidad de inversión definida como la actividad técnica que, puesta en marcha, permite lograr beneficios futuros de inversiones de capital. Pasa de una *idea tecnológica* a un *objeto real tecnológico* mediante cinco estudios:

1. **Estudio de mercado:** demanda, oferta, precio, comercialización.
2. **Estudio técnico:** tamaño óptimo de planta, localización, equipos, instalaciones, mano de obra.
3. **Estudio organizacional:** tipo y tamaño de la estructura, unidades externas, procedimientos administrativos, sistemas de información.
4. **Estudio legal:** contratos de arrendamiento, cédula catastral, registro mercantil, patentes de industria y comercio, SENIAT, ministerios (Ambiente, Trabajo), cuerpo de bomberos, instituciones municipales/estadales/nacionales (la lista es la que aparece en la presentación; es específica del contexto venezolano).
5. **Estudio económico-financiero:** flujos monetarios, tasa mínima de rendimiento y vida del proyecto, para elegir la alternativa. Es **solo una parte** de los aspectos asociados a un proyecto de inversión.

## 4. Pasos de un estudio económico
1. Identificar y definir los problemas o necesidades (fallas en procesos productivos, necesidades de mercado no satisfechas, mejoramiento tecnológico).
2. Establecer las **restricciones** (niveles de calidad, contaminación, empleo, seguridad, producción, beneficio mínimo exigido, inversión y áreas de inversión).
3. Generar ideas o proyectos de inversión (p. ej. para un equipo con fallas frecuentes: reacondicionarlo, reemplazarlo por uno igual, reemplazarlo por uno mejorado tecnológicamente).
4. **Estimar los flujos monetarios.** Fuentes: información interna (ventas, producción, inventarios, control de calidad, compras, mantenimiento, estados financieros, estudio de tiempos) y externa (informes gubernamentales, catálogos, bancarios, revistas). Técnicas: regresión lineal, promedio móvil, armonización exponencial, método Delphi, simulación.
5. Determinar la factibilidad económica (rentabilidad).
6. Tomar la decisión de inversión, que combina el resultado cuantitativo (modelo de ingeniería económica, análisis de sensibilidad) con asuntos **no económicos**.

## 5. Flujos monetarios
**Flujo monetario $F_t$:** entrada (+) o salida (-) de dinero en el período $t$; pueden ser estimaciones o valores observados. **Diagrama de flujos monetarios:** representación gráfica sobre una escala de tiempo; $t=0$ es el *inicio* del período 1 y $t=1$ su *final*. Entradas = flecha hacia arriba; salidas = flecha hacia abajo.

Componentes de un proyecto de inversión:

| Símbolo | Nombre | Definición / cálculo |
|---|---|---|
| II | Inversión inicial | $II = CF + CT$ |
| CF | Capital fijo | Gastos de adquisición de activos fijos tangibles (y compensación de intangibles) |
| CT | Capital de trabajo | Activos circulantes mínimos para operar hasta los primeros ingresos |
| IB | Ingresos brutos | $IB = p_v \cdot Q$ (precio de venta por volumen de ventas del año) |
| Cop | Costos operacionales | Todos los desembolsos para que el proyecto siga operando |
| VR | Valor residual | $VR = p_v - C_r$ (precio de venta del activo menos costo de remoción); puede ser positivo, cero o negativo; se ubica al final del último año |
| ISR | Impuesto sobre la renta | $ISR = T\cdot ING$, con $ING$ = ingresos gravables |
| P, R | Préstamo y cuotas | Financiamiento con capital de deuda |

Las estimaciones se hacen **a precios de hoy** (precio presente) para conservar el mismo poder de compra: si la mano de obra cuesta hoy 50.000.000 Bs/año, se estima igual para los años siguientes (la inflación se trata aparte, ver [[Ingeniería Económica - Tema 6 Inflación y rentabilidad]]).

### Ejemplo resuelto: clasificar partidas (inspirado en la evaluación del Tema 2)
Partidas: instalación de máquinas y equipos 1.200; seguro de transporte 340; entrenamiento 800; compra de terreno 25.000; inventario de materia prima 345; productos en proceso 270; efectivo en caja 525; materia prima 800; combustible 200; seguros 150; alquileres 300; ingresos brutos 3.200; valor residual 4.000.

- **Capital fijo:** terreno 25.000 + instalación 1.200 = 26.200 (activos fijos tangibles). El seguro de transporte (340) y el entrenamiento (800) son gastos de puesta en marcha que se **amortizan como activos intangibles** y suelen sumarse al capital fijo como "capital fijo intangible": 340+800 = 1.140, para un capital fijo total de 27.340.
- **Capital de trabajo:** 345 + 270 + 525 = 1.140.
- **Inversión inicial:** 27.340 + 1.140 = 28.480 en $t=0$.
- **Costos operacionales anuales:** 800 + 200 + 150 + 300 = 1.450.
- **Ingresos brutos:** 3.200 por año; **VR:** 4.000 en el último año.
Flujo neto anual antes de impuestos: $3.200 - 1.450 = 1.750$.

## Tarea del Tema 1
El archivo `Tema 1-Tarea.docx` solo contiene nombre del estudiante, cédula y el enlace a un video (https://youtu.be/nnpRqTF9GWE); no hay texto adicional que documentar.

## Errores comunes
- Meter el capital de trabajo en la depreciación: se recupera al final, no se deprecia.
- Mezclar flujos a precios corrientes con tasas reales (o viceversa).
- Olvidar el signo del valor residual cuando el costo de remoción supera el precio de venta.
- Confundir "alternativa" con "proyecto": una alternativa puede ser ninguno, uno o varios proyectos.

## Ejercicios propuestos
1. Una planta requiere maquinaria por 8.000, instalación 500, inventario inicial 700 y caja 300. Calcule CF, CT e II. (Resp.: CF=8.500, CT=1.000, II=9.500.)
2. Si $p_v=12$ y $Q=5.000$ unidades/año, ¿cuánto es IB? (Resp.: 60.000.)
3. ¿Qué signo tiene VR si se vende un equipo en 300 y retirarlo cuesta 450? (Resp.: negativo, -150.)

## Conexiones
[[Economía]] (sistemas económicos), [[Gerencia de Proyectos]] (estudios de factibilidad), [[Finanzas para Ingenieros]] (continuación), [[Fórmulas de Matemática Financiera]].

## Fuente
`Material/Tema 1-Introducción a la Matemática Financiera/Ingeniería Económica.pdf` (diapositivas, Luz Giugni según la presentación) y `Tema 1-Tarea.docx`. La clasificación de partidas del ejemplo es una resolución propia a partir del enunciado del Parcial 1 (ver [[Ingeniería Económica - Parcial 1 resuelto]]); verificar con el criterio del profesor el tratamiento de seguros de transporte y entrenamiento.
