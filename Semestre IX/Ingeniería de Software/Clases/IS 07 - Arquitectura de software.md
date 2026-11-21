---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 07 - Arquitectura de software

Materia: [[Ingeniería de Software]]
Anterior: [[IS 06 - Patrones de diseño]]
Siguiente: [[IS 08 - Pruebas de software]]

## Contexto y objetivo
La **arquitectura de software** es el conjunto de decisiones estructurales significativas: componentes, relaciones entre ellos, y los principios que guían su diseño y evolución. Son las decisiones "difíciles de cambiar". Objetivo: conocer los estilos arquitectónicos principales, relacionarlos con atributos de calidad, y documentar decisiones con el modelo C4 y ADR.

## Conceptos clave
- **Atributos de calidad** (drivers arquitectónicos): rendimiento, escalabilidad, disponibilidad, seguridad, modificabilidad, testabilidad, interoperabilidad, usabilidad. La arquitectura es el resultado de **negociar trade-offs** entre ellos (teorema CAP en sistemas distribuidos: consistencia, disponibilidad, tolerancia a particiones; solo dos de tres bajo partición).
- **Vista arquitectónica**: representación desde una perspectiva (Kruchten 4+1: lógica, de procesos, de desarrollo, física, y escenarios).
- **Arquitectura vs diseño**: la arquitectura fija la estructura global; el diseño detalla cada componente.

## Estilos arquitectónicos

### 1. Capas (layered)
Presentación, lógica de negocio, acceso a datos (y a veces dominio, infraestructura). Cada capa solo usa la inferior. 
+ Simple, separación de responsabilidades. - Posible "arquitectura de pasamanos" y sensibilidad a cambios en capas bajas.

### 2. Cliente-servidor y n-capas
El cliente solicita servicios; el servidor los provee. 3 capas físicas: navegador, servidor de aplicación, BD. Base de la web (ver [[Sistemas Distribuidos]]).

### 3. MVC / MVP / MVVM
Separa **Modelo** (datos y reglas), **Vista** (presentación), **Controlador** (entrada y coordinación). Frameworks: Django (MTV), Spring MVC, Rails, Laravel. MVVM: enlace de datos bidireccional (Angular, WPF).

### 4. Monolito modular
Un solo despliegue con módulos de bajo acoplamiento. Muy buen punto de partida para equipos pequeños: simple de desplegar y depurar.

### 5. Microservicios
Servicios pequeños, autónomos, desplegables de forma independiente, cada uno con su base de datos, comunicados por HTTP/gRPC o mensajería.
+ Escalado y despliegue independientes, equipos autónomos, tecnología heterogénea.
- Complejidad distribuida: latencia, consistencia eventual, observabilidad, pruebas de contrato, DevOps maduro.
Patrones asociados: API Gateway, Service Discovery, Circuit Breaker, Saga, CQRS, Event Sourcing, Strangler Fig (migración incremental).
Consejo: "monolito primero" salvo que haya razones de escala/organización.

### 6. Orientada a eventos
Productores publican eventos en un broker (Kafka, RabbitMQ); consumidores reaccionan. Desacopla en tiempo y espacio. Dificulta el seguimiento del flujo y la consistencia.

### 7. Pipes and filters / Pipeline
Flujo de datos a través de filtros (compiladores, ETL, comandos Unix).

### 8. Basada en microkernel (plug-ins)
Núcleo mínimo + extensiones (IDEs, navegadores).

### 9. Hexagonal (puertos y adaptadores) / Limpia / Cebolla
El **dominio** está en el centro y no depende de frameworks ni de la BD; se comunica por *puertos* (interfaces) implementados por *adaptadores* (REST, SQL, colas). Aplica la inversión de dependencias de [[IS 05 - Principios de diseño y SOLID]]. Resultado: dominio testeable sin infraestructura.

### 10. Serverless y arquitecturas en la nube
Funciones como servicio (FaaS), BaaS. Paga por uso, escala a cero; riesgo de dependencia de proveedor y arranque en frío.

