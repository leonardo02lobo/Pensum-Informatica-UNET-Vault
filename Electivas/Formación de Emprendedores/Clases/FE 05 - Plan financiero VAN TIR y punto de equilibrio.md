---
tags: [clase, electiva]
materia: Formación de Emprendedores
fuente: "conocimiento general"
---
# FE 05 - Plan financiero VAN TIR y punto de equilibrio

Materia: [[Formación de Emprendedores]]
Anterior: [[FE 04 - Plan de negocios y aspectos legales]]
Siguiente: [[FE 06 - Financiamiento y presentación pitch]]

## Contexto y objetivo
El plan financiero traduce el plan de negocios a cifras: inversión inicial, costos, ingresos, flujo de caja y criterios de decisión. El objetivo es calcular el punto de equilibrio, construir un flujo de caja proyectado y evaluar el proyecto con VAN, TIR y período de recuperación. Los fundamentos están en [[Ingeniería Económica]] y [[Finanzas para Ingenieros]].

## Teoría

### Inversión y costos
- **Inversión inicial**: activos fijos, intangibles (desarrollo, registro), capital de trabajo.
- **Costos fijos** (CF): no varían con el volumen (alquiler, salarios base).
- **Costos variables** (CV): proporcionales a las unidades (comisiones, nube por usuario).
- **Margen de contribución unitario**: $mc = P - cv$.

### Punto de equilibrio
Unidades: $Q^* = \dfrac{CF}{P - cv}$. En ventas monetarias: $V^* = \dfrac{CF}{1 - cv/P}$. Margen de seguridad: $\dfrac{Q - Q^*}{Q}$.

### Flujo de caja
$FC_t = \text{Ingresos}_t - \text{Egresos}_t - \text{Impuestos}_t - \text{Inversiones}_t$. El flujo en $t=0$ suele ser negativo (inversión).

### Criterios de evaluación
- **VAN** (valor actual neto) con tasa de descuento $i$ (costo de oportunidad o TMAR):
$$VAN=\sum_{t=0}^{n}\frac{FC_t}{(1+i)^t}$$
Se acepta si $VAN>0$.
- **TIR**: la tasa $r$ tal que $VAN(r)=0$. Se acepta si $r>i$.
- **Período de recuperación (payback)**: tiempo en que el flujo acumulado se hace cero; el **descontado** usa flujos actualizados.
- **Índice de rentabilidad**: $IR = 1 + \dfrac{VAN}{I_0}$.
- Limitaciones: la TIR puede ser múltiple si el flujo cambia de signo varias veces; el VAN depende de $i$.

## Ejemplo resuelto 1: punto de equilibrio
Servicio con CF mensuales de 6 000 USD, precio 25 USD y costo variable 10 USD.
$$Q^*=\frac{6000}{25-10}=400 \text{ unidades/mes}, \qquad V^* = 400\times 25 = 10\,000 \text{ USD}$$
Si se venden 500 unidades: utilidad $= 500\times15 - 6000 = 1\,500$ USD; margen de seguridad $=\dfrac{500-400}{500}=20\,\%$.

## Ejemplo resuelto 2: VAN, TIR y payback
Inversión inicial 50 000 USD. Flujos netos anuales: 12 000, 15 000, 18 000, 20 000 y 22 000. Tasa de descuento $i=12\,\%$.

| Año | Flujo | Factor $1/1{,}12^t$ | Valor actual | Acumulado simple |
|---|---|---|---|---|
| 0 | -50 000 | 1,0000 | -50 000,0 | -50 000 |
| 1 | 12 000 | 0,8929 | 10 714,3 | -38 000 |
| 2 | 15 000 | 0,7972 | 11 957,9 | -23 000 |
| 3 | 18 000 | 0,7118 | 12 812,0 | -5 000 |
| 4 | 20 000 | 0,6355 | 12 710,4 | 15 000 |
| 5 | 22 000 | 0,5674 | 12 483,4 | 37 000 |

- $VAN = -50\,000 + 10\,714{,}3 + 11\,957{,}9 + 12\,812{,}0 + 12\,710{,}4 + 12\,483{,}4 \approx 10\,678$ USD $>0$: se acepta.
- **TIR** (por tanteo/interpolación): a 19 % y 20 % el VAN cambia de signo; el valor exacto es $\approx 19{,}44\,\%$, mayor que 12 %: se acepta.
- **Payback simple**: el acumulado pasa de -5 000 (año 3) a +15 000 (año 4): $3+\dfrac{5000}{20000}=3{,}25$ años.
- **Payback descontado**: acumulado actualizado al año 4: -1 805; el año 5 aporta 12 483: $4+\dfrac{1805}{12483}\approx 4{,}14$ años.
- $IR = 1 + 10\,678/50\,000 = 1{,}21$.

### Cálculo con Python (verificación)
```python
def van(i, flujos):
    return sum(f / (1 + i) ** t for t, f in enumerate(flujos))

def tir(flujos, lo=0.0, hi=1.0):
    for _ in range(100):
        mid = (lo + hi) / 2
        if van(mid, flujos) > 0:
            lo = mid
        else:
            hi = mid
    return mid

f = [-50000, 12000, 15000, 18000, 20000, 22000]
print(round(van(0.12, f), 1), round(tir(f) * 100, 2))
```
Resultado esperado: 10677.99 y 19.44. En una hoja de cálculo: `=VNA(12%; B2:B6)+B1` y `=TIR(B1:B6)`.

### Análisis de sensibilidad
Con los flujos reducidos en 20 %: los flujos serían 9 600, 12 000, 14 400, 16 000, 17 600; el VAN a 12 % cae a $\approx -50\,000+0{,}8\times 60\,678 = -1\,458$, es decir, el proyecto pasa a ser inviable. Conclusión: es sensible a las ventas y conviene reducir la inversión o aumentar el margen. (Cálculo: la suma de valores actuales de los flujos es $60\,678$.)

## Errores comunes
- Usar utilidades contables en lugar de flujos de caja (ignorar depreciación como no efectivo, capital de trabajo e inversión).
- Mezclar flujos en moneda corriente con tasas reales (en economías con inflación alta, trabajar en USD o en términos reales de forma consistente).
- Elegir la tasa de descuento sin justificar.
- Aceptar solo por la TIR sin ver el VAN en proyectos mutuamente excluyentes.
- Olvidar el valor residual o el capital de trabajo.

## Ejercicios propuestos
1. CF = 9 000, P = 40, cv = 22: calcule el punto de equilibrio. *Respuesta: 500 unidades.*
2. Inversión 10 000; flujos 4 000, 5 000, 6 000; $i=10\,\%$. Calcule el VAN. *Respuesta: $3636{,}4+4132{,}2+4508{,}2-10000 \approx 2\,277$ USD.*
3. Con los flujos del ejercicio 2, ¿cuál es el payback simple? *Respuesta: 2 años y $\tfrac{1000}{6000}\approx$ 0,17: 2,17 años.*

## Conexiones con otras materias
[[Ingeniería Económica]], [[Finanzas para Ingenieros]], [[Economía]], [[Gerencia de Proyectos]], [[GT 06 - Evaluación de proyectos tecnológicos, incubadoras y políticas CyT]].

## Fuente
Conocimiento general; fórmulas estándar de evaluación de proyectos. Cifras ilustrativas calculadas en esta nota.
