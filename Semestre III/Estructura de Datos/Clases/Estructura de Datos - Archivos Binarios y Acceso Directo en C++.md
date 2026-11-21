---
tags: [clase, semestre-III]
materia: Estructura de Datos
---
# Estructura de Datos - Archivos Binarios y Acceso Directo en C++

Materia: [[Estructura de Datos]]
Anterior: [[Estructura de Datos - Tipos Abstractos de Datos y Plantillas en C++]]
Siguiente: [[Estructura de Datos - Métodos de Ordenamiento Interno y Externo]]

## Contexto y objetivo

Los datos en memoria RAM se pierden al cerrar el programa. El Tema 1 de [[Estructura de Datos]] (ver también Archivos binarios en C++) aborda la persistencia en almacenamiento secundario mediante flujos (`fstream`) en C++, comparando archivos de texto y binarios, e implementando operaciones CRUD con acceso secuencial y directo.

## 1. Archivos de texto vs. archivos binarios

| Característica | Archivo de texto | Archivo binario |
|---|---|---|
| Representación | Caracteres ASCII/UTF-8 legibles | Imagen exacta de los bytes en memoria |
| Separación | Delimitadores (`\n`, `;`, espacio) | Tamaño fijo del `struct` / registro |
| Acceso | Secuencial (longitud variable por línea) | Secuencial y **directo** ($O(1)$ por posición) |
| Uso típico | Reportes (`Estadistica.txt`), intercambio | Bases de datos locales, registros fijos |

## 2. Flujos y modos de apertura en `<fstream>`

- `ifstream`: solo lectura.
- `ofstream`: solo escritura.
- `fstream`: lectura y escritura simultánea.

Banderas combinables con `|`:
- `ios::in` (abrir para lectura; falla si no existe).
- `ios::out` (abrir para escritura; trunca si ya existe salvo que se combine con `ios::in` o `ios::app`).
- `ios::app` (escribir siempre al final).
- `ios::binary` (evita traducciones de fin de línea `\n` $\leftrightarrow$ `\r\n`).

Patrón seguro para abrir o crear un binario de lectura/escritura:
```cpp
fstream arc("flota.dat", ios::in | ios::out | ios::binary);
if (!arc) {
    arc.open("flota.dat", ios::out | ios::binary);
    arc.close();
    arc.open("flota.dat", ios::in | ios::out | ios::binary);
}
```

## 3. Acceso directo: `seekg`, `seekp` y `tellg`

Cuando todos los registros tienen tamaño fijo `sizeof(Registro)`, el registro de índice $i$ (empezando en $0$) comienza exactamente en el byte:
$$\text{offset}(i) = i \times \text{sizeof}(\text{Registro})$$

- `seekg(offset, origen)`: mueve el puntero de lectura (*get*).
- `seekp(offset, origen)`: mueve el puntero de escritura (*put*).
- Orígenes: `ios::beg` (inicio), `ios::cur` (posición actual), `ios::end` (final).
- Cantidad de registros en el archivo:
```cpp
arc.seekg(0, ios::end);
long nRegistros = arc.tellg() / sizeof(Registro);
```

## 4. CRUD completo sobre archivo binario

En C++, los registros binarios deben usar arreglos `char[]` de tamaño fijo en lugar de `std::string` (ya que `std::string` guarda un puntero interno a memoria dinámica, no los caracteres dentro del `struct`).

```cpp
struct Vehiculo {
    int id;
    char placa[12];
    char modelo[30];
    bool activo; // bandera para eliminación lógica
};

bool leerRegistro(fstream& arc, int idx, Vehiculo& v) {
    arc.clear(); // limpiar flags de EOF antes de reposicionar
    arc.seekg(idx * sizeof(Vehiculo), ios::beg);
    return static_cast<bool>(arc.read(reinterpret_cast<char*>(&v), sizeof(Vehiculo)));
}

void modificarRegistro(fstream& arc, int idx, const Vehiculo& v) {
    arc.clear();
    arc.seekp(idx * sizeof(Vehiculo), ios::beg);
    arc.write(reinterpret_cast<const char*>(&v), sizeof(Vehiculo));
}
```

**Eliminación lógica vs. física:**
- **Lógica**: marcar `v.activo = false` y reescribir en sitio ($O(1)$).
- **Física**: copiar solo los registros activos a un archivo temporal, borrar el original y renombrar ($O(n)$).

## Errores comunes

- Guardar `std::string` dentro de un `struct` y escribirlo con `write()`: al leerlo en otra ejecución, el puntero interno apunta a basura y provoca *segmentation fault*.
- No llamar a `arc.clear()` después de llegar a `EOF` en un ciclo `while (arc.read(...))`: las llamadas posteriores a `seekg`/`seekp` fallarán silenciosamente.
- Abrir un archivo existente con `ios::out | ios::binary` sin `ios::in`, borrando todo su contenido.

## Ejercicios propuestos

1. Si un archivo binario pesa `4800` bytes y `sizeof(Usuario) == 64`, ¿cuántos registros contiene y en qué byte inicia el registro con índice `10`?
2. ¿Por qué conviene usar eliminación lógica durante la operación normal y compactación física solo al cerrar?

**Respuestas:**
1. Contiene $4800 / 64 = 75$ registros; el índice `10` inicia en el byte $10 \times 64 = 640$.
2. Porque la eliminación lógica es $O(1)$ y no desplaza los índices de acceso directo de los demás registros.

## Conexiones

- Amplía Archivos binarios en C++.
- Es la base para el ordenamiento y la búsqueda externa en [[Estructura de Datos - Métodos de Ordenamiento Interno y Externo]] y [[Base de Datos I]].

## Fuente

Basado en `Material/Tema 1-Archivos Binarios y de Texto/Presentacion Archivos binarios.ppsx`, `primer proyecto-parcial 1.pdf` y los archivos de `Primer Proyecto Parcial 1/`.
