---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaIII-C02 GUI en Java - Manejo de eventos.pdf; TemaIII-C03 GUI en Java - Manejo de eventos(cont.).pdf; código en Material/Java/Practicas/Ejercicios/UV-C02 ManejoEventos
---
# Java GUI C02-C03 - Manejo de eventos (modelo de delegación)

Materia: [[Programación I]]

## Contexto y objetivo
Una ventana con botones no sirve si no reacciona. Los **eventos** son el mecanismo mediante el cual el usuario se comunica con la aplicación. Estas dos lecciones (la segunda es continuación de la primera, y existe una copia en `Practicas/Enunciados`) explican qué es un evento, sus tipos, el modelo **fuente - oyente - objeto evento** y las tres formas de escribir oyentes (clase adaptadora, clase interna con la interface, clase anónima). Incluyen los ejemplos con `Button`, `TextField` y `Label` del proyecto `UV-C02 ManejoEventos`. Se apoya en [[Programación I - Java C08 Interfaces]] (los oyentes son interfaces) y en [[Programación I - Java GUI C01 AWT contenedores y componentes]].

## 1. Qué es un evento
Un evento es una **encapsulación de información** enviada a la aplicación de forma **asíncrona** (cuando ocurre, no en un punto fijo del programa). Corresponde a acciones físicas (ratón, teclado) o lógicas (un valor cambió). La mayoría se generan automáticamente por las acciones del usuario, pero **si la aplicación no los trata, no hay respuesta**.

Clases: `java.util.EventObject` es la raíz; `java.awt.AWTEvent` hereda de ella y es la raíz de los eventos AWT; el resto (en `java.awt.event`) hereda de `AWTEvent`. Cuando el usuario interactúa, la información se guarda en un objeto de una de esas clases.

## 2. Tipos de eventos
**Bajo nivel (físicos)**: acciones elementales.
| Evento | Cuándo |
|---|---|
| `ComponentEvent` | esconder, mover, redimensionar, mostrar |
| `ContainerEvent` | añadir o eliminar un componente |
| `FocusEvent` | obtener o perder el foco |
| `KeyEvent` | pulsar, liberar o teclear una tecla |
| `MouseEvent` | entrar, salir, pulsar, soltar, clic |
| `MouseMotionEvent` | arrastrar o mover |
| `WindowEvent` | maximizar, minimizar, abrir, cerrar, activar, desactivar |

**Alto nivel (semánticos)**: tienen mayor significado.
| Evento | Significado |
|---|---|
| `ActionEvent` | una acción se ha ejecutado (clic en botón, Enter en un `TextField`, elegir un menú) |
| `AdjustmentEvent` | se ajustó un valor (barra de desplazamiento) |
| `ItemEvent` | cambió un estado (selección en `Checkbox`, `Choice`, `List`) |
| `TextEvent` | cambió un texto |

## 3. Modelo de delegación de eventos
Tres actores:
1. **Event source (fuente)**: el componente con el que interactúa el usuario (un `Button`).
2. **Event object**: encapsula la información (incluye una referencia a la fuente: `getSource()`; y datos como `getActionCommand()`, `getX()`, `getY()`).
3. **Event listener (oyente/escuchador)**: objeto que es notificado por la fuente cuando ocurre el evento y recibe el event object. Debe **implementar la interface** `XxxListener` correspondiente.

La fuente **registra** al oyente: `fuente.addXxxListener(oyente)` (`addActionListener`, `addMouseListener`, `addKeyListener`, `addWindowListener`, `addItemListener`, `addTextListener`...). El programador hace **dos tareas**: (a) registrar el oyente para el componente que generará el evento y (b) implementar los métodos manejadores (*event handlers*). Los oyentes están en `java.awt.event` y `javax.swing.event`.

Tres elementos al capturar un evento: la **interface** que maneja el evento, la **clase adaptadora** (si existe) y el **método** que se implementa. Ejemplo para cerrar la ventana: interface `WindowListener`, adaptadora `WindowAdapter`, método `windowClosing(WindowEvent)`, nombre del evento `WindowEvent`.

