---
tags: [clase, electiva]
materia: Introducción a la Inteligencia Artificial
fuente: "conocimiento general"
---
# IIA 05 - Lógica proposicional, primer orden y Prolog

Materia: [[Introducción a la Inteligencia Artificial]]
Anterior: [[IIA 04 - Juegos, minimax y poda alfa-beta]]
Siguiente: [[IIA 06 - Razonamiento con incertidumbre y redes bayesianas]]

## Contexto y objetivo
Un agente basado en conocimiento mantiene una **base de conocimiento** (BC) de sentencias en un lenguaje formal y razona con ella para inferir hechos nuevos. La lógica ofrece sintaxis, semántica y procedimientos de inferencia con garantías. Objetivo: razonar en lógica proposicional y de primer orden (LPO), aplicar resolución y programar en Prolog.

## Lógica proposicional
- **Sintaxis:** símbolos proposicionales y conectivos $\neg,\wedge,\vee,\Rightarrow,\Leftrightarrow$.
- **Semántica:** un modelo asigna verdadero/falso a cada símbolo; las tablas de verdad definen los conectivos.
- **Consecuencia lógica:** $KB\models\alpha$ si $\alpha$ es verdadera en todos los modelos en que lo es la BC.
- **Validez** (tautología), **satisfacibilidad** (SAT, NP-completo).
- **Inferencia:** enumeración de modelos ($2^n$), reglas (modus ponens $\frac{\alpha,\ \alpha\Rightarrow\beta}{\beta}$, eliminación de conjunción), y **resolución**: con cláusulas en forma normal conjuntiva (FNC), $\frac{\ell_1\vee\dots\vee\ell_k,\ \ m_1\vee\dots\vee m_n}{\text{cláusula sin }\ell_i\text{ y }m_j\text{ complementarios}}$. Se prueba $KB\models\alpha$ por refutación: añadir $\neg\alpha$ y derivar la cláusula vacía. La resolución es completa para refutación.
- **Cláusulas de Horn** (a lo sumo un literal positivo): encadenamiento hacia adelante (guiado por datos) y hacia atrás (guiado por metas) en tiempo lineal.

## Lógica de primer orden
Amplía con objetos, funciones, predicados y cuantificadores: $\forall x\,(Humano(x)\Rightarrow Mortal(x))$, $\exists x\,Padre(x,juan)$. Equivalencias: $\neg\forall x\,P\equiv\exists x\,\neg P$. Inferencia con **unificación** (hallar sustitución $\theta$ que iguale dos expresiones: unificar $Padre(x,juan)$ con $Padre(pedro,y)$ da $\{x/pedro,y/juan\}$) y resolución generalizada (con skolemización para eliminar $\exists$). LPO es semidecidible: si $KB\models\alpha$ la prueba termina; si no, puede no terminar.

## Sistemas basados en reglas y Prolog
Un sistema de producción tiene memoria de trabajo, reglas SI-ENTONCES y un motor de inferencia (sistemas expertos). **Prolog** implementa cláusulas de Horn con resolución SLD y retroceso (backtracking): programa = hechos y reglas; ejecución = consultas.

```prolog
% Hechos
padre(juan, maria).
padre(juan, pedro).
padre(pedro, ana).
% Reglas
abuelo(X, Z) :- padre(X, Y), padre(Y, Z).
hermano(X, Y) :- padre(P, X), padre(P, Y), X \= Y.
ancestro(X, Y) :- padre(X, Y).
ancestro(X, Y) :- padre(X, Z), ancestro(Z, Y).
% Consultas: ?- abuelo(juan, Z).   ->  Z = ana.
%            ?- ancestro(juan, ana).  ->  true.
```

Elementos: variables en mayúscula, átomos en minúscula, `:-` es "si", la coma es "y", `;` es "o". La búsqueda es en profundidad en orden de las cláusulas, así que el orden importa (la recursión izquierda puede ciclar). Listas: `[H|T]`. La negación es por fallo (`\+`), con supuesto de mundo cerrado.

## Ejemplo resuelto: resolución proposicional
BC: $P\Rightarrow Q$, $Q\Rightarrow R$, $P$. Demostrar $R$.
1. Cláusulas: $\neg P\vee Q$; $\neg Q\vee R$; $P$. Negar la consulta: $\neg R$.
2. Resolver $\neg P\vee Q$ con $P$: obtiene $Q$.
3. Resolver $Q$ con $\neg Q\vee R$: obtiene $R$.
4. Resolver $R$ con $\neg R$: cláusula vacía. Contradicción, por tanto $KB\models R$.

Unificación: $Conoce(juan,x)$ con $Conoce(y,madre(y))$: $\theta=\{y/juan,\ x/madre(juan)\}$.

## Código (Python)
Encadenamiento hacia adelante con cláusulas de Horn y verificación por tablas de verdad:
```python
from itertools import product

# reglas de Horn: (premisas, conclusión)
reglas = [({"P"}, "Q"), ({"Q"}, "R"), ({"R", "S"}, "T")]
hechos = {"P", "S"}

def adelante(reglas, hechos):
    conocidos = set(hechos)
    cambio = True
    while cambio:
        cambio = False
        for premisas, concl in reglas:
            if premisas <= conocidos and concl not in conocidos:
                conocidos.add(concl)          # modus ponens
                cambio = True
    return conocidos
print(adelante(reglas, hechos))               # {'P','S','Q','R','T'}

# consecuencia lógica por enumeración de modelos
def implica(kb, alfa, simbolos):
    for vals in product([False, True], repeat=len(simbolos)):
        m = dict(zip(simbolos, vals))
        if kb(m) and not alfa(m):
            return False
    return True

kb = lambda m: (not m["P"] or m["Q"]) and (not m["Q"] or m["R"]) and m["P"]
print(implica(kb, lambda m: m["R"], ["P", "Q", "R"]))   # True
```
Con `pyswip` se puede invocar SWI-Prolog desde Python.

## Errores comunes
- Confundir implicación $\Rightarrow$ con consecuencia $\models$ y con la flecha de Prolog.
- Pensar que $P\Rightarrow Q$ es falsa cuando $P$ es falsa (es verdadera).
- Cuantificar mal: $\forall x\,\exists y$ no es $\exists y\,\forall x$.
- Prolog: recursión izquierda infinita, orden incorrecto de cláusulas, olvidar el corte o su efecto.
- Ignorar el mundo cerrado de Prolog: lo no demostrable se toma como falso.

## Ejercicios propuestos
1. Traduce "todo estudiante que estudia aprueba" a LPO. *Respuesta: $\forall x\,(Estudiante(x)\wedge Estudia(x)\Rightarrow Aprueba(x))$.*
2. Pasa $P\Rightarrow Q$ a FNC. *Respuesta: $\neg P\vee Q$.*
3. ¿Qué responde `?- ancestro(pedro, X).` con la base dada? *Respuesta: `X = ana`.*

## Conexiones
- Lógica, tablas de verdad y demostraciones: [[Matemática Discreta]].
- Conjuntos difusos como generalización de la lógica: [[RNLD 05 - Conjuntos difusos y funciones de pertenencia]].
- Reglas en bases de datos (Datalog, restricciones): [[Base de Datos I]].

## Fuente
Conocimiento general (Russell y Norvig, caps. 7-9; documentación de SWI-Prolog). Verificar el temario con el programa oficial.
