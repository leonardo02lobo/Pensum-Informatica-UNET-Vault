---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaI-C04 Clases, Objetos y Métodos en Java.pdf
---
# Java C04 - Clases, objetos y métodos

Materia: [[Programación I]]

## Contexto y objetivo
Es la lección central de la Unidad I: cómo se **define una clase**, cómo se **instancian objetos**, qué papel juegan los constructores, los modificadores de acceso, los atributos y métodos (getters/setters), la referencia `this`, el "destructor" (que en Java no existe) y los arreglos de objetos. Incluye cinco prácticas guiadas (Máquina de Boletos, Fractal, Banco) que se documentan aquí. Viene precedida por el paradigma de POO (ver POO en Java - clases, herencia y polimorfismo) y se complementa con [[Programación I - Java C05 Sobrecarga, paso de objetos y modificadores]].

## 1. Clase y objeto
Una **clase** es una plantilla (plano) de la que se crean **instancias** (objetos). Define el *estado* (atributos) y el *comportamiento* (métodos). Un **objeto** es una instancia concreta con identidad y valores propios; los objetos de una misma clase interactúan de forma independiente, y se manejan por **referencia**.

```java
public class Vehiculo {
    // atributos (estado)
    private String make;
    private int milesPerGallon;

    // constructor por defecto
    public Vehiculo() { }

    // mutadores (setters)
    public void setMake(String m) { make = m; }
    public void setMilesPerGallon(int mpg) { milesPerGallon = mpg; }

    // accesadores (getters)
    public String getMake() { return make; }
    public int getMilesPerGallon() { return milesPerGallon; }
}
```
Convenciones: un archivo contiene normalmente **una** clase y se llama como ella (`Vehiculo.java`).

## 2. Constructores
Son métodos especiales que permiten **instanciar** la clase.
- Tienen el **mismo nombre** que la clase y **no tienen tipo de retorno** (ni siquiera `void`).
- Buena práctica: incluir uno **por defecto** (sin parámetros) que inicialice los atributos con valores base, y uno o varios **parametrizados**.
```java
public Vehiculo() { make = ""; milesPerGallon = 0; }
public Vehiculo(String m, int mpg) { make = m; milesPerGallon = mpg; }
```
Si no se escribe ningún constructor, el compilador crea uno por defecto vacío; si se escribe alguno con parámetros, **ya no** se genera el vacío automático.

## 3. Instanciación
Se usa el operador `new`, que reserva memoria en el *heap*, ejecuta el constructor y devuelve la **referencia**:
```java
public class VehiculoTester {
    public static void main(String[] args) {
        Vehiculo a = new Vehiculo();               // por defecto
        Vehiculo b = new Vehiculo("Toyota", 30);   // parametrizado
    }
}
```
`Vehiculo b2 = b;` no copia el objeto: ambas variables apuntan al mismo. Una variable referencia sin `new` vale `null`; usarla provoca `NullPointerException`.

## 4. Definición de métodos
```
<modificador> <static> <final> <synchronized> TipoRetorno nombre(parámetros) { ... }
```
- `static`: método de **clase**, se invoca sin objeto (`Math.abs(x)`).
- `final`: no puede ser redefinido por las subclases.
- `synchronized`: evita interferencia entre hilos sobre el objeto.
- La lista de parámetros son declaraciones separadas por coma. **En Java no existe paso por dirección**: los primitivos se pasan por **valor** y los objetos "por valor de la referencia" (el método recibe una copia de la referencia y puede modificar el objeto apuntado, pero no reasignar la referencia del llamador; ver [[Programación I - Java C05 Sobrecarga, paso de objetos y modificadores]]).
- Un método con tipo de retorno distinto de `void` **debe** terminar con `return valor;`.

## 5. Modificadores de acceso y tipos de clases
Una **clase** puede ser `public` (visible desde cualquier paquete) o *package* (sin modificador: solo visible dentro de su paquete). Un **paquete** es una colección de clases relacionadas. Según su "tipo": `abstract` (no instanciable, base para herencia/polimorfismo) o `final` (no se puede heredar).

