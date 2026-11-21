---
tags: [clase, electiva]
materia: Administración de Base de Datos
fuente: "~/Documentos/UNET/administracion DB (punto4_tablespaces.md, tablespaces_oracle.sql, COMANDOS_DBA_REFERENCIA.md) y conocimiento general"
---
# ADBD 02 - Tablespaces y almacenamiento

Materia: [[Administración de Base de Datos]]
Anterior: [[ADBD 01 - Arquitectura de Oracle]]
Siguiente: [[ADBD 03 - Volumetría y crecimiento]]

## Contexto y objetivo
El almacenamiento lógico de Oracle separa lo que ve el DBA (tablespaces, segmentos, extents, bloques) de lo físico (datafiles, bloques del sistema operativo). Objetivo: diseñar tablespaces funcionales, elegir la política de extents y de espacio en segmento, y consultar el uso de espacio.

## Teoría

### Jerarquía lógica
`Base de datos > Tablespace > Segmento > Extent > Bloque Oracle`, y físicamente `Tablespace > Datafile > Bloque del SO`.
- **Bloque**: unidad mínima de E/S (típicamente 8 KB).
- **Extent**: conjunto contiguo de bloques asignados a un segmento.
- **Segmento**: todo el almacenamiento de un objeto (tabla, índice, partición, undo, temporal, LOB).
- **Tablespace**: contenedor lógico formado por uno o más datafiles.

### Tipos de tablespace
Permanente, UNDO, TEMPORARY; SYSTEM y SYSAUX gestionados por Oracle. Un tablespace puede ser `BIGFILE` (un solo datafile enorme) o `SMALLFILE`. Puede ponerse `READ ONLY` (útil para datos archivables).

### Gestión de extents
- **Dictionary managed** (obsoleto, no existe en 18c) vs. **locally managed** (mapa de bits en el datafile): único modo actual.
- Políticas dentro de LMT:
  - `UNIFORM SIZE n`: extents fijos; sin fragmentación externa; conviene cuando se conoce el tamaño final del segmento.
  - `AUTOALLOCATE`: Oracle usa 64K, 1M, 8M, 64M; conviene con crecimiento incierto.

### Gestión de espacio en el segmento
- **MSSM** (manual): listas libres, `PCTUSED`, `FREELISTS`.
- **ASSM** (`SEGMENT SPACE MANAGEMENT AUTO`): mapas de bits; reduce contención en inserciones concurrentes. `PCTFREE` sigue vigente: reserva espacio en cada bloque para crecimiento de filas por `UPDATE`.

### Criterios de agrupación (del proyecto del comedor)
1. Agrupar por *naturaleza* de la tabla (patrón de escritura, ritmo de crecimiento), no por módulo funcional.
2. Separar datos de índices.
3. Aislar lo archivable para poder pasarlo a `READ ONLY` como unidad.

## Ejemplo resuelto
Del archivo `tablespaces_oracle.sql` del proyecto, un tablespace para catálogos estáticos (uniforme, sin autoextend) y otro transaccional (autoallocate con autoextend):

```sql
ALTER SESSION SET CONTAINER = XEPDB1;

-- Catálogos: pequeños y estables -> UNIFORM, sin crecimiento automático
CREATE TABLESPACE ts_comedor_estatico
    DATAFILE '/opt/oracle/oradata/XE/XEPDB1/ts_comedor_estatico01.dbf'
        SIZE 8M AUTOEXTEND OFF
    EXTENT MANAGEMENT LOCAL UNIFORM SIZE 64K
    SEGMENT SPACE MANAGEMENT AUTO
    LOGGING;

-- Operación transaccional: crece, tamaño final incierto -> AUTOALLOCATE
CREATE TABLESPACE ts_comedor_transac
    DATAFILE '/opt/oracle/oradata/XE/XEPDB1/ts_comedor_transac01.dbf'
        SIZE 64M AUTOEXTEND ON NEXT 16M MAXSIZE 512M
    EXTENT MANAGEMENT LOCAL AUTOALLOCATE
    SEGMENT SPACE MANAGEMENT AUTO
    LOGGING;
```
Paso a paso: (1) se entra a la PDB; (2) para catálogos con poco volumen un extent de 64K evita desperdicio; `AUTOEXTEND OFF` hace que un crecimiento inesperado falle de forma visible; (3) para la parte transaccional, `MAXSIZE` pone un tope que protege al disco.

Consultas de seguimiento:
```sql
SELECT tablespace_name, status FROM dba_tablespaces;
SELECT file_name, tablespace_name, bytes/1024/1024 MB FROM dba_data_files;

-- Libre vs total por tablespace
SELECT df.tablespace_name,
       ROUND(SUM(df.bytes)/1048576) total_mb,
       ROUND(NVL(MAX(fs.libre),0)/1048576) libre_mb
  FROM dba_data_files df
  LEFT JOIN (SELECT tablespace_name, SUM(bytes) libre
               FROM dba_free_space GROUP BY tablespace_name) fs
    ON fs.tablespace_name = df.tablespace_name
 GROUP BY df.tablespace_name;

-- Operaciones de mantenimiento
ALTER DATABASE DATAFILE '/ruta/x.dbf' RESIZE 128M;
ALTER TABLESPACE ts_comedor_audit READ ONLY;
```
Nótese que el material del proyecto usa `SUM` doble sobre una unión; la variante con subconsulta evita multiplicar filas libres por cada datafile.

## Errores comunes
- `AUTOEXTEND ON` sin `MAXSIZE`: el datafile puede llenar el disco.
- Un solo tablespace `USERS` para todo: no permite políticas diferenciadas.
- Dejar índices en el tablespace de datos.
- Usar `UNIFORM` grande para segmentos pequeños: desperdicio interno.
- Poner `PCTFREE` alto en tablas que solo se insertan.

## Ejercicios propuestos
1. Un tablespace UNIFORM de 1 MB aloja una tabla de 300 KB. ¿Cuánto espacio ocupa el segmento? *Respuesta: 1 MB (un extent).*
2. ¿Qué cláusula elimina la contención sobre listas libres? *Respuesta: `SEGMENT SPACE MANAGEMENT AUTO` (ASSM).*
3. Escribe el comando para dejar un tablespace de bitácoras de un ejercicio cerrado en solo lectura. *Respuesta: `ALTER TABLESPACE nombre READ ONLY;`.*

## Conexiones
[[Organización del Computador]] (bloques, E/S y almacenamiento), [[Sistemas Operativos]] (sistemas de archivos), [[Base de Datos II]] (índices y organización física).

## Fuente
`~/Documentos/UNET/administracion DB/punto4_tablespaces.md` y `tablespaces_oracle.sql` (diseño del Sistema de Comedor Universitario), `COMANDOS_DBA_REFERENCIA.md`. Teoría: Oracle Administrator's Guide, capítulo de tablespaces.
