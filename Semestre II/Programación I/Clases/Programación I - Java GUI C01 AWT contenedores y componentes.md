---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaIII-C01 GUI en Java - AWT contenedores y componentes.pdf; código en Material/Java/Practicas/Ejercicios/UV-C01 EjemplosAWT
---
# Java GUI C01 - AWT: contenedores, layouts y componentes

Materia: [[Programación I]]

## Contexto y objetivo
Primera lección de la Unidad de **Interfaz Gráfica de Usuario (GUI)**. Define qué es una GUI y presenta **AWT** (Abstract Window Toolkit, paquete `java.awt`): sus **contenedores** (`Frame`, `Window`, `Panel`, `Dialog`), los **administradores de disposición** (*layout managers*) y los **componentes** básicos (`Label`, `Button`, `TextField`, `Canvas`, `Choice`, `Checkbox`, `List`, `TextArea`). Incluye la documentación del proyecto de ejemplos `UV-C01 EjemplosAWT`. El resumen previo está en [[Programación I - Java GUI C02 Manejo de eventos]].

## 1. Qué es una GUI
Una *Graphical User Interface* permite interactuar con el programa mediante elementos visuales: ventanas, barras de menú, menús, campos de texto, botones... Ventajas: usuarios de nivel básico pueden usar los programas, familiarización rápida y menor tiempo de aprendizaje. Ejemplo: el cuadro "Fuente" de un procesador de texto reúne cuadros de texto, listas desplegables, combos, etiquetas, casillas de verificación y botones.

Java ofrece dos mecanismos:
| | AWT | Swing |
|---|---|---|
| Paquete | `java.awt` | `javax.swing` |
| Implementación | **nativa** (usa los widgets del sistema operativo) | casi todo en Java puro ("ligero") |
| Apariencia | la del SO; puede variar entre plataformas | uniforme / configurable (*look and feel*) |
Ver [[Programación I - Java GUI C04 Swing contenedores y componentes]].

## 2. Características de AWT
- Compuesto por **contenedores** y **componentes**; todo componente es una instancia de `Component` (o subclase); todo contenedor, de `Container` (que a su vez es un `Component`, así que un contenedor puede ir dentro de otro).
- No se usan posiciones fijas sino **disposiciones controladas** (layouts), para que la interfaz sea portable ante distintos tamaños/SO.
- Bajo nivel: teclado, ratón y manejo de eventos ([[Programación I - Java GUI C02 Manejo de eventos]]).

Jerarquía: `Object > Component > Container > {Window > {Frame, Dialog}, Panel}`; y `Component > {Button, Label, TextComponent > {TextField, TextArea}, Canvas, Checkbox, Choice, List, Scrollbar}`.

## 3. Layout managers
Un *Layout Manager* es el objeto que decide cómo se sitúan los componentes en un contenedor. AWT define cinco; también se puede escribir uno propio implementando `LayoutManager`.
| Layout | Descripción | Por defecto en |
|---|---|---|
| `BorderLayout` | cinco zonas: NORTH, SOUTH, EAST, WEST, CENTER (el centro ocupa el resto) | Frame, Window, Dialog |
| `FlowLayout` | los componentes se encadenan de izquierda a derecha como una lista, con espaciado configurable | Panel |
| `GridLayout` | rejilla de filas x columnas con celdas iguales | - |
| `CardLayout` | varias "tarjetas" superpuestas, se muestra una a la vez (se asocia a un `Choice` o botones) | - |
| `GridBagLayout` | rejilla con filas/columnas de distinto tamaño y componentes que ocupan varias celdas; el más flexible y complejo | - |

`setLayout(null)` desactiva el administrador: la posición y el tamaño se dan manualmente con `setBounds(x, y, ancho, alto)` (el PDF escribe "alto, ancho", pero el orden real es **ancho, alto**).

