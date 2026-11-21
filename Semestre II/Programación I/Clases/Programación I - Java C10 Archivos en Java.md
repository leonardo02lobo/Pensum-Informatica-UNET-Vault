---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Teoria/TemaII-C10 Archivos en Java.pdf
---
# Java C10 - Archivos en Java

Materia: [[Programación I]]

## Contexto y objetivo
Las variables y arreglos son **temporales**: al terminar el programa se pierden. Los **archivos de datos** guardan información de forma permanente en almacenamiento auxiliar. Esta lección (Unidad II del programa 2024-2) estudia tres modalidades: archivos de **texto** (flujo secuencial), **objetos serializados** y archivos **binarios**. Requiere dominar [[Programación I - Java C09 Gestión de errores y excepciones]], porque casi toda operación de E/S lanza `IOException`. El código de ejemplo está documentado en [[Programación I - Java Ejemplos de archivos]]. En Estructura de Datos se retoma el tema en C++: [[Estructura de Datos - Archivos Binarios y Acceso Directo en C++]].

## 1. Conceptos generales
- Un archivo contiene **bytes** o **caracteres** (texto) y se lee del mismo modo.
- Java tiene unas 20 clases de acceso a archivos (paquete `java.io`), cada una con métodos propios.
- Acceso **secuencial (de flujo)**: solo se puede leer el siguiente elemento; para llegar al último hay que leer los anteriores. Acceso **aleatorio**: posicionarse en cualquier byte (`RandomAccessFile`, no desarrollado en el PDF).
- Un **flujo (stream)** es la conexión entre el programa y el archivo. Siempre hay que **cerrarlo** (`close()`): de lo contrario no se garantiza que los datos se vacíen al disco.

## 2. Archivos de texto
Jerarquía usada:
| Lectura | Escritura |
|---|---|
| `FileReader` (caracteres desde archivo) | `FileWriter` (caracteres hacia archivo) |
| `BufferedReader` (búfer, `readLine()`) | `BufferedWriter` (búfer) |
| | `PrintWriter` (`print`, `println` como `System.out`) |

Patrón de **decoradores**: cada clase envuelve a la anterior para añadir una capacidad.

### Escritura
```java
FileWriter fw = new FileWriter("prueba.dat");          // abre/crea (sobrescribe)
BufferedWriter bw = new BufferedWriter(fw);            // añade búfer
PrintWriter salArch = new PrintWriter(bw);             // añade print/println
for (int n = 1; n <= 10; n++) salArch.print((int)(Math.random()*100) + " ");
salArch.println();
salArch.close();
```
`new FileWriter(nombre, true)` abre en modo **anexar** (append) en lugar de sobrescribir. Este ejemplo genera `prueba.dat` con diez enteros aleatorios entre 0 y 99 separados por espacios.

### Lectura línea a línea
```java
BufferedReader ent = new BufferedReader(new FileReader("prueba.dat"));
String linea = ent.readLine();
while (linea != null) {          // null indica fin de archivo
    System.out.println(linea);
    linea = ent.readLine();
}
ent.close();
```
`FileReader` abre el flujo y lanza `FileNotFoundException` si el archivo no existe.

### Archivos con objetos en formato de texto
Se guarda cada objeto como una línea (por ejemplo `nombre unidades precio`) mediante un método `getDatos()`; al leer, se parte la línea con `StringTokenizer` (o `split`) y se convierte con `Integer.parseInt`/`Float.parseFloat`, capturando `NumberFormatException` para ignorar líneas dañadas (ver el ejemplo del inventario).

### Lectura con Scanner
`Scanner` (java.util) lee del teclado **o de un archivo**: `new Scanner(new File("prueba.dat"))`.
```java
Scanner entrada = new Scanner(new File("prueba.dat"));
while (entrada.hasNextLong()) numero = entrada.nextLong();   // lee todos los enteros
entrada.close();
```
- Para varias líneas: `while (entrada.hasNextLine()) { String l = entrada.nextLine(); ... }`.
- Para leer con formato (nombre, entero, real): `next()`, `nextInt()`, `nextFloat()`; con `useDelimiter(...)` se define el separador.
- Advertencia del PDF: `nextFloat()` depende de la configuración regional (*locale*); en español los reales usan **coma** como separador decimal y un espacio extra al final de línea puede alterar la lectura. Solución: `entrada.useLocale(Locale.US)` o escribir los datos con un formato consistente.

