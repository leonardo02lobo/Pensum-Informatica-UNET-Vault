---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaII-C07 Polimorfismo y Clases Abstractas.pdf
---
# Java C07 - Polimorfismo y clases abstractas

Materia: [[Programación I]]

## Contexto y objetivo
El **polimorfismo** ("muchas formas") es uno de los pilares de la POO junto con encapsulamiento y herencia. Esta lección define el polimorfismo, distingue sus dos modalidades (basado en herencia y en sobrecarga), estudia *upcasting*, *downcasting*, invalidación de métodos, enlace dinámico, argumentos polimórficos y `instanceof`, y termina con **clases y métodos abstractos**. Cierra con un ejercicio práctico bancario que muestra cómo herencia + polimorfismo + abstracción producen un diseño flexible ([[Programación I - Java Proyecto Banco]]).

## 1. Definición
Polimorfismo: *mecanismo que permite definir e invocar funciones idénticas en nombre e interfaz pero con implementación diferente*. Se pueden definir varias clases con funcionalidad distinta, pero con métodos denominados igual, que el código cliente usa de manera intercambiable **en tiempo de ejecución**.

| Tipo | Se resuelve | En Java se logra con |
|---|---|---|
| Estático (ad hoc) | compilación | **sobrecarga** de métodos/constructores |
| Dinámico (de subtipos) | ejecución | herencia, clases abstractas e interfaces + **sobreescritura** |

## 2. Polimorfismo basado en herencia
Como una subclase **"es un"** tipo de su superclase, un objeto de la subclase puede referenciarse con una variable de la superclase:
```java
Bicicleta bike = new RoadBike();
```
El **tipo de la variable** (estático) no determina el **tipo del objeto** (dinámico). Analogía de las muñecas rusas: desde afuera se ve la muñeca grande (el tipo de la referencia), pero dentro hay una más pequeña (el objeto real); el compilador no mira dentro, la JVM sí lo hace al ejecutar.

### Colecciones heterogéneas
```java
Formas[] figuras = new Formas[10];
figuras[0] = new Circulo();
figuras[1] = new Triangulo();
figuras[2] = new Rectangulo();
for (Formas f : figuras) if (f != null) f.mensaje();   // cada una responde a su manera
```

### Upcasting (generalización)
Interpretar un objeto hijo como del tipo padre. Es automático y siempre seguro:
```java
Formas figura1 = new Circulo();
```
Con `figura1` solo se pueden usar los miembros declarados en `Formas`; si `Circulo` redefine un método de `Formas`, se ejecutará la versión de `Circulo`.

### Downcasting (especialización)
Convertir una referencia de tipo padre al tipo hijo; requiere **cast explícito** y es válido solo si el objeto real es de esa clase (si no, `ClassCastException`):
```java
Formas figura1 = new Circulo(10);
Circulo cir1 = (Circulo) figura1;
cir1.setRadio(50);          // ahora sí accesible
```

### Invalidación (sobreescritura) de métodos
Redefinir en la subclase un método con **mismo nombre, tipo de retorno y parámetros**, cambiando solo la lógica. La versión del padre queda oculta salvo que se invoque con `super`. Ejercicio de la lección: crear en `Formas` y en `Circulo` un método `mensaje()` que imprime el nombre de la clase:
```java
public class Formas {
    protected String color;
    public void mensaje() { System.out.println(this.getClass().getName()); }
    public void setColor(String c) { color = c; }
}
public class Circulo extends Formas {
    private float radio;
    @Override public void mensaje() { System.out.println(this.getClass().getName()); }
    public void setRadio(float r) { radio = r; }
}
// main:
Formas figura = new Circulo();
figura.mensaje();     // imprime "Circulo": se usa el método del OBJETO real
figura.setColor("Verde");   // OK: está en Formas
// figura.setRadio(20);     // ERROR de compilación: Formas no tiene setRadio
```
Observación clave: `this.getClass().getName()` devuelve la clase **real** del objeto, no la de la variable; por eso el mismo código en `Formas` ya imprimiría "Circulo" si no se sobrescribiera.

### Enlace (distribución) dinámico
Java decide **en ejecución** qué versión del método invocar según el tipo real del objeto (*dynamic binding / late binding*). El compilador solo verifica que el método exista en el **tipo de la referencia**; la JVM elige la implementación según el **objeto**. Por eso `figura.setColor("Verde")` compila y `figura.setRadio(20)` no, aunque el objeto sea un `Circulo`: para llamarlo hace falta downcasting.

