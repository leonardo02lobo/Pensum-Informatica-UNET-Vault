---
tags: [clase, semestre-VIII]
materia: Finanzas para Ingenieros
---
# Finanzas para Ingenieros - Criterios de Evaluación TIR, Verdadera Rentabilidad y B-C

Materia: [[Finanzas para Ingenieros]]
Anterior: [[Finanzas para Ingenieros - Valor del Dinero en el Tiempo, VPN y VAN]]
Siguiente: [[Finanzas para Ingenieros - Fundamentos Económicos, Mercancía y Sistema Financiero]]

## Contexto y objetivo
Evaluar proyectos mediante criterios relativos —**Tasa Interna de Retorno (TIR)**, **Verdadera Rentabilidad (VR / TIRM)** y **Relación Beneficio/Costo (B/C)**—, identificando las limitaciones matemáticas de la TIR clásica y cómo resolverlas correctamente en decisiones de inversión.

## 1. Tasa Interna de Retorno (TIR)
La **TIR** es la tasa de descuento $r$ que hace que el Valor Presente Neto del proyecto sea igual a cero:
$$\text{VPN}(r) = -I_0 + \sum_{t=1}^{n} \frac{F_t}{(1 + r)^t} = 0$$
- **Regla de decisión**: si $\text{TIR} > k$ (TMAR), aceptar; si $\text{TIR} < k$, rechazar.

### Limitaciones de la TIR clásica
1. **TIR múltiples**: según la regla de los signos de Descartes, si el flujo de caja cambia de signo más de una vez (proyectos no convencionales, p. ej., inversión inicial, ingresos intermedios y costo de cierre/desmantelamiento al final), pueden existir varias raíces reales positivas o ninguna.
2. **Supuesto implícito de reinversión**: la TIR asume matemáticamente que los flujos intermedios positivos se reinvierten a la misma TIR, lo cual es irreal cuando la TIR es muy alta (p. ej., $80\,\%$).
3. **Inconsistencia con el VPN en proyectos mutuamente excluyentes**: diferencias de escala o de perfil temporal pueden hacer que un proyecto tenga mayor TIR pero menor VPN. Siempre prevalece el **VPN** para maximizar riqueza.

## 2. Verdadera Rentabilidad (VR / TIRM)
Para corregir el supuesto de reinversión y eliminar las TIR múltiples, se define la **Verdadera Rentabilidad** (Tasa Interna de Retorno Modificada, **TIRM**):
1. Se llevan todos los flujos **negativos** a valor presente ($t=0$) usando la tasa de financiamiento $k_f$.
2. Se capitalizan todos los flujos **positivos** hasta el período final $n$ usando la tasa de reinversión realista $k_r$ (usualmente el costo de oportunidad $k$).
3. Se calcula la tasa única que iguala el valor presente de los egresos con el valor futuro de los ingresos:
$$\text{VR} = \left(\frac{\text{VF}(\text{flujos positivos}, k_r)}{|\text{VP}(\text{flujos negativos}, k_f)|}\right)^{1/n} - 1$$

### Ejemplo resuelto
Proyecto con flujo $[-1\,000, +800, +600]$ y tasa de reinversión/costo de oportunidad $k = 10\,\%$:
- $\text{VP}(\text{egresos}) = 1\,000$
- $\text{VF}(\text{ingresos en } t=2) = 800(1{,}10)^1 + 600 = 880 + 600 = 1\,480$
- $\text{VR} = \left(\frac{1\,480}{1\,000}\right)^{1/2} - 1 = \sqrt{1{,}48} - 1 \approx 21{,}66\,\%$

Mientras tanto, la TIR clásica da $\approx 26{,}5\,\%$ (sobrestima la rentabilidad real porque supone reinvertir los $\$800$ al $26{,}5\,\%$ en lugar de al $10\,\%$).

## 3. Relación Beneficio/Costo (B/C) e Índice de Rentabilidad (IR)
Mide cuántos dólares de beneficio presente se obtienen por cada dólar de costo presente, descontando ambos a la tasa $k$:
$$B/C = \frac{\text{VP}(\text{Beneficios}, k)}{\text{VP}(\text{Costos}, k)}$$
- Si $B/C > 1$, el proyecto es viable (equivale a $\text{VPN} > 0$).
- Muy útil bajo **racionamiento de capital** para ordenar proyectos independientes por eficiencia por unidad invertida.

## 4. Período de Recuperación (Payback)
- **Payback simple**: tiempo necesario para recuperar $I_0$ sin descontar flujos.
- **Payback descontado**: tiempo en que la suma de flujos descontados iguala a $I_0$. Mide liquidez/riesgo temporal, pero ignora flujos posteriores al corte.

## Errores comunes
- Elegir entre dos proyectos mutuamente excluyentes por tener mayor TIR cuando su VPN es menor (problema de escala).
- Calcular la TIR de un flujo no convencional sin verificar si hay múltiples cambios de signo.
- Dividir beneficios entre costos en $B/C$ sin haber descontado ambos al mismo período.

## Ejercicios propuestos
1. Un proyecto requiere $I_0 = \$2\,000$, genera $F_1 = \$1\,500$ y $F_2 = \$1\,500$, con $k = 10\,\%$. Calcule $B/C$ y la Verdadera Rentabilidad ($\text{VR}$).
   - *Respuesta*: $\text{VP}(\text{Beneficios}) = \frac{1\,500}{1{,}1} + \frac{1\,500}{1{,}21} = 1\,363{,}64 + 1\,239{,}67 = 2\,603{,}31$; $B/C = 2\,603{,}31 / 2\,000 \approx 1{,}30 > 1$. Para $\text{VR}$: $\text{VF}(\text{ingresos}) = 1\,500(1{,}1) + 1\,500 = 3\,150$; $\text{VR} = (3\,150/2\,000)^{1/2} - 1 \approx 25{,}50\,\%$.
2. ¿Por qué un proyecto con flujos $[-100, +230, -132]$ puede confundir a quien usa solo la función `TIR` de Excel?
   - *Respuesta*: tiene dos cambios de signo y dos TIR positivas ($10\,\%$ y $20\,\%$); Excel solo devuelve la primera raíz cercana al valor semilla.

## Conexiones
- Relación con el VPN en [[Finanzas para Ingenieros - Valor del Dinero en el Tiempo, VPN y VAN]].
- Evaluación de proyectos tecnológicos en [[Gerencia de Proyectos]] y [[Formación de Emprendedores]].

## Fuente
Basado en la ruta de aprendizaje de [[Finanzas para Ingenieros]] y `Material/Tema 1/Guía didáctica Finanzas_ingenieros_V20251.pdf`, `EJERCICIOS1.pdf` y `eJERCICIOS.pdf`.
