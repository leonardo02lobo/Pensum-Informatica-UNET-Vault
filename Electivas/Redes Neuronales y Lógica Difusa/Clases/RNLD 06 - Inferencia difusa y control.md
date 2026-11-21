---
tags: [clase, electiva]
materia: Redes Neuronales y Lógica Difusa
fuente: "conocimiento general"
---
# RNLD 06 - Inferencia difusa y control

Materia: [[Redes Neuronales y Lógica Difusa]]
Anterior: [[RNLD 05 - Conjuntos difusos y funciones de pertenencia]]
Siguiente: [[RNLD 07 - Sistemas neuro-difusos y algoritmos genéticos]]

## Contexto y objetivo
Un sistema de inferencia difusa (FIS) traduce conocimiento experto expresado en reglas lingüísticas a una función entrada-salida numérica. Es la base de los controladores difusos (lavadoras, aire acondicionado, frenos ABS, metro de Sendai). Objetivo: construir un FIS Mamdani y uno Sugeno, calcular una salida paso a paso y diseñar un controlador.

## Estructura de un FIS
1. **Fuzzificación:** convertir entradas nítidas en grados de pertenencia.
2. **Base de reglas:** `SI x es A Y y es B ENTONCES z es C`.
3. **Inferencia:** evaluar antecedentes y combinar consecuentes.
4. **Defuzzificación:** convertir el conjunto de salida en un número.

## Inferencia de Mamdani
- **Antecedente:** fuerza de disparo $\alpha_k=\min(\mu_{A_k}(x),\mu_{B_k}(y))$ (AND = mínimo).
- **Implicación:** recortar el consecuente $C_k$ al nivel $\alpha_k$: $\mu'_{C_k}(z)=\min(\alpha_k,\mu_{C_k}(z))$.
- **Agregación:** unir las salidas de todas las reglas con máximo: $\mu_C(z)=\max_k\mu'_{C_k}(z)$.
- **Defuzzificación (centroide):** $z^*=\dfrac{\int z\,\mu_C(z)\,dz}{\int\mu_C(z)\,dz}$.

Otros métodos: bisectriz, media de máximos, menor/mayor de los máximos.

## Inferencia de Takagi-Sugeno-Kang (Sugeno)
Consecuentes funcionales: `SI x es A Y y es B ENTONCES z = f(x,y)`. Orden cero: $z$ constante; orden uno: $z=px+qy+r$. Salida por promedio ponderado:

$$z^*=\frac{\sum_k\alpha_k z_k}{\sum_k\alpha_k}$$

No requiere defuzzificación costosa, es eficiente y se presta a optimización (base de ANFIS, ver siguiente clase).

## Controlador difuso
Esquema típico: error $e=r-y$ y cambio de error $\Delta e$ como entradas; incremento de la acción de control como salida. Se usan términos como NG, NP, Z, PP, PG (negativo grande... positivo grande) y una tabla de reglas de 5x5. Ventajas: no exige modelo matemático de la planta, tolera no linealidades. Desventajas: ajuste manual, sin garantías formales de estabilidad generales.

## Ejemplo resuelto (propina, Mamdani)
Entradas: servicio $s\in[0,10]$ y comida $c\in[0,10]$; salida propina $p\in[0,25]\%$. Reglas:
- R1: SI servicio es pobre O comida es mala ENTONCES propina baja.
- R2: SI servicio es bueno ENTONCES propina media.
- R3: SI servicio es excelente O comida es excelente ENTONCES propina alta.

Para $s=7$, $c=3$ supón: $\mu_{pobre}(7)=0$, $\mu_{mala}(3)=0{,}4$, $\mu_{bueno}(7)=0{,}6$, $\mu_{exc}(7)=0$, $\mu_{exc}(3)=0$.

1. R1 (OR = máximo): $\alpha_1=\max(0;0{,}4)=0{,}4$.
2. R2: $\alpha_2=0{,}6$.
3. R3: $\alpha_3=\max(0;0)=0$ (no se dispara).
4. Se recortan "baja" a 0,4 y "media" a 0,6, y se agregan con máximo.
5. Si, por simplicidad, representamos cada término por su centro (baja=5, media=13, alta=20) y calculamos aproximación de centroides por alturas: $p^*\approx\frac{0{,}4\cdot5+0{,}6\cdot13}{0{,}4+0{,}6}=9{,}8\%$. (El centroide continuo daría un valor cercano; el método de alturas equivale a un Sugeno de orden cero.)

Con Sugeno de orden cero y las mismas reglas: $p^*=\frac{0{,}4\cdot5+0{,}6\cdot13+0\cdot20}{1}=9{,}8\%$.

## Código
```python
import numpy as np

def tri(x, a, b, c):
    return np.maximum(np.minimum((x-a)/(b-a+1e-12), (c-x)/(c-b+1e-12)), 0)

z = np.linspace(0, 25, 501)                       # universo de la salida
baja, media, alta = tri(z,0,5,10), tri(z,5,13,21), tri(z,15,20,25)

def propina(servicio, comida):
    # fuzzificación (conjuntos de entrada triangulares)
    pobre = tri(servicio, -1, 0, 5); bueno = tri(servicio, 0, 5, 10)
    exc_s = tri(servicio, 5, 10, 11); mala = tri(comida, -1, 0, 5)
    exc_c = tri(comida, 5, 10, 11)
    # fuerza de disparo
    a1 = max(pobre, mala); a2 = bueno; a3 = max(exc_s, exc_c)
    # implicación (recorte) y agregación (máximo)
    agg = np.maximum.reduce([np.minimum(a1, baja),
                             np.minimum(a2, media),
                             np.minimum(a3, alta)])
    if agg.sum() == 0: return 0.0
    return (z * agg).sum() / agg.sum()            # centroide discreto

print(propina(7, 3), propina(10, 10), propina(0, 0))
```

Con `scikit-fuzzy`: `skfuzzy.control` ofrece `Antecedent`, `Consequent`, `Rule` y `ControlSystemSimulation`.

## Errores comunes
- Reglas incompletas: algún par de entradas no activa ninguna regla y la agregación queda en cero.
- Defuzzificar con centroide cuando el conjunto agregado es vacío.
- Demasiadas reglas (explosión combinatoria: $n^{\text{variables}}$).
- Confundir Mamdani (consecuentes difusos) con Sugeno (consecuentes funcionales).

## Ejercicios propuestos
1. Con dos reglas de Sugeno orden cero, $\alpha=(0{,}3;0{,}7)$ y salidas $(10,20)$, calcula $z^*$. *Respuesta: $(3+14)/1=17$.*
2. ¿Cuántas reglas tiene la base completa de 3 entradas con 5 términos cada una? *Respuesta: $5^3=125$.*
3. ¿Qué ventaja tiene Sugeno frente a Mamdani en optimización? *Respuesta: salida analítica y diferenciable, sin integración.*

## Conexiones
- Control y realimentación: [[Automatización]].
- Optimización de parámetros: [[Investigación de Operaciones II]].
- Programación de sistemas basados en reglas: [[IIA 05 - Lógica proposicional, primer orden y Prolog]].

## Fuente
Conocimiento general (Mamdani y Assilian 1975; Takagi y Sugeno 1985; Jang et al.). Verificar el temario con el programa oficial.
