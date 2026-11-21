---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 3-.../Rentabilidad de Proyecto I.pdf
---
# Ingeniería Económica - Tema 3: Criterios VA, EA y TIR

Materia: [[Ingeniería Económica]]
Anterior: [[Ingeniería Económica - Parcial 1 resuelto]]
Siguiente: [[Ingeniería Económica - Tema 3 Comparación de alternativas, costos y proyectos públicos]]

## Contexto y objetivo
"Criterios de decisión para la evaluación económica de alternativas de inversión". La **evaluación económica** es el análisis sistemático de costos y beneficios del proyecto técnico propuesto; aplica modelos de rentabilidad para conocer de forma anticipada el resultado global. Según su fin los proyectos son **privados** (maximizar el beneficio del inversionista; tasas altas) o **públicos** (bienestar social; tasas muy bajas).

## Elementos de un proyecto
Los flujos del Tema 1: $-II=-(CF+CT)$ en 0; $IB_t$, $-C_{op,t}$, $-ISR_t$; $+CT$ y $+VR$ al final. Reglas:
- Se estima **a precios de hoy** (mismo poder de compra).
- **Vida del proyecto $n$:** período de evaluación; depende de deseo de recuperar la inversión, vida contable, económica y útil de los activos, información futura, plazos de préstamos, necesidades de servicio, vida de las alternativas.
- **$i_{min}\ge CC$**; depende de costo de capital, riesgos e incertidumbres y oferta/demanda de capital.

## Modelos de rentabilidad
**Valor Actual (VA):** cantidad en $t=0$ equivalente a los flujos netos a $i_{min}$:
$$VA(i_{min})=F_0+\sum_{t=1}^nF_t(P/F,i_{min},t).$$
Decisión: VA>0 supera el mínimo exigido; =0 lo iguala; <0 pérdida.

**Equivalente Anual (EA):** serie uniforme equivalente: $EA=VA\,(A/P,i_{min},n)$. Mismo criterio de signo.

**Tasa Interna de Retorno (TIR, $i^*$):** rendimiento porcentual sobre la inversión pendiente de recuperar; tasa que hace $VA(i^*)=0$. Decisión: $i^*>i_{min}$ acepta; $=$ indiferente; $<$ rechaza.

## Ejemplos resueltos
**Ejemplo 1 (guía Tema 3, P2).** Flujos: -130.000; 36.000; 51.000; 61.000; 40.000 (Bs), $i_{min}=20\%$.
- $VA(20\%)=-130.000+36.000/1{,}2+51.000/1{,}44+61.000/1{,}728+40.000/2{,}0736=-130.000+30.000+35.417+35.301+19.290=-9.992$. Pérdida: no rentable.
- TIR: $VA(16\%)=+...$; por tanteo $i^*=16{,}04\%<20\%$ → rechazar.
- El proyecto es rentable si $i_{min}<16{,}04\%$.

**Ejemplo 2 (guía P3).** Flujos (miles de Bs): -2.000; 1.150 ×4; 1.350 en el año 5; $i_{min}=30\%$. $VA=-2.000+1.150(P/A,30\%,4)+...$ ; resultado $VA\approx+854{,}8$; $EA=VA(A/P,30\%,5)=+351{,}0$; $TIR=50{,}77\%$. Rentable. Si $i_{min}=60\%$ (sin cálculo): como VA decrece con $i$ y la TIR (50,8%) queda por debajo de 60%, el VA se vuelve negativo, el EA negativo y se rechaza.

**Ejemplo 3 (guía P1, gradiente).** Inversión 1.500 M; ganancias 800 M decreciendo 100 M por año hasta 0 (año 9); venta del equipo 300 M en el año 10; $i=12\%$. Flujos: -1.500; 800, 700,...,100, 0; +300. $VA(12\%)=+1.123{,}6$ M → conviene.

## Propiedades de la TIR
- Una TIR única está asegurada si el flujo cambia de signo una vez (inversión seguida de ingresos); con varios cambios pueden existir varias raíces (regla de Descartes).
- **No existe TIR en proyectos de solo costos.**
- La TIR **no sirve para comparar** alternativas excluyentes (solo dice si es rentable); para ello se usa VA/EA o la TIR del flujo incremental.
- Hay tres métodos de cálculo: tanteo e interpolación (con tablas), Newton/bisección, o funciones financieras (`TIR` en Excel; ver [[Finanzas para Ingenieros - Funciones financieras en Excel]]).

## Errores comunes
- Comparar un VA a distinta $i_{min}$ entre alternativas.
- Confundir TIR con costo de capital.
- Olvidar el valor residual o el capital de trabajo recuperable al final.

## Ejercicios propuestos
1. Flujos -10.000; 3.000 ×5; $i_{min}=10\%$: VA y decisión. (Resp.: $VA=+1.372$; conviene.)
2. Para el anterior, TIR. (Resp.: ≈15,2%.)
3. ¿Qué pasa con el VA si $i_{min}$ sube? (Resp.: disminuye.)

## Conexiones
[[Ingeniería Económica - Guía de ejercicios Tema 3 resuelta]], [[Gerencia de Proyectos]], [[Finanzas para Ingenieros]] (VPN, TIR, TIRM).

## Fuente
`Material/Tema 3-Rentabilidad de un Proyecto y Toma de Decisiones entre Proyectos. Primera Parte/Rentabilidad de Proyecto I.pdf` y `Guía de Ejercicios Tema 3.pdf`; cálculos numéricos propios.
