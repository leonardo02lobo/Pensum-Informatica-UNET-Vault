---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaI-C05 Sobrecarga de metodos, Paso de objetos y modificadores.pdf
---
# Java C05 - Sobrecarga, paso de objetos, varargs y static

Materia: [[Programación I]]

## Contexto y objetivo
Completa la base de clases de [[Programación I - Java C04 Clases, objetos y métodos]]. Se estudian seis temas: sobrecarga de constructores, sobrecarga de métodos, paso de objetos como parámetros, devolución de objetos, argumentos variables y el modificador `static` en atributos y métodos. Son los cimientos del polimorfismo estático (en tiempo de compilación) y de la distinción entre miembros de instancia y de clase.

## 1. Sobrecarga (overloading)
**Sobrecargar** es definir varios constructores o métodos con el **mismo nombre** pero **distinta firma**, es decir, distinto número y/o tipo (u orden de tipos) de parámetros. El tipo de retorno **no** forma parte de la firma: dos métodos que solo difieren en el retorno no son una sobrecarga válida (error de compilación).

### Sobrecarga de constructores
```java
public class Perro {
    private int peso;
    private int volumen;
    private String tipoLadrido;

    public Perro() { peso = 12; volumen = 4; tipoLadrido = "Woof"; }
    public Perro(int w, int l) { peso = w; volumen = l; tipoLadrido = "ARF!"; }
    public Perro(int w, int l, String bark) { peso = w; volumen = l; tipoLadrido = bark; }
}
```
Cómo resuelve Java la llamada: al ver `new Perro(...)`, busca entre los constructores del mismo nombre el que coincide en número y tipos de argumentos; si ninguno coincide **no compila**. Con conversión automática elige el más específico (p. ej. `new Perro(5, 'a')`: `char` se amplía a `int`).

Reglas importantes:
- Si no se escribe ningún constructor, la JVM/compilador proporciona uno por defecto vacío.
- Si se escribe al menos uno con parámetros, el constructor por defecto **no** se genera: hay que declararlo si se necesita.
- Un constructor puede llamar a otro con `this(...)` para evitar repetir código:
```java
public Perro() { this(12, 4, "Woof"); }
```

### Sobrecarga de métodos
```java
public void ladrar(String b) { System.out.println(b); }
public void ladrar()         { System.out.println(tipoLadrido); }
```
Ejemplos de la API estándar: `System.out.println` tiene versiones para `int`, `double`, `String`, `char[]`, `Object`...; `Math.abs` para `int`, `long`, `float`, `double`.

## 2. Objetos como parámetros
Un parámetro es una variable declarada en la cabecera del método que recibe un valor al invocarlo. Pueden ser primitivos u objetos (`String`, arreglos, clases propias):
```java
public int metodo(int a, double b, String c, MiClase d)
```
### Semántica de paso
Java **siempre pasa por valor**:
- Con **primitivos** se copia el valor; modificar el parámetro no afecta al original.
- Con **objetos** se copia la **referencia**; el método puede modificar el estado del objeto (los dos apuntan al mismo), pero si reasigna el parámetro (`p = new Punto()`), el llamador no lo ve.

```java
static void incrementa(int n) { n++; }                 // no afecta al original
static void mueve(Punto p) { p.x++; }                  // sí afecta al objeto
static void reemplaza(Punto p) { p = new Punto(0,0); } // no afecta a la variable del llamador

int a = 5; incrementa(a);          // a sigue valiendo 5
Punto q = new Punto(1,1);
mueve(q);                          // q.x == 2
reemplaza(q);                      // q sigue apuntando al objeto anterior
```
El paso de objetos facilita acceder a la información del objeto y permite modificarlo dentro del método (por ejemplo, `Banco.transferir(Cuenta origen, Cuenta destino, double monto)`).

## 3. Devolución de objetos
Es análoga a devolver un primitivo, solo que el tipo de retorno es una clase:
```java
public Complejo sumar(Complejo o) { return new Complejo(re + o.re, im + o.im); }
```
Se devuelve la **referencia**; si se devuelve un atributo mutable (por ejemplo un `ArrayList` interno) el llamador podría modificar el estado interno (rompiendo el encapsulamiento): conviene devolver una copia.

## 4. Argumentos variables (varargs)
Un método que acepta una cantidad variable de argumentos del **mismo tipo**:
```java
public int total(int... nums) {
    int sum = 0;
    for (int i = 0; i < nums.length; i++) sum += nums[i];
    return sum;
}
total();            // 0
total(4);           // 4
total(1, 2, 3, 4);  // 10
```
Internamente `nums` es un arreglo `int[]`. Ventaja: no hace falta crear y llenar un arreglo antes de llamar, y se pueden hacer llamadas con distinta cantidad de elementos. Restricciones: debe ser el **último** parámetro y solo puede haber uno por método.

