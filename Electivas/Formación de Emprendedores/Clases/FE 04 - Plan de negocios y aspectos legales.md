---
tags: [clase, electiva]
materia: Formación de Emprendedores
fuente: "conocimiento general"
---
# FE 04 - Plan de negocios y aspectos legales

Materia: [[Formación de Emprendedores]]
Anterior: [[FE 03 - Modelo de negocio Canvas y Lean Startup]]
Siguiente: [[FE 05 - Plan financiero VAN TIR y punto de equilibrio]]

## Contexto y objetivo
El **plan de negocios** documenta, de forma coherente y comunicable, cómo se creará y operará la empresa. Sirve para pensar, para conseguir financiamiento y para gestionar. El objetivo de esta clase es estructurar sus secciones (mercadeo, operaciones, organización, legal) y reconocer las figuras jurídicas básicas.

## Teoría

### Estructura del plan
1. **Resumen ejecutivo** (1 página; se escribe al final).
2. **Descripción de la empresa**: misión, visión, valores, objetivos SMART.
3. **Análisis del mercado** (clase [[FE 02 - Ideas, oportunidades y análisis de mercado]]).
4. **Plan de mercadeo**.
5. **Plan de operaciones**.
6. **Plan de organización y equipo**.
7. **Aspectos legales y regulatorios**.
8. **Plan financiero** (clase siguiente).
9. **Riesgos y plan de contingencia**; cronograma de hitos.

### Plan de mercadeo: las 4P (7P en servicios)
- **Producto**: atributos, marca, ciclo de vida.
- **Precio**: por costos (costo + margen), por valor percibido o por competencia.
- **Plaza** (distribución) y **Promoción** (comunicación, ventas, contenido).
- En servicios: personas, procesos y evidencia física.
- **Embudo de ventas**: conciencia, interés, consideración, compra, retención; con tasas de conversión por etapa.

**Precio por costos**: $P = \dfrac{CV_u}{1-m}$ donde $m$ es el margen bruto deseado sobre el precio.

### Plan de operaciones
Procesos clave, ubicación, infraestructura, proveedores, capacidad instalada, control de calidad. En software: arquitectura, metodología, entorno de nube, soporte. Se conecta con [[Gerencia de Proyectos]] para el cronograma de lanzamiento.

### Organización
Fundadores, roles, perfiles a contratar, esquema de remuneración, pacto de socios (reparto de acciones, vesting, salida). Vea la electiva [[Organización]] para estructuras.

### Aspectos legales (conceptos generales)
- **Formas jurídicas** habituales en Venezuela: firma personal, compañía anónima (C.A.), sociedad de responsabilidad limitada (S.R.L.), cooperativa. Cada una difiere en responsabilidad, capital y trámites. **Verificar con el programa oficial y con la normativa vigente**; los requisitos cambian.
- Registro mercantil, inscripción tributaria (RIF), licencias municipales, seguridad social y obligaciones laborales: contenidos que se detallan en [[Legislación, Valores y Proyecto de País]].
- **Propiedad intelectual**: marcas, derechos de autor, patentes, licenciamiento de software (ver [[GT 05 - Propiedad intelectual]]).
- **Contratos**: con clientes, proveedores y empleados; acuerdos de confidencialidad (NDA).
- **Protección de datos** y delitos informáticos: ver [[Delitos informáticos y firma electrónica]].

## Ejemplo resuelto: precio y embudo de ventas
Servicio SaaS: costo variable por cliente $CV_u = 6$ USD/mes; margen bruto objetivo $m = 80\,\%$.
$$P = \frac{6}{1-0{,}8} = 30 \text{ USD/mes}$$

Embudo mensual hipotético: 2 000 visitantes a la web; 5 % solicita demo $\rightarrow 100$; 20 % de las demos se convierte $\rightarrow 20$ clientes nuevos. Con presupuesto de marketing de 1 800 USD y ventas de 1 200 USD: $\text{CAC} = \dfrac{3\,000}{20} = 150$ USD.

Para duplicar clientes sin duplicar gasto, conviene actuar sobre las tasas: subir la conversión de demo a 40 % da 40 clientes con el mismo presupuesto, y CAC $=75$ USD.

## Cronograma de hitos (ejemplo)
| Hito | Mes |
|---|---|
| Constitución legal y registro | 1 |
| MVP validado con 10 clientes piloto | 3 |
| Lanzamiento comercial | 5 |
| Punto de equilibrio operativo (objetivo) | 14 |

## Errores comunes
- Plan de 80 páginas que nadie lee, sin resumen ejecutivo claro.
- Proyecciones financieras sin supuestos explícitos ("curva de palo de hockey").
- Omitir la sección legal y de riesgos.
- No definir el pacto de socios por "confianza".
- Fijar precios solo por costo, ignorando el valor percibido.

## Ejercicios propuestos
1. Costo variable 12 USD, margen bruto del 60 %: calcule el precio. *Respuesta: $12/0{,}4 = 30$ USD.*
2. Embudo: 5 000 visitas, 4 % a registro, 25 % de registros paga; ¿cuántos clientes y qué conversión total? *Respuesta: 50 clientes; 1 %.*
3. Enumere los apartados mínimos de un resumen ejecutivo. *Respuesta: problema, solución, mercado, modelo de ingresos, equipo, tracción, necesidad de capital.*

## Conexiones con otras materias
[[Legislación, Valores y Proyecto de País]], [[Organización]], [[Gerencia de Proyectos]], [[Economía]], [[Ingeniería de Software]].

## Fuente
Conocimiento general; marco legal a verificar con la normativa y el programa oficial. Cifras ilustrativas.
