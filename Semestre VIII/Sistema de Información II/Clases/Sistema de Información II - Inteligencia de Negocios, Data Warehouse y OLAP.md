---
tags: [clase, semestre-VIII]
materia: Sistema de Información II
---
# Sistema de Información II - Inteligencia de Negocios, Data Warehouse y OLAP

Materia: [[Sistema de Información II]]
Anterior: [[Sistema de Información II - Diseño Detallado con UML y Procesos BPMN]]
Siguiente: [[Sistema de Información II - Seguridad, Control de Acceso y Continuidad Operativa]]

## Contexto y objetivo
Comprender cómo los sistemas transaccionales alimentan plataformas de **Inteligencia de Negocios (BI)** mediante procesos **ETL**, **Almacenes de Datos (Data Warehouse)** con modelado dimensional (esquema estrella), **cubos OLAP**, **KPIs** y tableros gerenciales, conectando con el caso práctico [[Data Warehouse Atenciones Estudiantiles]].

## 1. OLTP vs. OLAP y el Data Warehouse
- **OLTP (*Online Transaction Processing*)**: bases de datos operacionales de los TPS. Altamente normalizadas (3FN) para evitar redundancia, optimizadas para inserciones/actualizaciones rápidas de registros individuales.
- **OLAP (*Online Analytical Processing*) / Data Warehouse (DWH)**: repositorio centralizado para análisis histórico. Según Bill Inmon, un DWH es *orientado a temas, integrado, no volátil y variante en el tiempo*.

## 2. Proceso ETL (Extracción, Transformación y Carga)
1. **Extracción (Extract)**: lee datos desde múltiples fuentes heterogéneas (BD relacionales, archivos CSV/Excel, APIs).
2. **Transformación (Transform)**: limpieza de nulos y duplicados, estandarización de formatos (fechas, cédulas, categorías), cálculo de métricas derivadas y resolución de claves subrogadas (*surrogate keys*).
3. **Carga (Load)**: inserta los datos limpios en el DWH (carga inicial o incremental periódica).

## 3. Modelado dimensional: esquema estrella y operaciones OLAP
En lugar de 3FN, el DWH utiliza el **esquema estrella** (*Star Schema*) de Ralph Kimball:
- **Tabla de hechos (*Fact Table*)**: en el centro, almacena métricas numéricas aditivas o semiaditivas (ej. `duracion_min`, `satisfaccion`, `cantidad_vendida`) y llaves foráneas hacia las dimensiones.
- **Tablas de dimensiones (*Dimension Tables*)**: rodean a la tabla de hechos y proveen el contexto descriptivo (*quién, qué, dónde, cuándo*): `dim_tiempo`, `dim_servicio`, `dim_estudiante`, `dim_sede`.

Operaciones analíticas sobre cubos OLAP:
- **Roll-up**: agregar datos subiendo en la jerarquía (ej. día $\to$ mes $\to$ año).
- **Drill-down**: desagregar bajando en la jerarquía (año $\to$ trimestre $\to$ mes).
- **Slice**: filtrar una dimensión fija (ej. solo año 2025).
- **Dice**: seleccionar un subcubo filtrando múltiples dimensiones.
- **Pivot**: rotar los ejes de análisis (filas por columnas).

## 4. KPIs y tableros gerenciales (Power BI)
Un **KPI** (*Key Performance Indicator*) mide el grado de cumplimiento de un objetivo estratégico (debe ser específico, medible, relevante y con meta definida).

### Ejemplo SQL sobre el DWH (caso Atenciones Estudiantiles)
```sql
-- KPI: atenciones mensuales y satisfacción promedio por año/mes
SELECT t.anio,
       t.mes,
       COUNT(*) AS total_atenciones,
       ROUND(AVG(h.satisfaccion), 2) AS satisfaccion_promedio
FROM dwh.hecho_atenciones h
JOIN dwh.dim_tiempo t ON h.id_tiempo = t.id_tiempo
GROUP BY t.anio, t.mes
ORDER BY t.anio, t.mes;
```

## Errores comunes
- Ejecutar consultas analíticas pesadas (`GROUP BY` sobre millones de filas históricas) directamente contra la base de datos OLTP de producción, degradando la operación diaria.
- Usar llaves naturales de negocio (p. ej., cédula o código cambiante) en lugar de **llaves subrogadas** enteras en las dimensiones del DWH.
- Crear métricas de vanidad en Power BI (gráficos llamativos sin meta ni decisión asociada) en lugar de KPIs accionables.

## Ejercicios propuestos
1. Para un DWH de ventas minoristas, identifique una tabla de hechos (con 2 métricas) y tres tablas de dimensiones.
   - *Respuesta*: `hecho_ventas` (métricas: `unidades_vendidas`, `monto_total`); dimensiones: `dim_tiempo`, `dim_producto`, `dim_sucursal` (o `dim_cliente`).
2. Si un gerente pasa de ver las ventas totales del año 2025 a desglosarlas por trimestre y luego por mes, ¿qué operación OLAP está realizando?
   - *Respuesta*: **Drill-down** (navegación hacia mayor nivel de detalle en la jerarquía de `dim_tiempo`).

## Conexiones
- Caso práctico del vault en [[Data Warehouse Atenciones Estudiantiles]].
- Fundamentos de almacenes y SQL analítico en [[Base de Datos II]] y [[Análisis y Procesamiento de Datos]].
- Soporte a la evaluación financiera de la empresa en [[Finanzas para Ingenieros - Estados Financieros y Razones Financieras]].

## Fuente
Basado en el programa orientativo de [[Sistema de Información II]] (Kimball, *The Data Warehouse Toolkit*; Laudon & Laudon, *Sistemas de Información Gerencial*).
