---
tags: [clase, semestre-VIII]
materia: Finanzas para Ingenieros
---
# Finanzas para Ingenieros - Valor del Dinero en el Tiempo, VPN y VAN

Materia: [[Finanzas para Ingenieros]]
Anterior: — (primera clase)
Siguiente: [[Finanzas para Ingenieros - Criterios de Evaluación TIR, Verdadera Rentabilidad y B-C]]

## Contexto y objetivo
Dominar el principio fundamental de las finanzas —el **valor del dinero en el tiempo**— y aplicar los criterios de **Valor Presente Neto (VPN / VAN)** y **Valor Futuro Neto (VFN)** para evaluar si un proyecto de ingeniería genera riqueza por encima de su costo de oportunidad.

## 1. Principio del valor del dinero en el tiempo
Un bolívar o dólar disponible hoy vale más que la misma cantidad en el futuro debido a tres factores:
1. **Costo de oportunidad**: el capital actual puede invertirse y generar intereses.
2. **Inflación**: pérdida progresiva del poder adquisitivo.
3. **Riesgo e incertidumbre**: el flujo futuro puede no materializarse.

Con una tasa de descuento (costo de oportunidad del capital) $k$ por período:
- **Capitalización (valor futuro)**: $VF = VP\,(1 + k)^n$
- **Actualización o descuento (valor presente)**: $VP = \dfrac{VF}{(1 + k)^n}$

## 2. Valor Presente Neto (VPN / VAN) y Valor Futuro Neto (VFN)
Dado un proyecto con inversión inicial $I_0$ (en $t=0$) y flujos netos de efectivo $F_t$ en los períodos $t = 1, 2, \dots, n$, descontados a la tasa mínima atractiva de rendimiento (TMAR o $k$):
$$\text{VPN} = \text{VAN} = -I_0 + \sum_{t=1}^{n} \frac{F_t}{(1 + k)^t}$$

De forma equivalente, llevando todos los flujos al horizonte final $n$ se obtiene el **Valor Futuro Neto (VFN)**:
$$\text{VFN} = \text{VPN} \cdot (1 + k)^n = -I_0(1+k)^n + \sum_{t=1}^{n} F_t(1+k)^{n-t}$$

### Regla de decisión
- $\text{VPN} > 0$: el proyecto rinde por encima de $k$ y **crea valor** (aceptar).
- $\text{VPN} = 0$: el proyecto rinde exactamente $k$ (indiferente).
- $\text{VPN} < 0$: el proyecto destruye valor respecto a la alternativa $k$ (rechazar).

## 3. Ejemplo resuelto: proyecto de automatización
Un sistema de software requiere una inversión inicial $I_0 = \$10\,000$ y genera ahorros netos de $F_1 = \$4\,000$, $F_2 = \$5\,000$ y $F_3 = \$5\,000$, con costo de oportunidad $k = 12\,\%$ anual.

$$\text{VPN} = -10\,000 + \frac{4\,000}{1{,}12} + \frac{5\,000}{1{,}12^2} + \frac{5\,000}{1{,}12^3}$$
$$\text{VPN} = -10\,000 + 3\,571{,}43 + 3\,985{,}97 + 3\,558{,}90 = +\$1\,116{,}30$$

Como $\text{VPN} > 0$, el proyecto es viable. Su $\text{VFN}$ al año 3 es $1\,116{,}30 \times 1{,}12^3 \approx +\$1\,568{,}32$.

### Verificación en Python
```python
def vpn(flujos, k):
    return sum(f / (1 + k)**t for t, f in enumerate(flujos))

flujos = [-10000, 4000, 5000, 5000]
print(f"VPN = {vpn(flujos, 0.12):.2f}")  # VPN = 1116.30
```

## 4. Comparación de proyectos con vidas útiles distintas
Si dos proyectos mutuamente excluyentes tienen horizontes diferentes (p. ej., 3 años vs. 6 años), **no se deben comparar sus VPN directamente**. Se debe igualar el horizonte mediante:
- **Mínimo común múltiplo (cadena de reemplazo)**: repetir los ciclos hasta igualar la duración.
- **Costo/Beneficio Anual Equivalente (VAE / CAUE)**: convertir el VPN en una anualidad constante durante su vida útil $n$:
  $$\text{VAE} = \text{VPN} \cdot \frac{k(1+k)^n}{(1+k)^n - 1}$$

## Errores comunes
- Sumar nominalmente flujos de distintos períodos sin descontarlos ($-10\,000 + 4\,000 + 5\,000 + 5\,000 = +4\,000$), ignorando el valor del dinero en el tiempo.
- Confundir la función `VNA` / `NPV` de Excel: en Excel, `NPV(k, F1:Fn)` asume que el primer argumento del rango está en $t=1$, por lo que $I_0$ debe restarse fuera de la función (`=NPV(k, B2:D2) + B1`).
- Mezclar flujos reales (sin inflación) con tasas nominales (con inflación).

## Ejercicios propuestos
1. Un servidor nuevo cuesta $\$6\,000$ y ahorra $\$2\,500$ al año durante 3 años, con valor de rescate nulo. Si $k = 10\,\%$, calcule el VPN.
   - *Respuesta*: $\text{VPN} = -6\,000 + 2\,500 \cdot \frac{1 - 1{,}1^{-3}}{0{,}1} \approx -6\,000 + 6\,217{,}13 = +\$217{,}13$ (viable).
2. Si el proyecto A (2 años) tiene $\text{VPN}_A = \$1\,200$ y el proyecto B (4 años) tiene $\text{VPN}_B = \$2\,000$ con $k = 10\,\%$, ¿cuál conviene según el VAE?
   - *Respuesta*: $\text{VAE}_A = 1\,200 \cdot \frac{0{,}1(1{,}1)^2}{1{,}1^2 - 1} \approx \$691{,}43/\text{año}$; $\text{VAE}_B = 2\,000 \cdot \frac{0{,}1(1{,}1)^4}{1{,}1^4 - 1} \approx \$630{,}94/\text{año}$. Conviene A.

## Conexiones
- Continuación directa de [[Ingeniería Económica]].
- Siguiente criterio de evaluación en [[Finanzas para Ingenieros - Criterios de Evaluación TIR, Verdadera Rentabilidad y B-C]].
- Aplicación en evaluación de proyectos TI en [[Gerencia de Proyectos]].

## Fuente
Basado en la ruta de aprendizaje de [[Finanzas para Ingenieros]] y `Material/Tema 1/Guía didáctica Finanzas_ingenieros_V20251.pdf`, `EJERCICIOS1.pdf` y `EjerciciosExcel.xlsx`.