## 3. Objetos serializados
**Serializar** es convertir un objeto en una secuencia de bytes que lo representan, para guardarlo en un archivo o transmitirlo por red; **deserializar** es reconstruirlo.
- La clase debe implementar la interface **`Serializable`** (interface *marcadora*, sin métodos, que sirve de bandera). Todos los atributos deben ser serializables (primitivos, `String`, etc.) o marcarse `transient` para excluirlos.
- Escritura: `FileOutputStream` envuelto en `ObjectOutputStream`; método `writeObject`.
- Lectura: `FileInputStream` envuelto en `ObjectInputStream`; método `readObject`, que devuelve `Object` y exige **casting**; lanza `ClassNotFoundException` además de `IOException`.

```java
public class Auto implements Serializable {
    String duenho, marca; int modelo;
    ...
}
// escribir
FileOutputStream salArch = new FileOutputStream("info.dat");
ObjectOutputStream salStream = new ObjectOutputStream(salArch);
salStream.writeObject(miAuto);
salStream.close();
// leer
FileInputStream entArch = new FileInputStream("info.dat");
ObjectInputStream entStream = new ObjectInputStream(entArch);
Auto c = (Auto) entStream.readObject();
entStream.close();
```
Los objetos se leen **en el mismo orden** en que se escribieron. Un archivo de objetos no es legible como texto (es binario); no se puede "editar a mano".

## 4. Archivos binarios
Los flujos de bytes (`FileInputStream`/`FileOutputStream`) y de datos (`DataInputStream`/`DataOutputStream`, con `writeInt`, `readDouble`, `writeUTF`...) guardan tipos primitivos en su representación binaria: más compactos y rápidos que el texto, pero no legibles por humanos. El archivo de objetos serializados es un caso particular. El orden de lectura debe coincidir con el de escritura.

## 5. Comparación
| Tipo | Clases | Legible | Uso típico |
|---|---|---|---|
| Texto | FileReader/Writer, BufferedReader, PrintWriter, Scanner | sí | configuración, listados, intercambio |
| Objetos | ObjectOutput/InputStream | no | persistir el estado de objetos completos |
| Binario | Data/File streams | no | datos numéricos, imágenes, sonido |

## Ejemplo resuelto: guardar y cargar una lista de cuentas
```java
class Cuenta implements Serializable { String cliente; double saldo; ... }
static void guardar(ArrayList<Cuenta> v, String f) throws IOException {
    try (ObjectOutputStream o = new ObjectOutputStream(new FileOutputStream(f))) {
        o.writeObject(v);          // ArrayList ya es Serializable
    }
}
@SuppressWarnings("unchecked")
static ArrayList<Cuenta> cargar(String f) throws IOException, ClassNotFoundException {
    try (ObjectInputStream i = new ObjectInputStream(new FileInputStream(f))) {
        return (ArrayList<Cuenta>) i.readObject();
    }
}
```
Se serializa la colección completa de una vez; es el patrón usado en el proyecto final y en el banco para "persistir" datos (ver [[Programación I - Java Proyecto final 2024]]).

## Errores comunes
- No cerrar el flujo (datos perdidos o archivo bloqueado).
- Olvidar que `FileWriter` **sobrescribe** el archivo.
- Leer objetos con tipos o en orden distinto al de escritura.
- Clase sin `implements Serializable` (`NotSerializableException`).
- Rutas relativas: el archivo se busca respecto al directorio de trabajo del proceso.
- Bucle de lectura que no actualiza `linea` (infinito).

## Ejercicios propuestos
1. Escriba 20 números aleatorios en un archivo y calcule su promedio leyéndolos con `Scanner`.
2. Guarde un inventario en texto (`nombre unidades precio`) y cargue solo los productos con existencias bajas.
3. Serialice un arreglo de `Estudiante` y recupérelo.
4. Explique la diferencia entre `PrintWriter` y `DataOutputStream`. *(Texto formateado vs. bytes de primitivos.)*

## Conexiones
Anterior: [[Programación I - Java C09 Gestión de errores y excepciones]]. Siguiente: [[Programación I - Java GUI C01 AWT contenedores y componentes]]. Ver también [[Programación I - Java Ejemplos de archivos]] y [[Programación I - Java GUI C05 Generalidades de GUI]].

## Fuente
`Material/Java/Teoria/TemaII-C10 Archivos en Java.pdf`.
