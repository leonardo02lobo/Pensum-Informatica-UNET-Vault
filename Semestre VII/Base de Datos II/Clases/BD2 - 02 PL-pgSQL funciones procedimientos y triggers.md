---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: conocimiento general + sql/02_funciones_scd2.sql de ~/Documentos/UNET/Base de datos 2
---
# BD2 - 02 PL/pgSQL: funciones, procedimientos y triggers

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 01 SQL avanzado CTE y funciones de ventana]]
Siguiente: [[BD2 - 03 Transacciones ACID y control de concurrencia]]

## Contexto y objetivo
La **programación del lado del servidor** mueve lógica a la base de datos: reglas que deben cumplirse sin importar qué aplicación escriba, menos viajes de red y operaciones atómicas. PL/pgSQL es el lenguaje procedural de PostgreSQL (equivalente a PL/SQL de Oracle). El objetivo: escribir funciones, procedimientos, disparadores y manejo de errores, y reconocer cuándo conviene (y cuándo no) ponerlos en el servidor.

## Estructura de un bloque
```sql
DO $$
DECLARE
  v_total INTEGER := 0;
BEGIN
  SELECT COUNT(*) INTO v_total FROM dwh.hecho_atenciones;
  RAISE NOTICE 'Total: %', v_total;
EXCEPTION
  WHEN division_by_zero THEN RAISE NOTICE 'Error';
END $$;
```
Secciones: `DECLARE` (variables), `BEGIN ... END` (cuerpo), `EXCEPTION` (manejo). `$$` es un delimitador de cadena (dollar quoting) que evita escapar comillas.

Elementos: asignación `:=`, `IF/ELSIF/ELSE`, `CASE`, `LOOP`, `WHILE`, `FOR i IN 1..10`, `FOR r IN SELECT ... LOOP` (cursor implícito), `RETURN`, `RETURN QUERY`, `PERFORM` (ejecuta una consulta descartando el resultado), `FOUND` (variable booleana: la última sentencia afectó filas), `%ROWTYPE` y `%TYPE`.

## Funciones vs procedimientos
| | Función (`CREATE FUNCTION`) | Procedimiento (`CREATE PROCEDURE`, PG 11+) |
|---|---|---|
| Invocación | `SELECT f(x)` | `CALL p(x)` |
| Valor de retorno | obligatorio (o `void`) | no devuelve (solo `INOUT`) |
| Control de transacción | no puede hacer `COMMIT` | puede `COMMIT`/`ROLLBACK` |
| Uso en consultas | sí | no |

Volatilidad: `IMMUTABLE` (mismo resultado siempre), `STABLE` (constante dentro de una consulta), `VOLATILE` (puede cambiar; valor por defecto). Declararla bien permite optimizaciones e índices sobre expresiones.

## Ejemplo real del proyecto: busca-o-crea
En `sql/02_funciones_scd2.sql` la función `dwh.obtener_id_tiempo(fecha)` implementa el patrón "lookup o creación" de una dimensión:
```sql
SELECT id_tiempo INTO v_id FROM dwh.dim_tiempo WHERE fecha = p_fecha;
IF FOUND THEN RETURN v_id; END IF;

INSERT INTO dwh.dim_tiempo (fecha, dia, mes, anio, semestre_academico)
VALUES (p_fecha, EXTRACT(DAY FROM p_fecha)::INT, ...,
        COALESCE(p_semestre, dwh.semestre_de(p_fecha)))
ON CONFLICT (fecha) DO NOTHING
RETURNING id_tiempo INTO v_id;

IF v_id IS NULL THEN   -- otra sesión lo creó entremedio
  SELECT id_tiempo INTO v_id FROM dwh.dim_tiempo WHERE fecha = p_fecha;
END IF;
```
Puntos clave: (1) `ON CONFLICT DO NOTHING` + relectura resuelve la **condición de carrera** entre sesiones concurrentes sin abortar; (2) se valida el parámetro nulo con `RAISE EXCEPTION`; (3) `dwh.semestre_de` es una función SQL `STABLE` que consulta una tabla de parámetros y devuelve `'Receso'` por defecto con `COALESCE`.