### Argumentos polimórficos
```java
public class Instrumento { public void tocar() { System.out.print("Instrumento.tocar()"); } }
class Guitarra extends Instrumento { public int nro_cuerdas; public void tocar() { System.out.println("Guitarra.tocar()"); } }
class Guzla extends Guitarra { public String tono; public void tocar() { System.out.println("Guzla.tocar()"); } }

public class Implementacion {
    public void afinar(Instrumento i) { i.tocar(); }          // acepta cualquier subtipo
    public void afinarTodo(Instrumento[] e) { for (Instrumento x : e) afinar(x); }
    public static void main(String[] a) {
        Instrumento[] orquesta = { new Guitarra(), new Guzla() };
        new Implementacion().afinarTodo(orquesta);   // Guitarra.tocar() / Guzla.tocar()
    }
}
```
Se puede agregar un nuevo instrumento (`Violin extends Instrumento`) sin tocar `afinar`: es el **principio abierto/cerrado**.

### instanceof y casting de objetos
Cuando hace falta una operación exclusiva de la subclase, se verifica el tipo real antes del cast:
```java
public void afinar(Instrumento i) {
    if (i instanceof Guzla) {          // preguntar primero por la más específica
        Guzla g = (Guzla) i; g.tono = "re"; g.tocar();
    } else if (i instanceof Guitarra) {
        Guitarra gt = (Guitarra) i; gt.nro_cuerdas = 5; gt.tocar();
    } else i.tocar();
}
```
Nota: como `Guzla extends Guitarra`, un objeto `Guzla` también es `instanceof Guitarra`; por eso el orden de las preguntas importa (el PDF pregunta primero por `Guitarra`, lo que hace inalcanzable la rama `Guzla`; es una trampa a evitar). Abusar de `instanceof` indica un mal diseño: casi siempre se resuelve mejor con un método polimórfico.

### Ejemplo de dominio: ajedrez
El diagrama de clases del ajedrez (Partida, Jugador, Tablero, Casilla, Pieza con subclases Peón, Torre, Caballo, Alfil, Rey, Reina) muestra que `Pieza` declara `puedeMover(destino)`, `puedeCapturar(destino)` y `movimientosPosibles()`, y la implementación depende de cada tipo de pieza: polimorfismo puro.

## 3. Polimorfismo por sobrecarga
Varios métodos con el mismo nombre y distinta lista de parámetros:
```java
public class Sumar {
    public float suma(float a, float b) { System.out.println("Estoy sumando reales"); return a + b; }
    public int suma(int a, int b)       { System.out.println("Estoy sumando enteros"); return a + b; }
}
```
(El PDF declara `float x = 1, float y = 2;`, lo cual no compila: correcto es `float x = 1, y = 2;`.) También aplica a constructores (`Rectangulo(x1,y1,x2,y2)` y `Rectangulo()`), con área $=(x_2-x_1)(y_2-y_1)$. Ver [[Programación I - Java C05 Sobrecarga, paso de objetos y modificadores]].

## 4. Clases abstractas
¿Para qué definir `Formas` si solo se crean `Circulo`, `Triangulo` y `Rectangulo`? Una **clase abstracta** no se puede instanciar, pero sí se pueden declarar **referencias** de ese tipo que apunten a objetos de sus subclases:
```java
public abstract class Formas { ... }
Formas x = new Formas();     // ERROR
Formas y = new Circulo();    // OK
```
Puede contener métodos totalmente implementados (heredados por las hijas), parcialmente implementados y **métodos abstractos** (solo prototipo, sin cuerpo): `public abstract void mostrarArea();`.

Reglas:
- Un método abstracto no tiene cuerpo, debe estar en una clase abstracta y debe ser **sobreescrito** en las subclases concretas.
- Si una clase tiene al menos un método abstracto, debe declararse `abstract`. Lo recíproco no es necesario: una clase abstracta puede no tener métodos abstractos.
- Una subclase de una clase abstracta debe implementar **todos** los métodos abstractos o declararse también abstracta.
- No existen constructores abstractos ni métodos `static abstract` (ni `final abstract`/`private abstract`, por contradicción semántica).
- Sí puede tener constructor (lo invocan las hijas con `super(...)`), atributos y métodos concretos.
- Una clase que no es abstracta se llama **concreta**.