## 4. Contenedores
### Frame
Ventana de alto nivel con **borde y título**; `BorderLayout` por defecto. Métodos: `setTitle`, `setSize`, `setBounds`, `setBackground`, `setVisible(true)`. Genera eventos de ventana, entre ellos `windowClosing` (clic en el botón cerrar), que por defecto **no hace nada**: hay que registrar un `WindowListener` para cerrar.
```java
public class FrameDemo {
    private Frame theFrame;
    public FrameDemo(String title) { theFrame = new Frame(title); }
    public void run() {
        theFrame.setSize(200, 200);
        theFrame.setBackground(Color.blue);
        theFrame.setVisible(true);
        theFrame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent evt) { System.exit(0); }
        });
    }
    public static void main(String[] args) { new FrameDemo("Frame Demo").run(); }
}
```
`WindowAdapter` es una clase adaptadora (implementa `WindowListener` con métodos vacíos) que permite sobrescribir solo `windowClosing`; aquí se usa una **clase anónima**.

### Window
Ventana **sin título ni borde**; requiere un `Frame` propietario. `BorderLayout` por defecto. Útil para pantallas de presentación (*splash*).

### Panel
Contenedor de propósito general, **sin manifestación visual propia** salvo su color de fondo; `FlowLayout` por defecto. Puede contener otros paneles (a diferencia de los contenedores de máximo nivel), lo que permite construir interfaces complejas anidando paneles con layouts distintos.
```java
Panel thePanel = new Panel();
thePanel.setSize(100, 100);
thePanel.setBackground(Color.red);
theFrame.setLayout(null);        // posición manual
theFrame.add(thePanel);          // panel rojo dentro de un frame azul
```
En el proyecto, `FrameCerrable extends Frame` (con `setBounds(50,50,300,300)`, fondo amarillo y layout `null`) contiene un `PanelPrueba` (panel rojo): "ventana amarilla cerrable con panel rojo", lanzada por `Principal`.

### Dialog
Ventana con borde y título para entradas del usuario; `BorderLayout` por defecto. Puede ser **modal** (bloquea las entradas a las demás ventanas hasta cerrarse) o no.
```java
Frame f = new Frame("Ejemplo");
Dialog d = new Dialog(f, "Ejemplo Cuadro de Dialogo", true);   // true = modal
d.setLayout(new GridLayout(2, 1));
d.add(new Label("Presione el Botón"));
d.add(new Button("OK"));
d.pack();                  // ajusta el tamaño a los componentes
d.setVisible(true);
```

## 5. Agregar componentes
Se añaden con `add(componente)`; su ubicación depende del layout. Con `BorderLayout`: `add(componente, BorderLayout.NORTH)`. Con layout `null` se usa `setBounds`. Ventajas del layout: la ventana se adapta a redimensionados y a distintas resoluciones.

## 6. Componentes
| Componente | Descripción | Detalles |
|---|---|---|
| `Label` | texto estático; constantes `LEFT`, `CENTER`, `RIGHT` para alinear | `new Label("Nombre:")` |
| `Button` | botón con título | `new Button("Aceptar")`; evento `ActionEvent` |
| `TextField` | una línea de texto; hereda de `TextComponent`; puede ser no editable (`setEditable(false)`) | `getText()`, `setText()` |
| `TextArea` | texto multilínea; constantes `SCROLLBARS_BOTH`, `_NONE`, `_HORIZONTAL_ONLY`, `_VERTICAL_ONLY` | `new TextArea(5, 20)` |
| `Canvas` | rectángulo vacío para dibujar o capturar eventos; se crean subclases y se sobrescribe `paint(Graphics)` | dibujo propio |
| `Choice` | lista desplegable de un solo elemento visible; implementa `ItemSelectable` y `addItemListener` | `add("opción")` |
| `Checkbox` | casilla de verificación; con un `CheckboxGroup` se convierte en **botones de radio** (solo uno activo) | `new Checkbox("Hombre", grupo, true)` |
| `List` | lista siempre visible con barra de desplazamiento; selección simple o múltiple | `new List(3)`, `add("Uno")` |

