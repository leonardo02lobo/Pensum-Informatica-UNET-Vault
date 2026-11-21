---
tags: [clase, semestre-II]
materia: Programación I
fuente: Material/Java/Practicas/Ejercicios/EjemplosArchivos/src (proyecto NetBeans)
---
# Java - Proyecto EjemplosArchivos (código de la lección de archivos)

Materia: [[Programación I]]

## Contexto
Proyecto NetBeans con **11 clases** numeradas en el orden en que se explican en [[Programación I - Java C10 Archivos en Java]]. Cada una demuestra una técnica distinta de E/S. Los archivos `.dat` incluidos (`prueba.dat`, `inventario.dat`, `inventario2.dat`, `autos.dat`) son la salida de estas clases.

| Clase | Qué demuestra |
|---|---|
| `CreaDatos_1` | escritura de texto con `FileWriter` + `BufferedWriter` + `PrintWriter` |
| `LeeDatos_2` | lectura línea a línea con `BufferedReader` |
| `Producto_3` | clase de dominio con `toString()` y `getDatos()` |
| `CreaInventario_4` | guardar objetos como texto (una línea por producto) |
| `LeeInventario_5` | leer, partir con `StringTokenizer`, convertir y validar |
| `Auto_6` | clase `Serializable` |
| `EscribeObjetoAutos_7` | `ObjectOutputStream.writeObject` |
| `LeeObjetoAutos_8` | `ObjectInputStream.readObject` con casting |
| `LeeScanner1/2/3` | lectura con `Scanner`: números, líneas, datos con formato |

## 1. CreaDatos_1 y LeeDatos_2
```java
FileWriter fw = new FileWriter("prueba.dat");
BufferedWriter bw = new BufferedWriter(fw);
PrintWriter salArch = new PrintWriter(bw);
for (int n = 1; n <= MAX; n++) {
    valor = (int)(Math.random() * 100);     // 0..99
    salArch.print(valor + " ");
}
salArch.println();
salArch.close();
```
`Math.random()` da un `double` en $[0,1)$; multiplicado por 100 y truncado con `(int)` produce enteros de 0 a 99. `LeeDatos_2` abre el mismo archivo y recorre con `while (linea != null)`, imprimiendo cada línea. El `main` declara `throws IOException` (se propaga en vez de tratarse).

## 2. Producto_3, CreaInventario_4, LeeInventario_5
`Producto_3` (nombre, unidades, precio, `DecimalFormat("0.##")`) tiene `toString()` (para mostrar: `nombre: unidades a BsF precio = total`) y `getDatos()` (formato para archivo: `nombre unidades precio`). `CreaInventario_4` crea tres productos (Tuercas 500 x 200, Arandelas 300 x 1000, Tornillos 25000 x 5), y escribe `getDatos()` de cada uno en `inventario.dat` dentro de un `try` con `catch (FileNotFoundException)` y `catch (IOException)` (el específico va primero).

`LeeInventario_5` hace el camino inverso:
```java
tokenizer = new StringTokenizer(linea);
nombre = tokenizer.nextToken();
try {
    unidades = Integer.parseInt(tokenizer.nextToken());
    precio   = Float.parseFloat(tokenizer.nextToken());
    items[cuenta++] = new Producto_3(nombre, unidades, precio);
} catch (NumberFormatException exc) {
    System.out.println("Error en la entrada. Linea ignorada");
}
```
Muestra **excepciones anidadas**: el `try` interno protege cada línea (una línea mala no detiene el proceso) y el externo protege la apertura. Total de cada producto: 500x200 = 100000; 300x1000 = 300000; 25000x5 = 125000.

## 3. Serialización: Auto_6, EscribeObjetoAutos_7, LeeObjetoAutos_8
`Auto_6 implements Serializable` (dueño, marca, modelo; constructor por defecto con "Sin dueño"/"sin marca"/2009 y uno parametrizado; método `escribe()`). Se escriben dos objetos (Fiat Siena 1999 y Ford Fiesta 2004) en `autos.dat` y se leen en el mismo orden con `(Auto_6) entStream.readObject()`. El `main` declara `ClassNotFoundException` además de `IOException`.

## 4. Scanner
- `LeeScanner1`: `new Scanner(new File("prueba.dat"))` y `while (entrada.hasNextLong()) numero = entrada.nextLong();` -> se queda con el **último** número del archivo (porque se sobrescribe `numero` en cada vuelta) y lo imprime.
- `LeeScanner2` (varias líneas) usa `hasNextLine()`/`nextLine()`.
- `LeeScanner3`: lee `inventario2.dat` con `useDelimiter` y extrae `next()`, `nextInt()`, `nextFloat()` por producto; muestra el problema de los reales con coma decimal y de espacios finales, ya señalado en la teoría.

## Qué aprender de este proyecto
1. Los tres niveles de envoltura de flujos y cuándo basta menos (`FileWriter` solo).
2. Fin de archivo: `readLine() == null`, `hasNext...() == false`.
3. Separar la **persistencia** de la clase de dominio (`getDatos()` vs `toString()`).
4. Diferencia texto/serializado y orden de lectura.

## Ejercicios propuestos
1. Modifique `CreaDatos_1` para anexar en vez de sobrescribir. *(`new FileWriter(arch, true)`.)*
2. Haga que `LeeInventario_5` calcule el valor total del inventario (suma de unidades x precio).
3. Serialice los tres `Producto_3` (requiere `Serializable`).

## Fuente
Carpeta `Material/Java/Practicas/Ejercicios/EjemplosArchivos/` (`src/*.java` y archivos `.dat`).
