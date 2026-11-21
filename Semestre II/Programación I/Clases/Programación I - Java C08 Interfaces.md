---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaII-C08 Interfaces.pdf
---
# Java C08 - Interfaces

Materia: [[Programación I]]

## Contexto y objetivo
Java no admite herencia múltiple de clases. Las **interfaces** resuelven el problema de definir *capacidades* comunes (volar, grabar, dibujar) en clases que no comparten jerarquía, y permiten que una clase cumpla varios "contratos" a la vez. La lección cubre sintaxis, restricciones, uso con `implements`, ejemplos de diseño (patos, figuras dibujables, medios ópticos), herencia entre interfaces, ambigüedades y la modificación segura de interfaces. Continúa el tema de [[Programación I - Java C07 Polimorfismo y clases abstractas]].

## 1. Qué es una interface
Declara **solo el contrato** (qué métodos existen) y no la implementación; es parecida a una clase abstracta pura. Reúne una colección de métodos que se implementan en otro lugar y puede incluir constantes. Ventajas:
- Captura similitudes entre clases **sin relación de herencia**.
- Muchas clases (de jerarquías distintas) pueden implementar la misma interface.
- Una clase puede implementar **varias** interfaces (a diferencia de `extends`, que admite una sola superclase).
- Son la base del polimorfismo "por capacidad": una variable de tipo interface puede referenciar cualquier objeto cuya clase la implemente.

## 2. Sintaxis y restricciones
```java
[public] interface NombreInterface [extends SuperInterface1, SuperInterface2] {
    // constantes
    [public] [static] [final] tipo NOMBRE = valor;
    // métodos
    [public] [abstract] tipoRetorno metodo(parámetros);
}
```
- Atributos: no admiten `private` ni `protected`; por defecto son **`public static final`** (constantes, deben inicializarse).
- Métodos: solo declaran comportamiento; por defecto son **`public abstract`**. No se pueden usar `private`, `protected`, `static`, `native`, `final` ni `synchronized` (en el programa del curso, basado en Java antiguo; desde Java 8 existen métodos `default` y `static`, y desde 9 `private`, que quedan fuera de este temario).

```java
public interface Control {
    final int CantCanales = 32;
    void EncenderApagar();     // enciende o apaga el televisor
    void CambiarCanal();       // cambia el canal activo
    void AjustarVolumen();     // ajusta el volumen actual
}
```

## 3. Uso de una interface: `implements`
La clase usa `implements Nombre` en su cabecera y **debe implementar todos** los métodos (con visibilidad `public`, porque en la interface son públicos); si no lo hace, debe declararse `abstract`.
```java
public class Televisor implements Control {
    private String marca; private float costo;
    public void EncenderApagar() { /* código */ }
    public void CambiarCanal()   { /* código */ }
    public void AjustarVolumen() { /* código */ }
    public void mostrar() { System.out.println(marca + " " + costo); }
}
```
(En el PDF los métodos aparecen sin `public`; eso no compila porque reduciría la visibilidad: deben ser `public`.)

## 4. Ejemplos de diseño del PDF
### 4.1 La capacidad "Volar"
`interface Volar { despegar(); volar(); aterrizar(); }`. La implementan `Avion` (que además es un `Vehiculo` y añade `hacerManiobras()`), `Pajaro` (es un `Animal`, añade `hacerNido()` y `ponerHuevos()`) y `Superman` (extiende `HomoSapien`, añade `saltarEdificios()` y `pararBalas()`). Una clase hereda de **una** clase e implementa **varias** interfaces:
```java
public class Avion extends Vehiculo implements Volar { ... }
public class Pajaro extends Animal implements Volar { ... }
public class Superman extends HomoSapien implements Volar { ... }
```
Esquema general: `public class C extends Super implements I1, I2 {...}`.

