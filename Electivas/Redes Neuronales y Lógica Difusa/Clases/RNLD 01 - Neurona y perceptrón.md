---
tags: [clase, electiva]
materia: Redes Neuronales y Lógica Difusa
fuente: "conocimiento general"
---
# RNLD 01 - Neurona y perceptrón

Materia: [[Redes Neuronales y Lógica Difusa]]
Anterior: (inicio de la serie)
Siguiente: [[RNLD 02 - Perceptrón multicapa y retropropagación]]

## Contexto y objetivo
Las redes neuronales artificiales (RNA) nacen de un modelo muy simplificado de la neurona biológica. Esta clase establece el bloque básico, la neurona artificial, y el primer algoritmo de aprendizaje, la regla del perceptrón. Al final debes poder: calcular la salida de una neurona, entrenar un perceptrón a mano y entender por qué un solo perceptrón no resuelve XOR.

## Neurona biológica y artificial
Una neurona biológica recibe señales por las dendritas, las integra en el soma y, si el potencial supera un umbral, dispara un impulso por el axón. La sinapsis modula la fuerza de cada conexión. El modelo de McCulloch y Pitts (1943) abstrae esto como:

$$y = f\Big(\sum_{i=1}^{n} w_i x_i + b\Big) = f(\mathbf{w}^T\mathbf{x} + b)$$

- $x_i$: entradas; $w_i$: pesos sinápticos; $b$: sesgo (equivale a un umbral $-b$).
- $f$: función de activación. Para el perceptrón clásico es el escalón (Heaviside): $f(z)=1$ si $z\ge 0$, $0$ en caso contrario.

Geométricamente, $\mathbf{w}^T\mathbf{x}+b=0$ es un hiperplano que separa el espacio en dos semiespacios: el perceptrón es un clasificador lineal.

## Regla de aprendizaje del perceptrón (Rosenblatt, 1958)
Con tasa de aprendizaje $\eta>0$, para cada patrón $(\mathbf{x},t)$ con salida $y$:

$$\mathbf{w} \leftarrow \mathbf{w} + \eta\,(t-y)\,\mathbf{x}, \qquad b \leftarrow b + \eta\,(t-y)$$

Si la salida es correcta, $t-y=0$ y no cambia nada. Si es incorrecta, el hiperplano se desplaza hacia el patrón mal clasificado.

**Teorema de convergencia:** si los datos son linealmente separables, el algoritmo converge en un número finito de pasos. Si no lo son (caso XOR), oscila indefinidamente.

### Variantes
- **Adaline / regla delta (Widrow-Hoff):** minimiza el error cuadrático de la salida lineal antes del umbral, $E=\tfrac12 (t-z)^2$, con $\Delta \mathbf{w} = \eta (t-z)\mathbf{x}$. Es descenso de gradiente y prepara el terreno para la retropropagación.

## Ejemplo resuelto: compuerta AND
Datos: $(0,0)\to0,\ (0,1)\to0,\ (1,0)\to0,\ (1,1)\to1$. Inicio $\mathbf{w}=(0,0)$, $b=0$, $\eta=1$.

