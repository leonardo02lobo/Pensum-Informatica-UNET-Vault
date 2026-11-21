---
tags: [materia, semestre-I]
semestre: I
---
# Matemática Discreta

**Semestre:** [[Semestre I]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- _Ninguna_

## Desbloquea
- [[Programación I]]

## Apuntes

### Descripción general y objetivos
Matemática Discreta estudia estructuras **finitas o numerables**: conjuntos, relaciones, lógica, grafos y árboles. Es la base formal de la informática (algoritmos, bases de datos, redes, compiladores). Prelación de [[Programación I]]. El Material evidencia un texto guía (Murillo Tsijli, *Introducción a la Matemática Discreta*) y cuatro bloques: conjuntos (I parcial), relaciones, árboles y grafos (III parcial). Programa oficial: verificar.

Notas hijas: [[Matemática Discreta - Teoría de conjuntos y operaciones básicas]], [[Matemática Discreta - Relaciones binarias y representaciones]], [[Matemática Discreta - Grafos, dígrafos y teoremas de Euler y Hamilton]].

### Contenido programático (según Material; verificar con el programa oficial)
1. **Teoría de conjuntos**: pertenencia, inclusión, conjunto universal y vacío, operaciones (unión, intersección, diferencia, complemento, diferencia simétrica), diagramas de Venn, cardinalidad, conjunto potencia, producto cartesiano, leyes del álgebra de conjuntos y simplificación.
2. **Lógica proposicional** (si el programa del lapso la incluye): conectivos, tablas de verdad, tautologías, equivalencias, cuantificadores.
3. **Relaciones**: relación binaria en AxA, dominio, rango, matriz y grafo de una relación; propiedades reflexiva, simétrica, antisimétrica, transitiva; relaciones de equivalencia y de orden.
4. **Grafos y dígrafos**: definiciones, grado, caminos y circuitos, conexidad, representación (matrices de adyacencia e incidencia), teoremas de grafos (suma de grados, Euler, Hamilton).
5. **Árboles**: árbol, raíz, hojas, profundidad, árbol binario y recorridos (preorden, inorden, postorden).

### Conceptos y fórmulas clave
- |A ∪ B| = |A| + |B| - |A ∩ B|; |P(A)| = 2^|A|; |A x B| = |A|·|B|.
- Leyes de De Morgan: (A ∪ B)' = A' ∩ B'; (A ∩ B)' = A' ∪ B'.
- Suma de grados: Σ gr(v) = 2|E|.
- Árbol con n vértices tiene n-1 aristas.
- Euler: un grafo conexo tiene circuito euleriano si todos los vértices tienen grado par.
- Árbol binario completo de altura h: hasta 2^(h+1) - 1 nodos.

### Ejemplo resuelto
Simplificar (A ∪ B) ∩ (A ∪ B'): por distributiva = A ∪ (B ∩ B') = A ∪ ∅ = A.

Recorrido: árbol con raíz R, hijos izq. I (hijos a, b) y der. D. Preorden: R I a b D; inorden: a I b R D; postorden: a b I D R.

### Relación con otras materias
[[Programación I]] y [[Estructura de Datos]] (árboles, grafos), [[Fundamentos de Lógica Digital]] (álgebra booleana como álgebra de conjuntos), [[Base de Datos I]] (relaciones), [[Investigación de Operaciones I]] (redes), [[Análisis Numérico]].

### Evaluación y consejos
- Según el Material: parciales por bloques (conjuntos, relaciones, grafos/árboles) y un crucigrama de repaso. Verificar ponderaciones.
- Haz demostraciones paso a paso citando la ley usada; practica Venn y matrices; resuelve los ejercicios del texto guía.

### Bibliografía recomendada
- Murillo Tsijli, M., *Introducción a la Matemática Discreta* (4.ª ed.).
- Johnsonbaugh, R., *Matemáticas discretas*.
- Grimaldi, *Matemáticas discreta y combinatoria*; Rosen, *Matemática discreta y sus aplicaciones*.

### Recursos del Material/
- [Introducción a la Matemática Discreta 4 Ed. - Murillo Tsijli](Material/GUIAS/Introducción%20a%20la%20Matemática%20Discreta%204%20Ed.%20-%20Manuel%20Murillo%20Tsijli.pdf): texto guía.
- [Matemáticas Discretas - Johnsonbaugh](Material/GUIAS/MATEMATICAS_DISCRETAS_Richard_Johnsonbau.pdf): libro de referencia.
- [Manual de acceso y uso de Zoom](Material/GUIAS/Manual%20de%20acceso%20y%20uso%20de%20Zoom.pdf): guía para clases virtuales.
- Carpeta `PARCIAL 1/`: teoría de conjuntos, leyes de conjuntos (Murillo Tsijli), ejercicios de simplificación (pág. 140), aperitivo de ejercicios y crucigrama de repaso (pdf/docx/xlsx).
- Carpeta `Relaciones/`: [Relaciones parte 1](Material/Relaciones/1%20Relacionesparte1bcarvajal.pdf) y [Relación binaria AxA parte 2](Material/Relaciones/2%20Relación%20binaria%20AxAparte2bcarvajal.pdf).
- Carpeta `Teorema de grafos /`: III parcial, mapas conceptuales de dígrafos, ejemplos de matrices de adyacencia e incidencia.
- [Árbol binario y profundidad (recorrido de árbol)](Material/Recorrido%20del%20Arbol/Árbol%20binario%20y%20profundidad%20(recorrido%20de%20árbol)..pdf): recorridos de árboles.
- [MAPA CONCEPTUAL](Material/Mapas%20/MAPA%20CONCEPTUAL.pdf): síntesis de la materia.
- Otros PDFs sueltos (CamScanner, WPS Office, pruebaIV, 1496160509, Compartir DOC-...): apuntes escaneados y pruebas.
