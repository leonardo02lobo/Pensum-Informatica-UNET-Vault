---
tags: [electiva]
---
# Desarrollo de Aplicaciones Web

Opción de [[Electivas]].

## Descripción
Construcción de aplicaciones web de extremo a extremo: interfaz, lógica de servidor, persistencia, seguridad y despliegue.

## Temario típico (verificar con el programa oficial)
1. Protocolo HTTP, arquitectura cliente-servidor, REST.
2. Front-end: HTML5, CSS3, JavaScript, frameworks (React, Vue), accesibilidad y diseño responsivo.
3. Back-end: Node.js/Express, Python (Django, Flask, FastAPI) o PHP/Java; APIs REST y JSON.
4. Persistencia: SQL (PostgreSQL, MySQL) y NoSQL (MongoDB); ORM.
5. Autenticación y seguridad: sesiones, JWT, OWASP Top 10 (XSS, CSRF, inyección SQL).
6. Despliegue: Git, Docker, CI/CD, nube.

## Ejemplo
```python
from fastapi import FastAPI
app = FastAPI()
@app.get("/saludo/{nombre}")
def saludo(nombre: str):
    return {"mensaje": f"Hola {nombre}"}
# uvicorn main:app --reload
```

## Relación con el pensum
[[Programación II]], [[Base de Datos I]], [[Base de Datos II]], [[Ingeniería de Software]], [[Sistemas Distribuidos]], [[Multimedia]], [[Sistemas Operativos]].

## Recursos y bibliografía
- MDN Web Docs; documentación de FastAPI, Express y React.
- Flanagan, D. *JavaScript: The Definitive Guide*.
- OWASP Top 10 y Cheat Sheets.
- freeCodeCamp, The Odin Project.
