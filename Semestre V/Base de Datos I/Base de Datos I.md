---
tags: [materia, semestre-V]
semestre: V
---
# Base de Datos I

**Semestre:** [[Semestre V]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Programación II]]
- [[Teoría General de Sistemas]]

## Desbloquea
- [[Multimedia]]
- [[Sistema de Información I]]

## Apuntes

### Descripción general y objetivos
Base de Datos I cubre el ciclo completo de una base de datos relacional: modelado conceptual (entidad-relación), modelo lógico/relacional, normalización, implementación en SQL (DDL y DML) sobre Oracle y consultas avanzadas (subconsultas, ROLLUP, CUBE). El curso se trabajó con **Oracle XE, SQL Developer y Data Modeler** y casos de estudio por equipo ("Gestión de Ventas de Productos de Entretenimiento", lapso 2025-1). Verificar con el programa oficial el sinóptico exacto.

### Contenido programático (según carpetas del Material, temas IV a VI)
1. **Modelo de datos y ER** (temas previos): entidades, atributos, relaciones, cardinalidad, supertipos/subtipos, arcos.
2. **Modelo relacional y normalización**: claves, integridad, 1FN-3FN/BCNF, transformación ER a relacional.
3. **Tema IV. Implementación con SQL**: DDL (CREATE/ALTER/DROP), restricciones (PK, FK, UNIQUE, CHECK, NOT NULL), secuencias/identity, triggers, DML (INSERT, UPDATE, DELETE, SELECT), scripts de volumen y casos de prueba.
4. **Tema V. SQL avanzado**: proyección, joins, funciones de grupo, GROUP BY/HAVING, subconsultas, ROLLUP, CUBE, GROUPING SETS.
5. **Tema VI**: caso de estudio final (equipo) integrando diseño e implementación (ver rar del Material).

### Conceptos clave
- **Clave primaria / foránea**, integridad referencial, **borrado lógico** (columna 'A'/'I' en lugar de DELETE).
- **Supertipo/subtipo**: generalización implementada como tabla padre con subtablas (o arco exclusivo).
- **Trigger**: código que se ejecuta ante INSERT/UPDATE/DELETE (p. ej. `INITCAP` de nombres, inmutabilidad de `cliente_id`).
- **ROLLUP**: subtotales jerárquicos; **CUBE**: todas las combinaciones (tabulación cruzada); **GROUPING()**: distingue filas de total.

### Código de ejemplo
```sql
CREATE TABLE ciudad (
  ciudad_id     NUMBER(10) GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  nombre_ciudad VARCHAR2(100),
  pais          VARCHAR2(100)
);

CREATE TABLE encomienda (
  encomienda_id NUMBER(10) GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  monto  NUMBER(12,2) CHECK (monto > 0),
  estado CHAR(1) DEFAULT 'A' CHECK (estado IN ('A','I'))   -- borrado lógico
);

CREATE OR REPLACE TRIGGER trg_initcap_cliente
BEFORE INSERT OR UPDATE ON cliente
FOR EACH ROW
BEGIN
  :NEW.nombre := INITCAP(:NEW.nombre);
END;
/

SELECT continente, pais, SUM(monto) total
FROM ventas GROUP BY ROLLUP (continente, pais);
```

### Ejemplo resuelto
Contar facturas por cliente y tienda (caso del Tema 5): `SELECT c.cliente_id, c.nombre, t.nombre_tienda, COUNT(f.factura_id) AS "Cantidad de Facturas" FROM cliente c JOIN factura f ON ... JOIN tienda t ON ... GROUP BY c.cliente_id, c.nombre, t.nombre_tienda ORDER BY c.cliente_id ASC, t.nombre_tienda DESC;`

### Relación con otras materias
Requiere [[Programación II]] y [[Teoría General de Sistemas]]. Desbloquea [[Sistema de Información I]] (diseño de sistemas sobre bases de datos) y [[Multimedia]]; continúa en [[Base de Datos II]] y [[Administración de Base de Datos]]. Notas hijas: [[SQL avanzado - ROLLUP CUBE y casos de estudio]] · [[Base de Datos I - Caso Transversal DB-GRV y PL-SQL]].

### Evaluación y consejos
- Entregas por equipo (diseño lógico/físico, scripts, casos de prueba) y exposiciones (hay plantilla de PowerPoint en el Material).
- Escribe scripts reproducibles (`esquemaScript.sql`, `volumen.sql`, `pruebas.sql`) y pruébalos desde cero.
- Documenta las restricciones de negocio como CHECK/trigger y cubre con casos de prueba.

### Bibliografía recomendada
- Date, C. J. *Introducción a los Sistemas de Bases de Datos*. Pearson.
- Silberschatz, Korth, Sudarshan. *Fundamentos de Bases de Datos*. McGraw-Hill.
- Elmasri y Navathe. *Fundamentos de Sistemas de Bases de Datos*.
- Manual de Oracle SQL (incluido en el Material).

### Recursos del Material/
Todo está bajo `Material/baseDatosI/`:
- Tema IV `materialDeApoyo/`: [SQL Lenguaje de Definición de Datos](Material/baseDatosI/temaIV/materialDeApoyo/SQL%20Lenguaje%20de%20Definicion%20de%20Datos%20v1.pdf), [Curso de SQL Básico](Material/baseDatosI/temaIV/materialDeApoyo/Curso%20de%20SQL%20Basico.pdf), Introducción a Oracle9i SQL 1-3 y manual completo de Oracle en español.
- Tema IV `casoEstudio/`: [codigo.sql](Material/baseDatosI/temaIV/casoEstudio/codigo.sql) (esquema completo con PK/FK/CHECK, arcos, triggers), [manuel diagrama.pdf](Material/baseDatosI/temaIV/casoEstudio/manuel%20diagrama.pdf), planilla de casos de prueba y carpeta del Equipo 9 (diseño lógico/físico, esquemaScript, volumen, pruebas).
- Tema V: [Caso Práctico SQL Avanzado](Material/baseDatosI/temaV/casoEstudio/Caso%20Practico%20SQL%20Avanzado%20Tema%205%202025-1.pdf), [Curso Consultas Avanzadas SQL](Material/baseDatosI/temaV/MaterialApoyo/Curso%20Consultas%20Avanzadas%20SQL.pdf) y [SQL Avanzado Cubos](Material/baseDatosI/temaV/MaterialApoyo/SQL%20Avanzado%20Cubos.pdf).
- Tema VI: caso de estudio comprimido (rar) del Equipo 9.
