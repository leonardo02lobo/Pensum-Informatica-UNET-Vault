---
tags: [clase, semestre-I]
materia: Computación I
---
# Computación I - Introducción a la computación y algoritmos

Materia: [[Computación I]]  
Siguiente: [[Computación I - Elementos del lenguaje C, tipos y operadores]]

## Contexto y objetivo
Esta clase introduce los fundamentos de la arquitectura de un computador, la representación binaria de la información y el concepto central de la asignatura: el **algoritmo** como método sistemático para resolver problemas antes de escribir código en C. Al finalizar, serás capaz de distinguir entre hardware y software, explicar el ciclo de compilación de un programa y diseñar soluciones mediante análisis Entrada–Proceso–Salida (EPS), pseudocódigo y diagramas de flujo.

## 1. Arquitectura básica: hardware, software y sistema binario
Un sistema computacional se compone de dos planos inseparables:
- **Hardware**: componentes físicos (CPU, memoria principal RAM, almacenamiento secundario, dispositivos de entrada/salida). La CPU ejecuta instrucciones aritmético-lógicas y coordina el flujo de datos.
- **Software**: conjunto de programas y datos que indican al hardware qué hacer. Se divide en *software de sistema* (sistema operativo, compiladores, controladores) y *software de aplicación*.

Internamente, toda información (números, caracteres, instrucciones) se representa en **sistema binario** (base $2$, dígitos `0` y `1`, llamados *bits*). Un grupo de $8$ bits forma un **byte**, capaz de representar $2^8 = 256$ valores distintos ($0$ a $255$ sin signo).

### Conversión decimal–binario
Para convertir un entero positivo de base $10$ a base $2$, se divide sucesivamente entre $2$ y se toman los residuos en orden inverso:
$$25_{10} \rightarrow 25 \div 2 = 12\,(1),\; 12 \div 2 = 6\,(0),\; 6 \div 2 = 3\,(0),\; 3 \div 2 = 1\,(1),\; 1 \div 2 = 0\,(1) \implies 11001_2$$

Para volver a base $10$, se suma cada bit multiplicado por su potencia de $2$:
$$11001_2 = 1\cdot 2^4 + 1\cdot 2^3 + 0\cdot 2^2 + 0\cdot 2^1 + 1\cdot 2^0 = 16 + 8 + 1 = 25_{10}$$

## 2. Lenguajes de programación, compiladores e intérpretes
Un programa escrito por humanos (*código fuente*) debe traducirse a *código máquina* para que la CPU lo ejecute:
- **Lenguaje de bajo nivel**: cercano al hardware (ensamblador, código máquina).
- **Lenguaje de alto nivel**: cercano al razonamiento humano (C, Python, Java).
- **Compilador**: traduce todo el código fuente a un archivo ejecutable antes de correrlo (ejemplo: `gcc` para C). Detecta errores de sintaxis en tiempo de compilación y produce programas muy rápidos.
- **Intérprete**: traduce y ejecuta instrucción por instrucción en tiempo de ejecución (ejemplo: Python).

### Ciclo edición–compilación–ejecución en C
1. **Edición**: escribir el código fuente en un archivo `.c` (ej. `programa.c`).
2. **Preprocesamiento y compilación**: el compilador procesa directivas (`#include`, `#define`), verifica sintaxis y genera código objeto.
3. **Enlazado (*linking*)**: une el código objeto con bibliotecas estándar (como `stdio.h`) para producir el ejecutable.
4. **Ejecución y prueba**: se corre el programa con datos de prueba y se verifican los resultados.

## 3. Algoritmos y análisis Entrada–Proceso–Salida (EPS)
Un **algoritmo** es una secuencia finita, ordenada y no ambigua de pasos que resuelve un problema. Todo algoritmo válido cumple tres propiedades fundamentales:
1. **Finito**: debe terminar después de un número limitado de pasos.
2. **Definido (determinista)**: ante las mismas entradas, siempre produce los mismos resultados.
3. **Preciso**: cada instrucción debe estar formulada sin ambigüedad.

Antes de programar, se realiza el **análisis EPS**:
- **Entradas**: datos necesarios que aporta el usuario o el sistema.
- **Proceso**: fórmulas, condiciones o transformaciones que convierten las entradas en resultados.
- **Salidas**: información final que se muestra o almacena.

## 4. Pseudocódigo y diagramas de flujo
El **pseudocódigo** expresa el algoritmo en lenguaje estructurado cercano al español o al inglés, sin atarse a la sintaxis estricta de un compilador. Los **diagramas de flujo** representan el mismo flujo de forma gráfica (óvalo para Inicio/Fin, paralelogramo para Entrada/Salida, rectángulo para Proceso, rombo para Decisión).

### Ejemplo resuelto: promedio de tres calificaciones
**Análisis EPS:**
- Entradas: `n1, n2, n3` (reales).
- Proceso: `prom <- (n1 + n2 + n3) / 3`.
- Salida: `prom`.

**Pseudocódigo:**
```text
Algoritmo PromedioNotas
    Definir n1, n2, n3, prom Como Real
    Escribir "Ingrese las tres calificaciones:"
    Leer n1, n2, n3
    prom <- (n1 + n2 + n3) / 3
    Escribir "El promedio es: ", prom
FinAlgoritmo
```

## Errores comunes
- Empezar a teclear código en C sin haber definido claramente las entradas, salidas y casos borde del problema.
- Diseñar algoritmos con ciclos infinitos (violando la propiedad de finitud).
- Confundir errores de compilación (sintaxis mal escrita) con errores lógicos (el programa compila pero calcula un resultado incorrecto).

## Ejercicios propuestos
1. Convierte $42_{10}$ a binario y verifica el resultado pasando de binario a decimal.  
   *Respuesta:* $42_{10} = 101010_2$ ($32 + 8 + 2 = 42$).
2. Realiza el análisis EPS y el pseudocódigo para calcular el área y el perímetro de un rectángulo dados su base y altura.  
   *Respuesta:* Entradas: `base`, `altura`. Proceso: `area <- base * altura`, `perimetro <- 2 * (base + altura)`. Salidas: `area`, `perimetro`.
3. Explica por qué la instrucción *"Sumar algunos números hasta cansarse"* no es un algoritmo válido.  
   *Respuesta:* Carece de precisión (no especifica qué números) y no garantiza finitud definida.

## Conexiones
- Materia principal: [[Computación I]]
- Nota resumen de sintaxis: [[Computación I - Elementos del lenguaje C, tipos y operadores]]
- Siguiente clase: [[Computación I - Elementos del lenguaje C, tipos y operadores]]
- Relación con el pensum: [[Matemática Discreta]] (lógica y sistemas formales), [[Programación I]] (continuación en POO), [[Fundamentos de Lógica Digital]] (sistemas numéricos binarios).

## Fuente
Basado en el programa oficial de [[Computación I]] (código `0415102T`) y la bibliografía recomendada (Joyanes Aguilar, *Fundamentos de programación*; Kernighan y Ritchie, *El lenguaje de programación C*).
