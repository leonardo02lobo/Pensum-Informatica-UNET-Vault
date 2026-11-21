---
tags: [materia, semestre-II]
semestre: II
---
# Programación I

**Semestre:** [[Semestre II]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Computación I]]
- [[Matemática Discreta]]

## Desbloquea
- [[Estructura de Datos]]
- [[Fundamentos de Lógica Digital]]

## Apuntes

### Descripción general y objetivos
Programación I (código 0416202T; prelaciones oficiales: Computación I y Matemática Discreta) introduce la **Programación Orientada a Objetos (POO)** con **Java** y **C++**, interfaces gráficas y manejo de archivos. Objetivo general del programa sinóptico: elegir técnicas avanzadas de POO para desarrollar aplicaciones sencillas, adaptables y mantenibles en el área científica o empresarial. Desbloquea [[Estructura de Datos]] y [[Fundamentos de Lógica Digital]]. Unidades de crédito: el sinóptico dice 3 y el analítico 4 (verificar con el programa oficial).

Notas hijas: [[Programación I - Java C04 Clases, objetos y métodos]], [[POO en C++ - constructores, herencia y punteros]], [[Programación I - Java GUI C02 Manejo de eventos]].

### Contenido programático (Programa analítico 2007-1 y planificación 2024-2)
**Unidad I. POO en Java (6 semanas, I parcial 30%)**: paradigmas; clases y objetos; UML y diagrama de clases; atributos y operaciones; abstracción, encapsulamiento, modularidad, herencia, polimorfismo; constructores y paso de parámetros por valor/referencia; modificadores `public`, `private`, `protected`; clases abstractas, interfaces, paquetes; excepciones y aserciones.
**Unidad II. Interfaz gráfica de usuario en Java (3 semanas, III parcial 20%)**: AWT (Frame, Dialog, Button, Label, List, Checkbox...), Swing y diferencias con AWT, JavaFX; gestión de eventos (objeto fuente, clases receptoras); integración, sonido y animaciones básicas.
**Unidad III. POO en C++ (5 semanas, II parcial 30%)**: clases y objetos; constructores por defecto, con parámetros y múltiples; inicialización dinámica; destructores; herencia simple y múltiple; polimorfismo; sobrecarga de funciones y operadores; funciones amigas y virtuales; clases abstractas.
**Unidad IV. Interfaces gráficas en C++ (2 semanas, IV parcial 15%)**: tecnología .NET, Visual Studio, WinForms (Label, TextBox, Button, menús, CheckBox, ListView, TreeView...), proyectos multiformulario, eventos.
La planificación 2024-2 del Material reordena: I POO en Java, II Archivos en Java, III GUI en Java, IV POO en C++, V conceptos avanzados; con parciales de 70/80/70 puntos más quizzes, prácticas y proyecto final (100). Las ponderaciones exactas varían por lapso: verificar con el programa del semestre.

### Conceptos clave
- **Clase**: plantilla; **objeto**: instancia con estado (atributos) y comportamiento (métodos).
- **Abstracción**, **encapsulamiento** (ocultar estado con `private` + getters/setters), **herencia** (`extends`), **polimorfismo** (misma interfaz, distinto comportamiento por sobrescritura), **modularidad**.
- **Clase abstracta**: no instanciable, puede tener métodos sin cuerpo; **interfaz**: contrato de métodos.
- **Sobrecarga** (mismo nombre, distinta firma) vs. **sobrescritura** (redefinir en la subclase).
- **Excepción**: evento anómalo manejado con `try/catch/finally`.
- **Puntero** (C++): variable que guarda una dirección; `new`/`delete` para memoria dinámica.

### Código de ejemplo (Java)
```java
abstract class Figura {
    protected String nombre;
    Figura(String nombre) { this.nombre = nombre; }
    abstract double area();
    public String toString() { return nombre + ": " + area(); }
}
class Circulo extends Figura {
    private double r;
    Circulo(double r) { super("Círculo"); this.r = r; }
    double area() { return Math.PI * r * r; }
}
class Rectangulo extends Figura {
    private double b, h;
    Rectangulo(double b, double h) { super("Rectángulo"); this.b = b; this.h = h; }
    double area() { return b * h; }
}
public class Main {
    public static void main(String[] args) {
        Figura[] fs = { new Circulo(2), new Rectangulo(3, 4) };
        for (Figura f : fs) System.out.println(f);   // polimorfismo
    }
}
```