### 4.2 El problema de los patos
Diseño inicial: clase abstracta `Pato` con `nadar()` concreto y `mostrar()`, `graznar()`, `volar()` abstractos; hijas `PatoReal`, `PatoCabezaRoja`, `PatodeGoma`.
- Problema 1: el pato de goma no vuela pero está obligado a implementar `volar()` (o ser abstracto).
- Problema 2: un `PatoSeñuelo` ni grazna ni vuela.
- **Solución**: sacar los comportamientos opcionales a interfaces `Vuelo` (`volar()`) y `Graznido` (`graznar()`). `Pato` conserva `nadar()` y `mostrar()` abstracto; `PatoReal` y `PatoCabezaRoja` implementan ambas, `PatodeGoma` solo `Graznido`, `PatoSeñuelo` ninguna. Lección: **no meter en la superclase comportamientos que no son comunes a todas las subclases**. Este es el germen del patrón *Strategy* (ver [[IS 04 - Modelado con UML]]).

### 4.3 Figuras dibujables
Clases existentes `Geometria` (abstracta: `area()`, `perimetro()`) con `Rectangulo` y `Circulo`, que no saben de gráficos. Se crean `RectanguloGrafico` y `CirculoGrafico` (añaden `color`) que heredan de las anteriores e **implementan `Dibujable`** (`setPosition(Point)`, `dibujar(Graphics)`). El `PanelDibujo` mantiene una colección 0..* de `Dibujable` y su `paint` llama `dibujar` en cada uno. La interfaz `Dibujable` es **polimórfica**: se comporta como rectángulo o como círculo según el objeto real. Se logra así extender clases que ya existían sin modificarlas.

### 4.4 Medios ópticos
`MedioOptico` (abstracta, `sizeinBytes`, `maxSizeinBytes`, `leer()`), hijas `CD-R` y `DVD-R` (solo lectura), y `CD-RW`/`DVD-RW` que además implementan `Grabable` (`grabar()`). Una clase `Burner` tiene una variable de tipo `Grabable` y acepta tanto CD como DVD regrabables vía polimorfismo.

### 4.5 Contadores
```java
public interface Contador { int MAX_INT = 2147483647; void avanzar(); int obtenerValor(); }
public class ContadorSegundos implements Contador {
    int valor; ContadorSegundos() { valor = 0; }
    public void avanzar() { valor++; if (valor > 60) valor = 0; }   // reinicia al pasar de 60
    public int obtenerValor() { return valor; }
}
public class ContadorInverso implements Contador {
    int valor; ContadorInverso() { valor = MAX_INT; }
    public void avanzar() { valor--; if (valor < 0) valor = MAX_INT; }
    public int obtenerValor() { return valor; }
}
```
Dos comportamientos distintos tras el mismo contrato; el código cliente trabaja con `Contador c`.

## 5. Herencia de interfaces
Una interface puede **extender** una o más interfaces (a diferencia de las clases, aquí sí hay herencia múltiple). Ejemplo: se quiere que un DVD/CD además de grabarse se pueda **clonar**. Dos soluciones:
1. Nueva interface `Clonable` implementada por `DVD-RW` y `CD-RW`.
2. Interface `GrabClon extends Grabable` con `clonar(MedioOptico origen)`. **Es preferible**: el `Burner` declara una variable `GrabClon` y puede grabar y clonar sin casting explícito.
```java
public interface GrabClon extends Grabable { void clonar(MedioOptico origen); }
```
En la clonación se usa `instanceof` para evitar copiar un CD-R en un DVD-RW (`if (origen instanceof DVDR) ...`).

Otro ejemplo (colores):
```java
public interface ColoresBase { int ROJO = 1, VERDE = 2, AZUL = 4; void ajustarColoresBase(); }
public interface ColoresArcoIris extends ColoresBase { int AMARILLO = 3, NARANJA = 5, INDIGO = 6, VIOLETA = 7; void ajustarColoresArcoIris(); }
public interface MasColores extends ColoresArcoIris, ColoresBase { int FUCSIA = 17, COBRE = 43, ESMERALDA = 90; void ajustarMasColores(); }
```
Las sub-interfaces **no implementan** métodos; la clase que implemente `MasColores` debe implementar los de **todas** las interfaces de la cadena (`ajustarColoresBase`, `ajustarColoresArcoIris`, `ajustarMasColores`).

