---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/UV-C05 GUI en Java - Generalidades.pdf; Material/Java/Practicas/Ejercicios/UV-C04 Generalidades; MenuEnJava (1); AnimacionesBasicas
---
# Java GUI C05 - Generalidades: animaciones, JavaDoc, rutas, imágenes, sonido y menús

Materia: [[Programación I]]

## Contexto y objetivo
Lección de cierre de la Unidad de GUI: reúne las herramientas necesarias para el **proyecto final** (juegos y aplicaciones con gráficos): animaciones con `Timer`, documentación con JavaDoc, rutas por defecto y `FileDialog`, carga de imágenes (`ImageIcon`, `MediaTracker`) y sonido (`Clip`). Se complementa con el material "CURSO JAVA - Menús" (menús en AWT) y con el proyecto `AnimacionesBasicas`, que integra todo. Antecedentes: [[Programación I - Java GUI C04 Swing contenedores y componentes]].

## 1. Animaciones con Timer
`javax.swing.Timer` simula el paso del tiempo: **genera automáticamente un `ActionEvent` cada cierto intervalo** (en milisegundos). Una animación es simplemente "cambiar algo y repintar cada N ms".
```java
Timer tiempo;
tiempo = new Timer(3000, new ActionListener() {          // cada 3 s
    public void actionPerformed(ActionEvent e) {
        // lo que hace el timer en cada tic
    }
});
tiempo.start();      // arrancar
tiempo.stop();       // detener
tiempo.restart();    // re-arrancar
```
Detalles: el `actionPerformed` se ejecuta en el hilo de eventos de Swing, así que debe ser breve; `setDelay(ms)` cambia la velocidad; `setRepeats(false)` hace que dispare una sola vez. Velocidad de cuadros: $\text{fps}=1000/\text{retardo}$ (25 ms equivalen a 40 fps).

## 2. Documentación con JavaDoc
Las clases y métodos se comentan con `/** Propósito */` (comentario de documentación). Pueden incluir etiquetas `@param`, `@return`, `@author`, `@throws`. En NetBeans se genera con clic derecho sobre el proyecto -> *Generate JavaDoc*, o menú *Build -> Generate JavaDoc for "Proyecto"*. La salida se guarda en `dist/javadoc` y el índice es `index.html`. (Por eso el Material contiene muchas carpetas `javadoc` generadas, que no se documentan aquí.)
```java
/**
 * Calcula el área de un círculo.
 * @param r radio (mayor que 0)
 * @return el área
 */
public double area(double r) { return Math.PI * r * r; }
```

## 3. Rutas por defecto y FileDialog
Un recurso (imagen, sonido) se localiza por **ruta**: relativa al directorio de trabajo, o al *classpath* con `getClass().getResource("imagenes/x.png")` (recomendado, funciona dentro del `.jar`). `FileDialog` (AWT) abre la ventana estándar de selección de archivo:
```java
FileDialog fd = new FileDialog(frame, "Abrir archivo", FileDialog.LOAD);
fd.setVisible(true);                       // bloquea (modal) hasta elegir
String nombre = fd.getDirectory() + fd.getFile();   // getFile() es null si se cancela
```
`FileDialog.SAVE` para guardar. En Swing el equivalente es `JFileChooser`.

## 4. Manejo de imágenes
`ImageIcon` carga una imagen desde una ruta/URL; se puede mostrar en un `JLabel` o dibujar con `g.drawImage(icon.getImage(), x, y, this)`.
```java
URL url = getClass().getResource("images/" + (i + 1) + ".PNG");
ImageIcon icono = new ImageIcon(url);
```
`ManejoImagenes` carga 67 cartas (`images/1.PNG` ... `images/67.PNG`) en un arreglo `ImageIcon images[]`: patrón típico de juegos de cartas. Con `MediaTracker` se garantiza que una imagen esté cargada antes de usarla: `tracker.addImage(img, 1); tracker.waitForID(1, 1000);` (espera como máximo 1 s por el ID 1). `ImageIcon` ya lo hace internamente.

### Patrón Singleton: ImageLoader
Las clases `ImageLoader` de `AnimacionesBasicas` y `Arkanoid` cargan **una sola vez** todas las imágenes:
```java
public class ImageLoader {
    private static ImageLoader instance = null;
    private ImageIcon images[];
    private ImageLoader() { /* carga cada png con getResource */ }
    public static ImageLoader getInstance() {
        if (instance == null) instance = new ImageLoader();
        return instance;
    }
    public ImageIcon getImage(int imageId) { ... }
}
```
Constructor **privado** + atributo `static` + método `getInstance()` = Singleton ([[IS 04 - Modelado con UML]]): garantiza una única instancia compartida, evitando cargar imágenes repetidamente.

## 5. Manejo de sonido
Con `javax.sound.sampled` (clase `ManejoSonido`):
```java
URL url = getClass().getResource("sonidos/imagine.mid");
AudioInputStream flujo = AudioSystem.getAudioInputStream(url);
AudioFormat format = flujo.getFormat();
DataLine.Info info = new DataLine.Info(Clip.class, format,
        (int)(flujo.getFrameLength() * format.getFrameSize()));
Clip reprod = (Clip) AudioSystem.getLine(info);
reprod.open(flujo);
reprod.start();                       // o reprod.loop(Clip.LOOP_CONTINUOUSLY)
System.in.read();                     // mantiene vivo el programa mientras suena
```
El constructor declara `UnsupportedAudioFileException`, `IOException` y `LineUnavailableException` (excepciones verificadas, ver [[Programación I - Java C09 Gestión de errores y excepciones]]). Un `Clip` carga el audio completo en memoria (apto para efectos cortos); el `System.in.read()` es necesario porque `start()` es asíncrono y el programa terminaría antes de oír nada.

