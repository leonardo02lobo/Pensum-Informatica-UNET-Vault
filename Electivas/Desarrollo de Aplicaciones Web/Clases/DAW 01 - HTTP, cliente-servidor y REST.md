---
tags: [clase, electiva]
materia: Desarrollo de Aplicaciones Web
fuente: "conocimiento general"
---
# DAW 01 - HTTP, cliente-servidor y REST

Materia: [[Desarrollo de Aplicaciones Web]]
Anterior: (inicio de la serie)
Siguiente: [[DAW 02 - HTML5, CSS3 y diseño responsivo]]

## Contexto y objetivo
Toda aplicación web descansa en el protocolo HTTP y en el modelo cliente-servidor. Entenderlos permite depurar con criterio y diseñar APIs coherentes. Objetivo: leer y escribir mensajes HTTP, elegir métodos y códigos de estado correctos y diseñar una API REST.

## Teoría

### Arquitectura cliente-servidor
El **cliente** (navegador, app móvil) inicia solicitudes; el **servidor** las atiende y responde. Capas típicas: presentación, lógica, datos. Una URL se compone de `esquema://host:puerto/ruta?consulta#fragmento`. Antes de HTTP ocurre: resolución DNS, conexión TCP (y TLS en HTTPS, puerto 443 por defecto; 80 para HTTP).

### Mensaje HTTP
Solicitud: línea de petición (método, ruta, versión), cabeceras, línea en blanco, cuerpo opcional. Respuesta: línea de estado, cabeceras, cuerpo. HTTP es **sin estado**: cada petición es independiente (las cookies, tokens o sesiones añaden estado).

### Métodos
| Método | Uso | Seguro | Idempotente |
|---|---|:-:|:-:|
| GET | Leer | sí | sí |
| POST | Crear / acción | no | no |
| PUT | Reemplazar | no | sí |
| PATCH | Modificar parcial | no | no (en general) |
| DELETE | Borrar | no | sí |

### Códigos de estado
2xx éxito (200 OK, 201 Created, 204 No Content); 3xx redirección (301, 304 Not Modified); 4xx error del cliente (400, 401 no autenticado, 403 sin permiso, 404, 409 conflicto, 422); 5xx error del servidor (500, 502, 503).

### Cabeceras importantes
`Content-Type`, `Accept`, `Authorization`, `Cache-Control`, `ETag`, `Set-Cookie`/`Cookie`, `Origin`, `Access-Control-Allow-Origin` (CORS), `Location`.

### REST
Estilo arquitectónico (Fielding): recursos identificados por URI, representaciones (JSON), interfaz uniforme, sin estado, cacheable, sistema en capas. Buenas prácticas: sustantivos en plural (`/api/libros`), verbos vía método HTTP, anidar con moderación (`/api/libros/5/resenas`), paginación (`?page=2&limit=20`), versionado (`/api/v1`), errores en JSON consistente.

Versiones: HTTP/1.1 (conexiones persistentes), HTTP/2 (multiplexado binario), HTTP/3 (sobre QUIC/UDP).

## Ejemplo resuelto
Diseñar la API de una biblioteca y ejecutar un ciclo completo.

1. Recursos: `/api/v1/libros` (colección) y `/api/v1/libros/{id}`.
2. Crear un libro:
```http
POST /api/v1/libros HTTP/1.1
Host: biblioteca.example
Content-Type: application/json
Accept: application/json

{"titulo": "Redes de Computadoras", "autor": "Tanenbaum", "anio": 2012}
```
Respuesta correcta:
```http
HTTP/1.1 201 Created
Location: /api/v1/libros/17
Content-Type: application/json

{"id": 17, "titulo": "Redes de Computadoras", "autor": "Tanenbaum", "anio": 2012}
```
3. Con `curl`, probando el ciclo:
```bash
curl -i -X POST https://biblioteca.example/api/v1/libros \
  -H "Content-Type: application/json" \
  -d '{"titulo":"Redes","autor":"Tanenbaum","anio":2012}'
curl -i https://biblioteca.example/api/v1/libros/17
curl -i -X PATCH https://biblioteca.example/api/v1/libros/17 \
  -H "Content-Type: application/json" -d '{"anio":2013}'
curl -i -X DELETE https://biblioteca.example/api/v1/libros/17   # 204
curl -i https://biblioteca.example/api/v1/libros/17             # 404
```
Tabla de diseño resultante:
| Operación | Método y ruta | Éxito | Error |
|---|---|---|---|
| Listar | GET /libros?page=1 | 200 | 400 |
| Leer uno | GET /libros/17 | 200 | 404 |
| Crear | POST /libros | 201 | 422 |
| Modificar | PATCH /libros/17 | 200 | 404 |
| Borrar | DELETE /libros/17 | 204 | 404 |

Caché condicional: el servidor responde `ETag: "abc"`; el cliente repite con `If-None-Match: "abc"` y recibe `304` sin cuerpo.

## Errores comunes
- Usar GET para operaciones que modifican datos.
- Devolver 200 con `{"error": ...}` en lugar del código adecuado.
- Verbos en la URL (`/crearLibro`).
- Confundir 401 (no identificado) con 403 (identificado pero sin permiso).
- Ignorar CORS: el navegador bloquea respuestas sin `Access-Control-Allow-Origin` adecuado.

## Ejercicios propuestos
1. ¿Qué código devuelve un POST que crea un recurso? *Respuesta: 201 Created con cabecera Location.*
2. ¿Por qué PUT es idempotente y POST no? *Respuesta: repetir PUT deja el mismo estado final; repetir POST puede crear duplicados.*
3. Diseña las rutas para reseñas de un libro. *Respuesta: `GET/POST /libros/{id}/resenas`, `DELETE /libros/{id}/resenas/{rid}`.*

## Conexiones
[[Comunicaciones I]] y [[Administración de Redes]] (TCP/IP, DNS), [[Sistemas Distribuidos]] (servicios, RPC y REST), [[Ingeniería de Software]] (diseño de APIs).

## Fuente
Conocimiento general: RFC 9110 (semántica HTTP), tesis de R. Fielding, MDN Web Docs.
