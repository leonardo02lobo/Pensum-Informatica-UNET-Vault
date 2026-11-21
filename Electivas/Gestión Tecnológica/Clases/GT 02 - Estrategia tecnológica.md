---
tags: [clase, electiva]
materia: Gestión Tecnológica
fuente: "conocimiento general"
---
# GT 02 - Estrategia tecnológica

Materia: [[Gestión Tecnológica]]
Anterior: [[GT 01 - Tecnología, innovación y curva S]]
Siguiente: [[GT 03 - Vigilancia tecnológica y prospectiva]]

## Contexto y objetivo
La estrategia tecnológica define qué tecnologías dominar, cómo obtenerlas y cómo se articulan con la estrategia del negocio. El objetivo es analizar el portafolio tecnológico, decidir entre hacer, comprar o aliarse, y fijar el nivel de inversión en I+D.

## Teoría

### Alineación con la estrategia empresarial
La estrategia tecnológica debe responder a la competitiva: **liderazgo en costos**, **diferenciación** o **enfoque** (Porter). Se pregunta: ¿qué tecnologías sostienen nuestras capacidades distintivas? El enfoque **basado en recursos** (RBV) busca activos valiosos, raros, difíciles de imitar y organizados (VRIO).

### Posturas tecnológicas
- **Líder**: invierte primero (riesgo alto, ventaja de pionero).
- **Seguidor rápido**: imita y mejora.
- **Seguidor tardío / adoptante**: compra tecnología madura.
- **Nicho**: especializa en una aplicación.
Elección según el ciclo de vida (curva S), capacidad financiera y protección (patentes).

### Clasificación de tecnologías (Arthur D. Little)
- **Emergentes**: potencial incierto; vigilar y experimentar.
- **Clave**: dan ventaja competitiva actual; proteger e invertir.
- **De base**: necesarias para competir, pero no diferencian.
- **Embrionarias/marchitas**: según etapa. Útil para priorizar I+D.

### Hacer, comprar o aliarse
Opciones: **I+D interna**, **compra o licencia** de tecnología, **alianzas y joint ventures**, **contratación de I+D externa**, **adquisición de empresas** (M&A), **innovación abierta**. Criterios: importancia estratégica, capacidad interna, tiempo, costo, riesgo, control.

### Portafolio y presupuesto de I+D
- **Matriz atractivo tecnológico vs. posición competitiva** (ADL, GE).
- **Intensidad de I+D**: $\text{Intensidad}=\dfrac{\text{Gasto en I+D}}{\text{Ventas}}\times100$.
- **Valor esperado de un proyecto de I+D**: $VE = p_t\,p_c\,V - C$, con $p_t$ prob. técnica, $p_c$ prob. comercial, $V$ valor presente de los beneficios, $C$ costo de desarrollo.
- **Hoja de ruta tecnológica (technology roadmap)**: calendario de capacidades, productos y tecnologías.

### Gestión de la tecnología en software
Arquitectura y deuda técnica como decisiones estratégicas; elección de plataformas (propietaria vs. libre); dependencia de proveedores (vendor lock-in). Conexión con [[Ingeniería de Software]].

## Ejemplo resuelto: portafolio de I+D por valor esperado
Se tienen tres proyectos (cifras hipotéticas en miles de USD):

| Proyecto | $p_t$ | $p_c$ | $V$ | $C$ | $VE=p_t p_c V - C$ |
|---|---|---|---|---|---|
| A: módulo de IA para soporte | 0,7 | 0,6 | 900 | 150 | 0,42·900-150 = 228 |
| B: nueva plataforma de datos | 0,5 | 0,8 | 1 500 | 400 | 0,40·1500-400 = 200 |
| C: tecnología radical (blockchain en logística) | 0,2 | 0,5 | 5 000 | 300 | 0,10·5000-300 = 200 |

Presupuesto de I+D: 600 (miles). Opciones: A+B cuesta 550, VE total 428; A+C cuesta 450, VE total 428; B+C cuesta 700 (excede).

Ratio $VE/C$: A=1,52; B=0,50; C=0,67. Con restricción de presupuesto se prefiere A+C (VE 428 con 450) que deja 150 libres para otro proyecto pequeño. Además, C aporta opciones estratégicas futuras (diversificación del riesgo). Decisión: A y C; B se pospone o se busca socio para compartir costo.

**Intensidad de I+D**: ventas anuales 8 000; gasto en I+D 600 $\Rightarrow$ 7,5 %: alta para una empresa de software en madurez; es coherente con una estrategia de seguidor rápido/líder en nicho.

## Errores comunes
- Elegir tecnología por moda (hype) sin vínculo con el negocio.
- Evaluar I+D sin probabilidades técnica y comercial.
- Ignorar la capacidad de absorción: sin personal capacitado la tecnología comprada no se aprovecha.
- Desarrollo interno de tecnologías de base que se pueden comprar.
- No revisar la hoja de ruta ante cambios del entorno.

## Ejercicios propuestos
1. $p_t=0{,}6$, $p_c=0{,}5$, $V=1\,000$, $C=200$: calcule el valor esperado. *Respuesta: 0,3·1000-200 = 100.*
2. Ventas 20 millones y gasto en I+D 1,4 millones: intensidad. *Respuesta: 7 %.*
3. Para cada tecnología (clave, base, emergente), indique la acción recomendada. *Respuesta: clave: invertir y proteger; base: comprar/estandarizar; emergente: vigilar y experimentar con proyectos piloto.*

## Conexiones con otras materias
[[Economía]], [[Ingeniería Económica]], [[Ingeniería de Software]], [[Gerencia de Proyectos]], [[Formación de Emprendedores]].

## Fuente
Escorsa y Valls; Porter; Arthur D. Little (matriz). Conocimiento general; cifras ilustrativas.