## 6. Menús (documento "CURSO JAVA - Menús")
Archivo HTML guardado de un curso en línea que explica los **menús AWT**: una barra de menús (`MenuBar`) contiene objetos `Menu` (File, Edit, Help) y cada menú contiene `MenuItem` (Abrir, Cerrar, Guardar, Salir) o submenús. Pasos (en cualquier orden): crear los `MenuItem`; crear los `Menu` y agregarles los items; crear la `MenuBar`, agregarle los menús y asociarla a la ventana (`frame.setMenuBar(barra)`).
- Los **sucesos de los `MenuItem`** (clic) hay que gestionarlos con `ActionListener`, como en los botones; los de los `Menu` (desplegar/ocultar) los gestiona el sistema.
- Constructores: `MenuItem()`, `MenuItem(String label)`, `MenuItem(String label, MenuShortcut s)` (acelerador, tecla rápida). Métodos: `addActionListener`, `setEnabled(boolean)` (deshabilitado se ve en gris), `setLabel`, `setActionCommand`/`getActionCommand` (varios items pueden compartir un gestor y distinguirse por la orden), `setShortcut`.
- `Menu`: `add(MenuItem)`, `addSeparator()`, `insert(item, index)`, `getItem(i)`, `getItemCount()`.
```java
MenuItem abrir = new MenuItem("Abrir"), cerrar = new MenuItem("Cerrar"),
         guardar = new MenuItem("Guardar"), salir = new MenuItem("Salir");
Menu file = new Menu("File");
file.add(abrir); file.add(cerrar); file.add(guardar); file.addSeparator(); file.add(salir);
MenuBar barra = new MenuBar(); barra.add(file);
frame.setMenuBar(barra);
salir.addActionListener(e -> System.exit(0));
```
En Swing: `JMenuBar`, `JMenu`, `JMenuItem` y `JPopupMenu`; se asigna con `setJMenuBar`. El programa de la guía didáctica también menciona menús emergentes (popup) en la Unidad III. (El HTML contiene también scripts publicitarios sin valor académico; el texto aparece con caracteres acentuados dañados por la codificación original.)

## 7. Proyecto AnimacionesBasicas (integración)
`MainFrame extends JFrame` con layout `null`: varios `JLabel` con imágenes (conchas de caracol/"shell" y dos fondos) posicionados con `setBounds`. Dos `Timer` con distintos periodos (100 ms y 25 ms) mueven los sprites y el cambio de cuadro (`shell_frame`); un `KeyAdapter` permite **ENTER** detener (`timer.stop()`), **BARRA ESPACIADORA** reanudar (`restart()`) y **flechas izquierda/derecha** desplazar el fondo 5 px (`background.setBounds(x±5, ...)`), con límites `LLEFT=23`, `LRIGHT=297` y una dirección `DIR` que se invierte al llegar al borde. `Main` instancia y muestra el frame. Demuestra: Timer, eventos de teclado, `ImageLoader` Singleton, layout nulo. La carpeta `UV-C04 Generalidades` repite el mismo proyecto junto a `ManejoImagenes` y `ManejoSonido`.

## Ejemplo resuelto: pelota que rebota
```java
public class Pelota extends JPanel {
    private int x = 10, y = 50, dx = 4;
    public Pelota() {
        new Timer(20, e -> { x += dx; if (x < 0 || x > getWidth() - 20) dx = -dx; repaint(); }).start();
    }
    @Override protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        g.fillOval(x, y, 20, 20);
    }
}
```
Cada 20 ms el Timer actualiza la posición, invierte la dirección en los bordes y llama `repaint()`, que provoca `paintComponent`. Es el bucle básico de cualquier juego: actualizar estado y redibujar ([[Programación I - Java Juegos Sokoban y Arkanoid]]).

## Errores comunes
- `getResource` devuelve `null` si la ruta es incorrecta (luego `NullPointerException` en `new ImageIcon(url)`): revisar mayúsculas/minúsculas y la carpeta dentro de `src`.
- Usar `java.util.Timer` en lugar de `javax.swing.Timer` para tocar componentes Swing.
- No llamar `repaint()` tras cambiar coordenadas.
- Cargar imágenes dentro del bucle de animación (lento): cargar una sola vez.
- Olvidar mantener vivo el programa al reproducir sonido.

## Ejercicios propuestos
1. Reloj digital con `Timer(1000, ...)` y un `JLabel`.
2. Slideshow que cambie de imagen cada 3 s.
3. Mover un `JLabel` con las flechas del teclado dentro de un `JFrame`.
4. Añadir un efecto de sonido al chocar la pelota con el borde.

## Conexiones
Anterior: [[Programación I - Java GUI C04 Swing contenedores y componentes]]. Siguiente: [[Programación I - C++ C01 Programación orientada a objetos]]. Aplicaciones: [[Programación I - Java Juegos Sokoban y Arkanoid]], [[Programación I - Java Proyecto final 2024]]. Archivos: [[Programación I - Java C10 Archivos en Java]].

## Fuente
`Material/Java/Teoria/UV-C05 GUI en Java - Generalidades.pdf`; `Material/Java/Practicas/Ejercicios/UV-C04 Generalidades/`; `AnimacionesBasicas/`; `MenuEnJava (1)/CURSO JAVA - Menús.htm`.