## 4. Formas de implementar el oyente
### a) Implementar la interface completa
```java
class CloseEvent implements WindowListener {
    public void windowClosing(WindowEvent e) { System.exit(0); }
    public void windowOpened(WindowEvent e) {}      // hay que definir TODOS los demás
    public void windowClosed(WindowEvent e) {}
    public void windowIconified(WindowEvent e) {}
    public void windowDeiconified(WindowEvent e) {}
    public void windowActivated(WindowEvent e) {}
    public void windowDeactivated(WindowEvent e) {}
}
frame.addWindowListener(new CloseEvent());
```
Aunque solo interese un método, hay que redefinir los demás (vacíos); si no, la clase quedaría **abstracta**. Esa incomodidad motiva los adaptadores.

### b) Clase adaptadora (Adapter)
Para cada interface oyente con **más de un método** existe una clase `Adapter` con todos los métodos vacíos; su nombre sustituye "Listener" por "Adapter". Hay siete: `ComponentAdapter`, `ContainerAdapter`, `FocusAdapter`, `KeyAdapter`, `MouseAdapter`, `MouseMotionAdapter`, `WindowAdapter`. Basta derivar y redefinir lo de interés:
```java
class CloseEvent extends WindowAdapter {
    public void windowClosing(WindowEvent e) { System.exit(0); }
}
frame.addWindowListener(new CloseEvent());
// o anónima:
frame.addWindowListener(new WindowAdapter() {
    public void windowClosing(WindowEvent e) { System.exit(0); }
});
```
Las interfaces con **un solo método** (`ActionListener`, `ItemListener`, `TextListener`, `AdjustmentListener`) no tienen adaptador; se implementa la interface directamente (con una clase anónima o interna).

### c) Que la propia clase implemente la interface
La ventana (`extends Frame implements ActionListener`) registra `this` como oyente. Es corto, pero todos los componentes comparten el mismo `actionPerformed` y hay que distinguirlos con `getSource()`; y si la interface tiene muchos métodos, todos aparecen en la clase.

## 5. Ejemplos del proyecto UV-C02
### Button con clases anónimas (Eventos1)
```java
button1 = new Button("Aceptar"); add(button1);
button2 = new Button("Cancelar"); add(button2);
button1.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent event) {
        System.out.println("Presionaste: " + event.getActionCommand());   // "Aceptar"
        System.out.println("Acciones de Aceptar");
    }
});
button2.addActionListener(new ActionListener() { ... "Acciones de Cancelar" ... });
addWindowListener(new WindowAdapter() { public void windowClosing(WindowEvent e) { System.exit(0); } });
```
Cada botón tiene su propio oyente anónimo. `getActionCommand()` devuelve por defecto el texto del botón.

### Button con clase interna (Eventos2)
```java
ManejaButton handler = new ManejaButton();
button1.addActionListener(handler);
button2.addActionListener(new ManejaButton());   // también anónimo
private class ManejaButton implements ActionListener {
    public void actionPerformed(ActionEvent event) {
        if (event.getSource() == button1)      System.out.println("Acciones de Aceptar");
        else if (event.getSource() == button2) System.out.println("Acciones de Cancelar");
    }
}
```
Un único oyente atiende a varios botones y los distingue con `getSource()`. Al ser clase **interna** puede acceder a los atributos (`button1`) de la ventana.

### TextField (TextFieldDemo_Eventos1 y 2)
Tres campos: uno con 10 columnas, otro con texto inicial y un tercero **no editable** (`setEditable(false)`). El `ActionEvent` de un `TextField` se dispara al pulsar **Enter** dentro del campo; `getActionCommand()` devuelve el texto escrito. La versión 2 usa una clase interna con un oyente común y `getSource()` para identificar el campo.

