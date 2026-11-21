---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 3/GerenciaProcesos.pdf
---
# Sistemas Distribuidos - 07 Gerencia de procesos y asignación de procesadores

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 06 SOA y servicios web]]
Siguiente: [[Sistemas Distribuidos - 08 Comunicación entre procesos]]

## Contexto y objetivo
Clase 3 (parte 3 de las diapositivas de la prof. Nimo): en un SD con muchos procesadores, un aspecto central es **cómo se usan**. Se estudian los modelos de organización de procesadores y los algoritmos que deciden en qué máquina ejecutar cada proceso.

## 1. Modelos de organización
1. **Estaciones de trabajo:** PC dispersas en una LAN, con o sin disco. Cada usuario tiene poder de cómputo propio y alta autonomía.
   - *Máquina inactiva:* sin usuarios esperando respuesta; el material la define como la que "lleva varios minutos sin entrada de teclado o ratón y no ejecuta procesos interactivos".
   - Búsqueda de máquina inactiva: **dirigida por el emisor** (la máquina sobrecargada pide "ayúdenme") o **dirigida por el receptor** (las ociosas anuncian "estoy disponible" a un administrador de procesos).
   - Problema: no hay reparto de carga; en entornos típicos se desperdicia ~80 % de los ciclos de CPU. Cuando la estación deja de estar inactiva (el dueño regresa): no hacer nada (el dueño nota mal rendimiento), **migrar el proceso** (costoso) o continuar con prioridad baja.
2. **Pila (pool) de procesadores:** conjunto de CPU asignadas dinámicamente según demanda; los usuarios usan terminales gráficas de alto rendimiento; no existe "propiedad" de procesadores.
3. **Híbrido:** combina estaciones y pool; el SO permite más de un hilo por proceso, y el lenguaje usa un hilo del núcleo para implementar grupos de hilos de usuario: flexibilidad y rendimiento máximo potencial.

## 2. Asignación de procesadores
Objetivo: decidir en qué procesador ejecutar un proceso y lograr **reparto y equilibrio de carga** (*load sharing/balancing*). Suposiciones: procesadores compatibles, velocidades posiblemente distintas, comunicación entre cualesquiera dos.

Tipos de carga:
- **Procesos cooperantes** (misma aplicación paralela): minimizar el tiempo de ejecución de la aplicación.
- **Procesos disjuntos** (usuarios distintos): maximizar la utilización de procesadores.

Propiedades de los algoritmos distribuidos: la información relevante se reparte entre máquinas; las decisiones se basan en información local; debe evitarse un punto único de fallo; **no existe reloj común** (ver nota 10).

### Clasificación
- **Deterministas vs heurísticos:** los deterministas requieren conocer de antemano el comportamiento de los procesos (raro); los heurísticos sirven cuando la carga es impredecible.
- **Centralizados vs distribuidos:** el centralizado reúne toda la información y decide mejor, pero se sobrecarga y es frágil; el distribuido necesita ordenar eventos. El material ilustra ambos con la **exclusión mutua** (nota 11): coordinador central frente a mensaje a todos con marcas de tiempo.
- Otras dimensiones habituales: óptimos vs subóptimos, locales vs globales, iniciados por emisor o receptor.

### Políticas (según el índice de la clase)
- **Transferencia:** cuándo un nodo debe enviar o aceptar trabajo (p. ej. umbral de carga: sobrecargado si cola > T alto, subcargado si < T bajo).
- **Selección:** qué proceso transferir (uno recién creado es barato de mover; uno largo compensa el costo).
- **Ubicación:** a qué nodo (sondeo aleatorio, sondeo de $k$ vecinos, difusión de ofertas).

## 3. Ejemplo resuelto: sondeo dirigido por el emisor
Umbral: un nodo con más de 4 procesos listos está sobrecargado. El nodo A (6 listos) sondea al azar a B (5), C (2). Política: acepta si cola < 3. B rechaza; C acepta. A transfiere un proceso nuevo a C (no migra uno en ejecución, evitando el costo de mover estado). Se limita a 3 sondeos por intento para no inundar la red; si ninguno acepta, ejecuta localmente.

## 4. Hilos
El modelo híbrido apoya en **hilos**: unidades de ejecución dentro de un proceso que comparten memoria; los hilos de usuario se multiplexan sobre hilos del núcleo. Mejoran el solapamiento de cálculo y E/S en servidores (por ejemplo un servidor con un hilo por petición). Ver [[Sistemas Operativos]].

## Errores comunes
- Migrar procesos sin considerar el costo de transferir su estado (memoria, descriptores, conexiones).
- Algoritmo con coordinador único en un SD que debe tolerar fallos.
- Suponer que todos los nodos ven la misma carga al mismo tiempo (información obsoleta).

## Ejercicios propuestos
1. Diferencie sondeo dirigido por emisor y por receptor. *R: el emisor busca ayuda cuando está cargado; el receptor anuncia disponibilidad cuando está ocioso. El primero conviene con carga baja, el segundo con carga alta.*
2. ¿Por qué falla el modelo de estaciones de trabajo en equilibrio de carga? *R: no reparte carga y desperdicia ciclos de las ociosas.*
3. ¿Cuál es el objetivo para procesos cooperantes? *R: minimizar tiempo de ejecución de la aplicación.*

## Conexiones
[[Sistemas Operativos]] (planificación, hilos), [[Sistemas Distribuidos - 11 Exclusión mutua y elección de líder]].

## Fuente
GerenciaProcesos.pdf (1404 palabras). Las políticas de transferencia/selección/ubicación aparecen en el índice del documento; su desarrollo aquí es conocimiento general.