1. $(0,0)$: $z=0\Rightarrow y=1$, $t=0$. Error $=-1$. $\mathbf{w}=(0,0)$, $b=-1$.
2. $(0,1)$: $z=-1\Rightarrow y=0$. Correcto.
3. $(1,0)$: $z=-1\Rightarrow y=0$. Correcto.
4. $(1,1)$: $z=-1\Rightarrow y=0$, $t=1$. Error $=+1$. $\mathbf{w}=(1,1)$, $b=0$.
5. Época 2: $(0,0)$: $z=0\Rightarrow y=1$, error $-1$ $\Rightarrow b=-1$. $(0,1)$: $z=0\Rightarrow y=1$, error $-1\Rightarrow \mathbf{w}=(1,0)$, $b=-2$. $(1,0)$: $z=-1\Rightarrow0$ ok. $(1,1)$: $z=-1\Rightarrow0$, error $+1\Rightarrow \mathbf{w}=(2,1)$, $b=-1$.
6. Épocas 3 a 5 (mismos pasos de corrección): $(0,1)$: $\mathbf{w}=(2,0), b=-2$; $(1,0)$: $(1,0), b=-3$; $(1,1)$: $(2,1), b=-2$; $(1,0)$: $(1,1), b=-3$; $(1,1)$: $(2,2), b=-2$; $(0,1)$: $(2,1), b=-3$.
7. La época 6 no produce errores: convergió con $\mathbf{w}=(2,1)$, $b=-3$. Verificación: $(1,1)\to 0\ge0\Rightarrow 1$; $(1,0)\to-1$, $(0,1)\to-2$, $(0,0)\to-3$, todos dan 0. (El resultado depende del orden de los patrones y de $\eta$; hay infinitas soluciones.)

## Código
```python
import numpy as np

class Perceptron:
    def __init__(self, n, eta=0.1):
        self.w = np.zeros(n)   # pesos
        self.b = 0.0           # sesgo
        self.eta = eta         # tasa de aprendizaje

    def predecir(self, x):
        return 1 if x @ self.w + self.b >= 0 else 0

    def entrenar(self, X, t, epocas=50):
        for ep in range(epocas):
            errores = 0
            for xi, ti in zip(X, t):
                e = ti - self.predecir(xi)       # error
                if e != 0:
                    self.w += self.eta * e * xi  # regla del perceptrón
                    self.b += self.eta * e
                    errores += 1
            if errores == 0:                     # convergió
                return ep + 1
        return None                              # no convergió

X = np.array([[0,0],[0,1],[1,0],[1,1]])
for nombre, t in [("AND", [0,0,0,1]), ("OR", [0,1,1,1]), ("XOR", [0,1,1,0])]:
    p = Perceptron(2)
    print(nombre, "épocas:", p.entrenar(X, np.array(t)))   # XOR -> None
```

## Limitación: el problema XOR
Minsky y Papert (1969) demostraron que un perceptrón de una capa no puede representar XOR porque las clases no son linealmente separables. La salida es añadir capas ocultas (clase siguiente) o características no lineales.

## Errores comunes
- Olvidar el sesgo $b$: obliga al hiperplano a pasar por el origen.
- Esperar convergencia con datos no separables.
- Confundir la salida binaria (escalón) con el gradiente: el escalón no es derivable, por eso se usan sigmoides en redes multicapa.
- Normalizar mal las entradas: escalas muy distintas hacen lento el aprendizaje.

## Ejercicios propuestos
1. Calcula la salida de una neurona con $\mathbf{w}=(0{,}5,-1)$, $b=0{,}2$, entrada $(2,1)$, activación escalón. *Respuesta: $z=0{,}2$, salida 1.*
2. Entrena a mano un perceptrón para OR con $\eta=1$ partiendo de ceros y verifica la solución. *Respuesta: p. ej. $\mathbf{w}=(1,1)$, $b=0$ tras pocas épocas.*
3. Explica con un dibujo por qué XOR no es separable linealmente. *Respuesta: los puntos $(0,1),(1,0)$ y $(0,0),(1,1)$ quedan en diagonales opuestas; ninguna recta los separa.*

## Conexiones
- Álgebra y cálculo del descenso de gradiente: [[Matemática III]] y [[Matemática IV]].
- Optimización: [[Investigación de Operaciones II]].
- Implementación en Python: [[Programación II]].
- Serie hermana en probabilidad y aprendizaje: [[AA 01 - Fundamentos del aprendizaje automático]].

## Fuente
Conocimiento general (Haykin, *Neural Networks and Learning Machines*; Rosenblatt 1958; Minsky y Papert 1969). Temario según [[Redes Neuronales y Lógica Difusa]] (verificar con el programa oficial).
