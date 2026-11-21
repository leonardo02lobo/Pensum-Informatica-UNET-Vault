---
tags: [materia, semestre-IV]
semestre: IV
---
# Programación II

**Semestre:** [[Semestre IV]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Estructura de Datos]]

## Desbloquea
- [[Base de Datos I]]
- [[Organización del Computador]]

## Apuntes

### Descripción general y objetivos

Programación II (código 0425401T / 0415405T según el documento; **verificar** el vigente) fortalece lo aprendido en [[Programación I]] y [[Estructura de Datos]] y abre la formación profesional: estilos de codificación, técnicas de resolución de **problemas de lógica matemática**, y (en la versión SEED UNET 4.0 de la Prof. Desirre Suárez) **desarrollo web dinámico con PHP, MySQL y patrón MVC**. El analítico histórico incluye además programación concurrente y comunicaciones (sockets TCP/UDP en Java y C#), por lo que el contenido real depende del lapso: verificar con el programa oficial y el docente.

Objetivo general de la guía didáctica: implementar programas usando técnicas lógico-matemáticas en entornos locales y web.

### Contenido programático

#### Versión analítico (unidades I a IV)
**I. Estilos de programación**: extensibilidad, verificabilidad, reparabilidad, evolución, comprensibilidad; nombres de variable, indentación, booleanos en decisiones, bucles y espaciado; estilos K&R, Allman, BSD KNF, Whitesmiths y GNU.

**II. Técnicas de programación y problemas lógicos** (C++): programación no estructurada, procedimental, modular, orientada a objetos y extrema; manejo de cadenas, **backtracking**, ejercicios geométricos y numéricos, combinatoria y grafos.

**III. Programación concurrente**: funciones de los sistemas operativos, concurrencia y su problemática, hilos (creación, arranque, suspensión, sincronización), interbloqueo.

**IV. Introducción a comunicaciones**: modelo OSI, IP/DNS, TCP y UDP, sockets y puertos, aplicaciones cliente-servidor en Java y C#.

Ponderación del analítico: 1.er parcial 32 % (U-I y II), 2.º parcial 34 % (U-III y IV), con 55 puntos de examen y 45 de proyectos/prácticas en el primero y 75/25 en el segundo.

#### Versión guía SEED UNET 4.0 (ruta de 16 semanas)
- Semanas 1-4: estilos de programación, técnicas (recursividad, combinatoria, árboles, grafos) y problemas de lógica matemática.
- Semana 5: Parcial 1.
- Semanas 6-8: diseño de páginas web y sitios web dinámicos (HTML, CSS, JavaScript).
- Semanas 9-10: bases de datos, PHP con MySQL.
- Semana 11: Parcial 2.
- Semanas 12-15: aplicaciones web con PHP y **MVC**, patrones de diseño, frameworks.
- Semana 16: Parcial 3.
Las actividades son individuales o en grupos de 2 a 4; se usan Classroom, Google Groups y GitHub.

### Conceptos clave

- **Estilo de codificación**: convenciones de nombres, sangrado y llaves que mejoran la legibilidad (ver guías de convenciones de Java y Python del Material).
- **Backtracking**: búsqueda exhaustiva con retroceso al detectar que una rama no conduce a solución.
- **Recursividad**: función que se define en términos de sí misma, con caso base.
- **BFS en cuadrículas**: camino más corto en laberintos/mapas.
- **Hilo (thread)**: flujo de ejecución dentro de un proceso; **condición de carrera** y **deadlock**.
- **MVC**: separación Modelo (datos), Vista (interfaz) y Controlador (lógica).
- **Netiqueta**: normas de comunicación en línea (documento del Material).

### Código de ejemplo

Backtracking: generar todas las permutaciones de un arreglo.

```cpp
void permutar(vector<int>& a, int k) {
    if (k == a.size()) { for (int x : a) cout << x << ' '; cout << '\n'; return; }
    for (int i = k; i < a.size(); i++) {
        swap(a[k], a[i]);
        permutar(a, k + 1);
        swap(a[k], a[i]);          // retroceso
    }
}
```

BFS con restricción (idea del acumulativo "Ruta del Tesoro"): estado = (fila, columna, X visitadas); se descartan estados con `X > K`.

```cpp
struct Estado { int f, c, x, pasos; };
queue<Estado> q; q.push({fe, ce, 0, 0});
// visitado[f][c][x] evita repetir estados
while (!q.empty()) {
    auto s = q.front(); q.pop();
    if (mapa[s.f][s.c] == 'T') return s.pasos;
    for (int d = 0; d < 4; d++) {
        int nf = s.f + df[d], nc = s.c + dc[d];
        if (!dentro(nf, nc) || mapa[nf][nc] == '#') continue;
        int nx = s.x + (mapa[nf][nc] == 'X');
        if (nx > K || visitado[nf][nc][nx]) continue;
        visitado[nf][nc][nx] = true;
        q.push({nf, nc, nx, s.pasos + 1});
    }
}
```

Hilos en Java:

```java
Thread t = new Thread(() -> System.out.println("Hola desde un hilo"));
t.start(); t.join();
```

### Ejemplos de problemas del Material

1. **Frecuencia de palabras** (Práctica 1, 2025-1): leer `texto.in` y `prohibidas.in`, ignorar mayúsculas y signos, y listar cada palabra con su frecuencia en orden alfabético (lista ordenada o `map`).
2. **Detección de minas** (Práctica 3): celda (i,j) es "mina" si `densidad + promedio de las 8 vecinas > 40`; en bordes se promedian solo los vecinos existentes.
3. **Juego de la Vida digital** (Primer examen, 25/06/25): autómata con presas, depredadores y espacios vacíos; reglas de nacimiento, muerte y movimiento por vecindad de 8 celdas.
4. **Ruta del tesoro** (Acumulativo, 20 pts): camino más corto en cuadrícula limitando las celdas peligrosas, con salida a archivo e imagen.

### Relación con otras materias

- Prelación: [[Estructura de Datos]] (listas, árboles, grafos, archivos).
- Desbloquea [[Base de Datos I]] (SQL y acceso desde aplicaciones, MySQL/PHP) y [[Organización del Computador]].
- Los temas de concurrencia y comunicaciones enlazan con [[Sistemas Operativos]] e [[Introducción a las Telecomunicaciones]].
- Los problemas combinatorios y de grafos se apoyan en [[Matemática Discreta]].

### Evaluación y consejos de estudio

- Parciales prácticos fuera de línea más un proyecto por corte. Rúbricas y porcentajes: ver la guía didáctica y verificar con el programa oficial.
- Entrenar con problemas estilo concurso: leer de archivo hasta EOF, formato de salida exacto.
- Probar con casos mínimos y máximos (por ejemplo N = 2 y N = 50 en las cuadrículas).
- Seguir una guía de estilo desde el primer día (Java/Python) y comentar solo lo necesario.
- Versionar con Git/GitHub.

### Bibliografía recomendada

- Hristov, A. (2007). *Manual de estilo de programación* (Creative Commons).
- Joyanes Aguilar, L. *Programación orientada a objetos*, McGraw-Hill.
- Deitel y Deitel. *Cómo programar en Java*, Prentice Hall.
- Calvert, K. y Donahoo, M. *TCP/IP Sockets in Java*, Morgan Kaufmann.
- Cormen et al. *Introduction to Algorithms*; Skiena. *The Algorithm Design Manual*.

### Recursos del Material/

- [Analítico (0425401T)](Material/0425401T-%20Programaci%C3%B3n%20II-%20Analitico%20(1).pdf): programa analítico por unidades (hay copias duplicadas con sufijo `(1)`).
- [Guía didáctica SEED UNET 4.0](Material/Guia%20didactica%20Pregrado%20SEED%20UNET%204.0%20Programacion%20II%20.pdf): ruta de aprendizaje semanal, cronograma y rúbricas.
- [Acumulativo para el Primer Corte.pdf](Material/Acumulativo%20para%20el%20Primer%20Corte.pdf): problema "Ruta del Tesoro" (BFS con límite de terreno peligroso).
- [P1Prog2_20251.pdf](Material/P1Prog2_20251.pdf): primer examen, Juego de la Vida digital.
- [PracticaI20251.pdf](Material/PracticaI20251.pdf), [P3PII20251.pdf](Material/P3PII20251.pdf), [Práctica 4.pdf](Material/Pr%C3%A1ctica%204.pdf): prácticas (frecuencia de palabras, detección de minas, gestión de inventario con clase `Data.h`).
- [convenciones-codigo-java.pdf](Material/convenciones-codigo-java.pdf), [Convenciones de código .pdf](Material/Convenciones%20de%20c%C3%B3digo%20.pdf) y [Guía de estilo para el código Python.pdf](Material/Gu%C3%ADa%20de%20estilo%20para%20el%20c%C3%B3digo%20Python.pdf): guías de estilo.
- [Estructura de Ensayo-1.pdf](Material/Estructura%20de%20Ensayo-1.pdf) y [Normas NETiqueta-1.pdf](Material/Normas%20NETiqueta-1.pdf): normas para trabajos escritos y comunicación.
- Nota: [II parcial 2025-1.pdf](Material/II%20parcial%202025-1.pdf) y [III parcial 2025-1.pdf](Material/III%20parcial%202025-1.pdf) corresponden en realidad a [[Fundamentos de Lógica Digital]] (están archivados aquí por error).
