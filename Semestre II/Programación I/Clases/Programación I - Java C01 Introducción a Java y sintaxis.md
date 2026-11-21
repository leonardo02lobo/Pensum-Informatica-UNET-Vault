---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaI-C01 Programación Orientada a Objetos (POO).pdf
---
# Java C01 - Introducción a Java, JVM y sintaxis básica

Materia: [[Programación I]]

## Contexto y objetivo
Esta primera lección de la Unidad I (POO en Java) presenta el lenguaje que se usará durante la mayor parte del curso: qué es Java, por qué es independiente de la plataforma, cómo se compila y se ejecuta un programa, y cuál es la sintaxis mínima (identificadores, constantes, tipos primitivos, operadores y estructura de un programa). El estudiante viene de [[Computación I]] (donde se programó en C, ver [[Computación I - Elementos del lenguaje C, tipos y operadores]]); por eso la lección insiste en lo que Java **simplifica** respecto a C/C++ (sin punteros, sin macros, sin gestión manual de memoria).

## 1. ¿Qué es Java?
Java es un lenguaje de alto nivel, con elementos de C y C++, acompañado de una gran biblioteca de clases, un soporte de ejecución estándar y una **máquina virtual**. Un programa Java es, en esencia, una **biblioteca de clases compiladas a bytecode**, organizadas en **paquetes jerárquicos**, basada en el paradigma orientado a objetos y usada tanto para aplicaciones convencionales como para Internet.

La promesa original de sus creadores fue **"Write Once, Run Anywhere"** (escríbelo una vez, ejecútalo en cualquier lugar): un lenguaje independiente de la plataforma con un entorno de ejecución ligero y gratuito para las plataformas más populares.

## 2. Características
| Característica | Explicación |
|---|---|
| Sencillo y familiar | Sintaxis basada en C, pero sin punteros, macros, registros (`struct`) ni `typedef`. Menos errores y aprendizaje más rápido. |
| Orientado a objetos | "Todo son objetos" (salvo los tipos primitivos). Ofrece encapsulamiento, herencia, polimorfismo y enlace dinámico. No incluye herencia múltiple de clases ni sobrecarga de operadores. |
| Independiente de la plataforma / neutral a la arquitectura | El compilador genera **bytecode**, no código de máquina; la JVM de cada plataforma lo interpreta. |
| Interpretado y compilado | Se compila a bytecode y luego la JVM lo interpreta o lo compila "just in time" (JIT) a código nativo. |
| Robusto | La ejecución dentro de la JVM evita que el programa bloquee el sistema; tipado estricto; memoria administrada por el sistema; verificación en compilación y ejecución. |
| Seguro | Modelo de "sandboxing", verificación de bytecode, cargador de clases y restricciones de acceso a red. |
| Multihilo | Un programa lanza varios hilos de ejecución que comparten código y variables (no son procesos nuevos). |
| Recolector de basura | Libera automáticamente la memoria de objetos que ya no se usan. |

### Por qué no hay herencia múltiple ni sobrecarga de operadores
Los diseñadores las consideraron de "menor utilidad" frente a su complejidad (el problema del rombo, operadores ambiguos). La herencia múltiple se sustituye por **interfaces** (ver [[Programación I - Java C08 Interfaces]]). En C++ sí existen ambas (ver [[Programación I - C++ C04 Herencia]]).

## 3. La máquina virtual (JVM) y el ciclo de compilación
La **JVM** es un programa escrito en código nativo de la plataforma destino que interpreta y ejecuta el código producido por el compilador de Java. Al compilar no se crea código máquina sino un pseudocódigo (**bytecode**) almacenado en archivos `.class`.

```
Ejemplo.java --(javac)--> Ejemplo.class --(java)--> ejecución en la JVM
   fuente            bytecode              intérprete / JIT
```

