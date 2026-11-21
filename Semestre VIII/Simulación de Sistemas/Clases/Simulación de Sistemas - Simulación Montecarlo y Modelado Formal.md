---
tags: [clase, semestre-VIII]
materia: Simulación de Sistemas
---
# Simulación de Sistemas - Simulación Montecarlo y Modelado Formal

Materia: [[Simulación de Sistemas]]
Anterior: [[Simulación de Sistemas - Simulación de Eventos Discretos y Lista de Eventos Futuros]]
Siguiente: [[Simulación de Sistemas - Verificación, Validación y Análisis de Salida]]

## Contexto y objetivo
Dominar el **método de Montecarlo** para estimar integrales, probabilidades y riesgos en sistemas estáticos o complejos, y estructurar el **modelado formal** de un sistema discreto (ecuaciones de transición de estado, diccionario de variables y especificación de eventos) tal como exige el Parcial II de la asignatura.

## 1. Simulación Montecarlo
La **simulación Montecarlo** utiliza muestreo aleatorio repetido ($N$ ensayos independientes) para aproximar cantidades numéricas deterministas o distribuciones de resultados bajo incertidumbre, apoyándose en la **Ley de los Grandes Números** y el **Teorema Central del Límite**.

### Ejemplo clásico: estimación de $\pi$
Se lanzan $N$ puntos $(X_i, Y_i)$ uniformes en el cuadrado unidad $[0,1]^2$. La probabilidad de caer dentro del cuarto de círculo unitario ($X_i^2 + Y_i^2 \le 1$) es $\pi / 4$, luego:
$$\hat{\pi} = 4 \cdot \frac{\text{puntos dentro}}{N}$$
El error estándar de la estimación decae como $O(1/\sqrt{N})$: para reducir el error a la décima parte, se requieren $100$ veces más muestras.

### Integración Montecarlo general
Para estimar $I = \int_a^b g(x)\,dx$:
$$I \approx (b - a)\,\frac{1}{N}\sum_{i=1}^{N} g(X_i), \qquad X_i \sim U(a,b)$$

### Aplicaciones en ingeniería e informática
- Análisis de riesgo financiero (valoración de portafolios, VaR) y presupuestos de proyectos.
- Confiabilidad de redes y sistemas con múltiples componentes que fallan aleatoriamente.
- Búsqueda heurística en árboles de juego (Monte Carlo Tree Search, MCTS).

## 2. Modelado formal de sistemas discretos
En la etapa de **modelo formal** (Parcial II), el sistema deja de describirse en lenguaje natural y se especifica matemáticamente mediante:
1. **Diccionario de variables**:
   - *Variables de estado* $S(t)$: definen completamente la situación del sistema en $t$ (ej. tesoro $G_i$, ejército $M_i$, descontento provincial $D_p$).
   - *Variables de flujo*: miden tasas o cambios ocurridos en un evento/período (recaudación $R_i$, gasto $X_i$).
   - *Variables auxiliares*: cálculos intermedios (renta provincial $I_p$).
   - *Parámetros* $\Theta$: constantes fijas durante la corrida (tasa impositiva, costo de mantenimiento).
   - *Entradas exógenas / aleatorias* $U$: perturbaciones externas o realizaciones aleatorias.
2. **Ecuación general de transición de estado**:
   $$S(\tau^+) = \Psi_e\big(S(\tau^-),\, \Theta,\, U\big)$$
   donde $\tau^-$ y $\tau^+$ denotan el instante inmediatamente anterior y posterior a la ejecución del evento $e$.

### Ejemplo formal (referencia de Age of Conquest)
Para un imperio $i$ en el turno $t$:
- Renta provincial: $I_p(t) = f(\text{población}_p, \text{tasa\_impuesto}, D_p)$
- Recaudación total: $R_i = \sum_{p \in P_i} I_p(t)$
- Costo de mantenimiento: $C_i = c_{\text{adm}}\,n_i + c_{\text{up}}\,M_i$
- Transición del tesoro con restricción de no negatividad:
  $$G_i(t+1) = \max\!\big(0,\; G_i(t) + R_i - C_i - X_i\big)$$
- Descontento provincial acotado: $D_p(t+1) = \text{clamp}\big(D_p(t) + \Delta D_p,\, 0,\, 100\big)$.

## Errores comunes
- Creer que duplicar $N$ en Montecarlo reduce el error a la mitad: el error disminuye con $\sqrt{N}$, por lo que duplicar $N$ solo reduce el error en un factor $\approx 1{,}41$.
- Mezclar variables de estado con variables auxiliares en el modelo formal sin especificar en qué instante ($\tau^-$ o $\tau^+$) se evalúa cada ecuación.
- Omitir cotas físicas/lógicas (como $\max(0, \cdot)$ o `clamp`) en las ecuaciones de estado, permitiendo tesoros negativos o porcentajes fuera de $[0, 100]$.

## Ejercicios propuestos
1. Use Montecarlo en Python para aproximar $\int_0^1 e^{-x^2}\,dx$ con $N = 100\,000$ muestras.
   - *Respuesta*: generar `x = rng.uniform(0, 1, 100000)` y calcular `np.mean(np.exp(-x**2))` ($\approx 0{,}7468$).
2. Clasifique las siguientes magnitudes de un sistema de inventario en estado, flujo o parámetro: (a) stock actual en almacén; (b) tamaño máximo de lote de pedido; (c) unidades vendidas hoy.
   - *Respuesta*: (a) estado; (b) parámetro; (c) flujo.

## Conexiones
- Detalle completo del modelo formal en [[Age of Conquest Simulación de Eventos Discretos]].
- Métodos numéricos e integración en [[Cálculo Numérico]].
- Validación estadística de las salidas en [[Simulación de Sistemas - Verificación, Validación y Análisis de Salida]].

## Fuente
Basado en [[Simulación de Sistemas]], [[Age of Conquest Simulación de Eventos Discretos]] y los documentos del Parcial II en `~/Documentos/UNET/Simulacio  de Sistemas`.
