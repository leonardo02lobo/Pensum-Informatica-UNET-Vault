---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaI-C06 Herencia.pdf
---
# Java C06 - Herencia

Materia: [[Programación I]]

## Contexto y objetivo
La **herencia** permite construir clases nuevas a partir de otras ya existentes, reutilizando su código. Esta lección cubre superclases y subclases, `extends`, la regla de herencia única, la composición ("tiene un"), el papel de los constructores y de `super`, la palabra `final` y la sobreescritura de métodos. Es el prerrequisito directo de [[Programación I - Java C07 Polimorfismo y clases abstractas]].

## 1. Concepto
Heredar es recibir de un predecesor: la subclase obtiene los atributos y métodos (no privados) de la superclase y puede añadir otros propios o redefinir los heredados. Beneficios:
- **Reutilización de código ya implementado** (se escribe una vez).
- **Reutilización de código ya probado** (menos depuración, menos errores).
- Modelado natural de jerarquías **general -> especializado**.

| Superclase (padre, base) | Subclase (hija, derivada) |
|---|---|
| Clase más general; contiene lo común | Clase más específica; hereda de la superclase |
| Sus miembros pasan a todas las subclases | Puede añadir atributos y métodos propios |

## 2. La palabra clave `extends`
```java
class Empleado {
    protected String nombre;
    protected int sueldo;
    Empleado(String nombre, int sueldo) { this.nombre = nombre; this.sueldo = sueldo; }
    public void aumentarSueldo(int porcentaje) { sueldo += (int)(sueldo * porcentaje / 100); }
    public void mostrar() {
        System.out.println("nombre: " + nombre);
        System.out.println("Sueldo: " + sueldo);
    }
}
class Ejecutivo extends Empleado {
    public int presupuesto;
    void asignarPresupuesto(int p) { presupuesto = p; }
}
```
Un `ObjEjecutivo` tiene `nombre`, `sueldo`, `aumentarSueldo`, `mostrar` (heredados) más `presupuesto` y `asignarPresupuesto`.

### Relación "es un" y regla de la herencia única
Un `Ejecutivo` **ES UN** `Empleado`, pero no al revés:
```java
Empleado objEmp = new Empleado("Esteban Chacon", 100);
objEmp.asignarPresupuesto(5000);   // ERROR: Empleado no tiene ese método
```
Java solo permite **herencia simple** de clases: `class Rectangulo extends Formas, Figuras` no compila. Como las superclases transmiten todo a sus descendientes (y a los descendientes de estos), una cadena de herencia suele bastar; la necesidad de "múltiples tipos" se cubre con interfaces ([[Programación I - Java C08 Interfaces]]). Todas las clases heredan, directa o indirectamente, de `java.lang.Object` (que aporta `toString()`, `equals()`, `hashCode()`...).

## 3. Ejemplos de jerarquías (diagramas de clases)
- **Red social**: la clase padre `Publicacion` (usuario, fechaHora, meGustan, comentarios; métodos `meGusta`, `noMeGusta`, `addComentario`, `mostrar`) agrupa lo común; `PublicacionMensaje` (mensaje) y `PublicacionFoto` (archivo, titulo) heredan de ella. Los objetos de las hijas **también son** objetos de tipo `Publicacion`. Resuelve la duplicación de código.
- **Vehículos**: `Vehiculo` (nroPuestos, placa) con hijas `Particular` (nroPuertas, dueño) y `Carga` (tara, capacidadCarga, `cargar(kilos)`); cada hija redefine `caracteristicas()`.
- **Figuras**: `Figura` (colorLinea, tipoLinea, x, y; `mover`, `rotar`, `pintar`) con hijas `SinDimensiones` (`Punto`), `UnaDimension` (`Linea`, `Arco`) y `DosDimensiones` (`Circulo`, `Poligono`). Una clase hija puede ser a su vez padre de otras: esto forma una **jerarquía de herencia**.
Estos diagramas se dibujan con UML (flecha con triángulo vacío hacia la superclase); ver [[Programación I - C++ C10 Introducción a diagramas de clases]].

## 4. Composición ("tiene un")
No toda relación es herencia. Cuando un objeto **contiene** instancias de otras clases se habla de composición (relación "tiene un"):
```java
public class Rueda { private int tamanho; private String marca; public Rueda() {} }
public class Auto {
    private String placa;
    private Rueda[] ruedas = new Rueda[4];
    public Auto() { for (int i = 0; i < ruedas.length; i++) ruedas[i] = new Rueda(); }
}
```
Criterio: usar herencia cuando "A es un B" (Ejecutivo es un Empleado); composición cuando "A tiene un B" (Auto tiene Ruedas). Regla práctica: *favorecer la composición sobre la herencia* cuando no hay una relación "es un" clara.

