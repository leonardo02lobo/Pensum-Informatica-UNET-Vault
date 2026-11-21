---
tags: [clase, electiva]
materia: Redes Neuronales y Lógica Difusa
fuente: "conocimiento general"
---
# RNLD 05 - Conjuntos difusos y funciones de pertenencia

Materia: [[Redes Neuronales y Lógica Difusa]]
Anterior: [[RNLD 04 - Redes RBF, Kohonen y Hopfield]]
Siguiente: [[RNLD 06 - Inferencia difusa y control]]

## Contexto y objetivo
En la lógica clásica un elemento pertenece o no a un conjunto. Conceptos como "temperatura alta", "persona joven" o "velocidad media" no tienen frontera nítida. Zadeh (1965) propuso los conjuntos difusos, donde la pertenencia es un grado en $[0,1]$. Objetivo: definir conjuntos difusos, construir funciones de pertenencia y operar con ellos.

## Definiciones
Dado un universo $X$, un **conjunto difuso** $A$ se define por su función de pertenencia $\mu_A:X\to[0,1]$. Un conjunto clásico es el caso en que $\mu_A\in\{0,1\}$.

Elementos asociados:
- **Soporte:** $\{x:\mu_A(x)>0\}$. **Núcleo:** $\{x:\mu_A(x)=1\}$.
- **Altura:** $\sup_x\mu_A(x)$; el conjunto es **normal** si la altura es 1.
- **Corte $\alpha$:** $A_\alpha=\{x:\mu_A(x)\ge\alpha\}$ (un conjunto clásico).
- **Variable lingüística:** variable cuyos valores son términos (bajo, medio, alto), cada uno modelado por un conjunto difuso.

## Funciones de pertenencia típicas
- Triangular $(a,b,c)$: $\mu(x)=\max\!\big(\min\!\big(\frac{x-a}{b-a},\frac{c-x}{c-b}\big),0\big)$.
- Trapezoidal $(a,b,c,d)$: $\mu(x)=\max\!\big(\min\!\big(\frac{x-a}{b-a},1,\frac{d-x}{d-c}\big),0\big)$.
- Gaussiana: $\mu(x)=\exp\!\big(-\frac{(x-m)^2}{2\sigma^2}\big)$.
- Sigmoidal y campana generalizada $\frac{1}{1+|\frac{x-c}{a}|^{2b}}$.

La forma se elige por simplicidad (triangular/trapezoidal) o suavidad (gaussiana). Suele bastar con 3 a 7 términos por variable, cubriendo el universo con solape.

## Operaciones
Operadores de Zadeh (los más usados):
- Unión: $\mu_{A\cup B}=\max(\mu_A,\mu_B)$.
- Intersección: $\mu_{A\cap B}=\min(\mu_A,\mu_B)$.
- Complemento: $\mu_{\bar A}=1-\mu_A$.

Generalización con **t-normas** (AND) y **t-conormas** o s-normas (OR):

| | T-norma | T-conorma |
|---|---|---|
| Zadeh | $\min(a,b)$ | $\max(a,b)$ |
| Probabilística | $a\cdot b$ | $a+b-ab$ |
| Łukasiewicz | $\max(0,a+b-1)$ | $\min(1,a+b)$ |

Una t-norma $T$ es conmutativa, asociativa, monótona y con elemento neutro 1. La t-conorma se obtiene por dualidad: $S(a,b)=1-T(1-a,1-b)$ (leyes de De Morgan).

Propiedad distintiva: en general $A\cap\bar A\ne\emptyset$ y $A\cup\bar A\ne X$ (se violan el tercero excluido y la no contradicción).

**Relaciones y composición:** una relación difusa $R\subseteq X\times Y$ tiene $\mu_R(x,y)$; la composición max-min es $\mu_{R\circ S}(x,z)=\max_y\min(\mu_R(x,y),\mu_S(y,z))$.

## Ejemplo resuelto
Universo: temperatura $x\in[0,40]$ °C. "Fría" = triangular(0,0,20) (hombro izquierdo); "Cálida" = triangular(10,20,30). Para $x=15$:

1. $\mu_{Fría}(15)=\frac{20-15}{20-0}=0{,}25$.
2. $\mu_{Cálida}(15)=\frac{15-10}{20-10}=0{,}50$.
3. Fría Y Cálida (mínimo): $\min(0{,}25;0{,}5)=0{,}25$. Con producto: $0{,}125$.
4. Fría O Cálida (máximo): $0{,}5$. Con suma probabilística: $0{,}25+0{,}5-0{,}125=0{,}625$.
5. NO Fría: $1-0{,}25=0{,}75$.
6. Corte $\alpha=0{,}5$ de Cálida: los $x$ con $\mu\ge0{,}5$ son $[15,25]$.

## Código
```python
import numpy as np
import matplotlib.pyplot as plt

def tri(x, a, b, c):
    # función triangular; maneja hombros si a==b o b==c
    izq = np.where(b > a, (x - a) / (b - a + 1e-12), 1.0)
    der = np.where(c > b, (c - x) / (c - b + 1e-12), 1.0)
    return np.clip(np.minimum(izq, der), 0, 1)

x = np.linspace(0, 40, 401)
fria   = tri(x, 0, 0, 20)
calida = tri(x, 10, 20, 30)

inter = np.minimum(fria, calida)       # t-norma min
union = np.maximum(fria, calida)       # t-conorma max
i15 = np.argmin(abs(x - 15))
print(fria[i15], calida[i15], inter[i15], union[i15])

plt.plot(x, fria, label="fría"); plt.plot(x, calida, label="cálida")
plt.plot(x, inter, "--", label="intersección"); plt.legend(); plt.show()

# Con scikit-fuzzy (pip install scikit-fuzzy):
# import skfuzzy as fuzz; fuzz.trimf(x, [10, 20, 30])
```

## Errores comunes
- Confundir pertenencia con probabilidad: $\mu=0{,}7$ expresa grado de verdad, no frecuencia de ocurrencia; las pertenencias no suman 1 necesariamente.
- Usar funciones de pertenencia sin solape (el sistema queda sin respuesta entre términos).
- Mezclar t-normas y t-conormas que no son duales.
- Olvidar que el universo de discurso debe cubrirse completamente.

## Ejercicios propuestos
1. Con $\mu_A(x)=0{,}6$ y $\mu_B(x)=0{,}3$, calcula unión e intersección de Zadeh. *Respuesta: 0,6 y 0,3.*
2. Evalúa la triangular $(2,5,8)$ en $x=6$. *Respuesta: $(8-6)/(8-5)=0{,}667$.*
3. Calcula $A\cap\bar A$ en $\mu_A=0{,}5$. *Respuesta: $\min(0{,}5;0{,}5)=0{,}5\neq0$.*

## Conexiones
- Lógica clásica y proposicional, base que se generaliza: [[Matemática Discreta]], [[IIA 05 - Lógica proposicional, primer orden y Prolog]].
- Contraste con probabilidad: [[Estadística I]], [[IIA 06 - Razonamiento con incertidumbre y redes bayesianas]].

## Fuente
Conocimiento general (Zadeh, "Fuzzy Sets", 1965; Jang, Sun y Mizutani, *Neuro-Fuzzy and Soft Computing*). Verificar el temario con el programa oficial.
