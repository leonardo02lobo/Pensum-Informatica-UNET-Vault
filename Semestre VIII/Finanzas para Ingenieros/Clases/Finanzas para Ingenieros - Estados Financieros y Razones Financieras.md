---
tags: [clase, semestre-VIII]
materia: Finanzas para Ingenieros
---
# Finanzas para Ingenieros - Estados Financieros y Razones Financieras

Materia: [[Finanzas para Ingenieros]]
Anterior: [[Finanzas para Ingenieros - Algoritmos Genéticos y Optimización de Portafolios]]
Siguiente: — (última clase)

## Contexto y objetivo
Interpretar los dos estados financieros básicos (**Balance General** y **Estado de Resultados**) y calcular las principales **razones financieras** de liquidez, endeudamiento, actividad y rentabilidad para diagnosticar la salud financiera de una empresa antes de invertir o aprobar un proyecto.

## 1. Estados financieros básicos
1. **Balance General (Estado de Situación Financiera)**: fotografía estática en una fecha dada que cumple la ecuación contable fundamental:
   $$\text{Activo} = \text{Pasivo} + \text{Patrimonio}$$
   - *Activo corriente*: caja, bancos, cuentas por cobrar, inventarios (convertibles en efectivo en $\le 1$ año).
   - *Activo no corriente*: propiedad, planta y equipo, intangibles (software, patentes).
   - *Pasivo corriente / no corriente*: obligaciones a corto y largo plazo.
   - *Patrimonio*: capital social y utilidades retenidas.
2. **Estado de Resultados**: resumen dinámico de ingresos, costos y gastos durante un período:
   $$\text{Ventas} - \text{Costo de ventas} = \text{Utilidad bruta}$$
   $$\text{Utilidad bruta} - \text{Gastos operativos} = \text{EBIT (Utilidad operativa)}$$
   $$\text{EBIT} - \text{Intereses} - \text{Impuestos} = \text{Utilidad neta}$$

## 2. Clasificación de razones financieras

### A. Razones de Liquidez (capacidad de pago a corto plazo)
- **Razón corriente** $= \dfrac{\text{Activo corriente}}{\text{Pasivo corriente}}$ (referencia saludable típica: $1{,}5\text{–}2{,}0$).
- **Prueba ácida** $= \dfrac{\text{Activo corriente} - \text{Inventarios}}{\text{Pasivo corriente}}$ (excluye el inventario por ser menos líquido).

### B. Razones de Endeudamiento (solvencia y apalancamiento)
- **Razón de endeudamiento** $= \dfrac{\text{Pasivo total}}{\text{Activo total}}$ (qué proporción de los activos se financia con deuda).
- **Cobertura de intereses** $= \dfrac{\text{EBIT}}{\text{Gastos por intereses}}$ (capacidad de cubrir el servicio de la deuda).

### C. Razones de Actividad (eficiencia operativa)
- **Rotación de inventarios** $= \dfrac{\text{Costo de ventas}}{\text{Inventario promedio}}$.
- **Período promedio de cobro** $= \dfrac{\text{Cuentas por cobrar}}{\text{Ventas a crédito / 365}}$.

### D. Razones de Rentabilidad
- **Margen neto** $= \dfrac{\text{Utilidad neta}}{\text{Ventas}}$.
- **ROA (Rendimiento sobre Activos)** $= \dfrac{\text{Utilidad neta}}{\text{Activo total}}$.
- **ROE (Rendimiento sobre Patrimonio)** $= \dfrac{\text{Utilidad neta}}{\text{Patrimonio}}$.

## 3. Ejemplo resuelto de diagnóstico
Una empresa tecnológica reporta: Activo corriente $= \$120\,000$ (incluye $\$30\,000$ de inventario), Activo total $= \$300\,000$, Pasivo corriente $= \$60\,000$, Pasivo total $= \$150\,000$, Patrimonio $= \$150\,000$, Ventas $= \$400\,000$, Utilidad neta $= \$36\,000$.
- **Razón corriente** $= 120\,000 / 60\,000 = 2{,}0$ (buena holgura a corto plazo).
- **Prueba ácida** $= (120\,000 - 30\,000) / 60\,000 = 1{,}5$ (cubre holgadamente sin depender del inventario).
- **Endeudamiento** $= 150\,000 / 300\,000 = 50\,\%$.
- **Margen neto** $= 36\,000 / 400\,000 = 9\,\%$.
- **ROA** $= 36\,000 / 300\,000 = 12\,\%$; **ROE** $= 36\,000 / 150\,000 = 24\,\%$.

## Errores comunes
- Interpretar una razón financiera aislada sin compararla contra el promedio del sector o su tendencia histórica.
- Usar **Ventas** en lugar de **Costo de ventas** en el numerador de la rotación de inventarios (el inventario está valorado al costo, no a precio de venta).
- Confundir utilidad contable con flujo de caja disponible: una empresa rentable en el Estado de Resultados puede quebrar por falta de liquidez.

## Ejercicios propuestos
1. Si una empresa tiene $\text{ROA} = 10\,\%$ y un endeudamiento (Pasivo/Activo) del $60\,\%$, ¿cuál es su $\text{ROE}$?
   - *Respuesta*: como $\text{Patrimonio}/\text{Activo} = 40\,\%$, entonces $\text{ROE} = \text{ROA} / 0{,}40 = 10\,\% / 0{,}40 = 25\,\%$.
2. ¿Qué indica una razón corriente de $2{,}5$ acompañada de una prueba ácida de $0{,}6$?
   - *Respuesta*: que la mayor parte del activo corriente está inmovilizada en inventarios de lenta realización, lo cual puede comprometer la liquidez inmediata.

## Conexiones
- Sistemas empresariales que generan y consolidan estos estados (ERP y BI) en [[Sistema de Información II]].
- Evaluación de viabilidad de emprendimientos en [[Formación de Emprendedores]] y [[Gerencia de Proyectos]].

## Fuente
Basado en la ruta de aprendizaje de [[Finanzas para Ingenieros]] y la bibliografía recomendada (Brigham & Houston; Ross, Westerfield & Jaffe).
