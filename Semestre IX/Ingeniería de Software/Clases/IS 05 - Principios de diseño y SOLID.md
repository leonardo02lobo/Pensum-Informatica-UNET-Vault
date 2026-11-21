---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 05 - Principios de diseño y SOLID

Materia: [[Ingeniería de Software]]
Anterior: [[IS 04 - Modelado con UML]]
Siguiente: [[IS 06 - Patrones de diseño]]

## Contexto y objetivo
Un buen diseño hace que el software sea fácil de cambiar. Los principios de diseño son heurísticas que orientan cómo dividir responsabilidades. Objetivo: entender cohesión/acoplamiento, aplicar los cinco principios SOLID con ejemplos de código antes/después y reconocer *code smells* que señalan violaciones.

## Conceptos fundamentales
- **Abstracción**: ocultar detalles irrelevantes y exponer lo esencial.
- **Encapsulamiento**: ocultar el estado interno tras una interfaz.
- **Modularidad**: dividir en módulos con interfaces claras.
- **Cohesión**: grado en que los elementos de un módulo pertenecen juntos (**alta es deseable**). Tipos de menor a mayor: coincidental, lógica, temporal, procedimental, comunicacional, secuencial, funcional.
- **Acoplamiento**: grado de dependencia entre módulos (**bajo es deseable**). De mayor a menor: por contenido, común (globales), de control, de sello (stamp), de datos, de mensajes.
- **Ley de Demeter**: un objeto solo debe hablar con sus "amigos inmediatos" (evitar `a.getB().getC().hacer()`).
- **DRY** (Don't Repeat Yourself), **KISS**, **YAGNI** (You Aren't Gonna Need It).
- **Composición sobre herencia**.

## Los principios SOLID (Robert C. Martin)

### S - Single Responsibility (Responsabilidad Única)
Una clase debe tener **una sola razón para cambiar**. 
Violación:
```python
class Informe:
    def calcular_totales(self): ...
    def guardar_en_bd(self): ...      # persistencia
    def imprimir_pdf(self): ...       # presentación
```
Cambian por razones distintas (reglas de negocio, BD, formato). Refactor: `Informe` (dominio), `InformeRepositorio`, `InformePdfRenderer`.

### O - Open/Closed (Abierto/Cerrado)
Abierto para extensión, cerrado para modificación. 
Violación: un `if tipo == "tarjeta" ... elif tipo == "paypal"` que crece cada vez que se añade un medio de pago. 
Refactor con polimorfismo:
```python
from abc import ABC, abstractmethod

class MedioPago(ABC):
    @abstractmethod
    def pagar(self, monto: float) -> bool: ...

class Tarjeta(MedioPago):
    def pagar(self, monto): print(f"Cobrando {monto} con tarjeta"); return True

class Transferencia(MedioPago):
    def pagar(self, monto): print(f"Esperando transferencia de {monto}"); return True

def checkout(medio: MedioPago, monto: float):
    return medio.pagar(monto)   # no cambia al añadir nuevos medios
```

### L - Liskov Substitution
Los objetos de una subclase deben poder sustituir a los de la superclase sin alterar la corrección del programa. 
Violación clásica: `Cuadrado` hereda de `Rectangulo`; `setAncho` en un cuadrado cambia también el alto y rompe el contrato de `Rectangulo` (ancho y alto independientes). Señales: subclases que lanzan `NotImplementedError`, que fortalecen precondiciones o debilitan postcondiciones. Solución: no usar herencia, o definir una jerarquía común `Figura` con `area()`.

### I - Interface Segregation
Muchas interfaces específicas son mejores que una general; ningún cliente debe depender de métodos que no usa.
```python
class Trabajador(ABC):
    @abstractmethod
    def trabajar(self): ...
    @abstractmethod
    def comer(self): ...        # un Robot no come
```
Refactor: `Trabajable` y `Alimentable` por separado.

### D - Dependency Inversion
Los módulos de alto nivel no deben depender de los de bajo nivel; ambos dependen de abstracciones. Las abstracciones no dependen de detalles.
```python
class NotificadorCorreo:
    def enviar(self, msg): ...

class ServicioPedidos:           # alto nivel
    def __init__(self, notificador):   # inyección de dependencias
        self.notificador = notificador
    def confirmar(self, pedido):
        self.notificador.enviar(f"Pedido {pedido} confirmado")

# En pruebas se inyecta un doble (mock) sin enviar correos reales.
```
**Inyección de dependencias** (por constructor, setter o contenedor/framework como Spring) es una técnica para lograr DIP; **Inversión de control** es el concepto más amplio.

## GRASP (Larman)
Patrones de asignación de responsabilidades: Experto en información, Creador, Controlador, Bajo acoplamiento, Alta cohesión, Polimorfismo, Fabricación pura, Indirección, Variaciones protegidas.

## Code smells y refactorización
Olores frecuentes: método largo, clase gigante (God object), lista larga de parámetros, código duplicado, *shotgun surgery* (un cambio toca muchas clases), *feature envy*, comentarios que explican código confuso, *switch* repetidos.
Refactorizaciones del catálogo de Fowler: Extraer método, Extraer clase, Mover método, Reemplazar condicional con polimorfismo, Introducir objeto parámetro. Regla: **refactoriza solo con pruebas que pasen antes y después**.

## Ejemplo resuelto: refactorizar un descuento
Código inicial:
```python
def total(pedido):
    t = sum(l.precio * l.cant for l in pedido.lineas)
    if pedido.cliente.tipo == "vip":      t *= 0.8
    elif pedido.cliente.tipo == "estudiante": t *= 0.9
    return t
```
Problemas: viola OCP (nuevo tipo = editar función) y mezcla cálculo con política.
Pasos:
1. Escribe pruebas de caracterización: vip 100 -> 80; estudiante 100 -> 90; normal 100 -> 100.
2. Extrae interfaz `PoliticaDescuento` con `aplicar(monto)`.
3. Crea `Vip`, `Estudiante`, `Normal`.
4. `Cliente` recibe su política (composición).
5. `total` queda: `monto = subtotal; return pedido.cliente.politica.aplicar(monto)`.
6. Ejecuta las pruebas: siguen pasando; añadir "empleado" ya no modifica `total`. (Este es el patrón Strategy: ver [[IS 06 - Patrones de diseño]]).

## Errores comunes
- Aplicar SOLID dogmáticamente y crear 20 clases para un `if` (sobreingeniería).
- Confundir DIP con inyección de dependencias.
- Herencia para reutilizar código en lugar de modelar "es-un".
- Interfaces con un solo implementador sin razón (abstracción prematura).

## Ejercicios propuestos
1. Una clase `Usuario` valida, guarda en BD y envía correo. ¿Qué principio viola? *Resp.: SRP.*
2. `Pinguino` hereda de `Ave` con `volar()`. ¿Qué principio? *Resp.: LSP; separar `AveVoladora`.*
3. Tu servicio instancia `new MySQLRepo()` dentro del constructor. ¿Problema y solución? *Resp.: viola DIP y dificulta pruebas; inyectar una interfaz `Repositorio`.*

## Conexiones
[[Programación II]] (POO), [[IS 06 - Patrones de diseño]], [[IS 07 - Arquitectura de software]], [[IS 08 - Pruebas de software]] (diseño testeable).

## Fuente
Conocimiento general. Martin, *Clean Code*, *Clean Architecture*; Fowler, *Refactoring*; Larman, *UML y Patrones*.