## 6. Atributos o métodos ambiguos
Si `ColoresImpresora extends ColoresBase` redefine la constante `ROJO = 5` (en la base vale 1), dentro de `Impresora` la referencia simple `ROJO` sería ambigua; se resuelve **calificando**: `ColoresBase.ROJO` (1) y `ColoresImpresora.ROJO` (5). Si dos interfaces declaran el mismo método (`ajustar()`) con la misma firma, la clase lo implementa una sola vez y sirve para ambas.

## 7. Modificación de interfaces
Una interface ya implementada **no debería modificarse**: agregar o quitar un método obliga a cambiar todas las clases que la implementan (en el ejemplo, `Figura` y `Televisor` tendrían que añadir `mostrar()`). Solución para añadir métodos: crear una **interface hija** (`HijaColoresBase extends ColoresBase` con `mostrar()`); las clases nuevas implementan la hija y las antiguas no se tocan. Moraleja: **diseñar con cuidado el contrato**.

## 8. Interface vs. clase abstracta
| Aspecto | Clase abstracta | Interface |
|---|---|---|
| Herencia | una sola (`extends`) | varias (`implements`) |
| Estado | atributos de instancia | solo constantes |
| Métodos | abstractos y concretos | abstractos (en el nivel del curso) |
| Constructores | sí | no |
| Cuándo usar | jerarquía "es un" con código común | capacidad transversal ("puede hacer") |

## Ejemplo resuelto: ordenar objetos por una capacidad
```java
interface Comparable2 { int comparar(Object o); }
class Alumno implements Comparable2 {
    String nombre; double nota;
    Alumno(String n, double p) { nombre = n; nota = p; }
    public int comparar(Object o) { return Double.compare(nota, ((Alumno) o).nota); }
}
static void ordenar(Comparable2[] v) {          // burbuja genérica
    for (int i = 0; i < v.length - 1; i++)
        for (int j = 0; j < v.length - 1 - i; j++)
            if (v[j].comparar(v[j + 1]) > 0) { Comparable2 t = v[j]; v[j] = v[j + 1]; v[j + 1] = t; }
}
```
`ordenar` sirve para cualquier clase que cumpla el contrato; es el mismo mecanismo de `java.lang.Comparable` y relevante para [[Estructura de Datos - Métodos de Ordenamiento Interno y Externo]].

## Errores comunes
- Implementar un método de interface sin `public`.
- Olvidar algún método (la clase queda incompleta: error o debe ser `abstract`).
- Intentar instanciar una interface (`new Control()` no compila; sí se pueden crear variables de ese tipo).
- Modificar una constante de interface (son `final`).
- Añadir métodos a una interface ya usada.

## Ejercicios propuestos
1. Defina `Imprimible` (`imprimir()`) e implemente en `Factura` y `Reporte`; haga un arreglo `Imprimible[]`.
2. Diseñe `Nadador`, `Corredor`, `Ciclista` y la clase `Triatleta` que implemente las tres. *(Una clase, tres interfaces.)*
3. ¿Qué imprime `ColoresBase.ROJO` y `ColoresImpresora.ROJO` en el ejemplo? *(1 y 5.)*
4. Explique por qué el diseño de patos con herencia pura es defectuoso.

## Conexiones
Anterior: [[Programación I - Java C07 Polimorfismo y clases abstractas]]. Siguiente: [[Programación I - Java C09 Gestión de errores y excepciones]]. Las interfaces son la base de los **oyentes de eventos** en [[Programación I - Java GUI C02 Manejo de eventos]] (`ActionListener`, etc.). Equivalente en C++: clases abstractas puras ([[Programación I - C++ C05 Polimorfismo]]).

## Fuente
`Material/Java/Teoria/TemaII-C08 Interfaces.pdf`.
