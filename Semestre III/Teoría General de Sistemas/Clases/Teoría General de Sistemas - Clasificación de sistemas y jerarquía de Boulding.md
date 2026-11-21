---
tags: [clase, semestre-III]
materia: Teoría General de Sistemas
---
# Teoría General de Sistemas - Clasificación de sistemas y jerarquía de Boulding

Materia: [[Teoría General de Sistemas]]
Anterior: [[Teoría General de Sistemas - Carácter dinámico, homeostasis y sinergia]]
Siguiente: [[Teoría General de Sistemas - Origen, evolución y enfoques de la TGS]]

## Contexto y objetivo

No todos los sistemas tienen la misma naturaleza ni el mismo nivel de complejidad. Esta clase cierra la **Unidad I** presentando los criterios de **clasificación de sistemas**, la **jerarquía de complejidad de Kenneth Boulding** (1956) y las técnicas de **agregación y disgregación** para analizar sistemas complejos.

## 1. Criterios de clasificación de sistemas

Un mismo sistema puede clasificarse simultáneamente según varios criterios:

| Criterio | Categorías | Definición y ejemplo |
| :--- | :--- | :--- |
| **Naturaleza** | **Físicos (concretos)** vs. **Abstractos (conceptuales)** | Físicos: compuestos por objetos tangibles (una computadora, un puente). Abstractos: compuestos por conceptos, planes o símbolos (un lenguaje de programación, una teoría matemática). |
| **Interacción con el entorno** | **Abiertos** vs. **Cerrados** | Abiertos: intercambian materia, energía o información con el entorno (una empresa, una célula). Cerrados: no intercambian nada con su entorno (modelo ideal en termodinámica; un termo perfecto). |
| **Origen** | **Naturales** vs. **Artificiales** | Naturales: existen sin intervención humana (ecosistema, sistema solar). Artificiales: diseñados por el ser humano (red de telecomunicaciones, ERP). |
| **Variable temporal** | **Discretos**, **Continuos** e **Híbridos** | Discretos: cambian de estado en instantes específicos (cola de banco, autómata finito). Continuos: cambian de forma ininterrumpida en el tiempo (flujo hidráulico, temperatura). Híbridos: combinan ambos (PLC con sensores analógicos y lógica digital). |
| **Control** | **Neutrales** vs. **Controlados** | Neutrales: no poseen mecanismo de autorregulación hacia una meta. Controlados: ajustan su comportamiento mediante retroalimentación. |
| **Previsibilidad** | **Determinísticos** vs. **Probabilísticos (estocásticos)** | Determinísticos: dada una entrada y un estado, la salida es única y predecible (máquina de Turing determinista). Probabilísticos: sus salidas están sujetas a incertidumbre y distribuciones de probabilidad (tráfico de red, clima). |

## 2. Jerarquía de los sistemas según Kenneth Boulding

En 1956, el economista Kenneth Boulding propuso una escala de nueve niveles de complejidad creciente para ordenar los sistemas del universo. Cada nivel incorpora las propiedades de los niveles anteriores y añade nuevas capacidades emergentes:

1. **Nivel 1 — Estructuras estáticas (marcos de referencia):** anatomía del universo, mapas, estructura cristalina, esquema de una base de datos en reposo.
2. **Nivel 2 — Sistemas dinámicos simples (relojería):** movimientos predeterminados y leyes mecánicas exactas (reloj mecánico, sistema solar clásico).
3. **Nivel 3 — Sistemas cibernéticos o de control (termostato):** capaces de autorregularse mediante retroalimentación negativa para mantener un equilibrio.
4. **Nivel 4 — Sistemas abiertos o autoestructurados (célula):** primer nivel con vida; intercambian materia y energía con el entorno para conservar su organización y reproducirse.
5. **Nivel 5 — Sistemas genético-sociales (planta):** división del trabajo entre partes diferenciadas (raíz, tallo, hojas) y crecimiento programado genéticamente, pero sin conciencia.
6. **Nivel 6 — Sistemas animales:** movilidad, comportamiento teleológico (dirigido a fines), receptores especializados (ojos, oídos) y procesamiento de información nerviosa.
7. **Nivel 7 — Sistemas humanos:** autoconciencia, lenguaje simbólico, capacidad de reflexión sobre el pasado y proyección del futuro.
8. **Nivel 8 — Organizaciones sociales:** empresas, universidades, Estados; sistemas complejos formados por individuos que comparten roles, cultura y comunicación.
9. **Nivel 9 — Sistemas trascendentales:** lo absoluto, lo metafísico y los interrogantes últimos más allá del conocimiento empírico actual.

> **Importancia práctica:** Boulding señaló que la ciencia suele dominar bien los niveles 1 al 3, pero los problemas más difíciles de la ingeniería, la economía y la informática residen en los niveles 7 y 8 (sistemas socio-técnicos).

## 3. Análisis de disgregación y agregación

Para estudiar un sistema complejo sin perderse en los detalles ni quedarse en la superficialidad, se aplican dos operaciones complementarias:

- **Disgregación (descomposición top-down):** dividir un sistema en sus **subsistemas** y componentes más simples para analizar su funcionamiento interno (por ejemplo, dividir un sistema web en frontend, backend, base de datos y red).
- **Agregación (síntesis bottom-up):** agrupar componentes o subsistemas relacionados en unidades de nivel superior (**suprasistemas**) para comprender el comportamiento global y sus interacciones con el entorno.

```
Suprasistema (Universidad)
   └── Sistema (Facultad de Ingeniería)
          ├── Subsistema (Control de Estudios)
          └── Subsistema (Departamento de Informática)
```

## Errores comunes

- **Confundir "sistema cerrado" con "sistema aislado o autónomo":** un software sin conexión a internet sigue recibiendo energía eléctrica e interacciones del usuario; por tanto, sigue siendo un sistema **abierto**. En la práctica, casi todos los sistemas reales son abiertos.
- **Asumir que todo sistema discreto es determinístico:** una simulación de colas en un servidor es discreta (llegadas y salidas por eventos), pero es **probabilística** porque los tiempos entre llegadas siguen distribuciones aleatorias.

## Ejercicios propuestos

1. **Clasifica un cajero automático (ATM)** según todos los criterios vistos.
   - *Respuesta:* Físico (hardware) y abstracto (software), abierto, artificial, híbrido (interfaz discreta y sensores físicos), controlado y mayormente determinístico (aunque la demanda de clientes es probabilística).
2. **Ubica en la escala de Boulding:** (a) un termostato; (b) una red neuronal biológica humana; (c) una empresa de desarrollo de software.
   - *Respuesta:* (a) Nivel 3; (b) Nivel 6/7 (como parte del ser humano); (c) Nivel 8.

## Conexiones

- La distinción entre sistemas discretos, continuos, determinísticos y probabilísticos es central en [[Simulación de Sistemas]] y [[Investigación de Operaciones I]].
- Los sistemas abstractos y formales se apoyan en [[Estructuras Discretas]] y [[Fundamentos de Lógica Digital]].
- Anterior: [[Teoría General de Sistemas - Carácter dinámico, homeostasis y sinergia]].
- Siguiente: [[Teoría General de Sistemas - Origen, evolución y enfoques de la TGS]].

## Fuente

- Basado en `Material/Introducción asignatura Teoría General de sistemas (1).pdf`, `Material/Parcial I de TGS.docx` y Boulding (1956).
