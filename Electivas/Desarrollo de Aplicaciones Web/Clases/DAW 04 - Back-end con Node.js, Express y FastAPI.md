---
tags: [clase, electiva]
materia: Desarrollo de Aplicaciones Web
fuente: "conocimiento general"
---
# DAW 04 - Back-end con Node.js, Express y FastAPI

Materia: [[Desarrollo de Aplicaciones Web]]
Anterior: [[DAW 03 - JavaScript, DOM y consumo de APIs]]
Siguiente: [[DAW 05 - Persistencia SQL, NoSQL y ORM]]

## Contexto y objetivo
El back-end recibe peticiones HTTP, aplica la lógica de negocio, accede a los datos y responde (normalmente JSON). Objetivo: construir una API REST con dos pilas representativas, Node.js con Express y Python con FastAPI, y entender middleware, validación y manejo de errores.

## Teoría

### Estructura típica
Capas: **rutas/controladores** (HTTP), **servicios** (lógica), **repositorios** (datos). Configuración por variables de entorno (12-factor). Servidor sin estado para escalar horizontalmente.

### Node.js y Express
Node.js ejecuta JavaScript con el motor V8 y un bucle de eventos con E/S no bloqueante: excelente para E/S, mal para cómputo intensivo (bloquea el hilo). Express: enrutador y cadena de **middleware**, funciones `(req, res, next)` ejecutadas en orden (log, parseo JSON, autenticación, rutas, manejador de errores al final).

### FastAPI
Framework ASGI de Python: tipado con anotaciones, **validación automática con Pydantic**, documentación OpenAPI en `/docs`, soporte `async`. Otras opciones: Flask (mínimo), Django (baterías incluidas, ORM y admin), PHP/Laravel, Java/Spring.

### Validación y errores
Nunca confiar en la entrada del cliente. Responder 400/422 con mensajes claros, 404 si no existe, 500 sin filtrar trazas internas. Registrar (logging) con niveles.

### Documentación de API
OpenAPI/Swagger describe rutas, esquemas y códigos; permite generar clientes y pruebas.

## Ejemplo resuelto
La API de libros en memoria (la capa de datos real se ve en DAW 05).

Express:
```js
// server.js  (npm init -y && npm i express)
import express from "express";
const app = express();
app.use(express.json());                              // middleware: parsea JSON
app.use((req, res, next) => {                         // middleware: log
  console.log(`${req.method} ${req.url}`);
  next();
});

let libros = [{ id: 1, titulo: "Redes", anio: 2012 }];
let sig = 2;

app.get("/api/v1/libros", (req, res) => res.json(libros));

app.get("/api/v1/libros/:id", (req, res) => {
  const l = libros.find((x) => x.id === Number(req.params.id));
  if (!l) return res.status(404).json({ error: "No existe" });
  res.json(l);
});

app.post("/api/v1/libros", (req, res) => {
  const { titulo, anio } = req.body;
  if (typeof titulo !== "string" || !titulo.trim())
    return res.status(422).json({ error: "titulo es obligatorio" });
  const nuevo = { id: sig++, titulo: titulo.trim(), anio };
  libros.push(nuevo);
  res.status(201).location(`/api/v1/libros/${nuevo.id}`).json(nuevo);
});

app.delete("/api/v1/libros/:id", (req, res) => {
  libros = libros.filter((x) => x.id !== Number(req.params.id));
  res.status(204).end();
});

app.use((err, req, res, next) => {                    // manejador de errores
  console.error(err);
  res.status(500).json({ error: "Error interno" });
});

app.listen(process.env.PORT ?? 3000, () => console.log("API lista"));
```
FastAPI equivalente:
```python
# main.py   pip install fastapi uvicorn   ->   uvicorn main:app --reload
from fastapi import FastAPI, HTTPException, Response
from pydantic import BaseModel, Field

app = FastAPI(title="Libros")

class LibroIn(BaseModel):
    titulo: str = Field(min_length=1, max_length=200)
    anio: int | None = Field(default=None, ge=1400, le=2100)

class Libro(LibroIn):
    id: int

libros: dict[int, Libro] = {1: Libro(id=1, titulo="Redes", anio=2012)}

@app.get("/api/v1/libros", response_model=list[Libro])
def listar():
    return list(libros.values())

@app.get("/api/v1/libros/{libro_id}", response_model=Libro)
def obtener(libro_id: int):
    if libro_id not in libros:
        raise HTTPException(status_code=404, detail="No existe")
    return libros[libro_id]

@app.post("/api/v1/libros", response_model=Libro, status_code=201)
def crear(dato: LibroIn):
    nuevo = Libro(id=max(libros, default=0) + 1, **dato.model_dump())
    libros[nuevo.id] = nuevo
    return nuevo

@app.delete("/api/v1/libros/{libro_id}", status_code=204)
def borrar(libro_id: int):
    libros.pop(libro_id, None)
    return Response(status_code=204)
```
Paso a paso: los middleware se ejecutan en orden de registro; la validación en Express es manual y en FastAPI es declarativa (un `anio` de 5 produce 422 automático); FastAPI genera `/docs` con la especificación OpenAPI. Prueba: `curl -i -X POST localhost:3000/api/v1/libros -H "Content-Type: application/json" -d '{"titulo":""}'` debe devolver 422.

## Errores comunes
- Guardar estado en memoria del proceso en producción (se pierde y no escala).
- Credenciales en el código en lugar de variables de entorno.
- Bloquear el bucle de eventos con cálculos largos.
- Devolver trazas de error al cliente.
- Olvidar el middleware de errores o `next(err)` en código asíncrono antiguo.

## Ejercicios propuestos
1. ¿Qué orden de middleware es incorrecto: `app.use(rutas); app.use(express.json())`? *Respuesta: el parseo JSON debe ir antes de las rutas que leen `req.body`.*
2. Añade en FastAPI `PUT /libros/{id}`. *Respuesta: función con `LibroIn`, 404 si falta, reemplaza y devuelve el libro.*
3. ¿Qué ventaja ofrece Pydantic? *Respuesta: valida y convierte tipos automáticamente y alimenta la documentación OpenAPI.*

## Conexiones
[[Programación II]] (programación estructurada y objetos), [[Sistemas Operativos]] (procesos, puertos), [[Ingeniería de Software]] (arquitectura por capas, pruebas), [[Sistemas Distribuidos]] (APIs y escalado).

## Fuente
Conocimiento general: documentación de Express, FastAPI y Node.js. El ejemplo de FastAPI parte del que aparece en la nota principal.
