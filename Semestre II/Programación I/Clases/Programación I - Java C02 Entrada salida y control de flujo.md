---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaI-C02 POO y Sintaxys Básica_.pdf
---
# Java C02 - Entrada/salida, conversiones y estructuras de control

Materia: [[Programación I]]

## Contexto y objetivo
Tras ver tipos y operadores, esta lección cubre lo necesario para escribir programas interactivos en consola: salida estándar, entrada estándar (con `BufferedReader` y con `Scanner`), conversión entre tipos, ámbito de variables y las estructuras de control (`if-else`, `switch`, operador ternario, `while`, `do-while`, `for`, `for-each`). Son los mismos conceptos de [[Computación I - Elementos del lenguaje C, tipos y operadores]] con la sintaxis y bibliotecas de Java.

## 1. Salida estándar
La clase `System` (paquete `java.lang`, importado automáticamente) tiene el objeto `System.out`:
- `System.out.print(x)`: escribe sin salto de línea.
- `System.out.println(x)`: escribe y salta de línea.
- `System.out.printf("%d %.2f%n", n, x)`: salida con formato (como `printf` de C).

```java
System.out.print("Hola ");
System.out.println("mundo");   // Hola mundo\n
```

## 2. Entrada estándar
`System.in` es un `InputStream` de **bytes**; `System.in.read()` devuelve el siguiente byte como `int` (o -1 al final). A diferencia de C no hay especificadores de formato (`scanf`), así que para leer cadenas y números se usan clases de apoyo.

### Con BufferedReader
Se "envuelve" `System.in` en un `InputStreamReader` (puente bytes -> caracteres) y este en un `BufferedReader`, que ofrece `readLine()`:
```java
import java.io.*;
public class Lectura {
    public static void main(String[] args) throws IOException {
        BufferedReader lector = new BufferedReader(new InputStreamReader(System.in));
        System.out.print("Edad: ");
        String linea = lector.readLine();      // lee una línea completa
        int edad = Integer.parseInt(linea);    // conversión String -> int
        System.out.println("Nació hacia " + (2025 - edad));
    }
}
```
`readLine()` puede lanzar `IOException` (excepción verificada), por eso el `throws` (ver [[Programación I - Java C09 Gestión de errores y excepciones]]). Los datos numéricos se leen como texto y se transforman con `parseXxx`.

### Con Scanner (java.util.Scanner)
Es la forma más cómoda:
```java
import java.util.Scanner;
Scanner input = new Scanner(System.in);
String nombre = input.next();        // una palabra (hasta espacio)
int n = input.nextInt();             // entero
double x = input.nextDouble();       // real
String linea = input.nextLine();     // línea completa
boolean hay = input.hasNext();       // ¿queda entrada?
input.close();
```
Trampa clásica: después de `nextInt()` queda el salto de línea en el búfer; un `nextLine()` inmediato devuelve la cadena vacía. Solución: llamar un `nextLine()` extra para consumirlo, o leer todo con `nextLine()` y convertir.

## 3. Conversión de tipos
### De cadena a número (clases envoltorio)
| Método | Resultado |
|---|---|
| `Byte.parseByte(s)` / `Short.parseShort(s)` | byte / short |
| `Integer.parseInt(s)` | int |
| `Long.parseLong(s)` | long |
| `Float.parseFloat(s)` / `Double.parseDouble(s)` | float / double |
| `Boolean.parseBoolean(s)` | boolean |

Si el texto no es válido se lanza `NumberFormatException`.

### Otras conversiones
- Número a cadena: `String.valueOf(num)` (o `"" + num`).
- Carácter a dígito y viceversa: `Character.digit(c, base)` y `Character.forDigit(d, base)`.
- Entre numéricos mediante objetos: `Float F = 3.1416f; int i = F.intValue(); double d = F.doubleValue();`.

### Conversión implícita y casting
Java amplía automáticamente en el sentido `byte -> short -> int -> long -> float -> double` (sin pérdida de rango). El camino inverso exige **casting** explícito, porque se puede perder información:
```java
long valorLargo = 99L;
int a = valorLargo;        // ERROR de compilación
int b = (int) valorLargo;  // OK
long c = 6;                // OK (int -> long)
int d = 99L;               // ERROR
double z = 12.414F;        // OK (float -> double)
float x = 12.414;          // ERROR: 12.414 es double
```
`(int) 3.99` da `3` (trunca, no redondea).

