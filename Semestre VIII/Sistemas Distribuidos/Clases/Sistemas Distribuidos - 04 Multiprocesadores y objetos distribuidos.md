---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 2/Clase 2.pdf y Multiprocesador.pdf
---
# Sistemas Distribuidos - 04 Multiprocesadores y objetos distribuidos

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 03 Modelo cliente-servidor y arquitecturas por capas]]
Siguiente: [[Sistemas Distribuidos - 05 Peer-to-peer]]

## Contexto y objetivo
Completa el catálogo de arquitecturas de la Clase 2: la **arquitectura multiprocesador** (el modelo "más simple") y la **arquitectura de objetos distribuidos** (OD), que elimina la distinción cliente/servidor. Para la parte de hardware multiprocesador véase la nota 02.

## 1. Arquitectura multiprocesador (software)
- El software está formado por varios procesos que pueden (no necesariamente) ejecutarse en procesadores distintos.
- Común en **sistemas grandes de tiempo real**: recogen información, deciden y envían señales para modificar el entorno, bajo un **planificador (scheduler)**.
- El uso de múltiples procesadores mejora rendimiento y adaptabilidad. La distribución de procesos puede ser **predeterminada** o decidida por un **despachador (dispatcher)**.
- **Ejemplo de las diapositivas, control de tránsito:** sensores y cámaras recogen flujo de tráfico y lo procesan localmente (procesador de señales); un procesador de flujo de tráfico alimenta consolas de operadores; los operadores indican a un proceso de control de semáforos qué hacer. Tres procesadores, cada uno con procesos de control de sensores, visualización y control de luces.

Relación con el hardware: sobre un multiprocesador fuertemente acoplado, estos procesos comparten memoria; sobre multicomputadoras débilmente acopladas, intercambian mensajes (nota 02).

## 2. Objetos distribuidos
### Limitaciones del modelo cliente-servidor
Clientes y servidores son diferentes; los clientes deben conocer los servicios y cómo contactar cada servidor; el diseñador debe planificar escalabilidad y balanceo de carga al añadir clientes.

### Idea
En una arquitectura de objetos distribuidos **se elimina la distinción cliente/servidor**: los componentes son objetos que **proporcionan y requieren** servicios; otros objetos llaman a esos servicios sin distinguir lógicamente quién es proveedor o receptor.
- Los objetos se distribuyen por varias computadoras y se comunican a través de middleware, el **intermediario de peticiones de objetos (ORB)**, que ofrece una interfaz transparente: un **bus de software**. El estándar típico es CORBA; en Java, RMI (ver nota 09).
- La decisión cliente rico/ligero **es irrelevante**: no hay que decidir de antemano dónde ubicar la lógica.
- Flexible y escalable: se añaden objetos/recursos según necesidad; permite reconfigurar el sistema dinámicamente.

### Ventajas y desventajas
Ventajas: flexibilidad en ubicación de servicios, extensibilidad, reutilización. Desventajas (conocimiento general): más complejo de diseñar que CS; el middleware añade sobrecarga; un fallo del ORB es crítico; difícil de verificar.

## 3. Ejemplo resuelto
*Subastas en línea con objetos:* `Subasta`, `Oferta`, `Usuario` y `Notificador` son objetos en máquinas diferentes. `Oferta.registrar()` llama a `Subasta.validarPuja()` y esta a `Notificador.avisar()`. Ningún objeto es "el servidor": cada uno es cliente de otros. Si la carga de `Notificador` crece, se replica el objeto y el ORB reparte llamadas; los demás objetos no cambian.

## Errores comunes
- Confundir objeto distribuido con servicio web: el primero mantiene identidad y estado remotos; el servicio web suele ser sin estado (ver nota 06).
- Suponer que la invocación remota es como la local: puede fallar parcialmente (nota 09).

## Ejercicios propuestos
1. ¿Qué papel cumple el ORB? *R: intermediario transparente de peticiones entre objetos (bus de software).*
2. ¿Qué diferencia hay entre scheduler y dispatcher? *R: el scheduler controla el orden de ejecución; el dispatcher asigna procesos a procesadores.*
3. ¿Por qué en OD es irrelevante cliente ligero vs rico? *R: no hay capas fijas; cada objeto decide dónde corre.*

## Conexiones
[[Sistemas Distribuidos - 09 RPC y RMI]], [[Sistemas Distribuidos - 03 Modelo cliente-servidor y arquitecturas por capas]], [[Sistemas Operativos]] (planificación).

## Fuente
Clase 2.pdf; Multiprocesador.pdf.
