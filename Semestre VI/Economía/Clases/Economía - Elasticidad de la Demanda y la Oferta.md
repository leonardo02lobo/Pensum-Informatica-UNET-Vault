---
tags: [clase, semestre-VI]
materia: Economía
---
# Economía - Elasticidad de la Demanda y la Oferta

Materia: [[Economía]]  
Anterior: [[Economía - Oferta y Equilibrio de Mercado]]  
Siguiente: [[Economía - Principios de la Producción y Escasez]]

## Contexto y objetivo

Medir la **sensibilidad** de la cantidad demandada u ofrecida ante variaciones en el precio mediante el concepto de **elasticidad**, diferenciando los casos de demanda elástica, inelástica, unitaria y los extremos teóricos (Guía 4, segundo parcial).

## 1. Definición de elasticidad precio de la demanda

La **elasticidad precio de la demanda ($E_p$)** mide el cambio porcentual en la cantidad demandada dividido entre el cambio porcentual en el precio:

$$E_p = \frac{\%\Delta Q}{\%\Delta P} = \frac{\Delta Q / Q}{\Delta P / P} = \frac{\Delta Q}{\Delta P} \cdot \frac{P}{Q}$$

Debido a la ley de la demanda, $\Delta Q / \Delta P < 0$, por lo que $E_p$ resulta negativa; en la práctica suele analizarse su **valor absoluto** $|E_p|$.

Para evitar que el resultado dependa de si el precio sube o baja entre dos puntos $(Q_1, P_1)$ y $(Q_2, P_2)$, se usa la **fórmula del punto medio (arco)**:
$$E_p = \frac{\frac{Q_2 - Q_1}{(Q_1 + Q_2)/2}}{\frac{P_2 - P_1}{(P_1 + P_2)/2}}$$

## 2. Tipos de elasticidad de la demanda

| Tipo | Condición | Interpretación económica | Ejemplo típico |
|---|---|---|---|
| **Demanda elástica** | $\|E_p\| > 1$ | Un cambio porcentual en el precio provoca un cambio porcentual *mayor* en la cantidad demandada. | Bienes de lujo, bienes con muchos sustitutos (boletos de cine, marcas específicas de gaseosa). |
| **Demanda inelástica** | $\|E_p\| < 1$ | Un cambio porcentual en el precio genera un cambio porcentual *menor* en la cantidad demandada. | Bienes de primera necesidad o sin sustitutos cercanos (insulina, sal, electricidad básica). |
| **Demanda unitaria** | $\|E_p\| = 1$ | El cambio porcentual en la cantidad demandada es exactamente igual al cambio porcentual en el precio. | Caso frontera teórico donde el ingreso total permanece constante. |
| **Perfectamente elástica** | $\|E_p\| \to \infty$ | Un cambio infinitesimal en el precio provoca una caída total de la cantidad demandada (curva horizontal). | Producto idéntico en competencia perfecta. |
| **Perfectamente inelástica** | $\|E_p\| = 0$ | La cantidad demandada no varía ante ningún cambio en el precio (curva vertical). | Medicamento vital de dosis fija. |

## 3. Relación entre elasticidad e ingreso total

El ingreso total del vendedor es $IT = P \cdot Q$.
- Si la demanda es **inelástica** ($|E_p| < 1$), subir el precio **aumenta** el ingreso total (la caída porcentual en $Q$ es menor que la subida en $P$).
- Si la demanda es **elástica** ($|E_p| > 1$), subir el precio **disminuye** el ingreso total (la caída en $Q$ más que compensa el mayor precio).
- Si $|E_p| = 1$, el ingreso total alcanza su **máximo**.

## 4. Ejemplo numérico resuelto

Con la función $D_x = 50 - 10P_x$, calculemos la elasticidad arco cuando el precio sube de $P_1 = 2$ ($Q_1 = 30$) a $P_2 = 3$ ($Q_2 = 20$):

$$\%\Delta Q = \frac{20 - 30}{(30 + 20)/2} = \frac{-10}{25} = -0.40 \quad (-40\%)$$
$$\%\Delta P = \frac{3 - 2}{(2 + 3)/2} = \frac{1}{2.5} = +0.40 \quad (+40\%)$$
$$E_p = \frac{-0.40}{0.40} = -1 \implies |E_p| = 1 \quad (\text{elasticidad unitaria})$$

Observa el ingreso total: $IT_1 = 2 \cdot 30 = 60$ y $IT_2 = 3 \cdot 20 = 60$.

## 5. Elasticidad de la oferta (breve referencia)

Análogamente, $E_o = \frac{\%\Delta Q_o}{\%\Delta P} \ge 0$. Depende principalmente de la capacidad de los productores para ajustar su producción y del **horizonte temporal** (en el largo plazo la oferta es más elástica que en el corto plazo).

## Errores comunes

- Confundir **pendiente** ($\Delta P / \Delta Q$) con **elasticidad**: en una recta de demanda lineal, la pendiente es constante, pero la elasticidad varía en cada punto (es elástica en precios altos e inelástica en precios bajos).
- Usar $Q_1$ y $P_1$ en lugar del punto medio cuando se pide elasticidad entre dos puntos sin indicar dirección.

## Ejercicios propuestos

1. El precio de un servicio de nube pasa de \$10 a \$12 y la cantidad de suscripciones baja de 500 a 450. Calcula la elasticidad arco y clasifícala.
   - *Respuesta:* $\%\Delta Q = -50/475 \approx -10.53\%$; $\%\Delta P = 2/11 \approx +18.18\%$; $|E_p| \approx 0.58 < 1$ (demanda **inelástica**).
2. Si una empresa vende un producto con demanda elástica ($|E_p| = 2.2$) y necesita aumentar sus ingresos brutos, ¿le conviene subir o bajar el precio?
   - *Respuesta:* Bajar el precio, ya que el aumento porcentual en cantidad vendida será más del doble que la reducción porcentual del precio.

## Conexiones

- Anterior: [[Economía - Oferta y Equilibrio de Mercado]]
- Siguiente: [[Economía - Principios de la Producción y Escasez]]
- Materia: [[Economía]]
- Materias relacionadas: [[Matemática I]], [[Matemática II]], [[Ingeniería Económica]], [[Finanzas para Ingenieros]]

## Fuente

- `Material/resumen  2do parcial.docx` (Guía 4: análisis de la demanda y tipos de elasticidad).
