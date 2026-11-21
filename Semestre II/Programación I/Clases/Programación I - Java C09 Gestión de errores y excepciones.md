---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaIII-C09 GestionErrores.pdf (y Material/Java/Teoria/UII-C01 GestionErrores .pdf)
---
# Java C09 - Gestión de errores: excepciones

Materia: [[Programación I]]

## Contexto y objetivo
Un programa robusto no debe "morir" ante un fichero inexistente, un índice fuera de rango o una entrada inválida: debe **detectar** el problema y, si es posible, **recuperarse**. Java usa **excepciones**: objetos que representan una condición anormal y que interrumpen el flujo normal. Esta lección (Unidad II del programa 2024-2) cubre qué es una excepción, la clase `Exception`/`Throwable`, `try-catch-finally`, `throws`/`throw` y las excepciones definidas por el programador. Es indispensable para [[Programación I - Java C10 Archivos en Java]].

## 1. Por qué tratar los errores
Una excepción es *un evento que interrumpe el flujo normal de instrucciones durante la ejecución*. Ejemplos: archivo no encontrado, índice fuera de rango, caída de red, fallo de disco. Las excepciones permiten:
- **Encapsular** los errores en clases.
- **Separar** el flujo normal del tratamiento de errores (el código "feliz" queda limpio).
- Programación **defensiva**, mayor robustez y fiabilidad.

Pseudocódigo motivador del PDF: `leerArchivo { abrir; determinar longitud; reservar memoria; copiar; cerrar }` puede fallar en cada paso (¿no abre?, ¿no hay memoria?, ¿falla la lectura?, ¿no cierra?). En lenguajes sin excepciones habría que anidar `if` tras cada paso; con excepciones, el error se **trata** donde se pueda o se **relanza** a un método superior de la pila.

## 2. La clase Exception y las más comunes
Las excepciones son clases; tienen un constructor vacío y otro con mensaje (`Exception(String mensaje)`). Métodos útiles: `getMessage()` (texto) y `printStackTrace()` (traza de la pila).

| Excepción | Cuándo ocurre |
|---|---|
| `ArithmeticException` | operación aritmética anómala, p. ej. división entera entre 0 |
| `NullPointerException` | acceso a un objeto cuya referencia vale `null` |
| `ArrayIndexOutOfBoundsException` / `IndexOutOfBoundsException` | índice inexistente en un arreglo o lista |
| `ClassCastException` | cast a una clase de la que el objeto no es instancia (`y = (Prueba) x`) |
| `NumberFormatException` | convertir a número una cadena con caracteres no numéricos |
| `IllegalArgumentException` | método llamado con un parámetro erróneo |
| `NegativeArraySizeException` | crear un arreglo con tamaño negativo |
| `NoClassDefFoundError`, `NoSuchFieldError`, `NoSuchMethodError` | clase/campo/método inexistente en ejecución |
| `OutOfMemoryError` | falla `new` por falta de memoria |
| `IOException`, `FileNotFoundException`, `EOFException` | errores de entrada/salida |

Cuando ocurre un error, el método **crea un objeto excepción** (con tipo y estado del programa) y lo entrega al sistema de ejecución (**lanza** la excepción). La JVM recorre la **pila de llamadas** hacia atrás buscando un método con un **manejador** apropiado; si llega a `main` sin encontrarlo, el programa termina con la traza de error.

## 3. Jerarquía: Throwable, Error, Exception
```
Object
 └─ Throwable
     ├─ Error                      (fallos graves de la JVM: StackOverflowError, OutOfMemoryError, VirtualMachineError, AWTError)
     └─ Exception
         ├─ RuntimeException       (no verificadas: ArithmeticException, NullPointerException,
         │                          NumberFormatException, IndexOutOfBoundsException, ClassCastException...)
         ├─ IOException            (verificada: FileNotFoundException, EOFException)
         └─ InterruptedException   (verificada: interrupción de un hilo)
```
- `Error`: no suelen capturarse; el programa no puede recuperarse.
- `RuntimeException` y subclases: excepciones **no verificadas** (unchecked): la gestión **no es obligatoria**.
- El resto de `Exception` son **verificadas** (checked): el compilador exige tratarlas (`try-catch`) o propagarlas (`throws`).
- Solo instancias de `Throwable` pueden lanzarse. Un `Throwable` guarda el estado de la pila de su hilo al crearse. Métodos: `getMessage()`, `printStackTrace()`, `printStackTrace(PrintStream)`, `printStackTrace(PrintWriter)`.

