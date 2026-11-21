---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 1/Clase 1.pdf y Clase 1 Complemento.pdf (A. Lafuente, UPV/EHU, cap. 1)
---
# Sistemas Distribuidos - 01 Introducción y definiciones

Materia: [[Sistemas Distribuidos]]
Siguiente: [[Sistemas Distribuidos - 02 Hardware, software y propiedades]]

## Contexto y objetivo
Esta clase abre la materia (diapositivas "Introducción a los Sistemas Distribuidos – Parte 1, Revisión Teórica", prof. Dahyana Nimo, UNET, semestre 2012-1, más un capítulo complementario de Alberto Lafuente, UPV/EHU). El objetivo es responder: ¿qué es un sistema distribuido (SD)?, ¿de qué evolución histórica procede?, ¿para qué se construye y qué problemas trae?

## 1. Evolución histórica de los modelos de sistema
El complemento recorre cómo cambió la forma de organizar el cómputo; cada modelo explica una motivación:

| Modelo | Idea central | Ejemplo / observación |
|---|---|---|
| Sistemas de lotes | Procesar en diferido, secuencialmente, paquetes de tarjetas perforadas | Hoy aún útil en cálculo intensivo (supercomputación) |
| Tiempo compartido centralizado (mediados de los 60) | Aprovechar la CPU, cara y escasa, con terminales interactivas | Todos los recursos son centrales |
| Teleproceso | Terminales remotos acceden a un central por una red (p. ej. telefónica) con protocolo propietario | Reservas, transacciones bancarias |
| Sistemas personales (años 80) | Un sistema dedicado a un usuario gracias al microprocesador | Inicialmente monousuario, sin protección |
| Sistemas en red | Máquinas autónomas conectadas; un servidor ofrece un recurso y los clientes lo solicitan | Interoperabilidad con TCP/IP |
| Sistemas distribuidos | Los recursos de las máquinas se integran y desaparece la dualidad local/remoto | Ubicación transparente |

La diferencia clave entre "en red" y "distribuido": en un sistema en red el usuario sabe que hay varias máquinas y dónde están los archivos (por ejemplo, copia un archivo con ftp a otro equipo); en un SD el usuario ve **un solo sistema**.

## 2. Definiciones
Las diapositivas ofrecen tres formulaciones equivalentes:
1. Colección de computadoras separadas físicamente y conectadas por una red, que el usuario percibe como un solo sistema.
2. Un sistema que "se ejecuta como un sistema centralizado" pero en realidad lo hace sobre múltiples CPU independientes, de forma **transparente**.
3. Colección de computadoras **autónomas** unidas por una red y equipadas con software de sistemas distribuidos, que les permite coordinar acciones y compartir recursos; los usuarios perciben una única computadora.

Lafuente sintetiza una definición operativa con cuatro rasgos: **(1) conjunto de computadores, (2) interconectados, (3) que comparten un estado, (4) ofreciendo una visión de sistema único**. El rasgo (2) lo comparten los sistemas en red y los distribuidos; el (3) es exclusivo de los distribuidos: en una red cada nodo tiene estado independiente, en un SD se define un **estado global**. Consecuencia: la *visión de sistema único* (SSI, *Single System Image*). Como los componentes pueden ser heterogéneos, hace falta una capa de software, el **middleware**, que oculta la distribución (la red la ocultan los protocolos y la arquitectura de cada máquina el sistema operativo).

Ejemplo canónico de las diapositivas: la **World Wide Web**, donde todo se ve como un documento aunque resida en millones de servidores.

## 3. Objetivos
- Resolver problemas demasiado grandes para una supercomputadora o mainframe sin perder flexibilidad para problemas pequeños.
- Compartir información y recursos (periféricos, datos, servicios).
- Economizar procesamiento y almacenamiento (relación costo/rendimiento de PC estándar).
- Alta disponibilidad y confiabilidad (tolerancia a fallos).

## 4. Ventajas y desventajas
**Ventajas** (según las diapositivas): compartición de información y periféricos; reparto de carga; si un nodo falla el sistema sigue; ejecución concurrente; confiabilidad (otras máquinas retoman el trabajo); comunicación entre usuarios; economía (varios PC frente a un mainframe); velocidad por colaboración (en teoría, depende de la red); distribución inherente de ciertas tareas; escalabilidad (añadir componentes sin degradar).

**Desventajas**: se requiere software especializado para coordinar los recursos; hay que establecer seguridad que garantice la integridad de la información; la red es ahora parte crítica (saturación, pérdidas); aparecen fallos parciales y problemas de consistencia que no existían en un sistema único.

## 5. Perspectivas: informática móvil y ubicua
El complemento anticipa dos evoluciones: la **informática móvil** (equipos que salen de la red local, funcionan desconectados, forman redes ad-hoc, Mobile IP) y los **sistemas ubicuos** (*pervasive*): dispositivos con capacidad de cómputo y comunicación que "desaparecen" en el entorno (teléfonos, tarjetas inteligentes, domótica, automoción). Los recursos se descubren dinámicamente (Jini, UPnP). Es el germen de lo que hoy se llama IoT; ver la conexión con [[Automatización - 06 IoT, MQTT, Node-RED y ThingsBoard]].

## 6. Ejemplo resuelto: ¿red o sistema distribuido?
*Caso:* una oficina con cinco PC, una impresora compartida y un servidor de archivos al que cada usuario se conecta mapeando una unidad `Z:`.
- ¿Computadores interconectados? Sí.
- ¿Comparten un estado global y se ve un sistema único? No: el usuario sabe que `Z:` es "otra máquina" y cada PC tiene su propio sistema operativo.
- **Conclusión:** es un sistema en red (con cliente/servidor), no un SD. Para serlo, el sistema de archivos debería ser un único espacio de nombres con ubicación y réplicas transparentes (p. ej. un sistema de archivos distribuido).

## Errores comunes
- Confundir "multiprocesador con memoria compartida" con SD: da imagen de sistema único pero por **centralización**; tiene una cola de ejecución y un solo sistema operativo (ver nota 02).
- Pensar que más máquinas siempre implica más velocidad: depende de la red y de la comunicación entre tareas.
- Olvidar que la transparencia es una propiedad **deseable** que a veces se relaja por rendimiento.

## Ejercicios propuestos
1. Enumere los cuatro rasgos de la definición de Lafuente. *R: conjunto de computadores, interconectados, estado compartido, visión de sistema único.*
2. ¿Por qué un sistema de teleproceso no es distribuido? *R: el sistema central monopoliza la gestión de recursos; los terminales no integran sus recursos.*
3. Indique dos ventajas y dos desventajas de un SD frente a un mainframe. *R: economía y tolerancia a fallos; complejidad de software y seguridad/red.*

## Conexiones
- Siguiente: [[Sistemas Distribuidos - 02 Hardware, software y propiedades]].
- Prerrequisito: [[Comunicaciones II]]; fundamentos de procesos en [[Sistemas Operativos]].

## Fuente
Clase 1.pdf (1881 palabras) y Clase 1 Complemento.pdf (capítulo 1 de A. Lafuente). Parafraseado y ampliado con conocimiento general.
