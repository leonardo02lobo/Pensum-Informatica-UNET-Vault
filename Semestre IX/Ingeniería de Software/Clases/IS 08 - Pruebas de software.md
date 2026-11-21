---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 08 - Pruebas de software

Materia: [[Ingeniería de Software]]
Anterior: [[IS 07 - Arquitectura de software]]
Siguiente: [[IS 09 - Calidad y métricas de software]]

## Contexto y objetivo
Probar es ejecutar el software con la intención de encontrar defectos y evaluar si cumple los requisitos. Dijkstra: "las pruebas muestran la presencia de errores, nunca su ausencia". Esta clase profundiza lo resumido en Pruebas y calidad de software: niveles, técnicas de diseño de casos, TDD y automatización, con ejemplos resueltos.

## Terminología (ISTQB)
- **Error** (equivocación humana) lleva a **defecto/falta** (bug en el código) que puede causar un **fallo** (comportamiento incorrecto en ejecución).
- **Verificación**: ¿construimos bien el producto? **Validación**: ¿construimos el producto correcto?
- **Caso de prueba**: entradas + precondiciones + resultado esperado. **Oráculo**: mecanismo para decidir si el resultado es correcto.
- **Cobertura**: porcentaje de elementos (sentencias, ramas, caminos, requisitos) ejercitados.
- Siete principios ISTQB: las pruebas demuestran presencia de defectos; las pruebas exhaustivas son imposibles; pruebas tempranas; agrupamiento de defectos; paradoja del pesticida (los mismos tests dejan de encontrar bugs); dependen del contexto; falacia de ausencia de errores.

## Niveles de prueba
1. **Unitarias**: un módulo/función/clase aislado (JUnit, pytest). Rápidas, automatizadas.
2. **De integración**: interacción entre módulos (descendente, ascendente, "big bang"; uso de stubs/drivers).
3. **De sistema**: el sistema completo contra los requisitos (funcionales y no funcionales).
4. **De aceptación (UAT)**: el cliente valida (alfa, beta).
Tipos transversales: **regresión** (tras cambios), **humo** (smoke: ¿arranca y funciona lo básico?), **exploratorias**, **rendimiento/carga/estrés**, **seguridad** (OWASP), **usabilidad**, **compatibilidad**.

**Pirámide de pruebas** (Cohn): muchas unitarias, algunas de integración/servicio, pocas E2E por UI (lentas y frágiles). Anti-patrón: "cono de helado".

## Pruebas de caja negra (sin ver el código)

### Partición de equivalencia
Divide el dominio de entrada en clases donde el sistema se comporta igual; una prueba por clase.
### Análisis de valores límite
Los errores abundan en los bordes: prueba mín-1, mín, mín+1, máx-1, máx, máx+1.

**Ejemplo resuelto.** Campo "edad" acepta enteros de 18 a 65.
- Clases: inválida baja (menor que 18), válida (18-65), inválida alta (mayor que 65), no numérica.
- Valores límite: 17, 18, 19, 64, 65, 66.
- Casos: 17 -> rechaza; 18 -> acepta; 19 -> acepta; 64 -> acepta; 65 -> acepta; 66 -> rechaza; "abc" -> error de formato; vacío -> error. Total: 8 casos con alta cobertura de riesgo.

### Tabla de decisión
Combina condiciones y acciones. Ejemplo descuento: (cliente VIP, compra mayor a 100): VIP y mayor: 20%; VIP y no mayor: 10%; no VIP y mayor: 5%; ninguno: 0%. 4 reglas, 4 casos.

### Transición de estados, grafos causa-efecto, pairwise (combinatoria de parámetros con herramientas como PICT).

## Pruebas de caja blanca (con el código)
Cobertura de **sentencias** (todas las líneas), **ramas/decisiones** (cada if en V y F), **condiciones** y **condición/decisión modificada (MC/DC, obligatoria en aviónica)**, **caminos**.

**Complejidad ciclomática de McCabe**: $V(G) = E - N + 2P$, o bien número de decisiones + 1. Es el número de caminos linealmente independientes, es decir, el mínimo de casos para cobertura de ramas.