Comandos básicos:
```bash
javac Ejemplo.java    # genera Ejemplo.class
java Ejemplo          # ejecuta (sin la extensión)
```
Ventajas frente a otros lenguajes interpretados: código compacto, eficiente (gracias al JIT) y "confidencial" (se distribuye el bytecode, no el fuente).

### Recolector de basura (Garbage Collector)
En C, C++ o Pascal el programador libera con `free`/`delete`. En Java el GC elimina en tiempo de ejecución los objetos **inalcanzables** (sin referencias). No se sabe con exactitud cuándo se ejecutará; si no falta memoria, puede no ejecutarse nunca. Por eso en Java no hay destructores (ver [[Programación I - Java C04 Clases, objetos y métodos]]).

### Programar en Java es "incrementar la biblioteca de clases"
Los programas se componen de clases y métodos. Aprender Java consiste en (a) aprender el lenguaje para escribir clases propias y (b) aprender a usar las extensas bibliotecas estándar (`java.lang`, `java.util`, `java.io`, `java.awt`, `javax.swing`...).

## 4. Sintaxis
### Identificadores
Nombres de variables, métodos y clases. Reglas:
- El primer carácter debe ser una letra (Java también admite `_` y `$`, pero el programa del curso exige letra).
- Distingue mayúsculas de minúsculas (`Hola` y `hola` son distintos).
- Puede contener `_` y dígitos, pero no como primer carácter.
- No puede ser palabra reservada (`class`, `public`, `short`...).

| Válidos | Inválidos | Motivo |
|---|---|---|
| `cont1`, `VARIABLE`, `Porc_Aprob`, `anhos` | `1cont` | empieza con dígito |
| | `cont-1` | el guion es el operador resta |
| | `Porc Aprob` | espacio |
| | `Hola!`, `#anhos` | símbolos no permitidos |
| | `short` | palabra reservada |

Convención de estilo: clases en `PascalCase` (`MaquinaBoletos`), métodos y variables en `camelCase` (`getSaldo`), constantes en `MAYUSCULAS` (`PI`).

### Constantes (literales)
- **Enteras**: decimal (`0`, `1`, `894`), octal (empieza con 0: `077`, `0472`) y hexadecimal (`0x1`, `0Xabcd`). Se almacenan en 32 bits (`int`); un sufijo `L` fuerza `long` (`99L`).
- **Coma flotante**: base 10 con punto decimal o exponente (`2E-8`, `5.6384e2`). Por defecto son `double` (64 bits); con sufijo `f`/`F` son `float` (`5.6384e2F`). Nota: en código Java real el separador decimal es el punto, no la coma.
- **Carácter**: un carácter entre comillas simples (`'a'`, `'9'`). Secuencias de escape con `\`: `\n` salto de línea, `\t` tabulador, `\\`, `\'`, `\"`.
- **Cadena**: entre comillas dobles; se implementan con la clase `String` (`String universidad = "UNET";`). Los `String` son **inmutables**.

### Tipos de datos primitivos
| Categoría | Tipo | Tamaño | Rango |
|---|---|---|---|
| Enteros | byte | 8 bits | -128 a 127 |
| | short | 16 bits | -32768 a 32767 |
| | int | 32 bits | -2 147 483 648 a 2 147 483 647 |
| | long | 64 bits | aprox. ±9.22·10^18 |
| Reales | float | 32 bits | aprox. ±3.4·10^38 (6-7 dígitos significativos) |
| | double | 64 bits | aprox. ±1.8·10^308 (15-16 dígitos) |
| Carácter | char | 16 bits | Unicode |
| Lógico | boolean | (1 bit lógico) | true / false |

El rango de un entero con signo de $n$ bits es $[-2^{n-1},\ 2^{n-1}-1]$; por eso `byte` va de $-2^7=-128$ a $2^7-1=127$. `String` no es primitivo: es una clase.

### Declaración de variables
`Tipo_Dato variable1, variable2, ...;` Toda variable debe declararse antes de usarse.
```java
byte edad;
long angulo, magnitud;
double velocidad;
char sexo;
```

