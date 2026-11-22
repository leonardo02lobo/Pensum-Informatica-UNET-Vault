---
tags: [electiva]
---
# Administración de Base de Datos

Opción de [[Electivas]].

## Descripción
Formación en el rol del DBA: instalar, configurar, asegurar, respaldar y afinar un sistema gestor, tomando como caso práctico Oracle. Amplía [[Base de Datos I]] y [[Base de Datos II]].

## Temario típico (verificar con el programa oficial)
1. Arquitectura de Oracle: instancia, SGA/PGA, procesos, archivos de control, datafiles y redo logs; multitenant (CDB/PDB).
2. Tablespaces y almacenamiento: diseño, estimación de volumetría y crecimiento.
3. Seguridad: usuarios, perfiles, roles, privilegios y auditoría.
4. Respaldo y recuperación: RMAN, modo ARCHIVELOG, flashback.
5. Afinamiento: planes de ejecución, índices, estadísticas.
6. Alta disponibilidad: Data Guard, RAC (introducción).

## Comandos de ejemplo
```sql
ALTER SESSION SET CONTAINER = XEPDB1;
CREATE TABLESPACE ts_datos DATAFILE 'datos01.dbf' SIZE 200M AUTOEXTEND ON;
CREATE PROFILE p_app LIMIT FAILED_LOGIN_ATTEMPTS 5 PASSWORD_LIFE_TIME 90;
CREATE ROLE r_taquilla; GRANT CREATE SESSION TO r_taquilla;
SELECT tablespace_name, ROUND(SUM(bytes)/1048576) mb FROM dba_data_files GROUP BY tablespace_name;
```

## Relación con el pensum
[[Base de Datos I]], [[Base de Datos II]], [[Sistemas Operativos]], [[Sistemas Distribuidos]], [[Organización del Computador]] (almacenamiento).

## Material del estudiante
En `~/Documentos/UNET/administracion DB` hay un proyecto completo (Sistema de Comedor Universitario) sobre Oracle 18c XE en Docker: modelo ER y físico, diseño de tablespaces, estimación de volumetría, perfiles y roles, scripts de auditoría, `COMANDOS_DBA_REFERENCIA.md` y un informe. Sirve como guía práctica de los temas anteriores.

## Bibliografía
- Oracle Database Administrator's Guide (documentación oficial).
- Bryla y Thomas. *OCA/OCP Oracle Database Administration*.
- Kyte, T. *Expert Oracle Database Architecture*.

## Material pesado (fuera del vault)
- `~/Documentos/UNET/administracion DB`
- Serie de prácticas Oracle 18c XE (Drive): [[Administración de Base de Datos - Prácticas Oracle 18c XE (DBCA, Arranque, Redo Logs y Seguridad)]]
