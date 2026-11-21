---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaIII-C04 GUI en Java - Swing contenedores y componentes.pdf; código en Material/Java/Practicas/Ejercicios/UV-C03 EjemplosSwing
---
# Java GUI C04 - Swing: contenedores y componentes

Materia: [[Programación I]]

## Contexto y objetivo
**Swing** (`javax.swing`) es la biblioteca de GUI que mejora a AWT: sus componentes están escritos en Java (no dependen del sistema operativo) y ofrecen más widgets y apariencia uniforme. La lección explica las **diferencias de código con AWT** y recorre los componentes `JLabel`, `JTextField`/`JPasswordField`, `JButton`, `JCheckBox`, `JRadioButton`, `JComboBox` y `JList` (selección simple y múltiple), con los ejemplos del proyecto `UV-C03 EjemplosSwing`. Parte de [[Programación I - Java GUI C01 AWT contenedores y componentes]] y reutiliza el modelo de [[Programación I - Java GUI C02 Manejo de eventos]].

## 1. De AWT a Swing: la regla de la "J"
Se importa `javax.swing.*` y los componentes se crean igual que en AWT **anteponiendo una J**: `JFrame`, `JButton`, `JLabel`, `JPanel`, `JTextField`, `JCheckBox`... (todos derivan de `JComponent`, que a su vez extiende `Container`/`Component` de AWT; los eventos siguen siendo los de `java.awt.event` más `javax.swing.event`).

| Tarea | AWT | Swing |
|---|---|---|
| Agregar componentes | `frame.add(c)` | `frame.getContentPane().add(c)` (desde Java 5 también vale `frame.add(c)`) |
| Layout | `frame.setLayout(null)` | `frame.getContentPane().setLayout(null)` |
| Cerrar la aplicación | `WindowListener` con `System.exit(0)` | `frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)` |
| Mostrar | `setVisible(true)` | `setVisible(true)` (`show()` está obsoleto) |

El **content pane** es el panel interno de un `JFrame` donde van los componentes (el `JFrame` tiene además *glass pane*, *layered pane* y barra de menús). Los diálogos sencillos se hacen con `JOptionPane.showMessageDialog(null, "mensaje")`, `showInputDialog` y `showConfirmDialog`.

Plantilla típica:
```java
public class Demo extends JFrame {
    public Demo() {
        super("Título");
        Container container = getContentPane();
        container.setLayout(new FlowLayout());
        // crear y añadir componentes + oyentes
        setSize(275, 100);
        setVisible(true);
    }
    public static void main(String[] args) {
        Demo app = new Demo();
        app.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```

## 2. Componentes
### JLabel
Etiqueta de solo lectura con texto, imagen o ambos: `new JLabel("Etiqueta")`, `new JLabel("texto", icono, SwingConstants.LEFT)`, `setToolTipText("ayuda")`, `setHorizontalTextPosition(...)`. Subclase de `JComponent`.

### JTextField y JPasswordField
Cajas de texto para entrada de una línea; `JPasswordField` oculta los caracteres tecleados (por defecto con eco `*`); `getPassword()` devuelve un `char[]` (no `String`, por seguridad). Al pulsar **Enter** se genera un `ActionEvent`. En el ejemplo del PDF se muestra con `JOptionPane` el texto del campo activo (el que tiene el *focus*): `JOptionPane.showMessageDialog(null, "textField1: " + event.getActionCommand())`.

### JButton
`ButtonDemo1` y `ButtonDemo2`: dos botones "Aceptar" y "Cancelar" en un `FlowLayout` con oyentes anónimos que muestran `JOptionPane.showMessageDialog(null, "Presionaste: " + e.getActionCommand())`.
```java
button1.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        JOptionPane.showMessageDialog(null, "Presionaste: " + e.getActionCommand());
    }
});
```
Los `JButton` admiten iconos (`new JButton("OK", new ImageIcon("ok.png"))`) y *rollover*.

### JCheckBox y JRadioButton
Ambos son subclases de `JToggleButton` con estado true/false. **JCheckBox**: se pueden marcar varios a la vez. **JRadioButton**: se agrupan en un `ButtonGroup` y solo uno puede estar activo. Se tratan con `ItemListener` (`itemStateChanged`, `event.getStateChange() == ItemEvent.SELECTED`).

`CheckBoxDemo`: un `JTextField` y dos casillas "Bold" e "Italic" con un oyente interno que compone el estilo sumando las constantes: `Font.BOLD + Font.ITALIC`. Como son casillas independientes, ambas pueden estar activas.
```java
field.setFont(new Font("Serif", valBold + valItalic, 14));
```
`RadioButtonDemo`: cuatro botones (Plain, Bold, Italic, Bold/Italic) con un `ButtonGroup` (`radioGroup.add(...)`); cada cambio asigna una fuente prefabricada al campo. Si no se añade el grupo, los radios no serían excluyentes.

