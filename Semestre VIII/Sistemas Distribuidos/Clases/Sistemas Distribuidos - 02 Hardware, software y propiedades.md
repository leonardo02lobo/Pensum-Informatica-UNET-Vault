---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 1/Clase 1.pdf, Clase 1 Complemento.pdf y Clase 2/Multiprocesador.pdf
---
# Sistemas Distribuidos - 02 Hardware, software y propiedades

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 01 Introducción y definiciones]]
Siguiente: [[Sistemas Distribuidos - 03 Modelo cliente-servidor y arquitecturas por capas]]

## Contexto y objetivo
Un SD se describe por su **hardware** (cómo se conectan las CPU y memorias), su **software** (qué sistema operativo da la ilusión de unidad) y las **propiedades** que debe ofrecer (transparencia, escalabilidad, fiabilidad, consistencia). Esta nota reúne esos tres ejes.

## 1. Conceptos de hardware
Se usa la taxonomía de Flynn. Para SD interesan las máquinas **MIMD** (múltiples instrucciones, múltiples datos), que se dividen por el modo de acceso a memoria:

- **Multiprocesadores** (memoria compartida): todas las CPU acceden a una memoria común. Pueden conectarse por bus o por conmutador. Existe un espacio de direcciones único.
- **Multicomputadoras** (memoria privada): cada CPU tiene su memoria local; se comunican por mensajes. Dos topologías populares con conmutador: **retícula** (malla, buena para problemas bidimensionales, grafos o visión) e **hipercubo** (cubo n-dimensional: $2^n$ nodos y cada nodo se conecta con $n$ vecinos; un hipercubo de 4 dimensiones son dos cubos de 8 vértices con sus vértices correspondientes unidos).

Cada categoría puede ser **con bus** (una red compartida; barata pero se satura) o **con conmutador** (cables punto a punto; escala mejor).

### Multiprocesadores según el capítulo 6 del material
- Un **multiprocesador** es una computadora con dos o más unidades de procesamiento sobre una memoria común, bajo un control integrado y un sistema operativo integrado.
- **Simétrico** si los procesadores tienen capacidad similar; **asimétrico** si no.
- Si cada procesador tiene una gran memoria local se trata de **multicomputadoras**, centralizadas o distribuidas.
- **Fuertemente acoplado:** comunicación por memoria común; velocidad del orden del ancho de banda de la memoria; cada CPU puede tener caché local. Limita el crecimiento la **contención de memoria** (dos o más procesadores accediendo a la misma unidad); se reduce aumentando el *interleaving* y asignando cuidadosamente los datos a los módulos.
- **Débilmente acoplado:** cada procesador con sus dispositivos de E/S y gran memoria local (*módulo computador*); se comunican por **transferencia de mensajes**; "muy débil", por eso se les llama sistemas distribuidos. El grado de acoplamiento lo determina la topología del sistema de mensajes. Son eficientes cuando la interacción entre tareas es mínima; los fuertemente acoplados soportan mucha interacción sin degradarse.

## 2. Conceptos de software: acoplamiento
| | Fuertemente acoplado | Débilmente acoplado |
|---|---|---|
| Retardo de mensajes | Corto | Grande |
| Tasa de transmisión | Alta | Baja |
| Imagen del usuario | Sistema único (ignorancia de la distribución) | Máquinas independientes (el usuario las conoce) |
| Ejemplo | Multiprocesador | Varias máquinas en red con distintos SO |

Las diapositivas resumen tres tipos de sistema operativo:
- **SO de red:** usuarios en estaciones independientes se comunican por un sistema de archivos compartido, pero cada uno domina su estación.
- **SO realmente distribuido (SD):** convierte toda la colección en un sistema integrado, como un sistema de tiempo completo tradicional.
- **Multiprocesador con tiempo compartido:** da imagen de sistema único **centralizando** todo (una cola de ejecución, un SO, un disco); por tanto **no es un SD**.

