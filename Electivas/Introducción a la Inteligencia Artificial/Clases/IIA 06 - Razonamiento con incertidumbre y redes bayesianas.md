---
tags: [clase, electiva]
materia: Introducción a la Inteligencia Artificial
fuente: "conocimiento general"
---
# IIA 06 - Razonamiento con incertidumbre y redes bayesianas

Materia: [[Introducción a la Inteligencia Artificial]]
Anterior: [[IIA 05 - Lógica proposicional, primer orden y Prolog]]
Siguiente: [[IIA 07 - Aprendizaje, PLN, visión y ética]]

## Contexto y objetivo
Los agentes rara vez tienen información completa y exacta: sensores ruidosos, entornos parcialmente observables, efectos estocásticos. La lógica pura no basta (no puede decir "probablemente"). La teoría de la probabilidad es el marco estándar. Objetivo: calcular con probabilidad condicional y Bayes, construir redes bayesianas y hacer inferencia por enumeración.

## Fundamentos de probabilidad
- Axiomas: $0\le P(a)\le1$, $P(\text{cierto})=1$, $P(a\vee b)=P(a)+P(b)-P(a\wedge b)$.
- Condicional: $P(a\mid b)=\frac{P(a\wedge b)}{P(b)}$. Regla del producto: $P(a\wedge b)=P(a\mid b)P(b)$.
- **Marginalización:** $P(X)=\sum_yP(X,y)$.
- **Independencia:** $P(a\mid b)=P(a)$; **independencia condicional:** $P(a\mid b,c)=P(a\mid c)$.
- **Teorema de Bayes:**
$$P(h\mid e)=\frac{P(e\mid h)P(h)}{P(e)}$$
con $P(e)=\sum_hP(e\mid h)P(h)$. Permite pasar de causa a efecto (fácil de estimar) a diagnóstico.
- Agente racional bajo incertidumbre: elige la acción de **máxima utilidad esperada**, $EU(a)=\sum_sP(s\mid a)U(s)$.

## Redes bayesianas
Grafo dirigido acíclico: un nodo por variable aleatoria, aristas de padres a hijos y, por nodo, una tabla de probabilidad condicional $P(X_i\mid\text{Padres}(X_i))$. Representa de forma compacta la conjunta:

$$P(x_1,\dots,x_n)=\prod_{i=1}^{n}P(x_i\mid\text{padres}(x_i)).$$

Con $n$ variables booleanas la conjunta tiene $2^n-1$ parámetros; la red con a lo sumo $k$ padres por nodo solo $n\,2^k$. Estructuras típicas: cadena (A→B→C), divergente o causa común (B←A→C: B y C independientes dado A) y convergente o colisionador (A→C←B: A y B independientes, pero dependientes dado C, el efecto "explaining away").

**Inferencia:**
- Exacta por enumeración: sumar sobre variables ocultas. Consulta $P(X\mid e)=\alpha\sum_yP(X,e,y)$. Eliminación de variables ahorra cálculo; es NP-difícil en general.
- Aproximada: muestreo (rechazo, ponderación por verosimilitud, MCMC/Gibbs).
- **Aprendizaje:** parámetros por máxima verosimilitud (conteos, suavizado de Laplace) o bayesianos; estructura por búsqueda y puntuación. Naive Bayes es una red con un padre (clase) y muchos hijos ([[AA 04 - SVM, k-NN y Naive Bayes]]). Modelos temporales: HMM y filtros de Kalman.

## Ejemplo resuelto 1: Bayes (prueba médica)
Prevalencia $P(E)=0{,}01$; sensibilidad $P(+\mid E)=0{,}95$; falsos positivos $P(+\mid\neg E)=0{,}05$.
1. $P(+)=0{,}95\cdot0{,}01+0{,}05\cdot0{,}99=0{,}0095+0{,}0495=0{,}059$.
2. $P(E\mid+)=\frac{0{,}0095}{0{,}059}=0{,}161$.
Solo 16 % pese a una prueba "de 95 %": la prevalencia baja domina (falacia de la tasa base).