## Disparadores (triggers)
Un trigger ejecuta una función ante `INSERT/UPDATE/DELETE/TRUNCATE`.
- Momento: `BEFORE` (puede modificar `NEW` o cancelar devolviendo `NULL`), `AFTER`, `INSTEAD OF` (vistas).
- Alcance: `FOR EACH ROW` o `FOR EACH STATEMENT`.
- Variables: `NEW`, `OLD`, `TG_OP`, `TG_TABLE_NAME`.
```sql
CREATE FUNCTION validar_satisfaccion() RETURNS trigger AS $$
BEGIN
  IF NEW.satisfaccion NOT BETWEEN 1 AND 5 THEN
     RAISE EXCEPTION 'Satisfacción fuera de rango: %', NEW.satisfaccion;
  END IF;
  RETURN NEW;
END $$ LANGUAGE plpgsql;
CREATE TRIGGER t_val BEFORE INSERT OR UPDATE ON dwh.hecho_atenciones
FOR EACH ROW EXECUTE FUNCTION validar_satisfaccion();
```
Nota: el proyecto prefiere restricciones `CHECK` declarativas (más simples y rápidas); use triggers cuando la regla no se pueda expresar así (auditoría, derivados, reglas entre tablas).

## Cursores
`DECLARE c CURSOR FOR SELECT ...; OPEN c; FETCH c INTO ...; CLOSE c;` Útiles para procesar fila a fila, pero la alternativa basada en conjuntos (un solo `UPDATE ... FROM`) casi siempre es más rápida.

## Manejo de excepciones
`EXCEPTION WHEN unique_violation THEN ...` ; `GET STACKED DIAGNOSTICS`. Un bloque con `EXCEPTION` crea un **subtransacción** implícita (savepoint): costo no despreciable en bucles.

## Ejemplo resuelto: transferencia atómica
```sql
CREATE PROCEDURE transferir(a INT, b INT, monto NUMERIC) LANGUAGE plpgsql AS $$
BEGIN
  UPDATE cuenta SET saldo = saldo - monto WHERE id = a AND saldo >= monto;
  IF NOT FOUND THEN RAISE EXCEPTION 'Saldo insuficiente'; END IF;
  UPDATE cuenta SET saldo = saldo + monto WHERE id = b;
END $$;
CALL transferir(1,2,100);
```
Si se lanza la excepción, la transacción completa se revierte. Ver [[BD2 - 03 Transacciones ACID y control de concurrencia]].

## Errores comunes
- Nombre de variable igual al de una columna (ambigüedad): prefijo `v_`/`p_`.
- Olvidar `RETURN NEW` en un trigger `BEFORE` (la fila se pierde).
- Triggers recursivos (un trigger que modifica su propia tabla).
- Lógica de negocio excesiva en el servidor: difícil de versionar y probar.
- Usar `SELECT INTO` sin `STRICT` cuando se espera exactamente una fila.

## Ejercicios propuestos
1. Escriba un trigger de auditoría que registre usuario, operación y fecha. *Resp.: función con `INSERT INTO bitacora VALUES (TG_TABLE_NAME, TG_OP, now(), current_user)`; `AFTER ... FOR EACH ROW`.*
2. ¿Por qué un procedimiento puede hacer `COMMIT` y una función no? *Resp.: la función se ejecuta dentro de la transacción de la consulta que la llama.*
3. Reescriba un cursor que suma por fila como un solo `UPDATE`. *Resp.: `UPDATE t SET x = s.v FROM (SELECT ...) s WHERE ...`.*

## Conexiones
Aplicación en [[BD2 - 08 SCD Tipo 2 y claves subrogadas]]. Relación con [[Administración de Base de Datos]].

## Fuente
`sql/02_funciones_scd2.sql` (fragmentos citados) y conocimiento general de PostgreSQL.