```java
public abstract class Figura {
    protected double x, y;
    public Figura(double i, double j) { x = i; y = j; }
    public abstract void mostrar_area();
}
public class Triangulo extends Figura {
    public Triangulo(double b, double h) { super(b, h); }
    public void mostrar_area() { System.out.println("Area de triangulo=" + (x * y * 0.5)); }
}
public class Rectangulo extends Figura {
    public Rectangulo(double b, double h) { super(b, h); }
    public void mostrar_area() { System.out.println("Area de rectangulo=" + (x * y)); }
}
```
(En el PDF las subclases omiten el constructor; en la práctica es necesario porque `Figura` solo tiene un constructor con parámetros.)

Otro ejemplo del PDF: `Figura` con `area()` y `volumen()` que devuelven 0.0 por defecto y `devolverNombre()` abstracto. Sirve de base para figuras 2D (que no redefinen `volumen`) y 3D.

## 5. Ejercicio práctico: sistema bancario (evolución del diseño)
Enunciado: un banco controla cuentas de clientes (corriente o de ahorros) con las opciones 1 Crear cuenta, 2 Consultar cuenta, 3 Realizar transacción, 4 Salir. El PDF muestra una **secuencia de diseños** cada vez mejor:
1. **Diseño ingenuo**: `Banco` 1..* `Cuenta` con `retirar` y `depositar`; no distingue tipos de cuenta.
2. **Nuevo requisito**: cada cuenta lleva el registro de transacciones; en la corriente solo se permiten Depósito y Cobro de cheque, en la de ahorros Depósito y Retiro. Se añade un atributo `tipo:int` en `Cuenta` y `Transaccion(tipo, monto)`.
3. **Fallas**: `realizarTransaccion` necesita condicionales por tipo de cuenta; `getMonto` necesita condicionales (retiro/cheque negativo, depósito positivo); agregar nuevos tipos obliga a modificar mucho código.
4. **Solución con herencia y polimorfismo**: `Transaccion` abstracta (método `getMonto()` y `mostrar()` abstractos) con hijas `Deposito` y `Retiro` (y `Cheque`); `Cuenta` abstracta con `addTransaccion(t)` y `mostrarEstadoCuenta()` abstractos, e hijas concretas `CuentaCorriente` y `CuentaAhorros` que aplican **solo las restricciones de su tipo**. Cada clase concreta implementa el método abstracto heredado. En UML, los nombres de clase y de método en **cursiva** indican abstracto.
Resultado: el modelo es abierto a modificaciones. Esta es exactamente la estructura del código `ProyectoBanco` documentado en [[Programación I - Java Proyecto Banco]].

## Ejemplo resuelto: figuras polimórficas
```java
abstract class Forma { abstract double area(); public String toString(){ return getClass().getSimpleName()+": "+area(); } }
class Circulo extends Forma { double r; Circulo(double r){this.r=r;} double area(){ return Math.PI*r*r; } }
class Cuadro  extends Forma { double l; Cuadro(double l){this.l=l;}  double area(){ return l*l; } }
Forma[] v = { new Circulo(1), new Cuadro(2) };
double total = 0; for (Forma f : v) total += f.area();   // pi + 4 = 7.14159...
```
El `for` no sabe qué hay en cada posición; el enlace dinámico selecciona `area()` correcto.

## Errores comunes
- Intentar `new` de una clase abstracta.
- Llamar a un método exclusivo de la subclase con una referencia de la superclase (error de compilación).
- Downcast sin verificar con `instanceof` (`ClassCastException`).
- Confundir sobrecarga (compilación) con sobreescritura (ejecución).
- Olvidar implementar algún método abstracto en la subclase concreta.
- Acceder a atributos por la referencia esperando polimorfismo: **los atributos no son polimórficos**, solo los métodos de instancia.

## Ejercicios propuestos
1. Diseñe `Empleado` abstracta con `calcularPago()` abstracto e hijas `Asalariado` y `PorHoras`; calcule la nómina de un arreglo.
2. ¿Qué imprime `Instrumento i = new Guzla(); i.tocar();`? *(`Guzla.tocar()`)*
3. ¿Es válido `abstract static void f();`? *(No.)*
4. Extienda el sistema bancario con `CuentaNomina` sin modificar `Banco`.

## Conexiones
Anterior: [[Programación I - Java C06 Herencia]]. Siguiente: [[Programación I - Java C08 Interfaces]]. En C++ el polimorfismo requiere `virtual`: [[Programación I - C++ C05 Polimorfismo]]. Ver también [[Programación I - Java C04 Clases, objetos y métodos]].

## Fuente
`Material/Java/Teoria/TemaII-C07 Polimorfismo y Clases Abstractas.pdf`.