### JComboBox
Lista desplegable con un elemento visible: `new JComboBox(colorNames)`, `setMaximumRowCount(12)`, `getSelectedIndex()`. En `ComboBoxDemo` se mantiene un arreglo paralelo de `Color` y, al seleccionar un nombre, se cambia el fondo del contenedor:
```java
colorComboBox.addItemListener(new ItemListener() {
    public void itemStateChanged(ItemEvent event) {
        if (event.getStateChange() == ItemEvent.SELECTED)
            container.setBackground(colors[colorComboBox.getSelectedIndex()]);
    }
});
```
Se comprueba `SELECTED` porque `itemStateChanged` se invoca también al **deseleccionar** el anterior (si no se filtra, se ejecutaría dos veces). Idea de diseño: arreglos paralelos indexados por la selección.

### JList
Muestra una serie de ítems seleccionables (uno o varios). Hereda de `JComponent`. Se coloca dentro de un `JScrollPane` para tener barras de desplazamiento: `container.add(new JScrollPane(colorList))`. `setVisibleRowCount(5)`, `setSelectionMode(ListSelectionModel.SINGLE_SELECTION)`. Usa `ListSelectionListener` (`valueChanged`) del paquete `javax.swing.event`.

**Selección múltiple** (`MultipleSelectionDemo`, dos listas y un botón que copia ítems de una a otra):
- `SINGLE_INTERVAL_SELECTION`: un rango contiguo (clic en el primero, **Shift** + clic en el último).
- `MULTIPLE_INTERVAL_SELECTION`: rangos y ítems discontinuos (con **Ctrl** + clic).
Se obtienen los seleccionados con `getSelectedValues()`/`getSelectedValuesList()`.

## 3. AWT frente a Swing
| Aspecto | AWT | Swing |
|---|---|---|
| Implementación | nativa (peso pesado) | Java puro (peso ligero) |
| Apariencia | depende del SO | independiente; Look & Feel configurable |
| Componentes | básicos | muchos más (JTable, JTree, JTabbedPane, JSlider...) |
| Prefijo | ninguno | `J` |
| Cierre | listener manual | `setDefaultCloseOperation` |
| Contenido | `add` directo | `getContentPane()` |
`JavaFX` (mencionado en el programa analítico) es la tecnología sucesora; no se desarrolla en el material.

## Ejemplo resuelto: conversor con Swing
```java
public class Conversor extends JFrame {
    private JTextField tfC = new JTextField(8);
    private JLabel lblF = new JLabel("= ? °F");
    public Conversor() {
        super("°C a °F");
        Container c = getContentPane();
        c.setLayout(new FlowLayout());
        JButton b = new JButton("Convertir");
        c.add(new JLabel("°C:")); c.add(tfC); c.add(b); c.add(lblF);
        b.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                try {
                    double cel = Double.parseDouble(tfC.getText());
                    lblF.setText("= " + (cel * 9 / 5 + 32) + " °F");
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(null, "Número inválido");
                }
            }
        });
        setSize(380, 80); setVisible(true);
    }
    public static void main(String[] a) { new Conversor().setDefaultCloseOperation(EXIT_ON_CLOSE); }
}
```
Muestra GUI + eventos + excepciones ([[Programación I - Java C09 Gestión de errores y excepciones]]): $F = \tfrac{9}{5}C + 32$; con 100 °C da 212 °F.

## Errores comunes
- Mezclar AWT y Swing (los componentes pesados tapan a los ligeros).
- Llamar a `frame.add()` con layout `null` sin `setBounds`.
- Olvidar `setDefaultCloseOperation` (la JVM sigue corriendo tras cerrar la ventana).
- No usar `JScrollPane` con `JList` largas.
- Olvidar el `ButtonGroup` en radios.
- Hacer `new JComboBox(array)` con arreglo de tipos distintos o usar el índice sin filtrar `SELECTED`.

## Ejercicios propuestos
1. Formulario de login con `JTextField`, `JPasswordField` y botón que valida contra constantes.
2. Selector de color con tres `JRadioButton` que pinta el fondo.
3. Lista de tareas: `JTextField` + botón "Agregar" que añade a un `DefaultListModel` mostrado en un `JList`.
4. Reescriba `ComboBoxDemo` para que además muestre el nombre del color en un `JLabel`.

## Conexiones
Anterior: [[Programación I - Java GUI C02 Manejo de eventos]]. Siguiente: [[Programación I - Java GUI C05 Generalidades de GUI]]. Resumen previo: [[Programación I - Java GUI C02 Manejo de eventos]]. Aplicaciones completas: [[Programación I - Java Juegos Sokoban y Arkanoid]].

## Fuente
`Material/Java/Teoria/TemaIII-C04 GUI en Java - Swing contenedores y componentes.pdf`; `Material/Java/Practicas/Ejercicios/UV-C03 EjemplosSwing/`.