### Operadores
- Aritméticos: `+ - * / %` (resto), `++`, `--`. El `+` también **concatena** cadenas: `"Ana" + " " + "Chacon"`.
- Asignación compuesta: `+=`, `-=`, `*=`, `/=`, `%=` (`a += b` equivale a `a = a + b`).
- Relacionales: `< <= > >= == !=`. Lógicos: `&&` (y), `||` (o), `!`.
- Precedencia (de mayor a menor): separadores, unarios, multiplicativos, suma/resta, desplazamiento de bits, relacionales, igualdad, `&`, `^`, `|`, `&&`, `||`, condicional `?:`, asignación.

Detalle importante: la división entre enteros es **entera**: `7 / 2 == 3`; y `7 % 2 == 1`. Para obtener `3.5` hace falta que uno de los operandos sea real: `7 / 2.0`.

### Estructura básica de un programa
```java
package Pruebas;          // paquete (opcional)
import java.io.*;         // importaciones

public class NombreClase {          // archivo: NombreClase.java
    // atributos (variables)
    // métodos (funciones)
    public static void main(String[] args) {
        // declaración de variables
        // instrucciones
    }
}
```
El archivo se llama igual que la clase pública. `main` es el punto de entrada: `public static void main(String[] args)`.

### Ejemplo de declaración y asignación
```java
public class Declaracion {
    public static void main(String[] args) {
        int i;                       // declaración
        int j = 0;                   // declaración + inicialización
        float pi = 3.414f;           // el sufijo f es obligatorio
        double magnitud = 25.698;
        boolean sw = true;
        char sexo;
        String cad1;
        String cad2 = "UNET";
        sexo = 'F';
        cad1 = "Programacion";       // ojo: terminar con ;
        i = 6;
    }
}
```
(El PDF original omite el `;` tras `cad1 = "Programacion"`: es un error de compilación que conviene notar.)

## Ejemplo resuelto
Calcular el área de un círculo de radio 2.5:
```java
public class Area {
    public static void main(String[] args) {
        final double PI = 3.14159265;     // constante
        double r = 2.5;
        double area = PI * r * r;         // 19.634954...
        System.out.println("Área = " + area);
    }
}
```
Paso a paso: se declara una constante (`final`), se evalúa `PI*r*r` con precedencia de izquierda a derecha y se concatena el resultado al texto.

## Errores comunes
- Olvidar el sufijo: `float x = 12.414;` falla porque `12.414` es `double`.
- `int v = 99L;` falla (pérdida de información); `long v = 6;` es correcto.
- Nombre de archivo distinto al de la clase pública.
- Usar un identificador con espacio o guion.
- Creer que `char` es de 8 bits (en Java son 16, Unicode).

## Ejercicios propuestos
1. Indique cuáles identificadores son válidos: `_x`, `2abc`, `total_1`, `class`, `Nota-final`. *(Con la regla del curso: `total_1` sí; `_x` según la regla estricta no; el resto no.)*
2. ¿Qué imprime `System.out.println(7 / 2 + " " + 7 % 2 + " " + 7 / 2.0);`? *(`3 1 3.5`)*
3. ¿Cuántos valores distintos admite un `short`? *(65 536)*
4. Escriba el comando para compilar y ejecutar `Hola.java`. *(`javac Hola.java` y `java Hola`)*

## Conexiones
- Siguiente tema: entrada/salida y control de flujo en [[Programación I - Java C02 Entrada salida y control de flujo]].
- Resumen previo de la materia: [[Programación I - Java C04 Clases, objetos y métodos]].
- Comparación con C: [[Computación I - Elementos del lenguaje C, tipos y operadores]].

## Fuente
`Material/Java/Teoria/TemaI-C01 Programación Orientada a Objetos (POO).pdf` (también copiado en `Material/Java/`).