### Métodos útiles de String
`length()`, `toUpperCase()`, `toLowerCase()`, `substring(i, j)`, `replace(a, b)`, `split(regex)`, `compareTo(otro)`, `equals(otro)`, `valueOf(...)`. Para comparar contenido se usa `equals`, **nunca** `==` (compara referencias).

## 4. Bloques y ámbito
Un **bloque** es el código entre `{` y `}`. El **ámbito** (scope) determina la vida de una variable: existe desde su declaración hasta el final del bloque en que fue declarada. No se puede redeclarar en un bloque interior una variable local con el mismo nombre que otra visible.
```java
for (int i = 0; i < 3; i++) { int sq = i * i; }
// aquí ni i ni sq existen
```

## 5. Sentencias condicionales
### if-else
```java
if (nota >= 10) {
    System.out.println("Aprobado");
} else if (nota >= 5) {
    System.out.println("Recuperación");
} else {
    System.out.println("Reprobado");
}
```
La condición debe ser `boolean` (en C valía cualquier entero; en Java `if (x = 5)` no compila). Sin llaves solo se asocia la instrucción siguiente. Comparar cadenas: `if (s1.equals(s2))`.

### switch
```java
switch (dia) {
    case 1: nombre = "lunes"; break;
    case 2: nombre = "martes"; break;
    default: nombre = "otro";
}
```
- Sin `break` hay **fall-through**: se ejecutan los casos siguientes hasta encontrar un `break`.
- La lámina indica que solo admite tipos enteros (`int`, `byte`, `short`, `char`); aclaración: no admite `long`, `float`, `double`, y desde Java 7 sí admite `String` y enumerados (el PDF es previo a eso; verificar versión usada en el curso).

### Operador ternario
`int x = c > 9 ? 6 : 7;` -> si `c>9` el valor es 6, si no 7. Equivale a un `if-else` que produce un valor.

## 6. Ciclos
| Ciclo | Cuándo evalúa | Mínimo de ejecuciones |
|---|---|---|
| `while (cond) {...}` | al inicio | 0 |
| `do {...} while (cond);` | al final | 1 |
| `for (init; cond; paso) {...}` | al inicio | 0 |
| `for (Tipo e : coleccion) {...}` | recorre todos | 0 |

```java
int i = 1, suma = 0;
while (i <= 10) { suma += i; i++; }        // 55

do { System.out.print("Opción: "); op = in.nextInt(); } while (op < 1 || op > 5);

for (int i = 0, j = 0; i + j < 20; i++, j--) { ... }   // varias variables

String[] arreglo = {"Maria", "Luis", "Jose", "Ana"};
for (String nombre : arreglo) System.out.println(nombre);   // for-each
```
El `for-each` no da acceso al índice y no sirve para modificar los elementos de un arreglo de primitivos.

## Ejemplo resuelto: promedio con validación
```java
Scanner in = new Scanner(System.in);
int n;
do { System.out.print("Cantidad (>0): "); n = in.nextInt(); } while (n <= 0);
double suma = 0;
for (int i = 1; i <= n; i++) {
    System.out.print("Nota " + i + ": ");
    suma += in.nextDouble();
}
System.out.printf("Promedio = %.2f%n", suma / n);
```
El `do-while` garantiza al menos una lectura; el `for` acumula; el promedio se calcula con `suma/n` donde `suma` es `double` (así no hay división entera).

## Errores comunes
- `nextLine()` tras `nextInt()` (ver arriba).
- Olvidar `break` en `switch`.
- Comparar `String` con `==`.
- División entera inesperada: `int p = 7 / 2 * 1.0;` da 3.
- Variable usada fuera de su ámbito.
- Bucle infinito por olvidar actualizar la variable de control.

## Ejercicios propuestos
1. Leer un entero y decir si es par o impar con ternario. *(`n % 2 == 0 ? "par" : "impar"`)*
2. Tabla de multiplicar del 1 al 10 de un número leído (`for`).
3. Sumar dígitos de un entero con `while` (`n % 10` y `n /= 10`).
4. Menú con `do-while` y `switch` hasta elegir "Salir".
5. ¿Qué resulta de `(int) 'A' + 1`? *(66)*

## Conexiones
- Anterior: [[Programación I - Java C01 Introducción a Java y sintaxis]]. Siguiente: [[Programación I - Java C04 Clases, objetos y métodos]].
- Estas mismas estructuras de control existen en C (ver [[Computación I - Elementos del lenguaje C, tipos y operadores]]) y se usan en los ejercicios de [[Programación I - Java Ejercicios C01 C02 C03 y su resolución]].

## Fuente
`Material/Java/Teoria/TemaI-C02 POO y Sintaxys Básica_.pdf`.
