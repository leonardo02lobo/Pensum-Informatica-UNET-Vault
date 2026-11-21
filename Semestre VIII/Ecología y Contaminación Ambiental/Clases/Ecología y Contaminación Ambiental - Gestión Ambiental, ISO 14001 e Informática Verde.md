---
tags: [clase, semestre-VIII]
materia: Ecología y Contaminación Ambiental
---
# Ecología y Contaminación Ambiental - Gestión Ambiental, ISO 14001 e Informática Verde

Materia: [[Ecología y Contaminación Ambiental]]
Anterior: [[Ecología y Contaminación Ambiental - Residuos Sólidos, Suelos y RAEE]]
Siguiente: — (última clase)

## Contexto y objetivo
Integrar los instrumentos técnicos, normativos y gerenciales de la **gestión ambiental** —Evaluación de Impacto Ambiental (EIA), norma **ISO 14001**, huella ecológica y legislación ambiental— con las prácticas de **Informática Verde (Green IT)** aplicables a centros de datos, desarrollo de software y proyectos de ingeniería.

## 1. Instrumentos de gestión ambiental
- **Evaluación de Impacto Ambiental (EIA)**: estudio técnico previo a la ejecución de un proyecto (obra civil, planta industrial, gran centro de datos) que identifica, predice y valora sus impactos ambientales, proponiendo medidas de *prevención, mitigación, corrección o compensación*. Culmina en un Plan de Manejo Ambiental.
- **Análisis de Ciclo de Vida (ACV)**: cuantifica los impactos de un producto o servicio "de la cuna a la tumba" (extracción de materias primas, manufactura, transporte, uso y disposición final).
- **Huella ecológica**: área de territorio ecológicamente productivo necesaria para producir los recursos que consume una población o actividad y asimilar sus desechos ($\text{ha globales}$).

## 2. Sistema de Gestión Ambiental (ISO 14001)
La norma internacional **ISO 14001** establece los requisitos para que una organización gestione sus aspectos ambientales de forma sistemática bajo el ciclo de mejora continua **PHVA** (*Planificar – Hacer – Verificar – Actuar*):
1. **Planificar**: identificar *aspectos ambientales* (elementos de las actividades que interactúan con el ambiente, p. ej., consumo eléctrico o generación de RAEE) y sus *impactos*, requisitos legales y objetivos.
2. **Hacer**: implementar controles operacionales, capacitación y preparación ante emergencias.
3. **Verificar**: monitorear indicadores, realizar auditorías internas y evaluar cumplimiento legal.
4. **Actuar**: corregir no conformidades y mejorar el desempeño ambiental.

## 3. Marco legal ambiental venezolano (referencia)
El ejercicio profesional en Venezuela se enmarca en la Constitución (derecho a un ambiente seguro, sano y ecológicamente equilibrado) y leyes específicas como la **Ley Orgánica del Ambiente**, la **Ley Penal del Ambiente** (tipifica delitos y sanciones por contaminación y manejo indebido de desechos) y la **Ley de Gestión Integral de la Basura** (además de decretos técnicos sobre calidad de aguas, aire y desechos peligrosos; *verificar siempre la normativa vigente y gacetas oficiales aplicables*).

## 4. Informática Verde (Green IT)
La industria TI representa una fracción creciente del consumo eléctrico mundial y de los residuos electrónicos. Sus principales líneas de acción son:
- **Eficiencia en Centros de Datos**: se mide con el indicador **PUE** (*Power Usage Effectiveness*):
  $$\text{PUE} = \frac{\text{Energía total consumida por el centro de datos}}{\text{Energía consumida por el equipamiento TI}}$$
  Un $\text{PUE}$ ideal es $1{,}0$; centros antiguos rondan $2{,}0$, mientras que instalaciones modernas optimizadas alcanzan $1{,}1\text{–}1{,}3$ mediante pasillos fríos/calientes confinados, refrigeración gratuita (*free cooling*) y virtualización/consolidación de servidores.
- **Software eficiente (Green Software)**: algoritmos de menor complejidad temporal/espacial, reducción de transferencias de red redundantes, apagado automático de instancias ociosas en la nube (*autoscaling*).
- **Uso responsable de IA y cómputo intensivo**: entrenamiento y despliegue eficiente de modelos, preferencia por centros de datos alimentados con energías renovables.

### Ejemplo de cálculo de PUE
Un centro de datos consume $1\,500\text{ MWh/año}$ en total, de los cuales $1\,000\text{ MWh/año}$ corresponden a servidores, almacenamiento y redes (los $500\text{ MWh}$ restantes se van en climatización, UPS e iluminación):
$$\text{PUE} = \frac{1\,500}{1\,000} = 1{,}50$$
Si mediante confinamiento de pasillos se reduce el consumo auxiliar a $250\text{ MWh/año}$, el nuevo $\text{PUE}$ baja a $1{,}25$, ahorrando $250\text{ MWh/año}$ (y sus emisiones de $\text{CO}_2\text{e}$ asociadas).

## Errores comunes
- Confundir **aspecto ambiental** (causa: emisión de gases, consumo de energía, generación de RAEE) con **impacto ambiental** (efecto: cambio climático, agotamiento de recursos, contaminación del suelo).
- Creer que ISO 14001 fija límites numéricos de emisión: la norma certifica el *sistema de gestión* y el compromiso de cumplimiento legal y mejora continua, no un estándar único de concentración de contaminantes.

## Ejercicios propuestos
1. Un centro de datos tiene $\text{PUE} = 1{,}8$ y su carga TI es de $200\text{ kW}$ continuos. ¿Cuánta potencia total demanda el edificio y cuánta potencia se destina a infraestructura auxiliar (refrigeración/pérdidas)?
   - *Respuesta*: potencia total $= 1{,}8 \times 200 = 360\text{ kW}$; potencia auxiliar $= 360 - 200 = 160\text{ kW}$.
2. Proponga tres métricas ambientales verificables para incluir en un proyecto de desarrollo de software o infraestructura TI.
   - *Respuesta*: (1) $\text{PUE}$ de la infraestructura; (2) $\text{g CO}_2\text{e}$ por transacción o por hora de cómputo; (3) porcentaje de hardware retirado entregado a gestores certificados de RAEE.

## Conexiones
- Marco legal y responsabilidad profesional en [[Legislación, Valores y Proyecto de País]] y [[Ciencia y Sociedad I]].
- Evaluación de proyectos y análisis de viabilidad en [[Gerencia de Proyectos]] y [[Gestión Tecnológica]].
- Eficiencia algorítmica y arquitectura de sistemas en [[Estructuras Discretas]] y [[Sistemas Operativos]].

## Fuente
Basado en el programa orientativo de [[Ecología y Contaminación Ambiental]] (norma ISO 14001; legislación ambiental venezolana de referencia; principios de Green IT).
