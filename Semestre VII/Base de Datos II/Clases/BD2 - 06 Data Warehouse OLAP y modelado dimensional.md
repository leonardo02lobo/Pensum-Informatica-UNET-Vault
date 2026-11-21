---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: conocimiento general (Kimball) + README.md del proyecto
---
# BD2 - 06 Data Warehouse, OLAP y modelado dimensional

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 05 Indices y optimizacion de consultas]]
Siguiente: [[BD2 - 07 DWH Atenciones DDL y modelo estrella]]

## Contexto y objetivo
Las bases de datos operacionales (OLTP) están diseñadas para registrar transacciones; analizar con ellas es lento y arriesgado. Un **almacén de datos (Data Warehouse, DWH)** reúne datos históricos e integrados para apoyar decisiones. Objetivo: distinguir OLTP/OLAP, conocer la arquitectura de un DWH y dominar el modelado dimensional de Kimball.

## Definición (Inmon)
Un DWH es una colección de datos **orientada a temas, integrada, variable en el tiempo y no volátil** que apoya la toma de decisiones.

## OLTP vs OLAP
| Aspecto | OLTP | OLAP |
|---|---|---|
| Propósito | operar el negocio | analizar |
| Operaciones | muchas lecturas/escrituras cortas | consultas agregadas grandes, lectura |
| Modelo | normalizado (3FN) | dimensional (estrella) |
| Datos | actuales | históricos |
| Usuarios | operadores, aplicaciones | analistas, directivos |
| Métrica | transacciones/s | tiempo de consulta |

## Arquitecturas
- **Inmon (corporativa)**: DWH central normalizado + *data marts* derivados.
- **Kimball (bus dimensional)**: *data marts* dimensionales conformados que se integran por dimensiones compartidas.
- Capas típicas: Fuentes → **Staging** (copia cruda) → DWH (presentación) → BI. El proyecto del vault usa tres esquemas: `stg`, `dwh`, `etl` (ver [[BD2 - 07 DWH Atenciones DDL y modelo estrella]]).

## Modelado dimensional (proceso de 4 pasos de Kimball)
1. Elegir el **proceso de negocio** (ej. atención a estudiantes).
2. Declarar el **grano** (qué es una fila de la tabla de hechos). Se decide **antes** que todo lo demás.
3. Identificar las **dimensiones** (quién, qué, dónde, cuándo, cómo).
4. Identificar los **hechos/métricas** (numéricos y, mejor, aditivos).

### Tabla de hechos
Contiene claves foráneas a las dimensiones + medidas. Tipos de medida: **aditiva** (suma en todas las dimensiones: duración), **semiaditiva** (saldo: no se suma en el tiempo), **no aditiva** (ratios, promedios: guardar numerador y denominador). Tipos de tabla de hechos: transaccional, snapshot periódico, snapshot acumulativo, sin hechos (*factless*).

### Dimensiones
Atributos descriptivos, desnormalizados, con **clave subrogada**. Tipos especiales:
- **Dimensión de tiempo/calendario**: siempre presente.
- **Degenerada**: un identificador que vive en el hecho (nº de factura).
- **Conformada**: compartida por varios hechos con el mismo significado.
- ***Junk* / de combinación**: reúne banderas de baja cardinalidad (el proyecto usa `dim_tipo_modalidad` = tipo × modalidad).
- **Rol múltiple** (*role-playing*): la misma dimensión (fecha) usada varias veces (fecha de pedido, de envío).
- **Miembro desconocido**: fila con clave -1 para hechos sin dimensión resoluble.

### Esquemas
- **Estrella**: dimensiones desnormalizadas directamente ligadas al hecho. Menos joins, más simple.
- **Copo de nieve**: dimensiones normalizadas en subtablas. Ahorra espacio, más joins.
- **Constelación**: varias tablas de hechos que comparten dimensiones.

## OLAP: operaciones
Cubo multidimensional: ejes = dimensiones, celdas = medidas.
- **Roll-up** (agregar subiendo jerarquía: mes→año) / **Drill-down**.
- **Slice** (fijar una dimensión) / **Dice** (subcubo con varios filtros).
- **Pivot** (rotar ejes).
Implementaciones: ROLAP (sobre tablas relacionales, SQL con `GROUP BY ROLLUP/CUBE`), MOLAP (cubos propios), HOLAP (híbrido).
```sql
SELECT t.anio, t.mes, tm.tipo, COUNT(*)
FROM dwh.hecho_atenciones h
JOIN dwh.dim_tiempo t USING (id_tiempo)
JOIN dwh.dim_apoyo a USING (id_apoyo)
JOIN dwh.dim_tipo_modalidad tm USING (id_tipo_modalidad)
GROUP BY ROLLUP (t.anio, t.mes), tm.tipo;
```

## ETL / ELT
**Extract** (leer fuentes), **Transform** (limpiar, validar, conformar, resolver claves), **Load** (cargar dimensiones primero y hechos después, por integridad referencial). Carga **inicial** vs **incremental** (marca de agua, CDC). Detalle práctico en [[BD2 - 09 ETL carga inicial y carga diaria]].

## Dimensiones lentamente cambiantes (SCD)
Tipo 0 (fijo), 1 (sobrescribir), 2 (nueva fila con vigencia), 3 (columna "anterior"), 6 (híbrido). Ver [[BD2 - 08 SCD Tipo 2 y claves subrogadas]].

## Ejemplo resuelto: diseñar un mini-DWH de ventas
- Proceso: ventas en tienda. Grano: **una línea de factura**.
- Dimensiones: producto, cliente, tienda, fecha. Hechos: cantidad (aditiva), monto (aditiva), precio unitario (no aditiva: se calcula monto/cantidad).
- Pregunta: "ventas por categoría y mes" = hecho → dim_producto, dim_fecha, `GROUP BY categoria, mes`.
Error típico: poner "total de la factura" en cada línea (se duplicaría al sumar).

## Errores comunes
- Mezclar granos en un mismo hecho.
- Usar claves del origen como claves del DWH (acoplamiento).
- Normalizar en exceso las dimensiones.
- Sumar medidas no aditivas.
- Cargar hechos antes que las dimensiones.

## Ejercicios propuestos
1. ¿Qué grano tendría "inscripciones por estudiante y materia"? *Resp.: una inscripción de un estudiante a una sección en un período.*
2. Clasifique "saldo de cuenta". *Resp.: semiaditiva (no se suma en el tiempo).*
3. Diferencie slice y dice. *Resp.: slice fija una dimensión; dice selecciona rangos en varias.*

## Conexiones
[[BD2 - 07 DWH Atenciones DDL y modelo estrella]], [[Análisis y Procesamiento de Datos]], [[Sistema de Información II]] (BI), [[Estadística I]].

## Fuente
Conocimiento general (Kimball y Ross, *The Data Warehouse Toolkit*; Inmon) y decisiones de diseño del `README.md` del proyecto.
