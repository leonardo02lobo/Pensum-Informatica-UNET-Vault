---
tags: [clase, electiva]
materia: Desarrollo de Aplicaciones Web
fuente: "conocimiento general"
---
# DAW 05 - Persistencia SQL, NoSQL y ORM

Materia: [[Desarrollo de Aplicaciones Web]]
Anterior: [[DAW 04 - Back-end con Node.js, Express y FastAPI]]
Siguiente: [[DAW 06 - Autenticación y seguridad web]]

## Contexto y objetivo
Una aplicación web real necesita guardar datos de forma duradera y consistente. Objetivo: elegir entre SQL y NoSQL, diseñar un esquema, usar consultas parametrizadas y un ORM, y comprender transacciones e índices.

## Teoría

### Relacional (PostgreSQL, MySQL)
Esquema fijo, claves primarias y foráneas, `JOIN`, transacciones **ACID** (atomicidad, consistencia, aislamiento, durabilidad). Adecuado cuando hay relaciones e integridad importantes. Ver [[Base de Datos I]] y [[Base de Datos II]].

### NoSQL
Modelos: **documentos** (MongoDB: JSON/BSON, esquema flexible), **clave-valor** (Redis: caché, sesiones), **columnas anchas** (Cassandra), **grafos** (Neo4j). Ventajas: escalado horizontal y esquema flexible; costo: joins y consistencia más limitada (teorema CAP: ante partición se elige consistencia o disponibilidad).

### Criterio de elección
| Necesidad | Opción |
|---|---|
| Integridad referencial, reportes, transacciones | SQL |
| Datos anidados que se leen juntos, esquema cambiante | Documentos |
| Caché, contadores, sesiones | Clave-valor |

### ORM
Mapea tablas a clases (SQLAlchemy, Django ORM, Prisma, Sequelize). Ventajas: productividad, migraciones, parametrización. Riesgos: consultas ineficientes, problema **N+1** (una consulta para la lista y una más por cada elemento relacionado). Siempre se debe poder leer el SQL generado.

### Migraciones
Cambios de esquema versionados (Alembic, Django migrations, Flyway) para reproducir la base en cualquier entorno.

## Ejemplo resuelto
Modelo: autores (1) a libros (N).

```sql
CREATE TABLE autor (
  id      SERIAL PRIMARY KEY,
  nombre  VARCHAR(100) NOT NULL UNIQUE
);
CREATE TABLE libro (
  id        SERIAL PRIMARY KEY,
  titulo    VARCHAR(200) NOT NULL,
  anio      INT CHECK (anio BETWEEN 1400 AND 2100),
  autor_id  INT NOT NULL REFERENCES autor(id) ON DELETE RESTRICT
);
CREATE INDEX ix_libro_autor ON libro(autor_id);

-- Transacción: crear autor y libro de forma atómica
BEGIN;
INSERT INTO autor(nombre) VALUES ('Tanenbaum') ON CONFLICT DO NOTHING;
INSERT INTO libro(titulo, anio, autor_id)
  SELECT 'Redes de Computadoras', 2012, id FROM autor WHERE nombre = 'Tanenbaum';
COMMIT;

-- Consulta con JOIN
SELECT a.nombre, COUNT(*) AS libros
  FROM autor a JOIN libro l ON l.autor_id = a.id
 GROUP BY a.nombre ORDER BY libros DESC;
```
Acceso parametrizado desde Python con SQLAlchemy (ORM):
```python
from sqlalchemy import ForeignKey, String, create_engine, select
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column, relationship, Session, selectinload

class Base(DeclarativeBase): pass

class Autor(Base):
    __tablename__ = "autor"
    id: Mapped[int] = mapped_column(primary_key=True)
    nombre: Mapped[str] = mapped_column(String(100), unique=True)
    libros: Mapped[list["Libro"]] = relationship(back_populates="autor")

class Libro(Base):
    __tablename__ = "libro"
    id: Mapped[int] = mapped_column(primary_key=True)
    titulo: Mapped[str] = mapped_column(String(200))
    autor_id: Mapped[int] = mapped_column(ForeignKey("autor.id"))
    autor: Mapped[Autor] = relationship(back_populates="libros")

engine = create_engine("postgresql+psycopg://user:pass@localhost/biblio")
with Session(engine) as s:
    # selectinload evita el problema N+1 (2 consultas en total)
    for a in s.scalars(select(Autor).options(selectinload(Autor.libros))):
        print(a.nombre, len(a.libros))
    # Parametrizado: el valor nunca se concatena al SQL
    q = select(Libro).where(Libro.titulo.ilike("%redes%"))
    print(s.scalars(q).all())
```
Equivalente en MongoDB (documento incrustado):
```js
db.autores.insertOne({
  nombre: "Tanenbaum",
  libros: [{ titulo: "Redes de Computadoras", anio: 2012 }]
});
db.autores.find({ "libros.anio": { $gte: 2010 } });
db.autores.createIndex({ nombre: 1 }, { unique: true });
```
Comentario: en el modelo documental el arreglo de libros se lee junto con el autor sin join; si un libro tuviera varios autores habría que duplicar o referenciar, y ahí SQL es más natural.

## Errores comunes
- Concatenar texto del usuario en SQL (inyección, DAW 06).
- No indexar claves foráneas ni columnas de filtro.
- Problema N+1 por cargar relaciones de forma perezosa en bucles.
- Usar MongoDB por moda cuando los datos son muy relacionales.
- Cambiar el esquema a mano en producción sin migración.

## Ejercicios propuestos
1. ¿Qué garantiza `BEGIN ... COMMIT` si falla la segunda sentencia y se hace `ROLLBACK`? *Respuesta: atomicidad; no queda el autor sin libro.*
2. Explica el N+1 con 100 autores. *Respuesta: 1 consulta de autores + 100 de libros = 101; con carga anticipada son 2.*
3. ¿Qué tipo de almacén sirve para guardar sesiones con expiración? *Respuesta: clave-valor como Redis, con TTL.*

## Conexiones
[[Base de Datos I]] (modelo relacional, SQL), [[Base de Datos II]] (transacciones, índices), [[Sistemas Distribuidos]] (CAP, replicación), [[Programación II]] (objetos y mapeo).

## Fuente
Conocimiento general: documentación de PostgreSQL, SQLAlchemy y MongoDB.