## 4. Tratamiento: try / catch / finally
```java
try {
    // código susceptible de lanzar una excepción
} catch (TipoExcepcion1 e) {
    // tratamiento
} catch (TipoExcepcion2 e) {
    // tratamiento
} finally {
    // se ejecuta SIEMPRE
}
```
- **try**: bloque donde se prevé la excepción; debe ir seguido de al menos un `catch` o un `finally`.
- **catch**: se ejecuta si la excepción coincide con su tipo. Se pueden poner varios, uno por excepción distinta; la JVM los compara **en orden** y ejecuta el primero compatible, luego continúa después de todo el `try-catch`. Los `catch` de subclases deben ir **antes** que los de superclases (si no, el compilador reporta código inalcanzable). No conviene capturar `Exception` de forma genérica "para todo": se esconden errores inesperados; mejor dejar propagar y avisar al usuario.
- **finally**: se ejecuta siempre (haya o no excepción, incluso con `return` o `break` dentro de `try`/`catch`); es opcional salvo que no haya `catch`. Sirve para dejar el programa en estado correcto (cerrar archivos, liberar recursos). Solo uno por `try`.

### Ejemplo de división segura
```java
public static double dividir(int x, int y) {
    try {
        return x / y;                 // si y == 0 lanza ArithmeticException
    } catch (ArithmeticException e) {
        System.out.println("División entre cero");
        return 0;
    } finally {
        System.out.println("fin de dividir");
    }
}
```
Flujos posibles: (a) sin excepción: se ejecuta `try`, luego `finally`; (b) con excepción coincidente: `catch` y luego `finally`; (c) con excepción no capturada: `finally` y la excepción sigue propagándose.

### Ejemplo del PDF: escribirLista
```java
public void escribirLista() {
    PrintWriter out = null;
    try {
        out = new PrintWriter(new FileWriter("out.txt"));
        for (int i = 0; i < SIZE; i++)
            out.println("valor: " + i + " = " + v[i]);
    } catch (ArrayIndexOutOfBoundsException e) {
        System.err.println("Indice fuera de rango");
    } catch (IOException e) {
        System.err.println("out.txt no puede ser abierto");
    } finally {
        if (out != null) out.close();
    }
}
```
El `try` puede terminar de tres formas: (1) `new FileWriter` falla (`IOException`), (2) `v[i]` falla (`ArrayIndexOutOfBounds`) o (3) todo bien. En los tres casos `finally` cierra el flujo. Desde Java 7 existe `try-with-resources` (`try (PrintWriter out = new PrintWriter(...)) {...}`), que cierra automáticamente; no aparece en el PDF.

## 5. Lanzamiento y propagación
Ante una excepción hay que **elegir**: tratarla (`try-catch`) o **lanzarla** hacia el llamador con `throws` en la cabecera:
```java
public void miMetodo() throws IOException, ClassNotFoundException { ... }
```
Si `main` llama a `m1`, `m1` a `m2`, `m2` a `m3` y `m3` lanza `X` sin manejarla, la excepción sube por `m2`, `m1` y `main`; si nadie la trata, el programa termina abruptamente. Se propaga cuando no es lógico tratarla donde se produjo (por ejemplo, un método de utilería no sabe cómo avisar al usuario).

Para **crear y lanzar** una excepción se usa `throw`:
```java
public FileInputStream(File f) throws IOException {
    if (!f.exists()) throw new IOException("No existe el archivo");
}
public void pop() throws EmptyStackException {
    if (size == 0) throw new EmptyStackException();
    ...
}
```
Diferencia: `throws` (con s) **declara**; `throw` **lanza** un objeto.

