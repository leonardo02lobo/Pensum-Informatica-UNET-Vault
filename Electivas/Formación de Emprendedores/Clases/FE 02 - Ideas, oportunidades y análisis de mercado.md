---
tags: [clase, electiva]
materia: Formación de Emprendedores
fuente: "conocimiento general"
---
# FE 02 - Ideas, oportunidades y análisis de mercado

Materia: [[Formación de Emprendedores]]
Anterior: [[FE 01 - El emprendedor y el proceso emprendedor]]
Siguiente: [[FE 03 - Modelo de negocio Canvas y Lean Startup]]

## Contexto y objetivo
Una buena idea no es una oportunidad hasta que se demuestra que existe un cliente con un problema real y dispuesto a pagar. Esta clase cubre técnicas de generación de ideas, criterios de evaluación y el análisis de mercado y competencia, incluyendo el dimensionamiento TAM-SAM-SOM.

## Teoría

### Generación de ideas
- **Lluvia de ideas (brainstorming)** y **SCAMPER** (Sustituir, Combinar, Adaptar, Modificar, Poner en otro uso, Eliminar, Reordenar).
- **Observación de problemas propios** y entrevistas de descubrimiento.
- **Design Thinking**: empatizar, definir, idear, prototipar, probar.
- **Tendencias tecnológicas**: nuevas capacidades abren problemas antes inviables.

### Oportunidad
Una oportunidad tiene cuatro rasgos: necesidad real, mercado con tamaño suficiente, ventana de tiempo y capacidad del equipo para ejecutar. Preguntas guía: ¿quién tiene el problema?, ¿cuánto le duele?, ¿cómo lo resuelve hoy?, ¿cuánto pagaría?

### Evaluación de ideas: matriz ponderada
Se asigna un peso $w_j$ a cada criterio y una calificación $c_{ij}$ a cada idea $i$:
$$P_i = \sum_j w_j\, c_{ij}, \qquad \sum_j w_j = 1$$

### Análisis del entorno y la competencia
- **PESTEL**: político, económico, social, tecnológico, ecológico, legal.
- **5 fuerzas de Porter**: rivalidad, amenaza de nuevos entrantes, de sustitutos, poder de proveedores y de clientes.
- **FODA**: fortalezas y debilidades (internas), oportunidades y amenazas (externas).
- **Mapa de competidores**: directos, indirectos y sustitutos; comparar en 2 ejes de valor.

### Segmentación y tamaño de mercado
- **Segmentación**: geográfica, demográfica, conductual, B2B por industria y tamaño de empresa.
- **Persona (buyer persona)**: arquetipo del cliente ideal.
- **TAM** (mercado total), **SAM** (mercado alcanzable con su modelo) y **SOM** (porción realista capturable a corto plazo).
- Enfoque **bottom-up**: $\text{Mercado} = N_{\text{clientes}} \times \text{Precio anual}$ (más confiable que el top-down).

### Investigación de mercado
Primaria (entrevistas, encuestas, observación) y secundaria (informes, estadísticas). Para encuestas, el tamaño de muestra para una proporción es
$$n = \frac{z^2\, p(1-p)}{e^2}$$
con $z=1{,}96$ (95 %), $p=0{,}5$ si se desconoce y error $e$. Vea [[Estadística I]] para el fundamento.

## Ejemplo resuelto 1: matriz de evaluación
Tres ideas: (A) app de citas médicas, (B) software de inventario para ferreterías, (C) plataforma de tutorías.

| Criterio | Peso | A | B | C |
|---|---|---|---|---|
| Tamaño de mercado | 0,30 | 4 | 3 | 3 |
| Capacidad técnica del equipo | 0,25 | 4 | 5 | 4 |
| Intensidad del dolor | 0,25 | 3 | 5 | 3 |
| Competencia (5 = poca) | 0,20 | 2 | 4 | 3 |

- $P_A = 0{,}30\cdot4+0{,}25\cdot4+0{,}25\cdot3+0{,}20\cdot2 = 1{,}2+1{,}0+0{,}75+0{,}4 = 3{,}35$
- $P_B = 0{,}9+1{,}25+1{,}25+0{,}8 = 4{,}20$
- $P_C = 0{,}9+1{,}0+0{,}75+0{,}6 = 3{,}25$

La idea B gana. Se valida antes de construir (entrevistas a 15 dueños de ferretería).

## Ejemplo resuelto 2: TAM-SAM-SOM bottom-up (idea B)
Supuestos (hipotéticos, para ilustrar): 20 000 ferreterías en el país objetivo; suscripción de 30 USD/mes = 360 USD/año.
- TAM $= 20\,000 \times 360 = 7{,}2$ millones USD/año.
- SAM: solo ferreterías con computador y conexión: 40 % $\rightarrow 8\,000$ clientes $\rightarrow 2{,}88$ millones USD.
- SOM a 3 años: 5 % del SAM $= 400$ clientes $\rightarrow 144\,000$ USD/año.

Conclusión: mercado modesto pero suficiente para un negocio pequeño rentable; para atraer capital de riesgo habría que ampliar a otros países o verticales.

## Ejemplo resuelto 3: tamaño de muestra
Se quiere estimar la proporción de ferreterías que usan Excel, con 95 % de confianza y error de $\pm 8\,\%$: $n = \dfrac{1{,}96^2\cdot 0{,}25}{0{,}08^2} = \dfrac{0{,}9604}{0{,}0064} = 150{,}06 \approx 151$ encuestas.

## Errores comunes
- Estimar el mercado como "si solo capturo el 1 % de China...".
- Preguntar a los clientes si "les gusta" la idea (sesgo de cortesía) en lugar de indagar su comportamiento pasado.
- Considerar que "no hay competencia": siempre existe un sustituto (incluida la hoja de cálculo).
- Elegir criterios y pesos después de preferir una idea.

## Ejercicios propuestos
1. Con 3 criterios y pesos 0,5/0,3/0,2 y calificaciones (5,3,2), (3,5,4), calcule el puntaje de cada idea. *Respuesta: 2,5+0,9+0,4 = 3,8 y 1,5+1,5+0,8 = 3,8; hay empate, así que se necesita otro criterio de desempate.*
2. Calcule TAM, SAM y SOM para una app con 50 000 clientes potenciales, precio 24 USD/año, 30 % alcanzable, 10 % capturable. *Respuesta: TAM 1,2 M; SAM 360 000; SOM 36 000 USD/año.*
3. Tamaño de muestra para $p=0{,}5$, 95 %, $e=5\,\%$. *Respuesta: 385.*

## Conexiones con otras materias
[[Economía]], [[Estadística I]], [[Ingeniería de Software]] (levantamiento de requisitos), [[Gestión Tecnológica]] (vigilancia tecnológica).

## Fuente
Conocimiento general (Porter, Osterwalder, Ries, Blank). Cifras de los ejemplos son hipotéticas.
