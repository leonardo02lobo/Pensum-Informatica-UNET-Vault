---
tags: [clase, semestre-VI]
materia: Sistema de Información I
fuente: conocimiento general
---
# SI1 - 03 Investigación preliminar y estudio de factibilidad

Materia: [[Sistema de Información I]]
Anterior: [[SI1 - 02 Ciclo de vida de desarrollo SDLC y metodologias]]
Siguiente: [[SI1 - 04 Determinacion de requisitos]]

## Contexto y objetivo
Antes de invertir en un sistema hay que decidir si **vale la pena**. La investigación preliminar define el problema y el alcance; el **estudio de factibilidad** responde si el proyecto es viable técnica, económica y operativamente. Termina en un informe que decide: proceder, modificar o abandonar.

## Investigación preliminar
Pasos: 1) recibir la solicitud (necesidad, problema u oportunidad); 2) **aclarar el problema** (distinguir síntomas de causas: diagrama de causa-efecto de Ishikawa, "5 porqués"); 3) fijar **alcance y objetivos** (SMART); 4) **estudiar el sistema actual** superficialmente (entrevistas breves, documentos); 5) preparar el informe.
Enunciado de alcance: qué incluye, qué **no** incluye, supuestos y restricciones.

## Tipos de factibilidad
- **Técnica**: ¿existe la tecnología y la experiencia? ¿se integra con la infraestructura?
- **Económica**: ¿los beneficios superan los costos?
- **Operativa**: ¿los usuarios lo aceptarán y usarán? ¿cambia la organización de forma manejable?
- **Legal / de cronograma** (a menudo se agregan): normativa, protección de datos, plazos.

## Costos y beneficios
**Costos**: de desarrollo (personal, licencias, hardware), operación (soporte, hospedaje, energía), capacitación, migración y mantenimiento. **Beneficios tangibles** (reducción de costos, aumento de ingresos, ahorro de tiempo) e **intangibles** (mejor imagen, satisfacción, mejor decisión).

## Métodos de evaluación económica
Sea $F_t$ el flujo neto del año $t$ (beneficio − costo), $i$ la tasa de descuento e $I_0$ la inversión inicial.
- **Valor presente neto**: $VPN=\sum_{t=1}^{n}\frac{F_t}{(1+i)^t}-I_0$. Aceptar si $VPN>0$.
- **Tasa interna de retorno (TIR)**: la $i$ que hace $VPN=0$; aceptar si $TIR>i$ requerida.
- **Relación beneficio/costo**: $B/C=\frac{VP(\text{beneficios})}{VP(\text{costos})}$; aceptar si $>1$.
- **Período de recuperación** (*payback*): tiempo hasta que el flujo acumulado cubre $I_0$.
Ver [[Ingeniería Económica]].

### Ejemplo resuelto
Inversión $I_0=10\,000$ USD; flujos netos: año 1: 4 000, año 2: 5 000, año 3: 6 000; $i=10\%$.
- $VP_1=4000/1.1=3636{,}36$; $VP_2=5000/1.21=4132{,}23$; $VP_3=6000/1.331=4507{,}89$.
- Suma = 12 276,48; $VPN=12\,276{,}48-10\,000=2\,276{,}48>0$: **factible económicamente**.
- *Payback*: acumulado año 1 = 4 000; año 2 = 9 000; año 3 = 15 000. Falta 1 000 de los 6 000 del año 3: $2+1000/6000\approx2{,}17$ años.
- $B/C=12\,276{,}48/10\,000=1{,}23>1$.

## Informe de factibilidad
Contenido: resumen ejecutivo, descripción del problema, alcance, alternativas (incluida "no hacer nada" y "comprar vs construir"), análisis por tipo de factibilidad, recomendación, plan preliminar y riesgos.

## Gestión de riesgos preliminar
Riesgo = probabilidad × impacto. Matriz 3×3, estrategias: evitar, mitigar, transferir, aceptar. Ver [[Gerencia de Proyectos]].

## Errores comunes
- Estimar solo costos de desarrollo y olvidar operación y mantenimiento.
- Contar beneficios intangibles como si fueran dinero seguro.
- Tomar el síntoma ("es lento") como el problema.
- No incluir la alternativa "no hacer nada".

## Ejercicios propuestos
1. Con $I_0=5000$, flujos 2000, 2000, 2000 e $i=8\%$, ¿VPN? *Resp.: $2000(0{,}9259+0{,}8573+0{,}7938)=5154{,}2$; VPN = 154,2 (marginal).*
2. ¿Qué tipo de factibilidad evalúa la resistencia al cambio? *Resp.: operativa.*
3. Enuncie dos beneficios intangibles. *Resp.: imagen institucional, satisfacción del usuario.*

## Conexiones
[[Ingeniería Económica]], [[Gerencia de Proyectos]], [[SI1 - 04 Determinacion de requisitos]].

## Fuente
Conocimiento general (Kendall y Kendall, Senn). La fórmula de VPN coincide con la de la nota principal [[Sistema de Información I]].
