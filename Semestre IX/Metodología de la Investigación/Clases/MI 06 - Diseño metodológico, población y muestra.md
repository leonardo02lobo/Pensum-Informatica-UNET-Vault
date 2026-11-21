---
tags: [clase, semestre-IX]
materia: Metodología de la Investigación
fuente: "conocimiento general"
---
# MI 06 - Diseño metodológico, población y muestra

Materia: [[Metodología de la Investigación]]
Anterior: [[MI 05 - Hipótesis, variables y operacionalización]]
Siguiente: [[MI 07 - Instrumentos, validez y confiabilidad]]

## Contexto y objetivo
El marco metodológico explica **cómo** se logrará cada objetivo: tipo y diseño, población y muestra, técnicas e instrumentos, procedimiento y análisis. Es lo que permite a otro evaluar y replicar tu trabajo. Objetivo: redactar este capítulo y calcular tamaños de muestra con distintos muestreos.

## Estructura del marco metodológico
1. Tipo, nivel y diseño de investigación (ver [[MI 02 - Enfoques y tipos de investigación]]).
2. Población y muestra (o unidades de análisis / informantes clave en cualitativa).
3. Técnicas e instrumentos de recolección de datos ([[MI 07 - Instrumentos, validez y confiabilidad]]).
4. Validez y confiabilidad.
5. Procedimiento o fases de la investigación (aquí va la **metodología de desarrollo de software**: Scrum, RUP, XP, cascada, con su justificación y las fases adaptadas a tus objetivos).
6. Técnicas de análisis de datos ([[MI 08 - Estadística aplicada a la investigación]]).
7. Consideraciones éticas.

## Población y muestra
- **Población (universo)**: conjunto de todos los elementos con una característica común, definido por contenido, lugar y tiempo. Ej.: "los 120 estudiantes inscritos en Redes en el período 2026-1".
- **Unidad de análisis**: elemento sobre el que se mide.
- **Muestra**: subconjunto representativo. **Censo**: se estudia toda la población (recomendable si $N$ es pequeño, p.ej. menos de 30-50).
- **Marco muestral**: lista de la que se extrae la muestra.
- **Parámetro** (población) vs **estadístico** (muestra).

### Tipos de muestreo
**Probabilístico** (cada elemento tiene probabilidad conocida; permite generalizar e inferir):
- **Aleatorio simple**: sorteo.
- **Sistemático**: cada $k=N/n$-ésimo elemento tras un inicio aleatorio.
- **Estratificado**: dividir en estratos homogéneos (carrera, sede) y muestrear en cada uno (afijación proporcional: $n_h = n\,N_h/N$).
- **Por conglomerados**: sortear grupos naturales (secciones, aulas) y estudiar todos sus miembros.
**No probabilístico** (no generalizable estadísticamente; frecuente en cualitativa y estudios pequeños):
- **Por conveniencia**, **intencional/criterial**, **por cuotas**, **bola de nieve**, **de casos típicos/extremos**.

### Tamaño de muestra
**Población finita, estimación de proporción**:
$$n = \frac{N\,Z^2\,p\,q}{e^2\,(N-1) + Z^2\,p\,q}$$
con $Z$ = 1.645 (90%), 1.96 (95%), 2.576 (99%); $p=0.5$ si se desconoce (máxima variabilidad), $q=1-p$, $e$ error máximo (p.ej. 0.05).

**Población infinita**: $n_0 = Z^2 p q / e^2$. Con $Z=1.96$, $p=q=0.5$, $e=0.05$: $n_0 = 3.8416\times 0.25/0.0025 = 384.16 \approx 385$.

**Ejemplo resuelto.** $N = 600$ estudiantes, confianza 95%, error 5%, $p=0.5$:
1. $Z^2 p q = 3.8416 \times 0.25 = 0.9604$.
2. Denominador: $0.0025 \times 599 + 0.9604 = 1.4975 + 0.9604 = 2.4579$.
3. Numerador: $600 \times 0.9604 = 576.24$.
4. $n = 576.24/2.4579 = 234.4 \approx 235$.
5. Con estratificación proporcional por 3 carreras (300, 200, 100): 117, 78, 39 (suman 234; ajusta a 235 redondeando).
Con error de 10%: denominador $0.01\times599+0.9604=6.95$, $n = 576.24/6.95 = 82.9 \approx 83$.

**Para estimar una media**: $n = (Z\sigma/e)^2$ (con corrección finita $n' = n/(1+n/N)$). **Para comparar dos grupos** (potencia): se usa análisis de potencia (G*Power; en Python `statsmodels.stats.power`).

```python
import math
def muestra_finita(N, Z=1.96, p=0.5, e=0.05):
    q = 1 - p
    return math.ceil(N * Z**2 * p * q / (e**2 * (N - 1) + Z**2 * p * q))

print(muestra_finita(600))        # 235
print(muestra_finita(600, e=0.10))  # 83
```

### Tamaño en cualitativa
No hay fórmula; se busca **saturación teórica** (nuevas entrevistas no aportan categorías nuevas). Rangos orientativos: entrevistas 8-30; grupos focales 3-6 grupos.

## Diseño del procedimiento (fases) en proyectos de software
Ejemplo con Scrum adaptado a los objetivos:
| Objetivo específico | Fase | Técnicas | Producto |
|---|---|---|---|
| Diagnosticar | Fase 1: Diagnóstico | Entrevista, observación | Informe de situación |
| Requisitos | Fase 2: Análisis | Historias de usuario | Product backlog |
| Diseñar | Fase 3: Diseño | UML, modelo de datos | Diagramas |
| Implementar | Fase 4: Sprints 1-4 | Codificación, pruebas | Incrementos |
| Evaluar | Fase 5: Evaluación | SUS, pruebas | Informe de resultados |
Justifica la metodología con criterios ([[IS 01 - Ciclo de vida y modelos de proceso]]).

## Validez del diseño
- **Interna**: la causa explica el efecto (amenazas: historia, maduración, selección, mortalidad experimental, instrumentación).
- **Externa**: generalización a otros contextos.
- **Constructo** y **de conclusión estadística**.
Controles: aleatorización, grupo de control, enmascaramiento (ciego), estandarización del procedimiento, estudio piloto.

## Errores comunes
- Llamar "muestra" a un grupo de conveniencia y luego generalizar a toda la población.
- Aplicar la fórmula con $N$ equivocada o mezclando parámetros.
- Describir la metodología de desarrollo sin vincularla a los objetivos.
- Omitir el criterio de inclusión y exclusión.
- No mencionar cómo se garantiza la ética (consentimiento, anonimato).

## Ejercicios propuestos
1. $N = 1000$, 95% de confianza, 5%: ¿n? *Resp.: 278.*
2. ¿Qué muestreo usarías para comparar tres sedes? *Resp.: estratificado por sede.*
3. ¿Cuándo hacer censo? *Resp.: cuando la población es pequeña y accesible.*

## Conexiones
[[Estadística I]] (muestreo), [[Estadística II]], [[Estructura del anteproyecto de investigación]], [[IS 10 - Gestión de proyectos y estimación]].

## Fuente
Conocimiento general. Hernández Sampieri; Arias; Cochran, *Sampling Techniques*.
