---
tags: [clase, semestre-VI]
materia: Economía
---
# Economía - Modelos Económicos, Variables y Flujo Circular

Materia: [[Economía]]  
Anterior: [[Economía - Problema Económico, Necesidades y Bienes]]  
Siguiente: [[Economía - Demanda, Ley de la Demanda y Desplazamientos]]

## Contexto y objetivo

Presentar los **instrumentos del análisis económico** correspondientes al primer parcial (Guía N° 3): cómo se construyen los modelos económicos, cómo se clasifican las variables (dependientes/independientes, endógenas/exógenas), cómo se representan gráficamente las funciones y cómo funciona el **flujo circular de la renta**.

## 1. Modelos en la economía

Un **modelo económico** es una representación simplificada de la realidad que utiliza relaciones lógicas, matemáticas o estadísticas entre variables económicas para explicar procesos productivos y predecir resultados.

Así como en ingeniería existen modelos matemáticos y estadísticos, en economía un esquema se construye seleccionando las variables relevantes y omitiendo detalles secundarios bajo el supuesto *ceteris paribus*.

## 2. Relaciones funcionales y tipos de variables

En economía se analiza siempre la relación **causa–efecto** entre variables mediante ecuaciones funcionales.

### Variables dependientes e independientes
- **Variable independiente (causa)**: es la que explica o provoca el cambio. Ejemplo: el precio de un bien ($P_x$).
- **Variable dependiente (efecto)**: es la que responde al cambio. Ejemplo: la cantidad demandada ($D_x$).

En una función simple de demanda:
$$D_x = f(P_x) \quad \text{(ceteris paribus)}$$

### Funciones de dos o más variables
En la realidad, un fenómeno suele depender de múltiples causas. Por ejemplo, la demanda de mantequilla ($D_m$) depende de su propio precio ($P_m$), pero también del precio de bienes relacionados como la margarina ($P_{\text{marg}}$) y del ingreso del consumidor ($Y$):
$$D_m = f(P_m, P_{\text{marg}}, Y)$$

### Variables endógenas y exógenas
- **Endógenas**: variables internas al sistema económico o modelo, cuyo valor es explicado por el propio modelo o puede ser gestionado dentro de él.
- **Exógenas**: variables externas que el sistema no controla directamente, pero que impactan sobre las variables endógenas.

> **Ejemplo de la cátedra (cultivos agrícolas):** la cantidad de fertilizante aplicada y el precio fijado son variables **endógenas** (decisión interna); las lluvias, sequías o plagas son variables **exógenas** (externas, no controlables).

## 3. Representación gráfica de funciones económicas

A partir de una tabla o ecuación lineal, se construye la gráfica en el primer cuadrante. Siguiendo la convención económica estándar (Marshall), el **precio ($P$)** suele ubicarse en el eje vertical y la **cantidad ($Q$ o $D_x$)** en el eje horizontal.

**Ejemplo del Material (Proyección de la demanda):**
Sea la función $D_x = 50 - 10 P_x$ para $P_x \in \{1, 2, 3, 4, 5\}$:

| $P_x$ (Precio) | $D_x = 50 - 10P_x$ (Cantidad demandada) |
|---|---|
| $1$ | $40$ |
| $2$ | $30$ |
| $3$ | $20$ |
| $4$ | $10$ |
| $5$ | $0$ |

Al graficar estos puntos se obtiene una recta con pendiente negativa, reflejando la relación inversa entre precio y cantidad demandada.

## 4. Flujo circular de la renta

El **flujo circular de la renta** explica cómo se genera, distribuye y gasta el ingreso en una economía simplificada entre dos agentes: **economías domésticas (familias)** y **empresas**, conectados a través de dos mercados: el **mercado de factores productivos** y el **mercado de bienes y servicios**.

```
             Flujo real (bienes y servicios) --->
  [Empresas] <---------------------------------- [Familias]
             <--- Flujo monetario (gasto / ingreso)
```

Surgen dos circuitos simultáneos:
1. **Flujo real (circula exteriormente)**: las familias ofrecen factores productivos (trabajo, tierra, capital) a las empresas, y las empresas entregan bienes y servicios a las familias.
2. **Flujo monetario (circula interiormente)**: las empresas pagan rentas (salarios, alquileres, intereses, beneficios) a las familias por sus factores, y las familias gastan ese dinero comprando bienes y servicios a las empresas.

De esta identidad contable fundamental se deduce que en una economía cerrada sin ahorro ni sector público:
$$\text{Renta} = \text{Ingreso} = \text{Gasto}$$

## Errores comunes

- Invertir la definición de **endógena** y **exógena**: recuerda *en-* = dentro del modelo/sistema, *exo-* = fuera del sistema.
- Confundir el **flujo real** (bienes, servicios y factores físicos/humanos) con el **flujo monetario** (dinero que circula en sentido opuesto).
- Calcular la pendiente gráfica como $\Delta D / \Delta P$ cuando el precio está en el eje vertical: si $P$ está en el eje $Y$ y $Q$ en el eje $X$, la pendiente visual es $\Delta P / \Delta Q = -1/10 = -0.1$.

## Ejercicios propuestos

1. Dada la función de demanda $D_x = 80 - 4 P_x$, construye la tabla para $P_x = 0, 5, 10, 15, 20$ e identifica la variable independiente y la dependiente.
   - *Respuesta:* Variable independiente: $P_x$; dependiente: $D_x$. Valores de $D_x$: $80, 60, 40, 20, 0$.
2. En una empresa de desarrollo de software, clasifica en endógenas o exógenas: *(a)* número de programadores contratados, *(b)* reforma tributaria nacional, *(c)* inversión en servidores propios.
   - *Respuesta:* *(a)* Endógena, *(b)* Exógena, *(c)* Endógena.

## Conexiones

- Anterior: [[Economía - Problema Económico, Necesidades y Bienes]]
- Siguiente: [[Economía - Demanda, Ley de la Demanda y Desplazamientos]]
- Materia: [[Economía]]
- Materias relacionadas: [[Matemática I]], [[Estadística I]], [[Ingeniería Económica]]

## Fuente

- `Material/resumen de la parte 2-Primer parcial.docx` (Guía N° 3: instrumentos del análisis económico, variables endógenas/exógenas, proyección de demanda, flujo circular de la renta).
