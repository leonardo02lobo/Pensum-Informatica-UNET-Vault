---
tags: [clase, semestre-VIII]
materia: Ecología y Contaminación Ambiental
---
# Ecología y Contaminación Ambiental - Dinámica Poblacional, Sucesión y Biodiversidad

Materia: [[Ecología y Contaminación Ambiental]]
Anterior: [[Ecología y Contaminación Ambiental - Ecosistemas, Flujo de Energía y Ciclos Biogeoquímicos]]
Siguiente: [[Ecología y Contaminación Ambiental - Contaminación del Agua y Tratamiento de Efluentes]]

## Contexto y objetivo
Modelar matemáticamente cómo crecen y se regulan las poblaciones biológicas, comprender cómo evolucionan las comunidades en el tiempo (sucesión ecológica) y cuantificar la biodiversidad mediante índices estándar empleados en estudios de impacto ambiental.

## 1. Parámetros demográficos de una población
Una **población** es un conjunto de individuos de la misma especie que ocupa un área determinada. Su tamaño $N(t)$ cambia por cuatro procesos básicos:
$$\Delta N = (B - D) + (I - E)$$
donde $B$ son nacimientos, $D$ muertes, $I$ inmigración y $E$ emigración. En poblaciones cerradas se define la **tasa intrínseca de crecimiento** $r = b - d$ (diferencia entre tasa de natalidad y mortalidad per cápita).

## 2. Modelos de crecimiento poblacional

### Crecimiento exponencial (potencial biótico)
Cuando los recursos son ilimitados, la velocidad de crecimiento es proporcional al tamaño actual de la población:
$$\frac{dN}{dt} = r\,N \quad \Longrightarrow \quad N(t) = N_0\,e^{r t}$$
Produce una curva en forma de **J**. Solo es sostenible de forma transitoria (colonización inicial o plagas sin depredadores).

### Crecimiento logístico (resistencia ambiental)
En condiciones reales, la escasez de alimento, espacio o la acumulación de desechos impone una **capacidad de carga** $K$ (máximo número de individuos que el ambiente puede sostener de forma indefinida):
$$\frac{dN}{dt} = r\,N\left(1 - \frac{N}{K}\right)$$
Su solución analítica es la curva sigmoidal en forma de **S**:
$$N(t) = \frac{K}{1 + \left(\frac{K - N_0}{N_0}\right)e^{-r t}}$$
- Si $N \ll K$, el factor $(1 - N/K) \approx 1$ y el crecimiento es casi exponencial.
- El punto de máxima tasa de crecimiento ocurre en $N = K/2$.
- Si $N > K$, la derivada es negativa y la población decrece hacia $K$.

### Ejemplo resuelto
Una población de peces en un embalse tiene $N_0 = 500$ individuos, $r = 0{,}08\text{ año}^{-1}$ y capacidad de carga $K = 2\,500$. Calcule la tasa de crecimiento instantánea inicial:
$$\left.\frac{dN}{dt}\right|_{t=0} = 0{,}08 \times 500 \times \left(1 - \frac{500}{2\,500}\right) = 40 \times 0{,}80 = 32\text{ individuos/año}$$

## 3. Estrategias reproductivas ($r$ y $K$) y relaciones interespecíficas
- **Estrategas $r$**: organismos pequeños, maduración rápida, alta fecundidad, poca inversión parental (insectos, malezas, bacterias); prosperan en ambientes inestables o recién perturbados.
- **Estrategas $K$**: organismos grandes, maduración lenta, pocas crías con alto cuidado parental (grandes mamíferos, árboles maduros); dominan en ecosistemas estables cercanos a $K$.

Interacciones entre especies: **competencia** ($-/-$), **depredación/parasitismo** ($+/-$), **mutualismo** ($+/+$), **comensalismo** ($+/0$) y **amensalismo** ($-/0$).

## 4. Sucesión ecológica
La **sucesión ecológica** es el reemplazo gradual y predecible de comunidades en un área a lo largo del tiempo:
- **Sucesión primaria**: inicia en un sustrato desprovisto de suelo y vida (roca volcánica recién solidificada, retroceso de glaciares). Comienza con *especies pioneras* (líquenes, musgos) que forman suelo.
- **Sucesión secundaria**: ocurre tras una perturbación (incendio, tala, abandono agrícola) donde el suelo y el banco de semillas permanecen. Es mucho más rápida que la primaria.
- **Comunidad clímax**: etapa relativamente estable y autorregulada en equilibrio con el clima y el suelo locales.

## 5. Biodiversidad e índice de Shannon-Wiener
La biodiversidad abarca diversidad **genética**, de **especies** y de **ecosistemas**. En inventarios biológicos se distingue entre **riqueza** ($S$, número de especies) y **equitatividad** (qué tan uniforme es la abundancia de cada especie).

El **índice de Shannon-Wiener** ($H'$) mide la diversidad combinando riqueza y equitatividad:
$$H' = -\sum_{i=1}^{S} p_i \ln(p_i)$$
donde $p_i = n_i / N$ es la proporción de individuos de la especie $i$ respecto al total $N$. Valores típicos en ecosistemas naturales oscilan entre $1{,}5$ y $3{,}5$; un monocultivo ($S=1$) tiene $H' = 0$.

### Ejemplo de cálculo de $H'$
En un muestreo se hallan 3 especies con abundancias $n_1 = 50$, $n_2 = 30$, $n_3 = 20$ ($N = 100$):
$$H' = -\big(0{,}5\ln(0{,}5) + 0{,}3\ln(0{,}3) + 0{,}2\ln(0{,}2)\big) \approx -\big(-0{,}3466 - 0{,}3612 - 0{,}3219\big) = 1{,}03$$

## Errores comunes
- Usar logaritmo base 10 sin aclararlo al calcular $H'$ (cambia la escala numérica respecto a $\ln$; siempre especificar la base).
- Confundir riqueza de especies ($S$) con diversidad ($H'$): dos áreas con $S=5$ tienen distinta diversidad si una está dominada al $96\,\%$ por una sola especie y la otra tiene $20\,\%$ de cada una.

## Ejercicios propuestos
1. Para una población con $r = 0{,}1\text{ mes}^{-1}$ y $K = 1\,000$, ¿en qué tamaño poblacional $N$ es máxima la velocidad de crecimiento $dN/dt$ y cuál es ese valor máximo?
   - *Respuesta*: en $N = K/2 = 500$, donde $dN/dt = 0{,}1 \times 500 \times 0{,}5 = 25\text{ individuos/mes}$.
2. Calcule el índice de Shannon $H'$ para una comunidad con 4 especies igualmente abundantes ($p_i = 0{,}25$).
   - *Respuesta*: $H' = -4(0{,}25 \ln 0{,}25) = \ln(4) \approx 1{,}386$.

## Conexiones
- Ecuaciones diferenciales ordinarias y modelos exponenciales en [[Matemática I]] y [[Matemática II]].
- Fundamentos probabilísticos de los índices de entropía en [[Estadística I]].
- Base para la evaluación de impacto ambiental en [[Ecología y Contaminación Ambiental - Gestión Ambiental, ISO 14001 e Informática Verde]].

## Fuente
Basado en el programa orientativo de [[Ecología y Contaminación Ambiental]] (Odum, *Ecología*; Miller, *Ciencia ambiental*).
