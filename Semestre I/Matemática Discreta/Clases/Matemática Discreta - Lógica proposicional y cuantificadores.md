---
tags: [clase, semestre-I]
materia: Matemática Discreta
---
# Matemática Discreta - Lógica proposicional y cuantificadores

Materia: [[Matemática Discreta]]  
Siguiente: [[Matemática Discreta - Teoría de conjuntos y operaciones básicas]]

## Contexto y objetivo
La **lógica matemática** proporciona el lenguaje formal para demostrar teoremas, verificar la validez de razonamientos y construir condiciones booleanas en programación y circuitos digitales. En esta clase se estudian las **proposiciones**, los **conectivos lógicos**, las **tablas de verdad**, las **tautologías y equivalencias lógicas**, y los **cuantificadores** universal y existencial.

## 1. Proposiciones y conectivos lógicos
Una **proposición** es un enunciado declarativo al que se le puede asignar un único valor de verdad: **verdadero ($V$ o $1$)** o **falso ($F$ o $0$)**. No son proposiciones las preguntas, órdenes ni expresiones ambiguas como *"x + 2 = 5"* (esta última es una *función proposicional* o predicado).

Los conectivos combinan proposiciones simples ($p, q, r$):
- **Negación ($\neg p$)**: invierte el valor de verdad.
- **Conjunción ($p \land q$)**: verdadera solo si ambas son verdaderas (*"y"*).
- **Disyunción inclusiva ($p \lor q$)**: falsa solo si ambas son falsas (*"o"*).
- **Condicional o implicación ($p \rightarrow q$)**: falsa únicamente cuando el antecedente $p$ es verdadero y el consecuente $q$ es falso.
- **Bicondicional ($p \leftrightarrow q$)**: verdadera cuando $p$ y $q$ tienen el mismo valor de verdad (*"si y solo si"*).

### Tabla de verdad resumen
| $p$ | $q$ | $\neg p$ | $p \land q$ | $p \lor q$ | $p \rightarrow q$ | $p \leftrightarrow q$ |
|---|---|---|---|---|---|---|
| $V$ | $V$ | $F$ | $V$ | $V$ | $V$ | $V$ |
| $V$ | $F$ | $F$ | $F$ | $V$ | $F$ | $F$ |
| $F$ | $V$ | $V$ | $F$ | $V$ | $V$ | $F$ |
| $F$ | $F$ | $V$ | $F$ | $F$ | $V$ | $V$ |

Para $n$ variables proposicionales, la tabla tiene $2^n$ filas.

## 2. Tautologías, contradicciones y equivalencias lógicas
- **Tautología**: proposición compuesta siempre verdadera para cualquier asignación de valores (ej. $p \lor \neg p$).
- **Contradicción**: siempre falsa (ej. $p \land \neg p$).
- **Contingencia**: toma valores $V$ y $F$ según el caso.

Dos proposiciones $P$ y $Q$ son **lógicamente equivalentes** ($P \equiv Q$) si $P \leftrightarrow Q$ es una tautología. Equivalencias fundamentales:
- **De Morgan**: $\neg(p \land q) \equiv \neg p \lor \neg q$; $\quad \neg(p \lor q) \equiv \neg p \land \neg q$.
- **Implicación**: $p \rightarrow q \equiv \neg p \lor q$.
- **Contrarrecíproca**: $p \rightarrow q \equiv \neg q \rightarrow \neg p$.
- **Doble negación**: $\neg(\neg p) \equiv p$.

## 3. Predicados y cuantificadores
Para enunciados con variables $P(x)$ sobre un dominio $D$:
- **Cuantificador universal ($\forall x \in D,\; P(x)$)**: *"Para todo $x$ en $D$, se cumple $P(x)$."* Es falso si existe al menos un **contraejemplo**.
- **Cuantificador existencial ($\exists x \in D,\; P(x)$)**: *"Existe al menos un $x$ en $D$ tal que $P(x)$."*

### Negación de cuantificadores
$$\neg(\forall x,\, P(x)) \equiv \exists x,\, \neg P(x) \qquad\qquad \neg(\exists x,\, P(x)) \equiv \forall x,\, \neg P(x)$$

## 4. Ejemplo resuelto: demostrar que $(p \rightarrow q) \equiv (\neg q \rightarrow \neg p)$
Por la equivalencia de la implicación:
$$\neg q \rightarrow \neg p \equiv \neg(\neg q) \lor \neg p \equiv q \lor \neg p \equiv \neg p \lor q \equiv p \rightarrow q$$
Esta equivalencia justifica las **demostraciones por contrarrecíproco** usadas en conjuntos y relaciones.

## Errores comunes
- Creer que $p \rightarrow q$ es falso cuando $p$ es falso (por tabla, si $p$ es $F$, la implicación siempre es $V$).
- Negar $\forall x,\, P(x)$ escribiendo $\forall x,\, \neg P(x)$ en lugar de $\exists x,\, \neg P(x)$.
- Olvidar las leyes de De Morgan al negar condiciones en `if` o `while` de [[Computación I]].

## Ejercicios propuestos
1. Construye la tabla de verdad de $\neg(p \land q) \rightarrow (\neg p \lor \neg q)$ y clasifícala.  
   *Respuesta:* Es una **tautología** (todas las filas resultan $V$ por ley de De Morgan).
2. Niega el enunciado: *"Todos los estudiantes aprobaron el primer parcial."*  
   *Respuesta:* *"Existe al menos un estudiante que no aprobó el primer parcial."* ($\exists x,\, \neg A(x)$).

## Conexiones
- Materia principal: [[Matemática Discreta]]
- Siguiente clase: [[Matemática Discreta - Teoría de conjuntos y operaciones básicas]]
- Relación con el pensum: [[Computación I - Estructuras de control selectivas]] (expresiones booleanas), [[Fundamentos de Lógica Digital]] (compuertas lógicas y álgebra booleana).

## Fuente
Basado en el programa oficial de [[Matemática Discreta]]; texto guía Murillo Tsijli, *Introducción a la Matemática Discreta* (4.ª ed.) y Johnsonbaugh, *Matemáticas discretas* (`Material/GUIAS/`).
