---
tags: [clase, electiva]
materia: Formación de Emprendedores
fuente: "conocimiento general"
---
# FE 03 - Modelo de negocio Canvas y Lean Startup

Materia: [[Formación de Emprendedores]]
Anterior: [[FE 02 - Ideas, oportunidades y análisis de mercado]]
Siguiente: [[FE 04 - Plan de negocios y aspectos legales]]

## Contexto y objetivo
Un **modelo de negocio** describe cómo una organización crea, entrega y captura valor. El Business Model Canvas lo representa en una página; Lean Startup propone validarlo con experimentos baratos. El objetivo es construir un canvas coherente y diseñar un MVP con métricas de validación.

## Teoría

### Los 9 bloques del Business Model Canvas
1. **Segmentos de clientes**: a quién servimos.
2. **Propuesta de valor**: qué problema resolvemos y qué beneficio entregamos.
3. **Canales**: cómo llegamos al cliente (venta directa, web, distribuidores).
4. **Relación con clientes**: autoservicio, asistencia personal, comunidad.
5. **Fuentes de ingresos**: venta, suscripción, licencia, comisión, publicidad, freemium.
6. **Recursos clave**: físicos, intelectuales, humanos, financieros.
7. **Actividades clave**: desarrollo, producción, plataforma, marketing.
8. **Socios clave**: proveedores, alianzas.
9. **Estructura de costos**: costos fijos y variables dominantes.

Coherencia: el lado derecho (cliente, valor, ingresos) debe ser consistente con el izquierdo (recursos, actividades, costos). Una forma de verificar: ingresos por cliente $>$ costo de adquirir y servir al cliente.

### Propuesta de valor (Value Proposition Canvas)
Se enlazan el **perfil del cliente** (tareas, dolores, ganancias) con el **mapa de valor** (productos, aliviadores de dolor, creadores de ganancia). Ajuste (fit) cuando cada dolor importante tiene un aliviador.

### Lean Startup
Ciclo **Construir - Medir - Aprender**:
- **Hipótesis**: supuestos críticos (de problema, de solución, de precio, de canal).
- **MVP** (Producto Mínimo Viable): la versión más simple que permite aprender sobre la hipótesis. Ejemplos: landing page, prototipo en papel, "mago de Oz" (manual por detrás), concierge.
- **Métricas accionables** frente a métricas de vanidad.
- **Pivote**: cambio estructurado de rumbo (de segmento, de producto, de canal, de monetización) basado en lo aprendido.
- **Contabilidad de la innovación**: definir antes del experimento el criterio de éxito.

### Métricas de unidad
- **CAC** (costo de adquisición de cliente) $= \dfrac{\text{gasto comercial y marketing}}{\text{clientes nuevos}}$
- **ARPU**: ingreso medio por usuario.
- **Churn** mensual $c$; vida media del cliente $\approx 1/c$ meses.
- **LTV** $\approx \dfrac{\text{ARPU}\times \text{margen bruto}}{c}$
- Regla práctica: $\text{LTV}/\text{CAC} \geq 3$ y recuperación de CAC en menos de 12 meses.

## Ejemplo resuelto: canvas de un SaaS de inventario para ferreterías

| Bloque | Contenido |
|---|---|
| Segmentos | Ferreterías pequeñas y medianas con 1 a 3 sucursales |
| Propuesta de valor | Controlar existencias y precios desde el móvil, sin hojas de cálculo |
| Canales | Visitas comerciales, WhatsApp, distribuidores de materiales |
| Relación | Onboarding asistido, soporte por chat |
| Ingresos | Suscripción mensual de 30 USD (hipotético) |
| Recursos | Equipo de desarrollo, servidor en la nube |
| Actividades | Desarrollo, soporte, ventas |
| Socios | Pasarela de pago, proveedores de hardware (lectores de barras) |
| Costos | Salarios, nube, comisiones de pago |

**Experimento MVP**: landing page con precio y botón "Solicitar demo", más 10 visitas a ferreterías. Criterio de éxito definido antes: al menos 5 de 10 aceptan una prueba piloto y 2 prepagan un trimestre.

**Cálculo de unidad (hipotético)**: ARPU 30 USD/mes, margen bruto 80 %, churn 4 % mensual, CAC 150 USD.
- LTV $= \dfrac{30\times 0{,}8}{0{,}04} = 600$ USD
- LTV/CAC $= 600/150 = 4$ (aceptable)
- Recuperación del CAC $= \dfrac{150}{30\times 0{,}8} = 6{,}25$ meses.

Si el churn fuese 10 %, LTV $= 240$ y LTV/CAC $= 1{,}6$: el modelo no sería sostenible, lo cual obligaría a pivotar o mejorar retención.

## Errores comunes
- Llenar el canvas una sola vez y no actualizarlo con evidencia.
- Un segmento tipo "todo el mundo".
- MVP demasiado completo (meses de desarrollo antes de hablar con clientes).
- Métricas de vanidad (descargas, visitas) sin conversión ni retención.
- Confundir pivote con abandono impulsivo.

## Ejercicios propuestos
1. Complete un canvas para un servicio de tutorías en línea y señale la hipótesis más riesgosa. *Respuesta: libre; suele ser disposición a pagar o canal de adquisición.*
2. ARPU 20 USD, margen 70 %, churn 5 %, CAC 90 USD: calcule LTV y LTV/CAC. *Respuesta: LTV 280 USD; relación 3,11.*
3. Proponga un MVP tipo "mago de Oz" para un servicio de recomendación de rutas de transporte. *Respuesta: formulario web y respuestas manuales por WhatsApp, midiendo recurrencia de uso.*

## Conexiones con otras materias
[[Ingeniería de Software]] y [[IS 01 - Ciclo de vida y modelos de proceso]] (iteración y entrega incremental), [[Gerencia de Proyectos]], [[Economía]].

## Fuente
Osterwalder y Pigneur, *Generación de Modelos de Negocio*; Ries, *El método Lean Startup*. Cifras ilustrativas.