Para **atributos y métodos** hay cuatro niveles:
| Modificador | Misma clase | Mismo paquete | Subclase (otro paquete) | Cualquier clase |
|---|---|---|---|---|
| `private` | sí | no | no | no |
| (package) | sí | sí | no | no |
| `protected` | sí | sí | sí | no |
| `public` | sí | sí | sí | sí |

## 6. Atributos
`<modificador> <static> <final> Tipo nombre <= expresión>;` Pueden ser primitivos u objetos de otra clase.
- `static`: un único valor compartido por todos los objetos (atributo de clase). Ej.: `System.out`.
- `final`: constante, no cambia tras su inicialización. `Math.PI` es `static final`.

## 7. Esquema de trabajo y encapsulamiento
Esquema recomendado: **atributos privados y métodos públicos**. Los privados solo son accesibles desde dentro de la clase (incluido su `main`), por lo que desde otra clase (`Principal`) hay que usar métodos públicos (por ejemplo `setValores`). Ejemplo del PDF con `Rectangulo` (x, y, ancho, alto, `desplazar(int,int)`):
- Dentro de `Rectangulo.main` se puede acceder a todo.
- Desde `Principal`, `r.ancho = 5;` o `r.desplazar(1,1)` (si es privado) **no compila**; si `desplazar` se cambia a `public`, sí.

Esto es **encapsulamiento**: se oculta el estado y se expone una interfaz controlada, lo que permite validar (por ejemplo, impedir un saldo negativo).

### Getters y setters
```java
public int getPrecio() { return precio; }          // accesador
public void setPrecio(int valor) { precio = valor; } // mutador
```

## 8. Destructor y recolector de basura
Java no tiene destructores como C++ (ver [[Programación I - C++ C03 POO en C++]]): cuando un objeto pierde todas sus referencias, el *garbage collector* libera su memoria en un momento no determinado. Existía `finalize()`, hoy desaconsejado.

## 9. La referencia `this`
Dentro de un método de instancia o constructor, `this` es la referencia al objeto actual. Se usa sobre todo cuando un parámetro **sombrea** un atributo:
```java
public class Point {
    private int x, y;
    public Point(int x, int y) { this.x = x; this.y = y; }
}
```
También sirve para encadenar constructores: `this(0, 0);` (debe ser la primera instrucción) y para pasar el objeto actual como argumento.

## 10. Vector (arreglo) de objetos
Se declara el arreglo y luego **cada posición** debe crearse con `new`; antes valen `null`:
```java
Vehiculo[] flota = new Vehiculo[3];
for (int i = 0; i < flota.length; i++) flota[i] = new Vehiculo();
flota[0].setMake("Ford");
System.out.println(flota[0].getMake());
```
Acceso a miembros: `vector[indice].atributo` / `vector[indice].metodo()`.

## 11. Pase de mensajes
Los objetos colaboran invocando métodos de otros. El PDF muestra un proyecto "Figuras" con `Circulo`, `Cuadro` y `Rectangulo` como clases que reciben mensajes (llamadas a métodos) desde una clase principal. Un mensaje = objeto receptor + nombre del método + argumentos.

## 12. Prácticas de laboratorio de la lección
**Práctica 01-03 - Máquina de Boletos Simple.** Se estudia una clase `MaquinaBoletos` con precio, saldo y total. Preguntas del enunciado y respuestas conceptuales:
- *¿Se puede imprimir el boleto sin completar el precio?* En la versión simple no se valida: es una debilidad que motiva validar en el método.
- *¿Se devuelve la diferencia si se paga de más?* No; la versión simple no calcula vuelto.
- *Dos máquinas*: cada objeto tiene su propio saldo y total; lo recaudado entre ambas es la suma de ambos `total`.
- *Atributo de clase:* en la versión simple no hay `static`; sería necesario para un total global.
- Ejercicios: escribir `getTotal()`, `setPrecio(int)` y `descontar(int monto)`:
```java
public void descontar(int monto) { precio = precio - monto; }
```
Quitar el `return` de `getPrecio()` produce el error de compilación *missing return statement*; `imprimirBoleto` e `insertarDinero` no retornan porque son `void` (realizan una acción).
**Práctica 02**: en `private int contador;` el modificador es `private`, tipo `int`, nombre `contador`; `protected Estudiante representado;` -> `protected`, `Estudiante`, `representado`; `public final PI;` es incorrecto (falta tipo). La declaración de un atributo **sí** termina en `;`. Atributo entero `estado`: `private int estado;`.

