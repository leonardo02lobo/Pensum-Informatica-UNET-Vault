---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: ~/Documentos/UNET/Comunicaciones 2/parcial 1 (README.md, docker-compose.yml)
---
# Comunicaciones II - 07 Contenedores Docker y arquitectura cliente-servidor

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 06 Capa de aplicación HTTP DNS correo FTP]]
Siguiente: [[Comunicaciones II - 08 Seguridad en redes criptografía y TLS]]

## Contexto y objetivo
El **Parcial 1** consistió en desplegar un "Blog Sencillo" de tres servicios en contenedores orquestados con Docker Compose. El objetivo didáctico: comprender la arquitectura de tres capas (presentación, lógica, datos), las redes entre contenedores, la persistencia con volúmenes y la configuración mediante variables de entorno.

## Contenedores frente a máquinas virtuales
Un **contenedor** es un proceso aislado con *namespaces* (PID, red, montajes, usuarios) y límites de recursos con *cgroups*; comparte el kernel del anfitrión. Es más ligero que una VM (que incluye un SO completo y hipervisor). Una **imagen** es una plantilla inmutable por capas; un contenedor es su instancia en ejecución. Ver procesos y aislamiento en [[Sistemas Operativos]].

## Arquitectura del proyecto
| Servicio | Tecnología | Puerto host | Rol |
|---|---|---|---|
| frontend | Astro (build estático) + Nginx | 8080 | interfaz web |
| backend | Node.js + TypeScript + Express | 3000 | API REST |
| database | PostgreSQL 16 | 5432 | persistencia |

Flujo: navegador -> `http://localhost:8080` (Nginx sirve HTML/JS estático) -> el JavaScript del navegador llama a `PUBLIC_API_URL` (`http://localhost:3000`) -> Express -> PostgreSQL por el nombre de servicio `database:5432`.

Nota arquitectónica: como la API es consumida *desde el navegador del host*, la URL que se incrusta en el build del frontend es la del host, no el nombre interno `backend`; en cambio el backend usa el nombre `database` porque ambos están dentro de la red Docker.

## Docker Compose: lectura comentada del `docker-compose.yml`
```yaml
services:
  database:
    image: postgres:16-alpine
    environment:                       # credenciales desde .env
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: ${DB_NAME}
    volumes:
      - pgdata:/var/lib/postgresql/data              # persistencia
      - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql:ro  # esquema inicial
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${DB_USER} -d ${DB_NAME}"]
      interval: 5s
      retries: 10
  backend:
    build: { context: ./backend }
    environment: { DB_HOST: database, DB_PORT: 5432, ... }
    depends_on:
      database: { condition: service_healthy }       # espera a que la BD responda
  frontend:
    build:
      context: ./frontend
      args: { PUBLIC_API_URL: ${PUBLIC_API_URL} }    # variable de build
    ports: ["8080:80"]
networks: { blog-net: { driver: bridge } }
volumes: { pgdata: }
```
Puntos clave:
- **Red bridge personalizada** `blog-net`: Docker proporciona DNS interno, de modo que `database` resuelve a la IP del contenedor.
- **Volumen nombrado** `pgdata`: los datos sobreviven a `docker compose down` (se borran solo con `-v`).
- **`/docker-entrypoint-initdb.d`**: scripts que la imagen oficial de PostgreSQL ejecuta solo en el primer arranque con volumen vacío.
- **`depends_on` + `healthcheck`**: orden de arranque basado en salud, no solo en "contenedor iniciado". Además el backend reintenta la conexión (defensa en profundidad).
- **Dockerfiles multi-stage**: etapa 1 compila (TypeScript/Astro), etapa final copia solo lo necesario -> imágenes pequeñas; el backend corre con `USER node` (mínimo privilegio).
- **Publicación de puertos** `host:contenedor` (NAT de Docker con iptables). El `5432:5432` es "opcional para pruebas"; en producción no se expone la BD (ver informe OSINT, punto 5).

## API REST del backend
GET/POST `/api/posts`, GET/PUT/DELETE `/api/posts/:id`, GET `/health`.
```bash
curl -X POST http://localhost:3000/api/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"Mi primera entrada","content":"Hola mundo"}'
```
El servidor debe validar entradas y usar **consultas parametrizadas** (`$1, $2`) para evitar inyección SQL.

## Ejecución y verificación
```bash
cp .env.example .env && docker compose up --build   # o ./start.sh
docker ps                                           # 3 contenedores
docker compose logs -f backend
./stop.sh        # conserva datos;  ./stop.sh -v  borra el volumen
```
Prueba de persistencia: crear entrada, `./stop.sh`, `./start.sh`: la entrada sigue ahí.

## Errores comunes
- Usar `localhost` dentro de un contenedor para llegar a otro (apunta a sí mismo): usar el nombre del servicio.
- Cambiar `init.sql` y no ver efecto: el script solo corre con volumen nuevo.
- Subir `.env` con contraseñas al repositorio (se incluye `.env.example` y `.gitignore`).
- Exponer el puerto de la base de datos al exterior sin necesidad.
- Variables de build del frontend: cambiar `PUBLIC_API_URL` exige reconstruir la imagen.

## Ejercicios propuestos
1. ¿Qué comando elimina contenedores, red y volúmenes? *Resp.: `docker compose down -v`.*
2. ¿Cómo agregaría un proxy inverso Nginx único en el puerto 80 para frontend y API? *Resp.: un servicio nginx con `location /` -> frontend y `location /api/` -> backend; ya no se publican 3000 y 8080.*
3. ¿Por qué `depends_on` simple no garantiza que la BD esté lista? *Resp.: solo espera a que el contenedor inicie, no a que acepte conexiones.*

## Conexiones
Capa de aplicación: [[Comunicaciones II - 06 Capa de aplicación HTTP DNS correo FTP]]. Aplicaciones web: [[Desarrollo de Aplicaciones Web]]. Bases de datos del proyecto: ver [[Base de Datos II]].

## Fuente
`~/Documentos/UNET/Comunicaciones 2/parcial 1/README.md` y `docker-compose.yml`. No se leyeron los fuentes de `backend/` y `frontend/` (solo README y compose).