### Código de ejemplo (C++)
```cpp
#include <iostream>
using namespace std;
class Animal {
public:
    virtual void sonido() { cout << "..." << endl; }
    virtual ~Animal() {}
};
class Perro : public Animal {
public:
    void sonido() override { cout << "Guau" << endl; }
};
int main() {
    Animal* a = new Perro();
    a->sonido();   // Guau (enlace dinámico)
    delete a;
}
```

### Ejemplo de manejo de excepciones (Java)
```java
try {
    int x = Integer.parseInt(texto);
    System.out.println(100 / x);
} catch (NumberFormatException e) {
    System.out.println("No es un número");
} catch (ArithmeticException e) {
    System.out.println("División entre cero");
} finally {
    System.out.println("Fin");
}
```

### Relación con otras materias
- Prerrequisitos: [[Computación I]] (C, estructuras de control, funciones) y [[Matemática Discreta]] (lógica, conjuntos, grafos).
- Continúa en [[Programación II]], [[Estructura de Datos]], [[Ingeniería de Software]] (UML, diseño OO), [[Desarrollo de Aplicaciones Web]] y [[Base de Datos I]].

### Evaluación y consejos
- Cuatro parciales con examen + práctica/proyecto (ver ponderaciones arriba); proyecto final integrando GUI. El Material trae exámenes de lapsos anteriores (2006 a 2025) para practicar.
- Diseña primero el diagrama de clases, programa por incrementos, prueba cada clase por separado, usa nombres claros y evita atributos públicos.

### Bibliografía recomendada
Del programa oficial: Joyanes Aguilar, *Programación orientada a objetos*; Deitel y Deitel, *Cómo programar en Java* y *Cómo programar en C/C++*; Barnes y Kölling, *Programación orientada a objetos con Java*; Booch, Rumbaugh y Jacobson, *El lenguaje unificado de modelado*; Larman, *Applying UML and Patterns*; Budd, *Introducción a la POO*; Lafore, *Data Structures & Algorithms in Java*.

### Recursos del Material/
- [Programa analítico](Material/0416202T-Programación%20I-Analitico.pdf) y [programa sinóptico](Material/0416202T-Programación%20I-Sipnotico.pdf): temario, objetivos, ponderaciones y bibliografía oficial.
- [Guía didáctica 2024-2](Material/GuiaDidactica_ProgramacionI_20242.pdf) y [Planificación 2024-2](Material/Planificacion2024-2_ProgramacionI.pdf): organización del lapso.
- [Actividades Nro 1 Intensivo](Material/Actividades%20Nro%201%20Intensivo.pdf), [Practica 2 Intensivo](Material/Practica%202%20%20Intensivo.pdf), [Práctica 4](Material/Práctica%204.pdf), [Segundo Parcial 2024-0](Material/Segundo%20%20Parcial_2024-0.pdf): prácticas y examen.
- `Material/C++.zip` y `Material/Muestras de exámenes ... (Parcial III)...zip`: archivos comprimidos de C++ y exámenes del III parcial.
- Carpeta `C++/`: clases de POO, herencia, polimorfismo (TemaV-C01 a C05), punteros, bits, separar tokens, diagramas de clases, primer parcial 2017-1 y `MisDatos.h`.
- Carpeta `Java/Teoria/` (y copia en `Java/`): temas I-C01 a C06 (POO, sintaxis, clases, sobrecarga, herencia), II-C07/C08/C10 (polimorfismo y clases abstractas, interfaces, archivos), III-C01 a C04 (GUI AWT, eventos, Swing), gestión de errores.
- Carpeta `Java/Ejercicios y Parciales/`: actividades 1-8, exámenes de parciales 1-3 (lapso 2024-2), proyecto final 2024-2 y práctica de GUI.
- Carpeta `Java/Practicas/Enunciados/`: enunciados y parciales históricos (2006-2025: ServicioSecreto, Cafetería, ControlVuelos, InventarioRopaDeportiva, MinisterioTierras, etc.).
- Carpeta `Java-Intensivo/`: material del curso intensivo.
