---
tags: [clase, semestre-VIII]
materia: Sistema de Información II
---
# Sistema de Información II - Implantación, Gestión del Cambio y Gobierno de TI

Materia: [[Sistema de Información II]]
Anterior: [[Sistema de Información II - Seguridad, Control de Acceso y Continuidad Operativa]]
Siguiente: — (última clase)

## Contexto y objetivo
Planificar la **implantación exitosa** de un sistema de información en una organización real (migración de datos, estrategias de conversión, pruebas de aceptación, capacitación y gestión del cambio), evaluar su **ROI de TI** y conocer los marcos de **Gobierno y Gestión de TI** (**COBIT** e **ITIL**).

## 1. Pruebas, migración de datos y estrategias de conversión
Antes de liberar a producción, se ejecutan pruebas de sistema y **pruebas de aceptación de usuario (UAT)** con casos reales del negocio. La **migración de datos** desde el sistema legado requiere limpieza, mapeo, carga de prueba y conciliación de totales (conteo de registros y sumas de control).

Estrategias de puesta en marcha (conversión):
1. **Directa (*Big Bang*)**: se apaga el sistema viejo y arranca el nuevo en una fecha fija. Menor costo operativo, pero máximo riesgo si ocurre una falla crítica.
2. **En paralelo**: ambos sistemas operan simultáneamente durante un período para comparar resultados. Muy segura, pero duplica el trabajo de los usuarios.
3. **Piloto**: se implanta primero en una sucursal o departamento para validar antes de extenderlo al resto.
4. **Por fases (incremental)**: se activan módulos progresivamente (ej. primero Inventario, luego Facturación).

## 2. Capacitación y Gestión del Cambio Organizacional
La principal causa de fracaso en proyectos de SI no es técnica, sino humana y organizacional:
- Resistencia al cambio por miedo a perder control, sobrecarga inicial o falta de comprensión.
- **Gestión del cambio**: involucrar a usuarios clave desde el análisis, comunicar beneficios con transparencia, designar *líderes de cambio* por área y brindar capacitación práctica por roles (no manuales genéricos).

## 3. Indicadores de calidad y ROI de TI
Para justificar la inversión ante la gerencia se mide el **Retorno sobre la Inversión (ROI)** y el **Costo Total de Propiedad (TCO)** (licencias, hardware/nube, desarrollo, capacitación y mantenimiento a 3–5 años):
$$\text{ROI} = \frac{\text{Beneficios netos} - \text{Costo total de inversión}}{\text{Costo total de inversión}} \times 100\,\%$$
Indicadores operativos post-implantación: tasa de adopción de usuarios, reducción de tiempo de ciclo del proceso, tasa de errores/retrabajos y **SLA** (*Service Level Agreement*, disponibilidad $\ge 99{,}9\,\%$).

## 4. Gobierno de TI: COBIT e ITIL (introducción)
- **COBIT** (*Control Objectives for Information and Related Technologies*): marco de **gobierno y gestión de TI** que alinea la tecnología con los objetivos estratégicos del negocio, gestiona riesgos y define controles auditables.
- **ITIL** (*Information Technology Infrastructure Library*): marco de mejores prácticas para la **gestión de servicios de TI (ITSM)**: mesa de ayuda (*service desk*), gestión de incidentes (restaurar servicio rápido), gestión de problemas (causa raíz) y gestión de cambios.

## Errores comunes
- Subestimar la **migración de datos** creyendo que basta con copiar tablas, cuando los datos históricos suelen tener duplicados, códigos obsoletos e inconsistencias.
- Elegir conversión *Big Bang* para un ERP crítico sin plan de contingencia ni vuelta atrás (*rollback*).
- Confundir **incidente** (interrupción puntual a resolver rápido en ITIL) con **problema** (causa raíz subyacente de uno o más incidentes).

## Ejercicios propuestos
1. Una empresa va a reemplazar su sistema de facturación y contabilidad en 12 sucursales. ¿Qué combinación de estrategias de conversión recomienda y por qué?
   - *Respuesta*: estrategia **piloto** en 1 sucursal (opcionalmente en paralelo las primeras semanas) para depurar fallos y validar la capacitación, seguida de despliegue **por fases** al resto de sucursales.
2. Un proyecto de SI cuesta $\$25\,000$ (desarrollo, migración y capacitación) y genera ahorros y beneficios por $\$35\,000$ en su horizonte de evaluación. Calcule el ROI.
   - *Respuesta*: $\text{ROI} = \frac{35\,000 - 25\,000}{25\,000} \times 100\,\% = 40\,\%$.

## Conexiones
- Evaluación financiera de proyectos en [[Finanzas para Ingenieros]] e [[Ingeniería Económica]].
- Gestión de alcance, cronograma y riesgos en [[Gerencia de Proyectos]].
- Continuidad del ciclo de desarrollo formal en [[Ingeniería de Software]].

## Fuente
Basado en el programa orientativo de [[Sistema de Información II]] (Laudon & Laudon, *Sistemas de Información Gerencial*; Kendall & Kendall, *Análisis y Diseño de Sistemas*).
