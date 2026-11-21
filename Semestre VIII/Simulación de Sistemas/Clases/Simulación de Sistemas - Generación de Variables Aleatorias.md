---
tags: [clase, semestre-VIII]
materia: Simulación de Sistemas
---
# Simulación de Sistemas - Generación de Variables Aleatorias

Materia: [[Simulación de Sistemas]]
Anterior: [[Simulación de Sistemas - Generación de Números Pseudoaleatorios y Pruebas Estadísticas]]
Siguiente: [[Simulación de Sistemas - Simulación de Eventos Discretos y Lista de Eventos Futuros]]

## Contexto y objetivo
Transformar números pseudoaleatorios uniformes $U \sim U(0,1)$ en realizaciones de **variables aleatorias** continuas y discretas (Exponencial, Uniforme, Normal, Weibull, Poisson, Binomial) mediante los métodos de **transformada inversa**, **aceptación-rechazo**, **convolución** y **composición**.

## 1. Método de la Transformada Inversa
Si una variable aleatoria continua $X$ tiene función de distribución acumulada $F(x)$ estrictamente creciente, entonces $U = F(X) \sim U(0,1)$, por lo que:
$$X = F^{-1}(U)$$

### Distribuciones clave por transformada inversa
1. **Uniforme continua $U(a, b)$**:
   $$X = a + (b - a)\,U$$
2. **Exponencial $\text{Exp}(\lambda)$** (tiempos entre llegadas de un proceso de Poisson):
   $$F(x) = 1 - e^{-\lambda x} = U \implies X = -\frac{1}{\lambda}\ln(1 - U)$$
   (Como $1-U$ también es $U(0,1)$, suele simplificarse a $-\frac{1}{\lambda}\ln(U)$ cuidando $U > 0$).
3. **Weibull($\alpha, \beta$)** (tiempos de falla y confiabilidad):
   $$X = \beta\big(-\ln(1 - U)\big)^{1/\alpha}$$

### Caso discreto (búsqueda por intervalos)
Dada una función de masa de probabilidad $p(x_i) = P(X = x_i)$ y su acumulada $F(x_i) = \sum_{j \le i} p(x_j)$, se genera $U \sim U(0,1)$ y se devuelve el primer $x_i$ tal que $U \le F(x_i)$.

### Ejemplo resuelto
Con $U = 0{,}375$, genere un tiempo de servicio exponencial con tasa $\lambda = 2\text{ clientes/min}$:
$$X = -\frac{1}{2}\ln(1 - 0{,}375) = -0{,}5\ln(0{,}625) \approx -0{,}5(-0{,}4700) = 0{,}235\text{ min}$$

## 2. Método de Convolución
Se aplica cuando la variable objetivo $Y$ puede expresarse como la suma de $k$ variables aleatorias independientes más simples: $Y = X_1 + X_2 + \dots + X_k$.
- **Erlang-$k$**: suma de $k$ exponenciales independientes con tasa $\lambda$:
  $$Y = -\frac{1}{\lambda}\sum_{i=1}^{k}\ln(U_i) = -\frac{1}{\lambda}\ln\left(\prod_{i=1}^{k} U_i\right)$$
- **Binomial($n, p$)**: suma de $n$ ensayos de Bernoulli($p$) independientes (contar cuántos $U_i \le p$).

## 3. Método de Aceptación y Rechazo
Cuando $F^{-1}(U)$ no tiene forma cerrada, se envuelve la densidad objetivo $f(x)$ con una función mayorante $c\,g(x) \ge f(x)$ para todo $x$, donde sabemos muestrear $g(x)$ y $c \ge 1$:
1. Generar $Y \sim g(y)$ y $U \sim U(0,1)$ independiente.
2. Si $U \le \dfrac{f(Y)}{c\,g(Y)}$, **aceptar** $X = Y$; de lo contrario, **rechazar** y volver al paso 1.
La eficiencia del método es $1/c$ (probabilidad de aceptación en cada intento).

## 4. Generación de la Distribución Normal: Box-Muller
Como la Normal estándar $N(0,1)$ no tiene $F^{-1}$ cerrada, se utiliza la transformación exacta de **Box-Muller** a partir de dos uniformes independientes $U_1, U_2 \sim U(0,1)$:
$$Z_1 = \sqrt{-2\ln(U_1)}\cos(2\pi U_2), \qquad Z_2 = \sqrt{-2\ln(U_1)}\sin(2\pi U_2)$$
Luego, para obtener $X \sim N(\mu, \sigma^2)$: $X = \mu + \sigma Z$.

```python
import math, random

def normal_box_muller(mu=0.0, sigma=1.0):
    u1 = max(random.random(), 1e-12)  # evita ln(0)
    u2 = random.random()
    z = math.sqrt(-2.0 * math.log(u1)) * math.cos(2.0 * math.pi * u2)
    return mu + sigma * z
```

## 5. Distribución de Poisson($\lambda$)
Aprovechando que el número de llegadas en una unidad de tiempo sigue $\text{Poisson}(\lambda)$ si los tiempos entre llegadas son $\text{Exp}(\lambda)$, se multiplican uniformes $U_i$ hasta que el producto caiga por debajo de $e^{-\lambda}$:
1. Inicializar $n = 0$, $P = 1$.
2. Generar $U \sim U(0,1)$ y hacer $P = P \cdot U$.
3. Si $P < e^{-\lambda}$, retornar $n$; si no, incrementar $n = n + 1$ y repetir el paso 2.

## Errores comunes
- Confundir la tasa $\lambda$ (clientes por unidad de tiempo) con la media $\mu = 1/\lambda$ en la distribución exponencial (en `random.expovariate(lambd)` de Python se pasa la tasa $\lambda$, mientras que en `numpy.random.Generator.exponential(scale)` se pasa la media $\beta = 1/\lambda$).
- Permitir $U = 0$ dentro de $\ln(U)$ sin protección numérica.
- Usar el método de aceptación-rechazo con una cota $c\,g(x)$ que no cubre por completo a $f(x)$ en algún tramo del dominio.

## Ejercicios propuestos
1. Escriba la fórmula de transformada inversa para generar una variable discreta con $P(X=1)=0{,}2$, $P(X=2)=0{,}5$, $P(X=3)=0{,}3$, y evalúela para $U = 0{,}65$.
   - *Respuesta*: acumulada $F(1)=0{,}2$, $F(2)=0{,}7$, $F(3)=1{,}0$. Como $0{,}2 < 0{,}65 \le 0{,}7$, se devuelve $X = 2$.
2. Con $U_1 = 0{,}1353$ y $U_2 = 0{,}25$, calcule $Z_1$ con Box-Muller.
   - *Respuesta*: $\sqrt{-2\ln(0{,}1353)} \approx \sqrt{4{,}00} = 2{,}0$; $\cos(2\pi \cdot 0{,}25) = \cos(\pi/2) = 0 \implies Z_1 = 0$.

## Conexiones
- Funciones de densidad, acumuladas y distribuciones en [[Estadística I]] y [[Estadística II]].
- Base para programar llegadas y servicios en [[Simulación de Sistemas - Simulación de Eventos Discretos y Lista de Eventos Futuros]].

## Fuente
Basado en [[Simulación de Sistemas]] (Law & Kelton, *Simulation Modeling and Analysis*; Banks et al., *Discrete-Event System Simulation*).