## 6. Excepciones definidas por el programador
Se crean heredando de `Exception` (verificada) o de `RuntimeException` (no verificada). Por convención tienen dos constructores: uno por defecto y otro con `String`, ambos invocando al padre con `super`.

Ejemplo del PDF: `DivisionPar` (prohíbe dividir por números pares; es un ejemplo didáctico):
```java
class DivisionPar extends Exception {
    public DivisionPar() { super(); }
    public DivisionPar(String msg) { super(msg); }
}
class Calculadora {
    public static double dividir(int x, int y) throws DivisionPar {   // propaga
        if (y % 2 == 0) throw new DivisionPar("No se permite dividir por pares");
        return (double) x / y;
    }
}
// uso
boolean repetir = true;
Scanner in = new Scanner(System.in);
do {
    try {
        System.out.print("x y: ");
        int x = in.nextInt(), y = in.nextInt();
        System.out.println(Calculadora.dividir(x, y));
        repetir = false;
    } catch (DivisionPar e) {
        System.out.println(e.getMessage());     // se vuelve a pedir (bandera = true)
    } catch (InputMismatchException e) {
        System.out.println("Debe escribir enteros"); in.nextLine();
    }
} while (repetir);
```
El método `dividir` declara `throws` porque no tiene sentido mostrar mensajes allí; el llamador decide. La **bandera** `repetir` implementa la repetición hasta que el dato sea válido.

Ejemplo bancario típico (usado en los exámenes): `SaldoInsuficienteException extends Exception` que se lanza en `retirar(monto)` si `monto > saldo`.

## 7. Buenas prácticas
- Capturar excepciones **específicas**.
- No dejar `catch` vacíos (se traga el error); al menos registrar `e.getMessage()`.
- Usar `finally` (o try-with-resources) para liberar recursos.
- Validar entradas antes de provocar la excepción cuando sea barato (por ejemplo, `y != 0`), reservando las excepciones para situaciones realmente excepcionales.
- No usar excepciones como control de flujo normal.

## Ejemplo resuelto: lectura robusta de un entero
```java
static int leerEntero(Scanner in) {
    while (true) {
        try {
            return Integer.parseInt(in.nextLine().trim());
        } catch (NumberFormatException e) {
            System.out.print("Valor inválido, intente de nuevo: ");
        }
    }
}
```
Traza con entrada `abc`, `12`: primera iteración lanza `NumberFormatException` -> catch -> repite; segunda devuelve 12.

## Errores comunes
- `catch (Exception e)` antes de `catch (IOException e)` (error de compilación: inalcanzable).
- Olvidar `throws` en un método que lanza una excepción verificada.
- Confundir `throw` y `throws`.
- Capturar y no hacer nada.
- Cerrar un recurso en el `try` y no en `finally` (si falla antes, queda abierto).
- Suponer que `finally` no se ejecuta tras `return`.

## Ejercicios propuestos
1. Escriba `int dividir(int a, int b)` que lance `IllegalArgumentException` si `b == 0`.
2. Cree `EdadInvalidaException` y úsela en `setEdad`. *(Lanzar si edad < 0 o > 150.)*
3. ¿Qué se imprime? `try { return 1; } finally { System.out.println("F"); }` *(Imprime F y devuelve 1.)*
4. Dibuje la jerarquía de `FileNotFoundException`. *(Throwable > Exception > IOException > FileNotFoundException.)*

## Conexiones
Anterior: [[Programación I - Java C08 Interfaces]]. Siguiente: [[Programación I - Java C10 Archivos en Java]]. Las excepciones se aplican en prácticas como [[Programación I - Java Ejemplos de archivos]] y [[Programación I - Java Proyecto Banco]]. En C++ el mecanismo análogo es `try/catch/throw` (fuera de este material).

## Fuente
`Material/Java/Teoria/TemaIII-C09 GestionErrores.pdf` y la versión `Material/Java/Teoria/UII-C01 GestionErrores .pdf` (contenido equivalente, renumerado como unidad II).
