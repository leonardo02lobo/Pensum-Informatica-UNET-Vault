---
tags: [tema, semestre-VII]
semestre: VII
---
# Data Warehouse Atenciones Estudiantiles

Nota hija de [[Base de Datos II]]. Resume el proyecto práctico guardado en `~/Documentos/UNET/Base de datos 2` (fuera del vault).

## Qué es
Un **almacén de datos en esquema estrella** sobre PostgreSQL (Docker), con **ETL en Python** y consumo desde **Power BI**. Cubre las fases 2 (carga) y 3 (consulta y visualización) del proyecto.

## Modelo
- **Hecho**: `hecho_atenciones`. **Grano**: una atención brindada a un estudiante por un asesor, en una fecha, mediante un servicio de apoyo.
- **Métricas**: `duracion_minutos`, `satisfaccion` (1 a 5).
- **Dimensiones**: `dim_tiempo`, `dim_estudiante`, `dim_carrera`, `dim_asesor`, `dim_apoyo`, `dim_tipo_modalidad`.
- **SCD Tipo 2** en `dim_estudiante` (clave de negocio: cédula) y vigencia en `dim_asesor`.
- **Claves subrogadas propiedad del DWH**: `id_tiempo` e `id_estudiante` las asigna una secuencia; el ETL las *resuelve* desde la clave de negocio (fecha, cédula), de modo que `dim_tiempo` crece sola y un estudiante nuevo entra a la dimensión.

## Estructura de archivos
| Carpeta | Contenido |
|---|---|
| `sql/01_ddl.sql` | Esquema `dwh` (tablas, claves, restricciones) |
| `sql/02_funciones_scd2.sql` | Funciones PL/pgSQL: `semestre_de(fecha)`, búsqueda o creación de dimensiones, lógica SCD2 |
| `sql/03_queries_preguntas.sql` | Las ocho preguntas de negocio resueltas con SQL analítico |
| `sql/04_vistas_powerbi.sql` | Vistas para el tablero |
| `sql/05_control_calidad.sql` | Controles de integridad (deben devolver 0 filas) |
| `sql/06_migracion_claves_subrogadas.sql` | Migración al esquema de claves propias |
| `etl/` | `extract.py`, `resolver.py`, `carga_inicial.py`, `carga_diaria.py`, `db.py`, `config.py` |
| `scheduler/` | cron y *timer* de systemd para la carga diaria |

## Flujo
1. `docker compose up -d` levanta PostgreSQL.
2. Se ejecuta el DDL y las funciones SCD2.
3. **Carga inicial**: dimensiones más ~5.499 hechos. **Carga diaria**: incremental (+21 hechos en el ejemplo).
4. Vistas para Power BI, controles de calidad y consultas.

## Ideas a recordar
- Todo día fuera de un semestre declarado en `calendario_semestre` es `'Receso'`.
- El origen **nunca** entrega claves subrogadas confiables: se resuelven siempre en el ETL (lookup o creación).
- Las consultas con SCD2 agrupan por la **versión** vigente el día del hecho.
- Un ETL robusto es **idempotente**: reejecutarlo no duplica datos.

Ver también [[Sistema de Información II]] y [[Análisis y Procesamiento de Datos]].