**Práctica 04 - Fractal.** Proyecto con paquetes `gráfico` (clases `Fractal`, `Ventana`) y `números` (clase `Complejo`). Se debe completar `Complejo` (aritmética de números complejos: suma, producto, módulo) para que compile y pintar un fractal (conjunto de Mandelbrot: iterar $z_{n+1}=z_n^2+c$ y ver si $|z|$ escapa de 2). Demuestra uso de **paquetes e import** y clases que colaboran.
```java
public class Complejo {
    private double re, im;
    public Complejo(double re, double im) { this.re = re; this.im = im; }
    public Complejo sumar(Complejo o) { return new Complejo(re + o.re, im + o.im); }
    public Complejo multiplicar(Complejo o) {
        return new Complejo(re*o.re - im*o.im, re*o.im + im*o.re);
    }
    public double modulo() { return Math.sqrt(re*re + im*im); }
}
```
(Fragmento ilustrativo del tipo de método esperado; el enunciado solo pide completar la clase.)

**Práctica 05 - Banco.** Clase `Cuenta` (cliente, cuenta, saldo; getters/setters; constructor parametrizado; `depositar`/`retirar` con validación; `mostrarEstadoCuenta`) y clase `Banco` con un vector (o `ArrayList`) de `Cuenta`, nombre de la entidad y un menú: 1 Abrir cuenta, 2 Consultar, 3 Depósito, 4 Retiro, 5 Salir, con método `iniciar()` que controla el ciclo. Diagrama de clases: `Banco` 1 --- 0..* `Cuenta` (asociación de composición/agregación). Se desarrolla con detalle en [[Programación I - Java Proyecto Banco]] y [[Programación I - Java Ejercicios C04 y práctica C06]].

## Ejemplo resuelto: clase Cuenta mínima
```java
public class Cuenta {
    private String cliente, numero;
    private double saldo;
    public Cuenta(String cliente, String numero, double saldo) {
        this.cliente = cliente; this.numero = numero; this.saldo = saldo;
    }
    public void depositar(double m) { if (m > 0) saldo += m; }
    public boolean retirar(double m) {
        if (m > 0 && m <= saldo) { saldo -= m; return true; }
        return false;
    }
    public double getSaldo() { return saldo; }
}
```
Traza: `Cuenta c = new Cuenta("Ana","001",100); c.depositar(50); c.retirar(200);` -> saldo 150, el retiro devuelve `false`.

## Errores comunes
- Declarar un tipo de retorno en el constructor (se convierte en un método normal y no se llama al instanciar).
- Olvidar `new` al llenar un arreglo de objetos (`NullPointerException`).
- Intentar acceder a un miembro `private` desde otra clase.
- Esperar que `b = a` copie el objeto.
- No usar `this` cuando el parámetro tiene el mismo nombre que el atributo (la asignación `x = x` no hace nada útil).

## Ejercicios propuestos
1. Escriba la clase `Rectangulo` con `area()` y `perimetro()`, atributos privados y validación (lados > 0).
2. Cree un arreglo de 5 `Cuenta` y calcule el saldo promedio.
3. Añada a `Vehiculo` un atributo `static int contador` que cuente cuántos vehículos se han creado. *(Incrementarlo en cada constructor.)*
4. Explique por qué `Math.abs(-3)` no requiere objeto. *(Es `static`.)*

## Conexiones
Anterior: [[Programación I - Java C02 Entrada salida y control de flujo]]. Siguiente: [[Programación I - Java C05 Sobrecarga, paso de objetos y modificadores]]. Diagramas de clases: [[Programación I - C++ C10 Introducción a diagramas de clases]], [[IS 04 - Modelado con UML]].

## Fuente
`Material/Java/Teoria/TemaI-C04 Clases, Objetos y Métodos en Java.pdf`.
