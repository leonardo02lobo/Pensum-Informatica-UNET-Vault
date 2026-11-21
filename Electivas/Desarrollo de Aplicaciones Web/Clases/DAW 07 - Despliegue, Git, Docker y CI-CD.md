---
tags: [clase, electiva]
materia: Desarrollo de Aplicaciones Web
fuente: "conocimiento general"
---
# DAW 07 - Despliegue, Git, Docker y CI-CD

Materia: [[Desarrollo de Aplicaciones Web]]
Anterior: [[DAW 06 - Autenticación y seguridad web]]
Siguiente: (fin de la serie)

## Contexto y objetivo
Una aplicación solo aporta valor cuando está desplegada y se puede actualizar sin riesgo. Objetivo: versionar con Git, empaquetar con Docker, automatizar pruebas y entrega con CI/CD, y conocer las opciones de nube.

## Teoría

### Git
Sistema de control de versiones distribuido. Conceptos: *commit*, rama (`branch`), fusión (`merge`) y reorganización (`rebase`), repositorio remoto, *pull request*. Flujos: *trunk-based* o *GitFlow*. Buen commit: pequeño, con mensaje que explica el porqué. `.gitignore` para `node_modules`, `.env`, binarios.

### Contenedores y Docker
Un contenedor empaqueta aplicación y dependencias sobre el kernel del anfitrión (a diferencia de una máquina virtual, que trae su propio kernel). **Imagen** (plantilla inmutable en capas) y **contenedor** (instancia). `Dockerfile` define la imagen; `docker compose` orquesta varios servicios (API, base de datos).

### Integración y entrega continuas
- **CI**: cada *push* ejecuta compilación, pruebas y análisis estático.
- **CD**: entrega (manual) o despliegue (automático) del artefacto aprobado.
Principios: pipeline como código, mismos artefactos en todos los entornos, configuración por variables de entorno, *rollback* rápido.

### Entornos y nube
Desarrollo, pruebas (staging), producción. Modelos: IaaS (VM), PaaS (Render, Fly.io, Heroku, Vercel), contenedores gestionados, *serverless*. Balanceador, HTTPS (certificados Let's Encrypt), dominio y DNS, registros y monitoreo.

## Ejemplo resuelto
Desplegar la API FastAPI (DAW 04) con PostgreSQL y un pipeline de CI.

Estructura:
```
proyecto/
  app/main.py
  requirements.txt
  Dockerfile
  docker-compose.yml
  .github/workflows/ci.yml
  tests/test_api.py
```
`Dockerfile`:
```dockerfile
FROM python:3.12-slim
WORKDIR /srv
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app ./app
RUN useradd -m appuser
USER appuser
EXPOSE 8000
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```
`docker-compose.yml`:
```yaml
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: biblio
    volumes:
      - datos:/var/lib/postgresql/data
  api:
    build: .
    environment:
      DATABASE_URL: postgresql+psycopg://postgres:${DB_PASSWORD}@db/biblio
      JWT_SECRET: ${JWT_SECRET}
    ports:
      - "8000:8000"
    depends_on:
      - db
volumes:
  datos:
```
Pipeline `ci.yml` (GitHub Actions):
```yaml
name: ci
on: [push, pull_request]
jobs:
  prueba:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with: { python-version: "3.12" }
      - run: pip install -r requirements.txt pytest httpx
      - run: pytest -q
      - run: docker build -t biblio-api:${{ github.sha }} .
```
Comandos de uso:
```bash
git init && git add . && git commit -m "API de libros inicial"
git switch -c feature/login
# ... trabajar ...
git push -u origin feature/login      # abre un pull request; el CI corre pruebas
echo "DB_PASSWORD=cambiar" > .env     # ¡.env en .gitignore!
docker compose up -d --build
curl -i localhost:8000/api/v1/libros
docker compose logs -f api
```
Paso a paso: la imagen instala dependencias antes de copiar el código para aprovechar el caché de capas; corre como usuario no root; las contraseñas viajan por variables de entorno, no en la imagen; el CI bloquea el *merge* si fallan las pruebas; el despliegue en un servidor consiste en `git pull` y `docker compose up -d --build`, o en publicar la imagen en un registro y que la plataforma la ejecute.

Prueba mínima:
```python
# tests/test_api.py
from fastapi.testclient import TestClient
from app.main import app

def test_listar():
    r = TestClient(app).get("/api/v1/libros")
    assert r.status_code == 200
```

## Errores comunes
- Subir `.env` o llaves a Git (si ocurre, rotar los secretos; borrar el commit no basta).
- Imágenes con `latest` o ejecutadas como root.
- Datos de la base de datos dentro del contenedor sin volumen.
- Desplegar sin pruebas ni plan de reversión.
- Commits gigantes que mezclan cambios.

## Ejercicios propuestos
1. ¿Por qué copiar `requirements.txt` antes que el código en el Dockerfile? *Respuesta: el caché de capas evita reinstalar dependencias si solo cambia el código.*
2. ¿Diferencia entre contenedor y máquina virtual? *Respuesta: el contenedor comparte el kernel del anfitrión; la VM virtualiza hardware con su propio sistema operativo.*
3. Comando para deshacer el último commit conservando los cambios. *Respuesta: `git reset --soft HEAD~1`.*

## Conexiones
[[Sistemas Operativos]] (procesos, aislamiento, cgroups), [[Ingeniería de Software]] (configuración, versiones, integración continua), [[Administración de Redes]] (puertos, DNS, proxy inverso), [[Sistemas Distribuidos]] (escalado, orquestación).

## Fuente
Conocimiento general: documentación de Git, Docker y GitHub Actions; Kim et al., *The DevOps Handbook*.
