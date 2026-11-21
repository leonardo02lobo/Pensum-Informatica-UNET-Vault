---
tags: [clase, semestre-VIII]
materia: Simulación de Sistemas
---
# Simulación de Sistemas - Simulación de Eventos Discretos y Lista de Eventos Futuros

Materia: [[Simulación de Sistemas]]
Anterior: [[Simulación de Sistemas - Generación de Variables Aleatorias]]
Siguiente: [[Simulación de Sistemas - Simulación Montecarlo y Modelado Formal]]

## Contexto y objetivo
Comprender la arquitectura interna de un simulador de **eventos discretos (DES)** basado en reloj asíncrono de próximo evento y **Lista de Eventos Futuros (LEF)**, implementando un sistema de colas $M/M/1$ en Python con colas de prioridad (`heapq`).

## 1. Enfoques de avance del tiempo y eventos discretos
En una simulación de eventos discretos, el estado del sistema **permanece constante** entre dos eventos consecutivos. Existen dos formas de avanzar el reloj de simulación $t$:
- **Incremento fijo de tiempo ($\Delta t$)**: el reloj avanza en pasos iguales; ineficiente si hay períodos sin actividad o impreciso si ocurren múltiples eventos en un mismo $\Delta t$.
- **Avance al próximo evento (reloj asíncrono)**: el reloj salta directamente al instante $t^*$ del evento más próximo registrado en la **Lista de Eventos Futuros (LEF)**. Es el estándar en DES.

### Enfoques de modelado
1. **Orientado a eventos**: se define una rutina por cada tipo de evento (llegada, salida, fin de turno) que actualiza el estado y programa nuevos eventos en la LEF.
2. **Orientado a procesos**: describe el ciclo de vida completo de una entidad (p. ej., `SimPy` con generadores `yield`).
3. **Barrido de actividades**: evalúa condiciones en cada paso de tiempo.

## 2. Componentes de un simulador orientado a eventos
- **Estado del sistema**: variables mínimas necesarias para describir el sistema en $t$ (p. ej., `cola`, `servidor_ocupado`).
- **Reloj de simulación**: variable global `reloj` con el tiempo actual.
- **Lista de Eventos Futuros (LEF)**: cola de prioridad ordenada por tiempo de ocurrencia `(tiempo, tipo_evento, datos)`. En [[Estructura de Datos]] se implementa eficientemente con un **min-heap** ($O(\log n)$ por inserción/extracción).
- **Contadores estadísticos**: acumuladores para métricas (clientes atendidos, área bajo la curva de longitud de cola $\int Q(t)\,dt$, tiempo ocupado del servidor).
- **Rutina principal (motor)**: inicializa $\to$ extrae el próximo evento de la LEF $\to$ avanza el reloj $\to$ actualiza estadísticas integrales $\to$ ejecuta la rutina del evento $\to$ repite hasta condición de parada.

## 3. Implementación de una cola $M/M/1$ con LEF en Python
Sistema con llegadas Poisson a tasa $\lambda = 8\text{ cli/h}$ y servicio exponencial a tasa $\mu = 10\text{ cli/h}$:

```python
import heapq, random

def simular_mm1(lam=8.0, mu=10.0, t_max=1000.0, semilla=42):
    random.seed(semilla)
    reloj = 0.0
    cola = 0
    ocupado = False
    area_cola = 0.0
    area_ocupado = 0.0
    atendidos = 0

    lef = [(random.expovariate(lam), "llegada")]

    while lef:
        t_ev, ev = heapq.heappop(lef)
        if t_ev > t_max:
            break
        dt = t_ev - reloj
        area_cola += cola * dt
        area_ocupado += (1.0 if ocupado else 0.0) * dt
        reloj = t_ev

        if ev == "llegada":
            heapq.heappush(lef, (reloj + random.expovariate(lam), "llegada"))
            if ocupado:
                cola += 1
            else:
                ocupado = True
                heapq.heappush(lef, (reloj + random.expovariate(mu), "salida"))
        elif ev == "salida":
            atendidos += 1
            if cola > 0:
                cola -= 1
                heapq.heappush(lef, (reloj + random.expovariate(mu), "salida"))
            else:
                ocupado = False

    return {
        "Lq_sim": area_cola / reloj,
        "rho_sim": area_ocupado / reloj,
        "atendidos": atendidos,
    }
```

Validación analítica ([[Investigación de Operaciones II]]): para $\lambda = 8, \mu = 10$, $\rho = \lambda/\mu = 0{,}80$ y $L_q = \frac{\rho^2}{1-\rho} = \frac{0{,}64}{0{,}20} = 3{,}20$ clientes en cola.

## 4. Aplicación en el proyecto del curso
En [[Age of Conquest Simulación de Eventos Discretos]], el reloj se representa como `turno.fase` (recaudación, planificación, movimiento, combate, fin), de modo que la LEF ordena los eventos dentro de cada turno y programa eventos de turnos posteriores.

## Errores comunes
- Olvidar actualizar las estadísticas ponderadas por tiempo (`area_cola += cola * dt`) **antes** de modificar el estado (`cola += 1`) al llegar un evento.
- No programar la *siguiente llegada* dentro de la rutina del evento `"llegada"`, deteniendo el flujo de entidades al primer cliente.
- Empates de tiempo en la LEF: si dos eventos ocurren exactamente en el mismo instante, usar un entero de desempate o prioridad explícita en la tupla `(tiempo, prioridad, evento)`.

## Ejercicios propuestos
1. En el código de la cola $M/M/1$, ¿qué ocurre si $\lambda = 12$ y $\mu = 10$ ($\rho > 1$)?
   - *Respuesta*: el sistema es inestable; la cola crece indefinidamente con el tiempo y `Lq_sim` aumenta sin converger a un valor estacionario.
2. Trace manualmente los primeros 3 eventos de la LEF si la primera llegada ocurre en $t=2$, la segunda en $t=5$, y los tiempos de servicio son $S_1 = 4$ y $S_2 = 2$.
   - *Respuesta*: $t=2$ (llegada 1, servidor ocupado, programa salida 1 en $t=6$); $t=5$ (llegada 2, entra a cola=1); $t=6$ (salida 1, toma a cliente 2 de cola=0, programa salida 2 en $t=8$).

## Conexiones
- Estructuras de datos heap/cola de prioridad en [[Estructura de Datos]] y [[Programación II]].
- Teoría de colas analítica para validar resultados en [[Investigación de Operaciones II]].
- Implementación del juego por turnos en [[Age of Conquest Simulación de Eventos Discretos]].

## Fuente
Basado en [[Simulación de Sistemas]] (Banks et al., *Discrete-Event System Simulation*; proyecto `Age of Conquest - Clon/`).
