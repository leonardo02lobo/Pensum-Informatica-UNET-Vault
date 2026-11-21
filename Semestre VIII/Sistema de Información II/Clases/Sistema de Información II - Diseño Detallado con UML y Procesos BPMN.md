---
tags: [clase, semestre-VIII]
materia: Sistema de Información II
---
# Sistema de Información II - Diseño Detallado con UML y Procesos BPMN

Materia: [[Sistema de Información II]]
Anterior: [[Sistema de Información II - Arquitectura de Sistemas de Información y APIs]]
Siguiente: [[Sistema de Información II - Inteligencia de Negocios, Data Warehouse y OLAP]]

## Contexto y objetivo
Traducir los requisitos funcionales en artefactos de **diseño detallado** mediante diagramas **UML** (casos de uso, clases, secuencia y componentes) y modelar los flujos organizacionales con **BPMN** (*Business Process Model and Notation*), asegurando consistencia entre procesos, software y base de datos.

## 1. Modelado de procesos de negocio con BPMN
Antes de automatizar, se modela el flujo de trabajo (*workflow*) entre áreas de la organización usando BPMN:
- **Piscinas (*Pools*) y Carriles (*Lanes*)**: representan participantes/organizaciones y roles internos (p. ej., *Estudiante*, *Asesor*, *Coordinador*).
- **Eventos**: inicio (círculo fino), intermedio (doble línea), fin (borde grueso).
- **Actividades / Tareas**: rectángulos redondeados con verbo en infinitivo (*Registrar solicitud*, *Validar requisitos*).
- **Compuertas (*Gateways*)**: rombos de decisión exclusiva (`X`, XOR), paralela (`+`, AND) o inclusiva (`O`).
- **Flujos de secuencia** (flecha continua dentro de un pool) y **flujos de mensaje** (flecha discontinua entre pools).

## 2. Diagramas UML esenciales para diseño detallado
1. **Diagrama y especificación de Casos de Uso**: define *quién* (actor) interactúa con el sistema y *qué* objetivo logra, detallando precondiciones, flujo normal, flujos alternos/excepciones y postcondiciones.
   ```text
   Caso de uso: "Registrar atención estudiantil"
   Actor: Asesor.
   Precondición: Asesor autenticado en el sistema.
   Flujo normal:
     1. Busca al estudiante por cédula.
     2. Selecciona el servicio y modalidad (presencial/virtual).
     3. Registra duración y observaciones.
     4. El sistema valida los datos, guarda la atención y emite confirmación.
   Excepción 1a: Estudiante no registrado -> ofrecer formulario de alta rápida.
   ```
2. **Diagrama de Clases (vista de diseño)**: especifica clases del dominio, atributos con tipos, métodos, visibilidad (`+`, `-`, `#`) y relaciones (asociación, agregación, composición, herencia, multiplicidad `1..*`). Sirve de puente directo hacia el modelo relacional y el código orientado a objetos.
3. **Diagrama de Secuencia**: muestra la interacción temporal entre objetos/capas (Actor $\to$ Controlador $\to$ Servicio $\to$ Repositorio/BD) mediante mensajes síncronos, asíncronos y retornos. Permite verificar que la arquitectura en capas se respeta.
4. **Diagrama de Componentes y Despliegue**: describe módulos físicos, APIs, librerías y nodos donde se ejecutan (servidor web, servidor de aplicaciones, SGBD).

## 3. Diseño de base de datos e interfaces (UI/UX)
- **Diseño de BD**: mapeo del diagrama de clases a tablas normalizadas (3FN) con llaves primarias/foráneas, índices y restricciones de integridad (`CHECK`, `NOT NULL`).
- **Diseño de interfaces**: prototipos (*wireframes*), consistencia visual, retroalimentación clara de errores, accesibilidad y reducción de clics en tareas frecuentes.

## Errores comunes
- Mezclar decisiones de negocio dentro de un diagrama de flujo técnico de código en lugar de usar **BPMN** para el proceso y **UML** para el software.
- Omitir los **flujos de excepción** en casos de uso (qué pasa si no hay stock, si falla la conexión o si el registro está duplicado).
- Diseñar diagramas de clases desconectados de los casos de uso o de la base de datos (atributos que nadie captura o métodos sin soporte de persistencia).

## Ejercicios propuestos
1. Para un proceso de compra en línea: el cliente envía el pedido; el sistema verifica stock (si hay, cobra y despacha en paralelo; si no hay, notifica rechazo). ¿Qué compuertas BPMN se requieren?
   - *Respuesta*: una compuerta exclusiva (`X`) para la condición de stock, y en la rama afirmativa una compuerta paralela (`+`) para ejecutar cobro y despacho simultáneamente.
2. En un diagrama de secuencia de 3 capas para "Consultar inventario", indique el orden correcto de llamadas.
   - *Respuesta*: `Usuario -> Vista/Controlador -> ServicioInventario -> RepositorioBD -> SGBD` y retorno de los datos en orden inverso.

## Conexiones
- Bases de la programación orientada a objetos en [[Programación II]].
- Modelado relacional previo en [[Base de Datos I]] y [[Base de Datos II]].
- Continuación hacia pruebas y calidad en [[Ingeniería de Software]].

## Fuente
Basado en el programa orientativo de [[Sistema de Información II]] (Kendall & Kendall, *Análisis y Diseño de Sistemas*).