### Label con eventos de ratón (LabelDemo_Eventos)
`Label` no genera `ActionEvent`, pero sí eventos de ratón. Se usa `MouseAdapter` (con `mouseEntered`/`mouseExited`) para cambiar el color del texto "Jugar" de azul a rojo al pasar el ratón, simulando un enlace/menú; y otro `MouseAdapter` en el `Frame` (`mousePressed`, `mouseReleased`) que imprime las coordenadas `e.getX()`, `e.getY()` del clic. Se usa layout `null` y `setBounds(110,80,100,30)`.

### Resumen de interfaces y métodos
| Interface | Métodos principales | Adaptador |
|---|---|---|
| `ActionListener` | `actionPerformed` | no |
| `ItemListener` | `itemStateChanged` | no |
| `TextListener` | `textValueChanged` | no |
| `MouseListener` | `mouseClicked/Pressed/Released/Entered/Exited` | `MouseAdapter` |
| `MouseMotionListener` | `mouseDragged`, `mouseMoved` | `MouseMotionAdapter` |
| `KeyListener` | `keyPressed`, `keyReleased`, `keyTyped` | `KeyAdapter` |
| `WindowListener` | `windowOpened/Closing/Closed/Iconified/Deiconified/Activated/Deactivated` | `WindowAdapter` |
| `FocusListener` | `focusGained`, `focusLost` | `FocusAdapter` |

## Ejemplo resuelto: contador con botones
```java
public class Contador extends Frame {
    private int n = 0;
    private Label lbl = new Label("0", Label.CENTER);
    public Contador() {
        super("Contador");
        Button mas = new Button("+"), menos = new Button("-");
        add(lbl, BorderLayout.CENTER); add(mas, BorderLayout.EAST); add(menos, BorderLayout.WEST);
        mas.addActionListener(e -> { n++; lbl.setText("" + n); });      // lambda (Java 8)
        menos.addActionListener(e -> { n--; lbl.setText("" + n); });
        addWindowListener(new WindowAdapter() { public void windowClosing(WindowEvent e){ System.exit(0);} });
        setSize(200, 80); setVisible(true);
    }
    public static void main(String[] a) { new Contador(); }
}
```
Flujo: clic en "+" -> la fuente `mas` notifica a su oyente -> `actionPerformed` incrementa `n` y actualiza la etiqueta. (Las lambdas no aparecen en el material; son equivalentes a las clases anónimas de un solo método.)

## Errores comunes
- Olvidar registrar el oyente (`add...Listener`): nada ocurre.
- Registrar el oyente equivocado (`addMouseListener` en lugar de `addActionListener`).
- Implementar la interface y no redefinir todos sus métodos.
- Escribir mal la firma (p. ej. `windowclosing`) y que el adaptador ignore el método: usar `@Override`.
- Hacer trabajo largo dentro del manejador y "congelar" la interfaz (los eventos se atienden en un solo hilo).
- Comparar `event.getActionCommand()` cuando el texto del botón cambia; mejor `getSource()`.

## Ejercicios propuestos
1. Un `TextField` y un `Button` "Saludar" que muestra "Hola, <nombre>" en un `Label`.
2. Cambie el color de fondo del `Frame` con tres botones (Rojo, Verde, Azul) usando un solo oyente.
3. Con `MouseMotionAdapter`, muestre la posición del ratón en la barra de título.
4. Valide con `KeyAdapter` que un campo solo reciba dígitos (consumir el evento con `e.consume()` en `keyTyped`).

## Conexiones
Anterior: [[Programación I - Java GUI C01 AWT contenedores y componentes]]. Siguiente: [[Programación I - Java GUI C04 Swing contenedores y componentes]]. Las excepciones se usan al validar entradas ([[Programación I - Java C09 Gestión de errores y excepciones]]). Resumen previo: GUI en Java - AWT, Swing y eventos.

## Fuente
`Material/Java/Teoria/TemaIII-C02 GUI en Java - Manejo de eventos.pdf` y `TemaIII-C03 GUI en Java - Manejo de eventos(cont.).pdf`; proyecto `Material/Java/Practicas/Ejercicios/UV-C02 ManejoEventos/`.
