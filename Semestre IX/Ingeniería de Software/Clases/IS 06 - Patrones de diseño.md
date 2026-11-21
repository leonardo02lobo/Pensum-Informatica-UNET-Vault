---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 06 - Patrones de diseño

Materia: [[Ingeniería de Software]]
Anterior: [[IS 05 - Principios de diseño y SOLID]]
Siguiente: [[IS 07 - Arquitectura de software]]

## Contexto y objetivo
Un **patrón de diseño** es una solución general y reutilizable a un problema recurrente de diseño en un contexto dado. Los 23 patrones del libro de la "Banda de los Cuatro" (GoF, 1994) se agrupan en creacionales, estructurales y de comportamiento. Objetivo: conocer los más usados, saber cuándo aplicarlos y verlos en código Python comentado.

## Anatomía de un patrón
Nombre, problema, contexto, solución (estructura y participantes), consecuencias (ventajas y costos). Un patrón no es una librería: se adapta.

## Creacionales (cómo crear objetos)

### Singleton
Garantiza una única instancia con punto de acceso global (configuración, pool de conexiones). Críticas: estado global, dificulta pruebas; preferible inyectar una instancia compartida.
```python
class Config:
    _instancia = None
    def __new__(cls):
        if cls._instancia is None:
            cls._instancia = super().__new__(cls)
            cls._instancia.valores = {}
        return cls._instancia

a, b = Config(), Config()
assert a is b           # misma instancia
```
(En entornos concurrentes se requiere sincronización.)

### Factory Method / Abstract Factory
Delega la creación a una fábrica para no acoplar al tipo concreto.
```python
class Notificacion: 
    def enviar(self, m): ...
class Correo(Notificacion):
    def enviar(self, m): print("Correo:", m)
class Sms(Notificacion):
    def enviar(self, m): print("SMS:", m)

def crear_notificacion(canal: str) -> Notificacion:
    return {"correo": Correo, "sms": Sms}[canal]()

crear_notificacion("sms").enviar("Hola")
```
**Abstract Factory** crea familias de objetos relacionados (p.ej. widgets de un tema visual).

### Builder
Construye objetos complejos paso a paso (consultas SQL, documentos). Evita constructores con 10 parámetros.

### Prototype
Clona un objeto existente (`copy.deepcopy`).

## Estructurales (cómo componer)

### Adapter
Convierte la interfaz de una clase en otra esperada por el cliente (integrar una API de terceros).
```python
class PagoLegacy:                 # API externa incompatible
    def hacer_cobro(self, cents): print("Cobro", cents)

class PagoAdapter:                # nuestra interfaz: pagar(monto_decimal)
    def __init__(self, legacy): self.legacy = legacy
    def pagar(self, monto): self.legacy.hacer_cobro(int(monto * 100))

PagoAdapter(PagoLegacy()).pagar(12.5)    # Cobro 1250
```

### Decorator
Añade responsabilidades dinámicamente envolviendo el objeto (alternativa a herencia). En Python, decoradores de función (`@cache`, `@login_required`) son el mismo espíritu.

### Facade
Interfaz simplificada a un subsistema complejo.

### Proxy
Sustituto que controla el acceso (virtual/lazy, protección, remoto, caché).

### Composite
Trata uniformemente objetos individuales y composiciones (árbol de carpetas/archivos, menús).

## De comportamiento (cómo interactúan)

### Strategy
Define una familia de algoritmos intercambiables (ver [[IS 05 - Principios de diseño y SOLID]]). Evita condicionales sobre el "tipo".

### Observer
Relación uno-a-muchos: cuando el sujeto cambia, notifica a sus observadores (eventos de UI, suscripciones, MVC, publicador/suscriptor).
```python
class Sujeto:
    def __init__(self): self._obs = []
    def suscribir(self, f): self._obs.append(f)
    def notificar(self, dato): [f(dato) for f in self._obs]

temperatura = Sujeto()
temperatura.suscribir(lambda t: print("Pantalla:", t))
temperatura.suscribir(lambda t: print("Alarma!" if t > 40 else "ok"))
temperatura.notificar(45)
```

### Command
Encapsula una petición como objeto (deshacer/rehacer, colas de trabajo, macros).

### State
El objeto cambia su comportamiento según su estado interno; sustituye `if estado == ...` por clases-estado (ver diagrama de estados en [[IS 04 - Modelado con UML]]).

### Template Method
El algoritmo se define en una clase base con pasos que las subclases redefinen.

### Iterator, Chain of Responsibility, Mediator, Memento, Visitor
- Iterator: recorrer sin exponer la estructura (en Python, `__iter__`/`__next__`).
- Chain of Responsibility: cadena de manejadores (middleware web).
- Mediator: centraliza la comunicación entre objetos.
- Memento: guarda/restaura estado.
- Visitor: añade operaciones a una jerarquía sin modificarla.

## Patrones arquitectónicos y de aplicación (no GoF)
MVC/MVP/MVVM, Repository, Unit of Work, DAO, Data Mapper vs Active Record, Dependency Injection, CQRS, Event Sourcing, Circuit Breaker, Saga (microservicios). Ver [[IS 07 - Arquitectura de software]].

## Cómo elegir
1. Describe el **problema** y la fuerza de cambio (¿qué variará?).
2. Busca el patrón cuyo *Intent* coincide.
3. Valida que el costo (clases adicionales) se justifique.
4. Nómbralo en el código/documentación para comunicarse con el equipo.
Regla: **encapsula lo que varía**.

## Ejemplo resuelto: notificaciones con Strategy + Observer + Factory
Problema: al registrar un préstamo vencido deben avisar por correo, SMS o ambos, según preferencia.
1. *Observer*: el evento `PrestamoVencido` notifica a una lista de manejadores.
2. *Factory*: `crear_notificacion(canal)` instancia el canal.
3. *Strategy*: cada canal implementa `enviar`.
4. Código: 
```python
evento = Sujeto()
for canal in usuario.canales:          # ["correo", "sms"]
    n = crear_notificacion(canal)
    evento.suscribir(lambda msg, n=n: n.enviar(msg))
evento.notificar("Su préstamo está vencido")
```
5. Añadir WhatsApp implica una clase nueva y una entrada en la fábrica; nada más cambia (OCP).

## Antipatrones
God Object, Spaghetti code, Golden hammer (usar la misma herramienta para todo), Copy-paste programming, *Lava flow* (código muerto que nadie borra), Singleton abusivo.

## Errores comunes
- "Patrón-itis": aplicar patrones sin problema que los justifique.
- Confundir Factory con Abstract Factory, o Decorator con Proxy (el decorador añade comportamiento; el proxy controla acceso).
- Implementar Singleton no seguro en hilos.
- Copiar la estructura de Java a Python sin aprovechar funciones de primera clase (Strategy puede ser una función).

## Ejercicios propuestos
1. Necesitas deshacer en un editor: ¿qué patrón? *Resp.: Command (y Memento).*
2. Debes integrar un proveedor con API distinta: ¿patrón? *Resp.: Adapter.*
3. Un menú contiene opciones y submenús recursivos: ¿patrón? *Resp.: Composite.*

## Conexiones
[[Programación II]], [[Estructura de Datos]] (Iterator, Composite), [[Sistemas Distribuidos]] (Proxy remoto, Circuit Breaker), [[IS 04 - Modelado con UML]].

## Fuente
Conocimiento general. Gamma, Helm, Johnson, Vlissides, *Design Patterns*; Freeman, *Head First Design Patterns*.