**Ejemplo.**
```python
def categoria(nota):
    if nota < 0 or nota > 20:       # decisión 1 (con 2 condiciones)
        return "invalida"
    if nota >= 10:                  # decisión 2
        return "aprobado"
    return "reprobado"
```
Decisiones = 2 (contando la compuesta como una), $V(G) = 3$ (con condiciones simples serían 3 decisiones y V = 4). Casos de ramas: nota=-1 (invalida), nota=15 (aprobado), nota=5 (reprobado). Para cobertura de condición añadir nota=25 para probar la segunda condición del `or`.

## Pruebas unitarias con pytest
```python
# archivo: descuento.py
def aplicar_descuento(monto, tipo):
    if monto < 0:
        raise ValueError("monto negativo")
    tasas = {"normal": 0.0, "estudiante": 0.10, "vip": 0.20}
    return round(monto * (1 - tasas[tipo]), 2)

# archivo: test_descuento.py
import pytest
from descuento import aplicar_descuento

@pytest.mark.parametrize("monto,tipo,esperado", [
    (100, "normal", 100.0),
    (100, "estudiante", 90.0),
    (100, "vip", 80.0),
    (0, "vip", 0.0),                  # valor límite
])
def test_descuentos(monto, tipo, esperado):
    assert aplicar_descuento(monto, tipo) == esperado

def test_monto_negativo():
    with pytest.raises(ValueError):
        aplicar_descuento(-1, "normal")

def test_tipo_desconocido():
    with pytest.raises(KeyError):
        aplicar_descuento(10, "otro")
```
Ejecuta `pytest -q --cov=descuento` (con pytest-cov) para ver cobertura.

## Dobles de prueba
**Dummy** (relleno), **Stub** (respuestas enlatadas), **Spy** (registra llamadas), **Mock** (verifica interacciones esperadas), **Fake** (implementación simple, como BD en memoria).
```python
from unittest.mock import Mock
def test_notifica_al_vencer():
    notificador = Mock()
    servicio = ServicioPrestamos(notificador)    # DIP: se inyecta
    servicio.marcar_vencido(prestamo_vencido)
    notificador.enviar.assert_called_once()
```

## TDD (Test-Driven Development)
Ciclo **Rojo, Verde, Refactor**: 1) escribe un test que falla; 2) escribe el mínimo código para pasarlo; 3) refactoriza manteniendo verde. Beneficios: diseño testeable, red de seguridad. **BDD** extiende con lenguaje de negocio (Gherkin; ver [[IS 03 - Casos de uso e historias de usuario]]).

## Pruebas de rendimiento y seguridad
- Carga (usuarios esperados), estrés (más allá del límite), resistencia (soak), picos (spike). Herramientas: JMeter, k6, Locust. Métricas: latencia p95/p99, throughput, tasa de error.
- Seguridad: análisis estático (SAST), dinámico (DAST), pruebas de penetración, OWASP Top 10.

## Gestión de defectos
Ciclo: nuevo, asignado, corregido, verificado, cerrado (o reabierto). Un buen reporte tiene título claro, pasos para reproducir, resultado esperado vs obtenido, entorno, severidad (impacto técnico) y prioridad (urgencia de negocio). Métrica útil: densidad de defectos = defectos/KLOC.

## Errores comunes
- Probar solo el "camino feliz".
- Tests acoplados a la implementación (se rompen al refactorizar).
- Tests que dependen del orden o de datos compartidos.
- Perseguir 100% de cobertura como fin y no como indicador.
- Dejar las pruebas para el final del proyecto.

## Ejercicios propuestos
1. Valores límite para "cantidad de 1 a 100 unidades". *Resp.: 0, 1, 2, 99, 100, 101.*
2. Calcula $V(G)$ de un grafo con 9 aristas, 8 nodos y 1 componente. *Resp.: 9-8+2 = 3.*
3. ¿Diferencia entre mock y stub? *Resp.: el stub devuelve datos fijos; el mock además verifica que se hicieron ciertas llamadas.*

## Conexiones
Pruebas y calidad de software, [[Estadística II]] (estimación de confiabilidad y pruebas de hipótesis sobre defectos), [[IS 11 - Gestión de configuración y DevOps]] (CI), [[Programación II]].

## Fuente
Conocimiento general. ISTQB Foundation Level; Myers, *The Art of Software Testing*; Beck, *Test-Driven Development by Example*; McCabe (1976).