## Ejemplo resuelto 2: red clásica de la alarma
Variables: Robo (R), Terremoto (T), Alarma (A), Juan llama (J). $P(R)=0{,}001$, $P(T)=0{,}002$; $P(A\mid R,T)$: (V,V) 0,95; (V,F) 0,94; (F,V) 0,29; (F,F) 0,001; $P(J\mid A)=0{,}90$, $P(J\mid\neg A)=0{,}05$. Calcular $P(J\wedge A\wedge R\wedge\neg T)$ y $P(A)$.
1. Conjunta: $P(R)P(\neg T)P(A\mid R,\neg T)P(J\mid A)=0{,}001\cdot0{,}998\cdot0{,}94\cdot0{,}90=8{,}44\times10^{-4}$.
2. $P(A)=\sum_{r,t}P(r)P(t)P(A\mid r,t)$:
 - (V,V): $0{,}001\cdot0{,}002\cdot0{,}95=1{,}9\times10^{-6}$.
 - (V,F): $0{,}001\cdot0{,}998\cdot0{,}94=9{,}38\times10^{-4}$.
 - (F,V): $0{,}999\cdot0{,}002\cdot0{,}29=5{,}79\times10^{-4}$.
 - (F,F): $0{,}999\cdot0{,}998\cdot0{,}001=9{,}97\times10^{-4}$.
 - Suma $\approx2{,}52\times10^{-3}$.

## Código
```python
from itertools import product

P_R, P_T = 0.001, 0.002
P_A = {(True, True): 0.95, (True, False): 0.94,
       (False, True): 0.29, (False, False): 0.001}
P_J = {True: 0.90, False: 0.05}

def conjunta(r, t, a, j):
    p = (P_R if r else 1 - P_R) * (P_T if t else 1 - P_T)
    p *= P_A[(r, t)] if a else 1 - P_A[(r, t)]
    p *= P_J[a] if j else 1 - P_J[a]
    return p

# inferencia por enumeración: P(Robo | Juan llama)
num = sum(conjunta(True, t, a, True) for t, a in product([True, False], repeat=2))
den = sum(conjunta(r, t, a, True) for r, t, a in product([True, False], repeat=3))
print("P(Robo | J) =", round(num / den, 4))      # ~0.0163

# Bayes con la prueba médica
prev, sens, fp = 0.01, 0.95, 0.05
print("P(E|+) =", round(sens * prev / (sens * prev + fp * (1 - prev)), 3))

# con pgmpy (pip install pgmpy) se arman redes y se consulta con VariableElimination
```

## Errores comunes
- Confundir $P(A\mid B)$ con $P(B\mid A)$ (falacia del fiscal).
- Ignorar la tasa base (prevalencia).
- Multiplicar probabilidades como si hubiera independencia sin justificarlo.
- Añadir aristas que crean ciclos; la red debe ser un DAG.
- Olvidar normalizar ($\alpha$) en la inferencia.

## Ejercicios propuestos
1. Con prevalencia 5 %, sensibilidad 90 % y falsos positivos 10 %, ¿cuánto vale $P(E\mid+)$? *Respuesta: $0{,}045/(0{,}045+0{,}095)=0{,}321$.*
2. ¿Cuántos parámetros necesita una tabla conjunta de 10 variables booleanas? *Respuesta: $2^{10}-1=1023$.*
3. En A→C←B, ¿son A y B independientes dado C? *Respuesta: no; observar el efecto C las hace dependientes.*

## Conexiones
- Probabilidad, Bayes y distribuciones: [[Estadística I]] y [[Estadística II]].
- Teoría de decisión y utilidad: [[Investigación de Operaciones II]].
- Alternativa al tratamiento probabilístico de lo vago: [[RNLD 05 - Conjuntos difusos y funciones de pertenencia]].

## Fuente
Conocimiento general (Russell y Norvig, caps. 12-14; Pearl 1988). Verificar el temario con el programa oficial.
