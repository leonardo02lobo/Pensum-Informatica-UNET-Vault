---
tags: [clase, electiva]
materia: Gestión Tecnológica
fuente: "conocimiento general"
---
# GT 03 - Vigilancia tecnológica y prospectiva

Materia: [[Gestión Tecnológica]]
Anterior: [[GT 02 - Estrategia tecnológica]]
Siguiente: [[GT 04 - Transferencia de tecnología y licenciamiento]]

## Contexto y objetivo
Las decisiones tecnológicas requieren información del entorno. La **vigilancia tecnológica** (VT) la obtiene y analiza de forma sistemática; la **inteligencia competitiva** (IC) la convierte en decisiones; la **prospectiva** explora futuros posibles. El objetivo es ejecutar un ciclo de VT con indicadores bibliométricos y de patentes, y aplicar técnicas prospectivas básicas.

## Teoría

### Conceptos
- **Vigilancia tecnológica**: proceso organizado de captura, análisis, difusión y uso de información sobre ciencia y tecnología relevante (norma española UNE 166006 para el sistema de VT/IC).
- **Inteligencia competitiva**: información sobre competidores, clientes, proveedores, regulación; orientada a decisiones.
- **Tipos de vigilancia**: tecnológica, competitiva, comercial, del entorno.
- **Prospectiva**: construye escenarios de futuro para actuar hoy; diferente de pronóstico (extrapolación).

### Ciclo de vigilancia
1. **Planificación**: necesidades de información y factores críticos de vigilancia (qué decisión apoya).
2. **Búsqueda y captación**: fuentes (patentes, artículos, normas, ferias, páginas web, redes, clientes).
3. **Análisis y validación**: filtrar, clasificar, evaluar fiabilidad.
4. **Difusión**: boletines, tableros, alertas.
5. **Explotación y decisión**; **retroalimentación**.

### Fuentes
- **Patentes**: Espacenet, Google Patents, WIPO Patentscope.
- **Literatura científica**: Scopus, Web of Science, Google Scholar, arXiv.
- **Fuentes abiertas**: GitHub (actividad de proyectos), foros, conferencias, informes de consultoras.
Búsqueda con operadores booleanos (AND, OR, NOT), truncamientos y códigos de clasificación (CIP/IPC, CPC).

### Indicadores bibliométricos y de patentes
- Número de documentos por año y por país/empresa.
- **Tasa de crecimiento anual compuesta**: $\text{TCAC}=\left(\dfrac{N_f}{N_i}\right)^{1/n}-1$.
- **Índice de especialización**: $IE=\dfrac{\text{part. del actor en la tecnología}}{\text{part. del actor en el total}}$.
- **Mapas de co-ocurrencia** de palabras clave y redes de colaboración.
- **Vida media** de la patentes citadas; **ratio de dependencia científica** (citas a artículos).

### Prospectiva: técnicas
- **Delphi**: consulta anónima iterativa a expertos hasta alcanzar consenso.
- **Escenarios** (Schwartz): identificar fuerzas motrices e incertidumbres críticas (2 ejes) y construir 4 futuros.
- **Roadmapping**, **análisis de tendencias** y **análisis morfológico**.
- **Curva de Gartner (hype cycle)**: auge de expectativas, valle de desilusión, meseta de productividad.

## Ejemplo resuelto: análisis de patentes
Se vigila el tema "baterías de estado sólido" (tema y cifras hipotéticos, solo ilustrativos). Solicitudes publicadas por año (hipotético): 2019: 400; 2024: 1 250.

**TCAC** $=\left(\dfrac{1250}{400}\right)^{1/5}-1=3{,}125^{0{,}2}-1$. Como $\ln 3{,}125=1{,}1394$; $/5=0{,}2279$; $e^{0{,}2279}=1{,}256$, luego TCAC $\approx 25{,}6\,\%$ anual: tecnología en crecimiento.

**Especialización**: la empresa X tiene 150 de las 1 250 solicitudes de 2024 (12 %), pero solo 1,5 % de todas las solicitudes del sector de baterías. $IE=12/1{,}5=8$: fuerte especialización.

**Estrategia de búsqueda** (pseudocódigo de consulta):
`("solid state" OR "solid-state") AND (battery OR cell) AND IPC:H01M`

Resultado: el análisis sugiere vigilar a X (posible líder), explorar licencias o alianzas y evaluar si hay libertad de operación (FTO) en nuestro nicho; esto enlaza con [[GT 05 - Propiedad intelectual]].

### Escenarios (ejemplo mínimo)
Ejes: velocidad de adopción de IA generativa (baja/alta) y regulación (laxa/estricta). Cuatro escenarios: "Salvaje oeste" (alta/laxa), "IA regulada" (alta/estricta), "Adopción lenta" (baja/laxa), "Estancamiento regulado" (baja/estricta). Se prueba la robustez de cada decisión estratégica en los cuatro.

## Errores comunes
- Vigilar "todo": sin factores críticos de vigilancia la información es ruido.
- Confundir cantidad de patentes con calidad (una familia de patentes cuenta varias veces).
- No validar fuentes (rumores en redes).
- Producir informes que nadie usa: sin decisión asociada, no hay IC.
- Tratar la prospectiva como adivinación; es un ejercicio de preparación.

## Ejercicios propuestos
1. Documentos por año: 120 y 480 en 4 años; calcule TCAC. *Respuesta: $4^{1/4}-1\approx 41{,}4\,\%$.*
2. Un actor tiene 6 % en la tecnología y 2 % del total: $IE$. *Respuesta: 3.*
3. Construya 2 ejes para escenarios del mercado de IoT en 2030. *Respuesta: libre; p.ej. disponibilidad de conectividad y costo de sensores.*

## Conexiones con otras materias
[[Introducción a la Inteligencia Artificial]], [[Análisis y Procesamiento de Datos]], [[Estadística I]], [[Gerencia de Proyectos]].

## Fuente
Escorsa y Valls; norma UNE 166006 (verificar vigencia); Espacenet/Google Patents/WIPO. Cifras ilustrativas.