Ejemplos del proyecto:
```java
// Botones de radio
CheckboxGroup a = new CheckboxGroup();
Checkbox c1 = new Checkbox("Hombre", a, true);
Checkbox c2 = new Checkbox("Mujer", a, false);

// Lista con 3 filas visibles
List lista = new List(3);
lista.add("Uno"); lista.add("Dos"); lista.add("Tres"); lista.add("Cuatro");

// Canvas con dibujo
CanvasDemo can = new CanvasDemo() {
    public void paint(Graphics g) {
        g.setColor(Color.CYAN);  g.fillRect(15, 15, ancho-350, alto-200);
        g.setColor(Color.BLACK); g.drawRect(10, 10, ancho-30, alto-30);
        g.drawString("hola", 100, 120);
        g.fillOval(150, 120, 30, 30);
        g.fillArc(200, 170, 60, 60, 90, 90);
        g.drawImage(img, 270, 30, this);   // imagen cargada con ImageIcon
    }
};
```
`Graphics` ofrece primitivas: `drawLine`, `drawRect`, `fillRect`, `drawOval`, `fillOval`, `drawArc`, `fillArc`, `drawString`, `drawImage`, `setColor`, `setFont`. `paint` es invocado por el sistema cada vez que hay que redibujar; se fuerza con `repaint()`.

El proyecto contiene una clase por componente (`ButtonDemo`, `TextFieldDemo`, `TextAreaDemo`, `LabelDemo`, `ChoiceDemo`, `ScrollBarDemo`, `WindowDemo`, `DialogPrueba`, `PanelPrueba`, `ButtonPrueba`...). Todas siguen el mismo esquema: crear el `Frame`, fijar tamaño y layout, crear/añadir el componente, `setVisible(true)` y registrar el cierre.

## Ejemplo resuelto: formulario simple
```java
Frame f = new Frame("Registro");
f.setLayout(new GridLayout(3, 2, 5, 5));         // 3 filas, 2 columnas, huecos de 5 px
f.add(new Label("Nombre:"));  f.add(new TextField(15));
f.add(new Label("Sexo:"));
Panel p = new Panel();
CheckboxGroup g = new CheckboxGroup();
p.add(new Checkbox("M", g, true)); p.add(new Checkbox("F", g, false));
f.add(p);
f.add(new Button("Aceptar")); f.add(new Button("Cancelar"));
f.pack(); f.setVisible(true);
```
Un `Panel` auxiliar permite meter dos casillas en una sola celda de la rejilla: anidamiento de contenedores.

## Errores comunes
- La ventana nunca se ve: falta `setVisible(true)` (o tamaño 0).
- La ventana no se cierra: falta el `WindowListener`.
- Con layout `null`, olvidar `setBounds` (el componente queda invisible).
- Mezclar `add` sin conocer el layout por defecto (Frame usa Border: añadir dos componentes sin zona hace que se solapen en el centro).
- Confundir el orden de `setBounds(x, y, ancho, alto)`.
- Mezclar componentes AWT y Swing en la misma ventana.

## Ejercicios propuestos
1. Cree un `Frame` con `BorderLayout` que tenga un `Label` al norte, un `TextArea` al centro y dos botones al sur (en un `Panel`).
2. Calculadora de 4x4 con `GridLayout`.
3. Un `Choice` con tres paneles que cambien con `CardLayout` *(requiere eventos, ver el siguiente tema)*.
4. Dibuje una cara sonriente en un `Canvas`.

## Conexiones
Anterior: [[Programación I - Java C10 Archivos en Java]]. Siguiente: [[Programación I - Java GUI C02 Manejo de eventos]]. Swing: [[Programación I - Java GUI C04 Swing contenedores y componentes]].

## Fuente
`Material/Java/Teoria/TemaIII-C01 GUI en Java - AWT contenedores y componentes.pdf`; proyecto `Material/Java/Practicas/Ejercicios/UV-C01 EjemplosAWT/`.