## 5. El modificador `static`
Con variables de instancia, cada objeto creado con `new` tiene su propia copia. `static` cambia la asociación: el elemento pertenece a la **clase**, no a las instancias, y es compartido por todas.

```java
public class Empleado {
    private String apellido;
    private String nombre;
    private static String miCompania = "Oracle";   // una sola copia
}
Empleado e1 = new Empleado("Smith", "Mary");
Empleado e2 = new Empleado("Jones", "Sally");
// e1 y e2 tienen cada uno su apellido y nombre, pero comparten miCompania
```
Esquema de memoria:
```
 e1: apellido=Smith, nombre=Mary  \
                                   > comparten  miCompania = "Oracle"
 e2: apellido=Jones, nombre=Sally /
```

### Atributos estáticos (variables de clase)
- Una sola copia en memoria; mismo valor para todas las instancias.
- Si son `public`, cualquier clase puede modificarlas; para evitar cambios se declaran `static final` (constantes: `Math.PI`).
- Típicos usos: contadores de instancias, constantes, configuración global.

### Métodos estáticos (de clase)
- Existen una sola vez; se invocan con `NombreClase.metodo()` (no hace falta un objeto): `Math.sqrt(9)`.
- Solo pueden acceder directamente a **atributos estáticos** y a **otros métodos estáticos**: no tienen `this`, así que no saben a qué objeto se refieren.
- Pueden ser `public`, `protected`, de paquete o `private`.
- `main` es `static` precisamente para que la JVM lo invoque sin crear ningún objeto.

Ejemplo del PDF (clase `Tortuga`): una variable estática `numTanks` cuenta los tanques disponibles y una variable de instancia `tankNum` indica en qué tanque está cada tortuga. Un contador estático:
```java
public class Tortuga {
    private static int numTanks = 0;     // compartido
    private int tankNum;                 // propio
    public Tortuga() { tankNum = ++numTanks; }
    public static int getNumTanks() { return numTanks; }
}
new Tortuga(); new Tortuga();
System.out.println(Tortuga.getNumTanks());   // 2
```
Nota: el PDF afirma que los métodos estáticos "se pueden redefinir en subclases"; en rigor se **ocultan** (method hiding), no se sobrescriben con enlace dinámico (ver [[Programación I - Java C07 Polimorfismo y clases abstractas]]).

## Ejemplo resuelto: sobrecarga + varargs + static
```java
public class Calc {
    private static int usos = 0;
    public static int suma(int a, int b)       { usos++; return a + b; }
    public static double suma(double a, double b) { usos++; return a + b; }
    public static int suma(int... v) { usos++; int s = 0; for (int x : v) s += x; return s; }
}
Calc.suma(2, 3);        // 5      (elige suma(int,int))
Calc.suma(2.5, 3);      // 5.5    (int -> double: suma(double,double))
Calc.suma(1,2,3,4);     // 10     (varargs)
```
Orden de resolución: primero coincidencia exacta, luego ampliación de tipos, y varargs al final.

## Errores comunes
- Creer que cambiar solo el tipo de retorno sobrecarga un método.
- Acceder a un atributo de instancia desde un método `static` (`non-static variable cannot be referenced from a static context`).
- Pensar que Java pasa objetos "por referencia": se pasa la referencia por valor.
- Olvidar escribir el constructor por defecto después de crear uno parametrizado.
- Modificar una constante `static final` (no compila).

## Ejercicios propuestos
1. Sobrecargue `area` en `Figuras` para círculo (radio), rectángulo (base, altura) y triángulo (3 lados con Herón: $A=\sqrt{s(s-a)(s-b)(s-c)}$, $s=(a+b+c)/2$).
2. Escriba `static double promedio(double... notas)`. *(Dividir la suma entre `notas.length`; considerar el caso vacío.)*
3. Prediga la salida: `static void f(int[] v){ v[0]=9; v=new int[]{7}; }` llamado con `int[] a={1,2}; f(a); System.out.println(a[0]);`. *(Imprime 9.)*
4. Añada a `Cuenta` un contador estático del número total de cuentas abiertas.

## Conexiones
Anterior: [[Programación I - Java C04 Clases, objetos y métodos]]. Siguiente: [[Programación I - Java C06 Herencia]]. En C++ el equivalente a la sobrecarga también incluye operadores (ver [[Programación I - C++ C03 POO en C++]]).

## Fuente
`Material/Java/Teoria/TemaI-C05 Sobrecarga de metodos, Paso de objetos y modificadores.pdf`.
