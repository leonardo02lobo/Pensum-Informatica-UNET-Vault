---
tags: [clase, electiva]
materia: Administración de Base de Datos
fuente: "~/Documentos/UNET/administracion DB (CONFIGURACION_INICIAL_DBA_COMEDOR.md, parcial 3/README.md) y conocimiento general"
---
# ADBD 05 - Perfiles y usuarios

Materia: [[Administración de Base de Datos]]
Anterior: [[ADBD 04 - Segmentos Undo, Temp y constraints]]
Siguiente: [[ADBD 06 - Roles, privilegios y auditoría]]

## Contexto y objetivo
La seguridad en Oracle se apoya en tres piezas: **usuarios** (identidad), **perfiles** (límites de recursos y política de contraseñas) y **roles/privilegios** (qué se puede hacer, ver ADBD 06). Objetivo: crear perfiles por grupo funcional, usuarios con cuota y demostrar los límites.

## Teoría

### Usuario y esquema
Un usuario es dueño de un **esquema** (sus objetos). `CREATE USER` define: autenticación, `DEFAULT TABLESPACE`, `TEMPORARY TABLESPACE`, `QUOTA` y `PROFILE`. Sin cuota un usuario no puede crear segmentos (ORA-01950).

### Perfil
Conjunto con nombre de límites:
- **Recursos** (se aplican solo si `RESOURCE_LIMIT=TRUE`; desde 12c lo es por defecto en PDB): `SESSIONS_PER_USER`, `CPU_PER_SESSION`, `CPU_PER_CALL`, `CONNECT_TIME`, `IDLE_TIME`, `LOGICAL_READS_PER_SESSION/CALL`, `PRIVATE_SGA`, `COMPOSITE_LIMIT`.
- **Contraseña** (siempre activos): `FAILED_LOGIN_ATTEMPTS`, `PASSWORD_LIFE_TIME`, `PASSWORD_GRACE_TIME`, `PASSWORD_REUSE_TIME`, `PASSWORD_REUSE_MAX`, `PASSWORD_LOCK_TIME`, `INACTIVE_ACCOUNT_TIME`, `PASSWORD_VERIFY_FUNCTION`.

El perfil `DEFAULT` es la línea base: todo valor no especificado en otro perfil se hereda de él. `SYS` y `SYSTEM` también lo usan; modificarlo afecta la expiración de sus claves.

## Ejemplo resuelto (modelo del Sistema de Comedor)
Del `CONFIGURACION_INICIAL_DBA_COMEDOR.md`: cuatro grupos funcionales (`SUPER_ADMIN`, `ADMIN`, `TAQUILLERO`, `BENEFICIARIO`), cada uno con su perfil, más ajuste de `DEFAULT`.

```sql
ALTER SESSION SET CONTAINER = XEPDB1;

-- Antes: límites de fábrica
SELECT resource_name, limit FROM dba_profiles
 WHERE profile = 'DEFAULT' ORDER BY resource_type DESC, resource_name;

-- Ajuste de la línea base
ALTER PROFILE DEFAULT LIMIT
    SESSIONS_PER_USER 10
    CONNECT_TIME 480
    IDLE_TIME 30
    FAILED_LOGIN_ATTEMPTS 5
    PASSWORD_LIFE_TIME 90
    PASSWORD_GRACE_TIME 7
    PASSWORD_LOCK_TIME 1/24
    PASSWORD_VERIFY_FUNCTION ora12c_verify_function;

-- Perfil restrictivo para beneficiarios (un comensal consulta poco)
CREATE PROFILE perf_comedor_beneficiario LIMIT
    SESSIONS_PER_USER 1
    CPU_PER_CALL 1000
    CONNECT_TIME 15
    IDLE_TIME 5
    LOGICAL_READS_PER_CALL 5000
    FAILED_LOGIN_ATTEMPTS 3
    PASSWORD_LIFE_TIME 180;

-- Usuario sin cláusula PROFILE: hereda DEFAULT
CREATE USER u_default_comedor IDENTIFIED BY "Def_2026#cmd"
    DEFAULT TABLESPACE users QUOTA 0 ON users
    TEMPORARY TABLESPACE ts_comedor_temp;
GRANT CREATE SESSION TO u_default_comedor;

-- Usuario con perfil propio
CREATE USER u_portal_comedor IDENTIFIED BY "Por_2026#cmd"
    PROFILE perf_comedor_beneficiario
    DEFAULT TABLESPACE users QUOTA 0 ON users;
GRANT CREATE SESSION TO u_portal_comedor;
```
Pruebas del informe:
1. `SELECT username, expiry_date - created FROM dba_users WHERE username='U_DEFAULT_COMEDOR';` muestra 90 días: el cambio de `DEFAULT` se heredó.
2. `ALTER USER u_default_comedor IDENTIFIED BY "abc";` falla con `ORA-28003` (la función de verificación rechaza claves triviales).
3. Cinco intentos fallidos de conexión dejan la cuenta en `LOCKED(TIMED)`; `ALTER USER ... ACCOUNT UNLOCK;` la restablece.
4. Una segunda sesión de un usuario con `SESSIONS_PER_USER 1` produce `ORA-02391`.

Ver quién es quién: `SELECT username, account_status, profile FROM dba_users;`.

## Errores comunes
- Creer que los límites de recursos no se aplican (revisar `RESOURCE_LIMIT`).
- Modificar `DEFAULT` sin considerar que `SYS`/`SYSTEM` lo heredan; mejor un perfil aparte para cuentas administrativas.
- Contraseñas en scripts versionados; usar gestores de secretos o variables.
- Dar `UNLIMITED TABLESPACE` en lugar de cuotas concretas.

## Ejercicios propuestos
1. ¿Qué perfil tiene un usuario creado sin `PROFILE`? *Respuesta: `DEFAULT`.*
2. Escribe un perfil que bloquee 1 hora tras 3 fallos. *Respuesta: `CREATE PROFILE p LIMIT FAILED_LOGIN_ATTEMPTS 3 PASSWORD_LOCK_TIME 1/24;`.*
3. ¿Qué error aparece al crear una tabla sin cuota? *Respuesta: `ORA-01950: no privileges on tablespace`.*

## Conexiones
[[Sistemas Operativos]] (usuarios, permisos, límites ulimit), [[Base de Datos II]] (seguridad y autorización), [[Administración de Redes]] (control de acceso y políticas).

## Fuente
`~/Documentos/UNET/administracion DB/CONFIGURACION_INICIAL_DBA_COMEDOR.md` y `parcial 3/README.md`. Los nombres y claves son del proyecto de ejemplo (didácticos; no reutilizar).
