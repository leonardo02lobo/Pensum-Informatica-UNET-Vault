---
tags: [materia, semestre-IX]
semestre: IX
---
# Ingeniería de Software

**Semestre:** [[Semestre IX]] · [[Pensum Ingeniería Informática UNET]] · [[Fuentes Oficiales UNET]]

**Código oficial:** `425901` / `0426901` · **Unidades de crédito:** 3 UC · **Núcleo:** Ingeniería de la Información

## Prelaciones (cursar antes)
- [[Sistemas Distribuidos]]
- [[Sistema de Información II]]

## Desbloquea
- _Ninguna_

## Apuntes

### Descripción general y objetivos
La Ingeniería de Software aplica un enfoque sistemático, disciplinado y cuantificable al desarrollo, operación y mantenimiento del software (definición IEEE). La materia integra lo aprendido en [[Sistema de Información II]] (análisis y diseño de sistemas) y [[Sistemas Distribuidos]] (arquitecturas) para producir software de calidad dentro de plazo y presupuesto.

Objetivos típicos:
- Comprender el ciclo de vida del software y seleccionar un modelo de proceso adecuado.
- Elicitar, especificar y validar requisitos.
- Diseñar arquitecturas y componentes con UML y patrones.
- Planificar, estimar, probar y asegurar la calidad de un proyecto de software.

### Contenido programático (típico; verificar con el programa oficial)
**Unidad 1. Introducción y procesos de software.** Crisis del software, naturaleza del software, modelos de proceso: cascada, incremental, prototipado, espiral, Proceso Unificado (RUP) y métodos ágiles. Ver [[IS 01 - Ciclo de vida y modelos de proceso]].

**Unidad 2. Ingeniería de requisitos.** Requisitos funcionales y no funcionales, elicitación (entrevistas, cuestionarios, observación, historias de usuario), casos de uso, documento ERS (IEEE 830 / ISO 29148), validación y gestión de cambios, trazabilidad.

**Unidad 3. Modelado y diseño.** Análisis orientado a objetos, UML (casos de uso, clases, secuencia, actividades, estados, componentes, despliegue), principios SOLID, patrones de diseño, estilos arquitectónicos (capas, cliente-servidor, MVC, microservicios, orientada a eventos). Ver [[IS 04 - Modelado con UML]].

**Unidad 4. Construcción, pruebas y calidad.** Pruebas unitarias, de integración, de sistema y de aceptación; caja blanca y negra; TDD; métricas; revisiones e inspecciones; CMMI, ISO/IEC 25010, ISO 9001. Ver [[IS 08 - Pruebas de software]].

**Unidad 5. Gestión de proyectos de software.** Planificación, WBS, estimación (puntos de función, COCOMO II, planning poker), gestión de riesgos, configuración y versiones (Git), mantenimiento y evolución, DevOps/CI-CD.

### Conceptos clave
- Ciclo de vida (SDLC), artefacto, baseline, trazabilidad.
- Acoplamiento y cohesión; abstracción, encapsulamiento, modularidad.
- Deuda técnica, refactorización, código limpio.
- Verificación ("¿construimos bien el producto?") vs validación ("¿construimos el producto correcto?").

### Fórmulas y ejemplos
COCOMO básico (modo orgánico): esfuerzo en persona-mes y tiempo de desarrollo.

```
E = 2.4 * (KLOC)^1.05      # persona-mes
D = 2.5 * (E)^0.38         # meses
N = E / D                  # personas promedio
```

Complejidad ciclomática de McCabe: `V(G) = E - N + 2P` (aristas, nodos, componentes conexos), que da el número mínimo de casos de prueba de caja blanca por caminos independientes.

Patrón Strategy en Python:

```python
from abc import ABC, abstractmethod

class Descuento(ABC):
    @abstractmethod
    def aplicar(self, monto: float) -> float: ...

class SinDescuento(Descuento):
    def aplicar(self, monto): return monto

class Estudiante(Descuento):
    def aplicar(self, monto): return monto * 0.8

class Factura:
    def __init__(self, estrategia: Descuento): self.estrategia = estrategia
    def total(self, monto): return self.estrategia.aplicar(monto)
```

### Relación con otras materias
- [[Sistema de Información II]]: análisis y diseño de sistemas, casos de uso, diseño de BD.
- [[Sistemas Distribuidos]]: arquitecturas cliente-servidor, middleware y servicios.
- [[Base de Datos II]] y [[Base de Datos I]]: persistencia y modelado de datos.
- [[Programación II]] y [[Estructura de Datos]]: base de POO y estructuras.
- [[Metodología de la Investigación]], [[TAP Tesis]] y [[TAP Pasantía]]: aplicar el proceso de software al proyecto de grado.
- [[Gerencia de Proyectos]] (electiva): gestión formal con PMBOK.

### Evaluación y consejos
Suele evaluarse con parciales teóricos más un proyecto de desarrollo en equipo (ERS, diseño UML, implementación y pruebas) con exposición. Consejos: versionar todo desde el día uno, escribir requisitos verificables, no dejar las pruebas para el final y documentar decisiones de diseño.

### Bibliografía
- Sommerville, I. *Ingeniería de Software*. Pearson.
- Pressman, R. y Maxim, B. *Ingeniería del Software: un enfoque práctico*. McGraw-Hill.
- Larman, C. *UML y Patrones*. Pearson.
- Gamma, Helm, Johnson, Vlissides. *Design Patterns*. Addison-Wesley.
- Martin, R. *Clean Code* y *Clean Architecture*.
- Beck, K. *Extreme Programming Explained*; *Manifiesto Ágil* (agilemanifesto.org).

### Notas hijas
- [[IS 01 - Ciclo de vida y modelos de proceso]]
- [[IS 04 - Modelado con UML]]
- [[IS 08 - Pruebas de software]]

### Material
No hay carpeta Material/ en esta materia.
