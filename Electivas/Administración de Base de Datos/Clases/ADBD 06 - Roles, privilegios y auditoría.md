---
tags: [clase, electiva]
materia: Administración de Base de Datos
fuente: "~/Documentos/UNET/administracion DB (COMANDOS_DBA_REFERENCIA.md, parcial 3/README.md, parcial 4/README.md, auditoria_perfiles_roles.sh) y conocimiento general"
---
# ADBD 06 - Roles, privilegios y auditoría

Materia: [[Administración de Base de Datos]]
Anterior: [[ADBD 05 - Perfiles y usuarios]]
Siguiente: [[ADBD 07 - Respaldo y recuperación con RMAN]]

## Contexto y objetivo
Los privilegios definen qué puede hacer cada cuenta. Los **roles** agrupan privilegios para administrarlos por grupo funcional. Esta clase cubre el principio de mínimo privilegio, la delegación (`ADMIN OPTION`, `GRANT OPTION`) y cómo auditar lo concedido, con base en los Informes 3 y 4 del proyecto del comedor.

## Teoría

### Privilegios
- **De sistema**: derecho a una acción (`CREATE SESSION`, `CREATE TABLE`, `ALTER USER`).
- **De objeto**: derecho sobre un objeto concreto (`SELECT ON comedor.consumptions`), incluso por columna (`UPDATE (col)`).

### Roles
Colección con nombre de privilegios y otros roles (jerarquía). Pueden estar protegidos por contraseña y activarse con `SET ROLE`. Desde la perspectiva de diseño: un rol por función (`ROL_COMEDOR_OPERACION`) y una cuenta por persona.

### Delegación
- `WITH ADMIN OPTION` (sistema y roles): el receptor puede re-conceder; al revocarle, lo que él concedió **permanece**.
- `WITH GRANT OPTION` (objeto): el receptor puede re-conceder; al revocarle, la revocación **cascada** a lo que él concedió.

Asimetría del `REVOKE` (tema del Informe 4): quitar un privilegio de sistema/rol no revierte las concesiones hechas con `ADMIN OPTION`, mientras que el de objeto sí cascada.

### Reglas de delegación encontradas en el proyecto (Informe 4)
| Concesión | En un ROL | Al USUARIO |
|---|:-:|:-:|
| Privilegio de sistema (con o sin ADMIN OPTION) | cabe | cabe |
| Rol (con o sin ADMIN OPTION) | cabe | cabe |
| Privilegio de objeto | cabe | cabe |
| Privilegio de objeto WITH GRANT OPTION | ORA-01926 | cabe |
| UNLIMITED TABLESPACE | ORA-01931 | cabe |
| Cuota sobre tablespace | no aplica | cabe |
| CONNECT THROUGH (proxy) | no aplica | cabe |

Además: un privilegio de objeto recibido por un rol no se puede re-conceder (ORA-01031), aunque el `ADMIN OPTION` recibido por rol sí es utilizable. Consecuencia de diseño: el rol lleva lo que cabe y se concede directo al usuario lo que no cabe.

### Auditoría
Registrar quién hizo qué. Opciones: **auditoría unificada** (12c+): `CREATE AUDIT POLICY`, `AUDIT POLICY`, consulta en `UNIFIED_AUDIT_TRAIL`; trazas de aplicación (tabla `audit_logs`, como en el comedor); y consultas al diccionario para auditar **lo concedido**.

## Ejemplo resuelto: roles jerárquicos y verificación
```sql
ALTER SESSION SET CONTAINER = XEPDB1;

-- Piezas
CREATE ROLE rol_comedor_conexion;
GRANT CREATE SESSION TO rol_comedor_conexion;

CREATE ROLE rol_comedor_portal;
GRANT rol_comedor_conexion TO rol_comedor_portal;
-- Vista para el portal (el beneficiario no toca tablas directamente)
CREATE VIEW comedor.v_portal_consumos AS
  SELECT id, fecha, plato FROM comedor.consumptions;
GRANT SELECT ON comedor.v_portal_consumos TO rol_comedor_portal;

-- Rol operativo con UPDATE por columna
CREATE ROLE rol_comedor_operacion;
GRANT rol_comedor_portal TO rol_comedor_operacion;
GRANT INSERT ON comedor.consumptions TO rol_comedor_operacion;
GRANT UPDATE (estado) ON comedor.consumptions TO rol_comedor_operacion;

-- Asignar al usuario
GRANT rol_comedor_operacion TO u_taquilla_comedor;
```
Auditoría de lo concedido (inspirada en `COMANDOS_DBA_REFERENCIA.md`):
```sql
SELECT grantee, granted_role, admin_option FROM dba_role_privs
 WHERE grantee LIKE 'U\_%COMEDOR' ESCAPE '\';
SELECT grantee, privilege, admin_option FROM dba_sys_privs
 WHERE grantee LIKE 'ROL\_COMEDOR%' ESCAPE '\';
SELECT grantee, owner, table_name, privilege, grantable FROM dba_tab_privs
 WHERE owner = 'COMEDOR' ORDER BY grantee, table_name;
```
Delegación con GRANT OPTION (directo al usuario por la regla ORA-01926):
```sql
GRANT SELECT ON comedor.consumptions TO u_adminapp_comedor WITH GRANT OPTION;
GRANT rol_comedor_gestion TO u_adminapp_comedor WITH ADMIN OPTION;
ALTER USER comedor GRANT CONNECT THROUGH u_adminapp_comedor;  -- conexión proxy
```
Prueba positiva y negativa del informe: conectado como `u_portal_comedor`, `SELECT` sobre la vista funciona; `SELECT` sobre la tabla base da `ORA-00942`. El resultado del proyecto: 28/28 comprobaciones (Informe 3) y 31/31 (Informe 4) con dictamen `PASA`.

Auditoría unificada básica:
```sql
CREATE AUDIT POLICY pol_comedor_ddl ACTIONS CREATE TABLE, DROP TABLE, ALTER TABLE;
AUDIT POLICY pol_comedor_ddl;
SELECT event_timestamp, dbusername, action_name, object_name
  FROM unified_audit_trail ORDER BY event_timestamp DESC FETCH FIRST 10 ROWS ONLY;
```

## Errores comunes
- Conceder `DBA` o `ANY` privileges "para que funcione".
- Confundir `ADMIN OPTION` con `GRANT OPTION` y esperar cascada en ambos.
- Dar privilegios sobre tablas base en vez de vistas.
- No revisar las concesiones tras retirar a un administrador (ver script `36_limpieza.sql` del proyecto).

## Ejercicios propuestos
1. ¿Por qué `GRANT ... WITH GRANT OPTION` a un rol falla? *Respuesta: ORA-01926; Oracle no lo permite en roles.*
2. Un usuario con ADMIN OPTION concedió un rol y luego se le revoca el rol. ¿Qué pasa con el receptor final? *Respuesta: conserva el rol.*
3. Consulta que lista quién puede leer `comedor.consumptions`. *Respuesta: `SELECT grantee, privilege FROM dba_tab_privs WHERE table_name='CONSUMPTIONS';`.*

## Conexiones
[[Base de Datos II]] (autorización y vistas), [[Sistemas Operativos]] (permisos y mínimo privilegio), [[Sistemas Distribuidos]] (delegación e identidad).

## Fuente
`~/Documentos/UNET/administracion DB/parcial 3/README.md`, `parcial 4/README.md`, `COMANDOS_DBA_REFERENCIA.md`, `auditoria_perfiles_roles.sh`. Teoría: Oracle Database Security Guide.
