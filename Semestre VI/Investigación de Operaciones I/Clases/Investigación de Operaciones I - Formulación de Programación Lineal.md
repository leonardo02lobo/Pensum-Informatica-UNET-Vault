---
tags: [clase, semestre-VI]
materia: Investigación de Operaciones I
---
# Investigación de Operaciones I - Formulación de Programación Lineal

Materia: [[Investigación de Operaciones I]]  
Anterior: [[Investigación de Operaciones I - Introducción y Metodología de la IO]]  
Siguiente: [[Investigación de Operaciones I - Método Gráfico y Casos Especiales]]

## Contexto y objetivo

Dominar la **formulación de modelos de Programación Lineal (PL)** según el Tema 2 del aula virtual (Prof. Mariela Borges): identificar variables con sus unidades, escribir la función objetivo y las restricciones, verificar los supuestos de la PL y modelar casos clásicos (producción, mezclas, distribución y agrícolas).

## 1. Modelo general de Programación Lineal

Un modelo de PL optimiza una función lineal sujeta a restricciones lineales:

$$\text{Max (o Min)} \quad Z = \sum_{j=1}^{n} c_j x_j$$
$$\text{sujeto a:} \quad \sum_{j=1}^{n} a_{ij} x_j \; (\le, =, \ge) \; b_i, \quad i = 1, \dots, m$$
$$x_j \ge 0, \quad j = 1, \dots, n$$

## 2. Supuestos fundamentales de la PL

1. **Proporcionalidad**: la contribución de cada variable $x_j$ a $Z$ y a cada restricción es estrictamente proporcional a su valor ($c_j x_j$, $a_{ij} x_j$); no hay economías de escala ni costos fijos de arranque.
2. **Aditividad**: la función objetivo y el uso total de cada recurso son la suma directa de las contribuciones individuales de todas las actividades; no hay términos cruzados como $x_1 x_2$.
3. **Divisibilidad**: las variables pueden tomar valores reales continuos (fraccionarios), no necesariamente enteros.
4. **Certeza**: todos los coeficientes ($c_j, a_{ij}, b_i$) son constantes determinísticas conocidas.

## 3. Ejemplos clásicos de formulación

### A. Modelo de producción (del programa)
Una fábrica produce mesas ($x_1$) y sillas ($x_2$) con utilidades de \$50 y \$30 por unidad. Cada mesa requiere 4 m² de madera y 2 h de mano de obra; cada silla requiere 3 m² de madera y 1 h. Se dispone de 240 m² de madera y 100 h semanales.

$$\text{Max } Z = 50x_1 + 30x_2$$
$$\text{s.a.} \quad 4x_1 + 3x_2 \le 240 \quad \text{(madera, } m^2\text{)}$$
$$\phantom{\text{s.a.}} \quad 2x_1 + x_2 \le 100 \quad \text{(horas)}$$
$$\phantom{\text{s.a.}} \quad x_1, x_2 \ge 0$$

### B. Modelo de mezclas (dieta o refinación)
Se desean mezclar dos ingredientes $A$ y $B$ (en kg/lote: $x_1, x_2$) con costos \$4/kg y \$6/kg para obtener al menos 100 kg de producto, cumpliendo que la proporción de $A$ sea al menos $30\%$ del total y la de $B$ no supere $50$ kg:

$$\text{Min } Z = 4x_1 + 6x_2$$
$$\text{s.a.} \quad x_1 + x_2 \ge 100$$
$$\phantom{\text{s.a.}} \quad x_1 \ge 0.30(x_1 + x_2) \iff 0.70x_1 - 0.30x_2 \ge 0$$
$$\phantom{\text{s.a.}} \quad x_2 \le 50, \quad x_1, x_2 \ge 0$$

### C. Modelo agrícola y de distribución
En modelos agrícolas, $x_{ik}$ suele representar hectáreas asignadas al cultivo $i$ en la parcela $k$, sujeto a disponibilidad de tierra, agua (m³/ha) y rotación. En distribución, $x_{ij}$ representa unidades enviadas del origen $i$ al destino $j$.

## Errores comunes

- Definir variables sin especificar **unidades y período** (ej. escribir "$x_1$ = mesas" en lugar de "$x_1$ = cantidad de mesas a fabricar por semana").
- Dejar restricciones no lineales como cocientes $\frac{x_1}{x_1+x_2} \ge 0.3$ sin linealizarlas multiplicando por $(x_1+x_2)$.
- Omitir las condiciones de no negatividad $x_j \ge 0$.

## Ejercicios propuestos

1. Una empresa ensambla dos tipos de servidores: Básicos ($x_1$, utilidad \$200) y Avanzados ($x_2$, utilidad \$350). Cada Básico requiere 3 h de ensamblaje y 1 h de pruebas; cada Avanzado requiere 5 h de ensamblaje y 2 h de pruebas. Se dispone de 150 h de ensamblaje y 55 h de pruebas. Formula el modelo de PL.
   - *Respuesta:* $\text{Max } Z = 200x_1 + 350x_2$ s.a. $3x_1 + 5x_2 \le 150$, $x_1 + 2x_2 \le 55$, $x_1, x_2 \ge 0$.

## Conexiones

- Anterior: [[Investigación de Operaciones I - Introducción y Metodología de la IO]]
- Siguiente: [[Investigación de Operaciones I - Método Gráfico y Casos Especiales]]
- Materia: [[Investigación de Operaciones I]]
- Materias relacionadas: [[Matemática IV]], [[Economía]]

## Fuente

- `Material/Tema 2. Libro sobre Formulación de Programación Lineal (P.L.). _ AULAVIRTUAL.pdf` (Prof. Mariela Borges, aula virtual UNET).