## Comparativa rápida
| Estilo | Escalabilidad | Complejidad | Ideal para |
|---|---|---|---|
| Capas/monolito | Media (vertical, horizontal si sin estado) | Baja | CRUD, equipos pequeños |
| Microservicios | Alta | Alta | Organizaciones grandes, dominios separados |
| Eventos | Alta | Media-Alta | Integración, flujos asíncronos |
| Hexagonal | Neutral | Media | Dominios ricos, alta testabilidad |

## Tácticas arquitectónicas (ejemplos)
- Rendimiento: caché, balanceo de carga, procesamiento asíncrono, índices.
- Disponibilidad: redundancia, replicación, health checks, failover.
- Seguridad: autenticación y autorización (OAuth2/OIDC, JWT), cifrado en tránsito (TLS) y en reposo, principio de mínimo privilegio.
- Modificabilidad: interfaces estables, ocultar información, configuración externa.

## Documentación: modelo C4 y ADR
**C4** (Simon Brown) usa cuatro niveles de zoom: **Contexto** (sistema y actores), **Contenedores** (aplicaciones/BD desplegables), **Componentes** (módulos dentro de un contenedor), **Código** (clases; opcional).

**ADR (Architecture Decision Record)**: documento corto por decisión.
```
# ADR-004: Usar PostgreSQL como base de datos principal
Estado: Aceptada (2026-03-10)
Contexto: Necesitamos transacciones ACID y consultas relacionales; equipo conoce SQL.
Decisión: PostgreSQL 16 administrado.
Consecuencias: (+) integridad referencial; (-) escalado de escrituras requiere particionado.
Alternativas consideradas: MongoDB, MySQL.
```
Se versionan en el repositorio (docs/adr).

## ATAM (evaluación)
Architecture Tradeoff Analysis Method: se definen escenarios de calidad (árbol de utilidad), se analizan puntos de sensibilidad, compromisos y riesgos.

## Ejemplo resuelto: arquitectura para el sistema de préstamos
Requisitos clave: 50 usuarios, acceso desde red interna, un solo equipo de 2 desarrolladores, presupuesto nulo.
1. Atributos prioritarios: modificabilidad, simplicidad de despliegue, seguridad básica.
2. Descarta microservicios (costo operativo injustificado).
3. Elección: **monolito modular en 3 capas** (Django o Spring Boot): módulos `equipos`, `prestamos`, `reportes`; API REST interna + vistas; PostgreSQL.
4. Despliegue: un contenedor Docker + proxy Nginx; respaldos con `pg_dump` programado.
5. Registro: ADR-001 "Monolito modular", ADR-002 "PostgreSQL"; diagrama C4 nivel 2.
6. Plan de evolución: si "reportes" requiere escalar, extraerlo a servicio (Strangler).

## Errores comunes
- Elegir microservicios por moda ("resume-driven development").
- Compartir una BD entre microservicios (acoplamiento oculto).
- No definir requisitos de calidad medibles antes de decidir.
- Arquitectura "de PowerPoint" que no coincide con el código.
- Ignorar observabilidad (logs, métricas, trazas).

## Ejercicios propuestos
1. Un sistema recibe 10 000 eventos/s de sensores IoT. ¿Estilo? *Resp.: orientado a eventos con broker (Kafka/MQTT) y procesamiento en streaming.*
2. ¿Qué nivel de C4 muestra una BD y una app web como cajas desplegables? *Resp.: nivel 2, Contenedores.*
3. Explica por qué el dominio hexagonal es más fácil de probar. *Resp.: depende de interfaces, así que los adaptadores se sustituyen por dobles.*

## Conexiones
[[Sistemas Distribuidos]], [[Base de Datos II]], [[Desarrollo de Aplicaciones Web]] (electiva), [[Administración de Redes]], [[IS 11 - Gestión de configuración y DevOps]].

## Fuente
Conocimiento general. Bass, Clements, Kazman, *Software Architecture in Practice*; Richards y Ford, *Fundamentals of Software Architecture*; Brown, *The C4 model*; Nygard, "Documenting Architecture Decisions".