## 5. Constructores en la herencia
- Los constructores **no se heredan**.
- La subclase puede escribir los suyos o usar el predeterminado (si no declara ninguno, se le da uno sin argumentos; si declara alguno, ya no).
- Para inicializar la parte heredada se usa `super(...)`, que invoca el constructor del padre y **debe ser la primera sentencia**:
```java
public class Formas {
    private String color;
    public Formas() { color = ""; }
    public Formas(String c) { color = c; }
}
public class Rectangulo extends Formas {
    private int ancho, alto;
    public Rectangulo(String color, int ancho, int alto) {
        super(color);               // inicializa el atributo privado del padre
        this.ancho = ancho; this.alto = alto;
    }
}
```
Si el constructor de la hija no contiene `this(...)` ni `super(...)`, el compilador inserta **`super()`** implícito. Si el padre solo tiene constructores con parámetros y ninguno por defecto, esto produce **error de compilación**. El orden de ejecución es siempre de arriba hacia abajo: primero el constructor de la superclase, luego el de la subclase.

## 6. `super` para métodos y atributos
`super.metodo()` invoca la versión del padre; permite **extender** (no reemplazar) el comportamiento:
```java
public class Ejecutivo extends Empleado {
    public int presupuesto;
    @Override
    public void mostrar() {
        super.mostrar();                              // nombre y sueldo
        System.out.println("Presupuesto: " + presupuesto);
    }
}
```
Se puede llegar a miembros de cualquier superclase de la cadena, no solo la inmediata (mediante la cadena de `super`).

## 7. Sobreescritura (overriding)
Una subclase puede redefinir un método heredado con **mismo nombre, mismo tipo de retorno y misma lista de argumentos** pero distinto cuerpo. Diferencias con la sobrecarga:
| Sobrecarga | Sobreescritura |
|---|---|
| Misma clase (o jerarquía), **distinta** firma | Subclase, **misma** firma |
| Se resuelve en compilación | Se resuelve en ejecución (enlace dinámico) |
Reglas: no puede reducir la visibilidad (si el padre es `public`, la hija también), no puede sobrescribir métodos `final`, `static` ni `private`. Se recomienda `@Override` para que el compilador detecte errores de firma.

## 8. `final` en la herencia
- Clase `final`: no puede tener subclases (`String`, `Math`). Sus métodos son implícitamente finales.
- Método `final`: no se puede sobrescribir.
- Atributo `final`: constante.

## Ejemplo resuelto
```java
class Vehiculo {
    protected String placa;
    Vehiculo(String placa) { this.placa = placa; }
    String caracteristicas() { return "Placa " + placa; }
}
class Carga extends Vehiculo {
    private int tara;
    Carga(String placa, int tara) { super(placa); this.tara = tara; }
    @Override String caracteristicas() { return super.caracteristicas() + ", tara " + tara; }
}
public class Demo {
    public static void main(String[] a) {
        Vehiculo v = new Carga("AB123", 2000);   // un Carga ES UN Vehiculo
        System.out.println(v.caracteristicas()); // Placa AB123, tara 2000  (enlace dinámico)
    }
}
```
Se ve la cadena: `new Carga` -> `Vehiculo(placa)` -> `Carga(tara)`, y la llamada ejecuta la versión de `Carga` aunque la variable sea de tipo `Vehiculo`.

## Errores comunes
- Olvidar `super(...)` cuando el padre no tiene constructor sin argumentos.
- Acceder a un atributo `private` del padre (usar `protected` o getters).
- Usar herencia para reutilizar código cuando no existe relación "es un".
- Poner `super(...)` que no es la primera instrucción.
- Cambiar el tipo de retorno o los parámetros creyendo que se sobrescribe (en realidad se sobrecarga o no compila).

## Ejercicios propuestos
1. Diseñe `Cuenta` -> `CuentaAhorro` y `CuentaCorriente` (ver [[Programación I - Java Proyecto Banco]]).
2. ¿Compila `class A { A(int x){} } class B extends A { }`? *(No: falta `super(int)` explícito, no existe `A()`.)*
3. Dibuje el diagrama de clases de `Persona`, `Estudiante`, `Profesor`.
4. Explique por qué `Auto` no debería extender `Rueda`. *(Un auto no "es una" rueda; la tiene: composición.)*

## Conexiones
Anterior: [[Programación I - Java C05 Sobrecarga, paso de objetos y modificadores]]. Siguiente: [[Programación I - Java C07 Polimorfismo y clases abstractas]]. En C++: [[Programación I - C++ C04 Herencia]]. Resumen anterior: [[Programación I - Java C04 Clases, objetos y métodos]]. Práctica con herencia: [[Programación I - Java Ejercicios C01 C02 C03 y su resolución]].

## Fuente
`Material/Java/Teoria/TemaI-C06 Herencia.pdf`.
