---
tags: [clase, semestre-VIII]
materia: Sistema de Información II
---
# Sistema de Información II - Arquitectura de Sistemas de Información y APIs

Materia: [[Sistema de Información II]]
Anterior: [[Sistema de Información II - Ciclo de Vida y Tipos de Sistemas Empresariales]]
Siguiente: [[Sistema de Información II - Diseño Detallado con UML y Procesos BPMN]]

## Contexto y objetivo
Diseñar la **arquitectura de software** de sistemas de información empresariales separando responsabilidades por capas (3 capas / MVC), comparando estilos cliente-servidor, servicios web **REST** y **microservicios**, y considerando criterios de despliegue en la nube.

## 1. Arquitectura en capas y patrón MVC
Separar responsabilidades evita el acoplamiento rígido entre la interfaz gráfica, las reglas de negocio y el almacenamiento:
1. **Capa de presentación (Frontend / UI)**: interacción con el usuario (web, móvil, escritorio), validación básica de formularios y consumo de servicios.
2. **Capa de lógica de negocio (Backend / Dominio)**: reglas empresariales (p. ej., "el stock no puede quedar negativo", cálculo de impuestos, flujos de aprobación).
3. **Capa de acceso a datos (Persistencia)**: consultas SQL/ORM, transacciones y conexión con el SGBD.

En aplicaciones web, el patrón **MVC** (*Modelo–Vista–Controlador*) organiza la presentación y el flujo de peticiones separando el *Modelo* (datos y reglas), la *Vista* (renderizado) y el *Controlador* (orquestador de entrada/salida).

## 2. Cliente-Servidor y Servicios Web (APIs REST)
En la arquitectura **cliente-servidor**, el cliente solicita recursos y el servidor procesa y responde. Actualmente la integración entre módulos y sistemas externos se realiza mediante **APIs REST** sobre HTTP/HTTPS con intercambio en **JSON**:
- Recursos identificados por URI (ej. `/api/v1/productos/42`).
- Verbos HTTP semánticos: `GET` (consultar), `POST` (crear), `PUT`/`PATCH` (actualizar), `DELETE` (eliminar).
- **Sin estado (*stateless*)**: cada petición contiene la información necesaria (p. ej., token JWT en cabecera `Authorization`).
- Códigos de respuesta estándar: `200 OK`, `201 Created`, `400 Bad Request`, `401 Unauthorized`, `404 Not Found`, `500 Internal Server Error`.

### Ejemplo de contrato REST (inventario)
```http
POST /api/v1/movimientos HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token>

{
  "id_producto": 105,
  "tipo": "SALIDA",
  "cantidad": 5
}
```
Si el stock actual es $3$, la capa de negocio rechaza la operación con `409 Conflict` o `422 Unprocessable Entity` indicando `"Stock insuficiente"`.

## 3. Monolito modular vs. Microservicios y Nube
- **Monolito modular**: un único artefacto desplegable con módulos internos bien desacoplados. Ideal para equipos pequeños/medianos: menor complejidad operativa y transacciones ACID simples.
- **Microservicios**: cada dominio de negocio (Facturación, Inventario, Autenticación) es un servicio independiente con su propia base de datos y ciclo de despliegue. Aporta escalabilidad independiente, pero introduce latencia de red, consistencia eventual y complejidad en observabilidad y orquestación.
- **Computación en la nube**: modelos **IaaS** (servidores virtuales), **PaaS** (plataformas administradas) y **SaaS** (software listo para usar, p. ej. ERP en la nube).

## Errores comunes
- Colocar reglas de negocio críticas exclusivamente en el frontend (JavaScript), permitiendo que un cliente malicioso las evada llamando directo a la API.
- Adoptar microservicios prematuramente cuando un monolito modular bien diseñado resuelve el problema con una fracción del costo operativo.
- Exponer claves primarias secuenciales o mensajes de error internos de SQL en las respuestas de la API.

## Ejercicios propuestos
1. Diseñe los endpoints REST básicos (método, ruta y código de éxito) para gestionar el recurso `atenciones` de un sistema universitario.
   - *Respuesta*: `GET /api/v1/atenciones` (`200`), `GET /api/v1/atenciones/{id}` (`200`), `POST /api/v1/atenciones` (`201`), `PATCH /api/v1/atenciones/{id}` (`200`), `DELETE /api/v1/atenciones/{id}` (`204`).
2. ¿En qué capa debe validarse que una factura no pueda emitirse con monto negativo y por qué?
   - *Respuesta*: en la **capa de lógica de negocio** (además de restricciones `CHECK` en base de datos como segunda línea de defensa), porque garantiza la regla sin importar qué cliente o interfaz consuma el servicio.

## Conexiones
- Desarrollo web e interfaces en [[Desarrollo de Aplicaciones Web]].
- Persistencia relacional y transacciones en [[Base de Datos II]] y [[Administración de Base de Datos]].
- Diseño detallado de componentes en [[Sistema de Información II - Diseño Detallado con UML y Procesos BPMN]].

## Fuente
Basado en el programa orientativo de [[Sistema de Información II]] (Kendall & Kendall, *Análisis y Diseño de Sistemas*; Laudon & Laudon, *Sistemas de Información Gerencial*).
