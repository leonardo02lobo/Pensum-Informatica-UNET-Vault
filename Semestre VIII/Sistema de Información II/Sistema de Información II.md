---
tags: [materia, semestre-VIII]
semestre: VIII
---
# Sistema de Información II

**Semestre:** [[Semestre VIII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Base de Datos II]]

## Desbloquea
- [[Ingeniería de Software]]

## Apuntes

### Descripción general y objetivos
Sistema de Información II continúa [[Sistema de Información I]] y [[Base de Datos II]]: pasa del análisis a la **construcción y gestión de sistemas de información empresariales**: diseño detallado, arquitectura, inteligencia de negocios (BI), integración con almacenes de datos, seguridad y gobierno de TI. Desbloquea [[Ingeniería de Software]]. El contenido oficial no está en el vault: **verificar con el programa sinóptico de la UNET**; lo siguiente es un temario típico coherente con su prelación.

### Contenido programático (orientativo)
1. **Repaso del ciclo de vida de un SI**: planificación, análisis, diseño, implementación, mantenimiento; metodologías (cascada, iterativas, ágiles).
2. **Tipos de sistemas**: TPS, MIS, DSS, EIS, ERP, CRM, SCM; sistemas de apoyo a la decisión.
3. **Arquitectura de SI**: capas (presentación, negocio, datos), cliente/servidor, servicios web y APIs REST, microservicios, computación en la nube.
4. **Diseño detallado**: modelado UML (casos de uso, clases, secuencia, componentes), diseño de interfaces, diseño de base de datos y de procesos de negocio (BPMN).
5. **Inteligencia de negocios**: almacén de datos, ETL, cubos OLAP, KPIs y tableros (Power BI); minería de datos introductoria (ver [[Data Warehouse Atenciones Estudiantiles]]).
6. **Seguridad y control**: confidencialidad, integridad, disponibilidad; control de acceso, auditoría, respaldo y continuidad.
7. **Implantación y gestión**: capacitación, migración de datos, pruebas, gestión del cambio, indicadores de calidad y ROI de TI; gobierno de TI (COBIT, ITIL; mención).
8. **Proyecto integrador**: desarrollo de un SI para una organización real.

### Conceptos clave
- **Sistema de información**: conjunto de personas, procesos, datos y tecnología que recolecta, procesa, almacena y distribuye información para decisiones y control.
- **ERP**: sistema integrado que unifica procesos (finanzas, inventario, RR. HH.).
- **KPI**: indicador clave de desempeño.
- **BPMN**: notación para modelar procesos de negocio.
- **Trazabilidad**: vínculo entre requisito, diseño, código y prueba.
- **Tres capas / MVC**: separación de presentación, lógica y datos.

### Código de ejemplo
```sql
-- KPI típico: atenciones por mes y satisfacción promedio (consulta sobre el DWH)
SELECT date_trunc('month', t.fecha) AS mes,
       COUNT(*) AS atenciones, ROUND(AVG(h.satisfaccion),2) AS satisfaccion
FROM dwh.hecho_atenciones h JOIN dwh.dim_tiempo t USING (id_tiempo)
GROUP BY 1 ORDER BY 1;
```
```
Caso de uso: "Registrar atención"
Actor: Asesor.  Flujo: 1) busca estudiante por cédula 2) selecciona servicio
3) registra duración y modalidad 4) guarda 5) sistema valida y confirma.
Excepción: estudiante no registrado -> ofrecer alta.
```

### Ejemplo resuelto breve
Definir requisitos para un sistema de control de inventario: entidades (Producto, Movimiento, Proveedor), reglas (stock no negativo, punto de reorden), reportes (rotación, existencias críticas) y KPI (exactitud de inventario = ítems correctos / ítems contados).

### Cómo se relaciona con otras materias
[[Base de Datos II]] (almacenes y ETL), [[Sistema de Información I]], [[Administración de Base de Datos]], [[Análisis y Procesamiento de Datos]], [[Desarrollo de Aplicaciones Web]], [[Organización]] (estructura de la empresa), [[Teoría General de Sistemas]]; habilita [[Ingeniería de Software]] y [[Gerencia de Proyectos]].

### Evaluación y consejos de estudio
Probablemente evaluación mediante parciales y un proyecto integrador (verificar con el programa oficial). Consejos: documente requisitos y modelos antes de programar, hable con usuarios reales, use control de versiones y mida resultados con indicadores.

### Bibliografía recomendada
- Laudon, K. y Laudon, J. *Sistemas de Información Gerencial*.
- Kendall, K. y Kendall, J. *Análisis y Diseño de Sistemas*.
- O'Brien, J. *Sistemas de Información Gerencial*.
- Kimball, R. *The Data Warehouse Toolkit*.

### Recursos
No hay `Material/` ni material pesado asociado en esta nota.
