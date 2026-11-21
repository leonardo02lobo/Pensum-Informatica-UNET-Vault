---
tags: [clase, electiva]
materia: Introducción a la Inteligencia Artificial
fuente: "conocimiento general"
---
# IIA 01 - Agentes racionales y entornos

Materia: [[Introducción a la Inteligencia Artificial]]
Anterior: (inicio de la serie)
Siguiente: [[IIA 02 - Búsqueda no informada e informada]]

## Contexto y objetivo
La IA moderna se organiza alrededor del concepto de **agente**: algo que percibe su entorno mediante sensores y actúa sobre él mediante actuadores. Esta clase da un marco común (Russell y Norvig) para todo el curso. Objetivo: describir un problema con el esquema REAS, clasificar entornos y programar agentes simples.

## Breve historia
- 1943 McCulloch y Pitts (neuronas); 1950 Turing y su prueba de imitación; 1956 taller de Dartmouth, donde nace el término "inteligencia artificial".
- 1960s-70s: razonamiento simbólico, primeros sistemas expertos; primer "invierno de la IA" por promesas incumplidas.
- 1980s: sistemas expertos comerciales; retropropagación. Segundo invierno.
- 1990s-2000s: enfoque probabilístico y estadístico, aprendizaje automático.
- 2010s en adelante: aprendizaje profundo, grandes datos y GPU; modelos generativos y de lenguaje.

Cuatro enfoques clásicos: pensar o actuar, de forma humana o racional. Este curso se centra en **actuar racionalmente**.

## Agente racional
Un agente implementa una **función de agente** que mapea la historia de percepciones a acciones. Un agente es **racional** si, para cada secuencia de percepciones, elige la acción que maximiza el valor esperado de la **medida de desempeño**, dado lo que ha percibido y su conocimiento previo. Racional no es omnisciente ni perfecto: maximiza lo esperado, no lo real.

**Descripción REAS** (o PEAS): Rendimiento, Entorno, Actuadores, Sensores.

| | Taxi autónomo | Aspiradora robot |
|---|---|---|
| Rendimiento | seguridad, tiempo, costo | limpieza, energía |
| Entorno | calles, peatones, tráfico | habitaciones, obstáculos |
| Actuadores | volante, acelerador, freno | ruedas, aspirador |
| Sensores | cámaras, GPS, lidar | sensor de suciedad, choque |

## Propiedades de los entornos
- **Observable** (totalmente) o parcialmente observable.
- **Determinista** o estocástico (si hay incertidumbre en el efecto de las acciones); estratégico si depende de otros agentes.
- **Episódico** o secuencial (las decisiones afectan el futuro).
- **Estático** o dinámico (cambia mientras el agente delibera); semidinámico si cambia el puntaje.
- **Discreto** o continuo.
- **Un agente** o multiagente (cooperativo/competitivo).

Ajedrez: observable, determinista (estratégico), secuencial, semidinámico, discreto, multiagente. Taxi: parcialmente observable, estocástico, secuencial, dinámico, continuo, multiagente. El caso más difícil es el de este último.

## Tipos de agentes
1. **Reactivo simple:** reglas condición-acción sobre la percepción actual; solo funciona si el entorno es totalmente observable.
2. **Reactivo basado en modelo:** mantiene un estado interno (modelo de cómo evoluciona el mundo).
3. **Basado en objetivos:** elige acciones que lleven a una meta (búsqueda y planificación).
4. **Basado en utilidad:** maximiza una función de utilidad cuando hay metas en conflicto o incertidumbre.
5. **Agente que aprende:** elemento de aprendizaje, crítico, generador de problemas y elemento de desempeño.

## Ejemplo resuelto: aspiradora de dos casillas
Mundo con casillas A y B, cada una limpia o sucia. Percepción: (posición, estado). Acciones: Izquierda, Derecha, Aspirar. Medida: +1 por casilla limpia por paso de tiempo.

Agente reactivo simple: si está sucia, aspirar; si no, ir a la otra casilla.
1. Inicio en A, ambas sucias: percibe (A, sucia) y aspira.
2. Percibe (A, limpia), va a B.
3. Percibe (B, sucia) y aspira.
4. Con ambas limpias oscila entre A y B, perdiendo energía; un agente con modelo (recuerda que todo está limpio) podría detenerse, y uno basado en utilidad ponderaría el costo de moverse.

## Código
```python
import random

class Aspiradora:
    """Agente reactivo simple."""
    def programa(self, percepcion):
        pos, estado = percepcion
        if estado == "sucia":
            return "aspirar"
        return "derecha" if pos == "A" else "izquierda"

class Entorno:
    def __init__(self):
        self.estado = {"A": random.choice(["sucia", "limpia"]),
                       "B": random.choice(["sucia", "limpia"])}
        self.pos = "A"
        self.puntaje = 0

    def percibir(self):
        return (self.pos, self.estado[self.pos])

    def ejecutar(self, accion):
        if accion == "aspirar":
            self.estado[self.pos] = "limpia"
        elif accion == "derecha":
            self.pos = "B"
        elif accion == "izquierda":
            self.pos = "A"
        # medida de desempeño: casillas limpias por paso
        self.puntaje += sum(1 for v in self.estado.values() if v == "limpia")

agente, mundo = Aspiradora(), Entorno()
for t in range(10):
    mundo.ejecutar(agente.programa(mundo.percibir()))
print("puntaje:", mundo.puntaje, mundo.estado)
```

## Errores comunes
- Confundir racionalidad con perfección u omnisciencia.
- Definir la medida de desempeño según lo que el agente "debería hacer" y no el estado deseado del entorno.
- Clasificar mal el entorno (p. ej. suponer determinista uno estocástico).
- Usar un agente reactivo simple en un entorno parcialmente observable.

## Ejercicios propuestos
1. Describe con REAS un termostato inteligente. *Respuesta: rendimiento = confort y ahorro; entorno = casa; actuadores = calefactor/enfriador; sensores = temperatura, presencia.*
2. Clasifica el póker. *Respuesta: parcialmente observable, estocástico, secuencial, estático, discreto, multiagente.*
3. ¿Qué tipo de agente es un filtro de spam que se actualiza con la retroalimentación del usuario? *Respuesta: agente que aprende.*

## Conexiones
- Estructuras (colas, grafos) para implementar agentes: [[Estructura de Datos]].
- Lógica base: [[Matemática Discreta]].
- Control y retroalimentación: [[Automatización]].
- Agentes que aprenden: [[AA 01 - Fundamentos del aprendizaje automático]].

## Fuente
Conocimiento general (Russell y Norvig, *Inteligencia Artificial: un enfoque moderno*, caps. 1-2). Verificar el temario con el programa oficial.