## 3. Propiedades deseables (Lafuente §1.2 y diapositivas)
### 3.1 Transparencia
El usuario y las aplicaciones ven los recursos como gestionados por una sola máquina virtual. Aspectos:
- **De identificación (nombres):** los nombres de recursos no dependen de la topología ni del nodo.
- **De ubicación:** no se sabe en qué nodo reside el recurso ni si es local o remoto; permite **migración** sin afectar aplicaciones. (En NFS la transparencia de identificación depende de que todos los clientes monten el recurso en el mismo punto: responsabilidad del administrador.)
- **De migración:** el SO mueve archivos sin que el usuario lo note.
- **De réplica:** el SO crea copias para tolerar fallos.
- **De concurrencia/compartición:** varios usuarios trabajan sobre el mismo archivo.
- **De paralelismo:** una aplicación se ejecuta en varias máquinas sin que el usuario lo sepa.
- **De rendimiento:** implementar las demás transparencias cuesta; en la práctica se relajan.

### 3.2 Otros desafíos de diseño (diapositivas)
**Flexibilidad** (núcleo monolítico vs microkernel; el microkernel deja servicios fuera), **confiabilidad** (disponibilidad, seguridad, tolerancia a fallos), **desempeño** (tiempo de respuesta, uso de CPU, memoria y tráfico de red) y **escalabilidad**.

### 3.3 Escalabilidad
Capacidad de crecer sin degradar. Problemas típicos: espacios de nombres (jerárquicos y particionados) y complejidad/rendimiento (algoritmos centralizados son cuellos de botella). Reglas prácticas: no usar componentes centralizados (un servidor, una tabla, un algoritmo), decisiones con información local, no suponer reloj global.

### 3.4 Fiabilidad y tolerancia a fallos
- **Disponibilidad:** fracción de tiempo operativo: $A = \dfrac{MTTF}{MTTF + MTTR}$.
- **Tolerancia a fallos:** aun con alta disponibilidad, un fallo en un instante crítico puede ser grave; se logra con **redundancia** (réplicas) y recuperación. Ver [[Sistemas Distribuidos - 12 Tolerancia a fallos, transacciones y consenso]].

### 3.5 Consistencia
Qué ven los procesos cuando hay datos replicados o cachés. Cuanto más fuerte la consistencia, más coordinación y menor rendimiento: de nuevo un compromiso.

## 4. Ejemplo resuelto
*Un servicio con $MTTF = 990$ h y $MTTR = 10$ h.* $A = 990/1000 = 0{,}99$, es decir 99 % (unas 87,6 h de caída al año). Con dos réplicas independientes, la indisponibilidad conjunta es $0{,}01^2 = 10^{-4}$, disponibilidad 99,99 %. Ilustra por qué la réplica aumenta la disponibilidad, a costa de mantener consistencia entre copias.

## Errores comunes
- Llamar "distribuido" a un multiprocesador SMP.
- Creer que transparencia total es siempre deseable: ocultar la red puede esconder latencias y fallos parciales (fallacias de la computación distribuida).
- Suponer que la contención de memoria desaparece con más CPU.

## Ejercicios propuestos
1. ¿Cuántas aristas tiene un hipercubo de dimensión $n$? *R: $n\,2^{n-1}$.*
2. Clasifique: cuatro PC con sistemas operativos distintos que comparten una carpeta de red. *R: débilmente acoplado, SO de red.*
3. ¿Qué transparencia viola un usuario que debe escribir `ftp servidor3`? *R: ubicación/acceso.*

## Conexiones
[[Sistemas Operativos]] (hilos, procesos); [[Organización del Computador]] (memoria y buses); [[Comunicaciones II]] (red).

## Fuente
Clase 1.pdf, Clase 1 Complemento.pdf, Multiprocesador.pdf (Cap. 6, Cap06.doc 2004).
