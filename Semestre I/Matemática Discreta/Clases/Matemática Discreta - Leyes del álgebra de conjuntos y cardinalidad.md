---
tags: [clase, semestre-I]
materia: Matemática Discreta
---
# Matemática Discreta - Leyes del álgebra de conjuntos y cardinalidad

Materia: [[Matemática Discreta]]  
Anterior: [[Matemática Discreta - Teoría de conjuntos y operaciones básicas]] · Siguiente: [[Matemática Discreta - Relaciones binarias y representaciones]]

## Contexto y objetivo
En el I parcial es habitual demostrar identidades conjuntistas y simplificar expresiones complejas **sin recurrir a diagramas de Venn**, justificando cada paso mediante las **leyes del álgebra de conjuntos**. Asimismo, los problemas de conteo en encuestas o sistemas se resuelven aplicando el **principio de inclusión–exclusión** sobre cardinalidades.

## 1. Leyes del álgebra de conjuntos
Existe una correspondencia directa entre estas leyes, la lógica proposicional y el álgebra booleana de [[Fundamentos de Lógica Digital]]:

| Ley | Unión | Intersección |
|---|---|---|
| **Idempotencia** | $A \cup A = A$ | $A \cap A = A$ |
| **Conmutativa** | $A \cup B = B \cup A$ | $A \cap B = B \cap A$ |
| **Asociativa** | $(A \cup B) \cup C = A \cup (B \cup C)$ | $(A \cap B) \cap C = A \cap (B \cap C)$ |
| **Distributiva** | $A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$ | $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$ |
| **Identidad (Neutro)** | $A \cup \emptyset = A$ | $A \cap U = A$ |
| **Dominación** | $A \cup U = U$ | $A \cap \emptyset = \emptyset$ |
| **Complemento** | $A \cup A' = U$ | $A \cap A' = \emptyset$ |
| **De Morgan** | $(A \cup B)' = A' \cap B'$ | $(A \cap B)' = A' \cup B'$ |
| **Absorción** | $A \cup (A \cap B) = A$ | $A \cap (A \cup B) = A$ |
| **Doble complemento** | $(A')' = A$ | — |
| **Definición de diferencia** | $A - B = A \cap B'$ | — |

## 2. Ejemplo resuelto de simplificación algebraica
Simplificar la expresión $[(A \cap B) \cup (A \cap B')]' \cup A$ citando cada ley:

1. Factorizamos $A$ usando la **ley distributiva**:
   $$[A \cap (B \cup B')]' \cup A$$
2. Por **ley del complemento** ($B \cup B' = U$):
   $$(A \cap U)' \cup A$$
3. Por **ley de identidad** ($A \cap U = A$):
   $$A' \cup A$$
4. Por **ley del complemento**:
   $$U$$

> [!tip] Estrategia para simplificar diferencias
> Siempre convierte primero todas las diferencias $X - Y$ a $X \cap Y'$ antes de aplicar De Morgan o distributiva.

## 3. Cardinalidad y principio de inclusión–exclusión
Para dos conjuntos finitos $A$ y $B$:
$$|A \cup B| = |A| + |B| - |A \cap B|$$
Para tres conjuntos finitos $A, B, C$:
$$|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|$$

### Ejemplo de conteo
En un grupo de $60$ estudiantes de Semestre I, $35$ cursan Computación I ($C$), $30$ cursan Matemática Discreta ($M$) y $15$ cursan ambas. ¿Cuántos no cursan ninguna de las dos?
1. $|C \cup M| = 35 + 30 - 15 = 50$.
2. Fuera de la unión: $60 - 50 = 10$ estudiantes.

## Errores comunes
- Aplicar De Morgan dejando el mismo operador: escribir $(A \cup B)' = A' \cup B'$ en lugar de cambiar $\cup$ por $\cap$.
- No citar la ley utilizada en cada paso de la demostración (penalizado en los parciales de Matemática Discreta).
- Sumar directamente $|A| + |B|$ en problemas de conteo olvidando restar la intersección $|A \cap B|$.

## Ejercicios propuestos
1. Simplifica $(A - B) \cup (A \cap B)$ paso a paso.  
   *Respuesta:* $(A \cap B') \cup (A \cap B) = A \cap (B' \cup B) = A \cap U = A$.
2. Simplifica $[(A' \cup B)' \cap A]'$.  
   *Respuesta:* $[(A \cap B') \cap A]' = (A \cap B')' = A' \cup B$.

## Conexiones
- Materia principal: [[Matemática Discreta]]
- Nota resumen: [[Matemática Discreta - Teoría de conjuntos y operaciones básicas]]
- Anterior: [[Matemática Discreta - Teoría de conjuntos y operaciones básicas]]
- Siguiente: [[Matemática Discreta - Relaciones binarias y representaciones]]
- Conexión directa: [[Fundamentos de Lógica Digital]] (leyes idénticas en álgebra de Boole).

## Fuente
Material de [[Matemática Discreta]] en `Material/PARCIAL 1/` (`2 Leyes de Conjuntos Murillo Tsijli.pdf`, `3 Conociendo las leyes o propiedades de conjuntos..pdf`, `4 Ejm usando leyes o propiedades de conjuntos..pdf`, `Ejer. propuestos Simplifc de teoría de conjuntos pag 140 texto tsijli.pdf`).
