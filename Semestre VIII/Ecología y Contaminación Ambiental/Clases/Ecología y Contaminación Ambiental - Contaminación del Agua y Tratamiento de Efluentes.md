---
tags: [clase, semestre-VIII]
materia: Ecología y Contaminación Ambiental
---
# Ecología y Contaminación Ambiental - Contaminación del Agua y Tratamiento de Efluentes

Materia: [[Ecología y Contaminación Ambiental]]
Anterior: [[Ecología y Contaminación Ambiental - Dinámica Poblacional, Sucesión y Biodiversidad]]
Siguiente: [[Ecología y Contaminación Ambiental - Contaminación Atmosférica y Cambio Climático]]

## Contexto y objetivo
Analizar los principales parámetros físico-químicos y biológicos que miden la calidad del agua, comprender el mecanismo de la eutrofización y estudiar las etapas de una planta de tratamiento de aguas residuales (PTAR).

## 1. Fuentes y tipos de contaminación hídrica
- **Fuentes puntuales**: descargas localizadas y medibles (tuberías industriales, colectores cloacales municipales).
- **Fuentes difusas**: escorrentía agrícola (fertilizantes y plaguicidas), escorrentía urbana (aceites, metales), erosión de suelos.

Principales contaminantes: materia orgánica biodegradable, nutrientes ($\text{N}$, $\text{P}$), patógenos, metales pesados ($\text{Hg}$, $\text{Cr}$, $\text{Pb}$), hidrocarburos, microplásticos y **contaminación térmica** (descarga de agua caliente de sistemas de enfriamiento que reduce la solubilidad del oxígeno).

## 2. Parámetros clave de calidad del agua
1. **Oxígeno Disuelto (OD)**: concentración de $\text{O}_2$ en el agua ($\text{mg/L}$). A $20\,^\circ\text{C}$ y $1\text{ atm}$, la saturación en agua dulce es $\approx 9{,}1\text{ mg/L}$; la vida piscícola requiere por lo general $\text{OD} \ge 5\text{ mg/L}$.
2. **Demanda Bioquímica de Oxígeno ($\text{DBO}_5$)**: cantidad de oxígeno consumida por microorganismos aerobios durante 5 días a $20\,^\circ\text{C}$ en la oscuridad para oxidar la materia orgánica biodegradable.
   - Modelo de decaimiento de primer orden:
     $$L_t = L_0\,e^{-k t} \qquad \Longrightarrow \qquad \text{DBO}_t = L_0\left(1 - e^{-k t}\right)$$
     donde $L_0$ es la DBO última ($\text{mg/L}$) y $k$ es la constante de desoxigenación ($\text{día}^{-1}$).
3. **Demanda Química de Oxígeno (DQO)**: oxígeno equivalente necesario para oxidar químicamente la materia orgánica (biodegradable y no biodegradable) con un oxidante fuerte ($\text{K}_2\text{Cr}_2\text{O}_7$). Siempre se cumple $\text{DQO} \ge \text{DBO}_5$; la relación $\text{DBO}_5/\text{DQO}$ indica biodegradabilidad (si es $> 0{,}4$, el efluente es fácilmente biodegradable).
4. **Sólidos Suspendidos Totales (SST)**, turbidez, pH y coliformes fecales.

### Ejemplo resuelto de DBO
Un agua residual tiene $L_0 = 240\text{ mg/L}$ y $k = 0{,}23\text{ día}^{-1}$. Calcule la $\text{DBO}_5$:
$$\text{DBO}_5 = 240\left(1 - e^{-0{,}23 \times 5}\right) = 240\left(1 - e^{-1{,}15}\right) = 240(1 - 0{,}3166) \approx 164{,}0\text{ mg/L}$$

## 3. Autodepuración y eutrofización
Cuando un río recibe una descarga orgánica, el OD cae inicialmente por la actividad microbiana y luego se recupera por reaireación atmosférica (**curva de caída del oxígeno o de Streeter-Phelps**). Si la carga orgánica supera la capacidad de asimilación, el río entra en **anoxia** ($\text{OD} \approx 0$) y predominan procesos anaerobios (malos olores por $\text{H}_2\text{S}$ y $\text{CH}_4$).

La **eutrofización** ocurre en lagos y embalses cuando el exceso de nitratos y fosfatos provoca una floración masiva de algas; al morir, su descomposición bacteriana agota el oxígeno de las capas profundas y causa mortandad de peces.

## 4. Tratamiento de aguas residuales (PTAR)
El tratamiento convencional se organiza en etapas secuenciales:
1. **Pretratamiento**: cribado (rejas) para sólidos gruesos, desarenador y trampa de grasas.
2. **Tratamiento primario (físico)**: sedimentación primaria en decantadores para remover sólidos sedimentables ($\approx 50\text{–}65\,\%$ de SST y $25\text{–}40\,\%$ de $\text{DBO}_5$).
3. **Tratamiento secundario (biológico)**: microorganismos oxidan la materia orgánica disuelta y coloidal. Sistemas comunes: *lodos activados*, *filtros percoladores* y *lagunas de estabilización*. Remueve hasta $85\text{–}95\,\%$ de la $\text{DBO}_5$.
4. **Tratamiento terciario o avanzado**: remoción de nutrientes ($\text{N}$, $\text{P}$), filtración fina, adsorción con carbón activado, ósmosis inversa y desinfección (cloración, radiación UV u ozono).
5. **Línea de lodos**: espesamiento, digestión anaerobia (genera biogás $\text{CH}_4$), deshidratación y disposición final.

## Errores comunes
- Confundir $\text{DBO}_5$ con $\text{DQO}$: la DQO incluye compuestos orgánicos recalcitrantes que las bacterias no pueden degradar en 5 días.
- Pensar que la temperatura alta beneficia la oxigenación del agua: a mayor temperatura, *disminuye* la solubilidad del $\text{O}_2$ y *aumenta* la tasa metabólica bacteriana.

## Ejercicios propuestos
1. Si una muestra de agua industrial presenta $\text{DBO}_5 = 120\text{ mg/L}$ y $\text{DQO} = 600\text{ mg/L}$, ¿es recomendable tratarla únicamente con lodos activados convencionales?
   - *Respuesta*: $\text{DBO}_5/\text{DQO} = 0{,}20 < 0{,}4$, lo que indica baja biodegradabilidad; requerirá pretratamiento químico/fisicoquímico antes o en lugar del tratamiento biológico.
2. En la cuenca del río Torbes (Táchira), enumere dos fuentes puntuales y dos difusas típicas de contaminación.
   - *Respuesta*: puntuales: descargas de colectores cloacales urbanos y efluentes de tenerías/industrias; difusas: escorrentía de agroquímicos en zonas agrícolas y lavado de vías urbanas.

## Conexiones
- Estequiometría, concentraciones ($\text{mg/L}$, ppm) y reacciones redox en [[Química General I]].
- Modelos de decaimiento exponencial en [[Matemática I]].
- Relación con el impacto de la refrigeración de centros de datos en [[Ecología y Contaminación Ambiental - Gestión Ambiental, ISO 14001 e Informática Verde]].

## Fuente
Basado en el programa orientativo de [[Ecología y Contaminación Ambiental]] (Kiely, *Ingeniería Ambiental*; Masters, *Introducción a la Ingeniería Medioambiental*).
