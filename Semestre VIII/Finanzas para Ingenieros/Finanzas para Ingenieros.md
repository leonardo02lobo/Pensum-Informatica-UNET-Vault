---
tags: [materia, semestre-VIII]
semestre: VIII
---
# Finanzas para Ingenieros

**Semestre:** [[Semestre VIII]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Ingeniería Económica]]

## Desbloquea
- _Ninguna_

## Apuntes

### Descripción general y objetivos
Finanzas para Ingenieros (código 0423804T, Departamento de Ingeniería Informática, Núcleo de Tecnología Aplicada; guía didáctica de abril 2025 del docente Feijoo Colomine Duran, modalidad virtual en UNET Virtual) entrega las herramientas financieras para **evaluar si una solución técnica es viable financieramente**: valor del dinero en el tiempo, relación **rendimiento-riesgo**, teoría de portafolios, y lectura de **estados financieros y razones financieras**. Se evalúa de forma continua con actividades formativas y proyectos ("aprender haciendo"). Prerrequisito: [[Ingeniería Económica]]. Como conducta de entrada se pide dominio de un lenguaje de propósito general (Java, C++ o Python).

Nota hija con el proyecto: [[Modelo de Markowitz y Algoritmo Genético]].

### Contenido programático (ruta de aprendizaje de la guía)
1. **Valor del dinero en el tiempo y criterios de evaluación**: VPN, VFN, VAN, relación entre ellos; relación Beneficio/Costo; criterios por rentabilidad (TIR, **verdadera rentabilidad**); conceptos económicos: mercancía y su doble carácter (valor de uso y de cambio), teorías del valor objetiva y subjetiva, el trabajo como fuente de valor, modos de producción y **sistema financiero venezolano**.
2. **Rendimiento y riesgo**: rendimiento esperado, varianza, desviación estándar, covarianza y correlación; diversificación; **teoría de portafolios de Markowitz**, frontera eficiente, CAPM (introducción); optimización con **algoritmos genéticos** y multiobjetivo (MOEA).
3. **Balance general, estado de resultados y razones financieras**: liquidez, endeudamiento, rentabilidad y actividad; razones de mercado; análisis e interpretación para decisiones de inversión.
(Ponderaciones y cronograma exactos: ver la guía didáctica o verificar con el programa oficial; la guía asigna, por ejemplo, 10 % a la primera tarea.)

### Conceptos clave
- **Valor presente neto**: VPN = Σ Fₜ/(1+k)ᵗ − I₀.
- **TIR**: tasa que anula el VPN. **Verdadera rentabilidad (VR / TIRM)**: reinvierte los flujos a una tasa explícita, evita TIR múltiples.
- **Rendimiento esperado** E(R) = Σ pᵢRᵢ; **riesgo** σ = √Var(R).
- **Diversificación**: el riesgo de la cartera depende de las **covarianzas**; con correlación < 1 el riesgo baja.
- **Frontera eficiente**: carteras con máximo rendimiento para cada nivel de riesgo.
- **Ratio de Sharpe**: (E(Rp) − Rf)/σp.
- **Razón corriente** = Activo corriente / Pasivo corriente; **ROE** = Utilidad neta / Patrimonio; **ROA** = Utilidad neta / Activos; **endeudamiento** = Pasivo total / Activo total.
- **Enfermedad holandesa**: efecto de un auge de recursos naturales que aprecia la moneda y debilita otros sectores (tema de un trabajo del Material).

### Fórmulas y código
```
Cartera:   E(Rp) = Σ xᵢ E(Rᵢ)
           σp²  = Σᵢ Σⱼ xᵢ xⱼ σᵢⱼ ,  con Σ xᵢ = 1,  xᵢ ≥ 0
Markowitz: min σp²  sujeto a  E(Rp) = R*,  Σ xᵢ = 1
2 activos: σp² = x²σ₁² + (1−x)²σ₂² + 2x(1−x)ρσ₁σ₂
```

```python
import numpy as np
# Rendimientos semanales (filas = semanas, columnas = activos)
R = np.log(precios[1:] / precios[:-1])
mu = R.mean(axis=0) * 52           # rendimiento anualizado
S  = np.cov(R.T) * 52              # covarianzas anualizadas
def fitness(x):                    # función objetivo para el algoritmo genético
    x = x / x.sum()
    rend, riesgo = x @ mu, np.sqrt(x @ S @ x)
    return (rend - 0.04) / riesgo  # Sharpe con Rf = 4 %
```

### Ejemplo resuelto breve
Activos A (E=10 %, σ=20 %) y B (E=14 %, σ=30 %), ρ = 0,2, mitad y mitad: E(Rp) = 12 %; σp² = 0,25(0,04)+0,25(0,09)+2(0,25)(0,2)(0,2)(0,3) = 0,01+0,0225+0,006 = 0,0385 → σp ≈ 19,6 %, menor que el de A pese a un rendimiento mayor: eso es diversificación.

### Cómo se relaciona con otras materias
Continúa [[Ingeniería Económica]] y [[Economía]]; usa [[Estadística I]] y [[Estadística II]] (media, varianza, covarianza), [[Matemática IV]] (álgebra matricial y optimización), y [[Introducción a la Inteligencia Artificial]] / [[Aprendizaje Automático]] (algoritmos genéticos, optimización). Relevante para [[Formación de Emprendedores]] y [[Gerencia de Proyectos]].

### Evaluación y consejos de estudio
Evaluación continua con tareas, ejercicios en Excel y proyecto final (portafolio de criptomonedas con Markowitz y algoritmo genético, junio 2025). Consejos: practique en Excel/Python con datos reales semanales, valide que los pesos sumen 1, interprete los resultados (no solo calcule) y relacione cada razón financiera con una decisión.

### Bibliografía recomendada
- Brigham y Houston. *Fundamentos de Administración Financiera*.
- Ross, Westerfield y Jaffe. *Finanzas Corporativas*.
- Bodie, Kane y Marcus. *Principios de Inversiones*.
- Markowitz, H. (1952). *Portfolio Selection*, Journal of Finance.
- Coello Coello, C. *Introducción a la Computación Evolutiva* (en Material).

### Recursos del Material/
- [Guía didáctica](Material/Tema%201/Guía%20didáctica%20Finanzas_ingenieros_V20251.pdf): objetivos, ruta de aprendizaje, evaluación.
- Tema 1: [EJERCICIOS1.pdf](Material/Tema%201/EJERCICIOS1.pdf), [eJERCICIOS.pdf](Material/Tema%201/eJERCICIOS.pdf), [conceptos_Mercado_y_Modos_de_Produccion.pdf](Material/Tema%201/conceptos_Mercado_y_Modos_de_Produccion.pdf), `FINANZAS.ppt`, `EjerciciosExcel.xlsx`, trabajo [Enfermedad Holandesa](Material/Tema%201/Enfermedad%20Holandesa-%20Douglas%20Aliendres%20V31123065%20&%20Leonardo%20Lobo%20V31489733.pdf), `Zona de Descargas-20250505.zip`.
- Tema 2: [apuntes.pdf](Material/Tema%202/apuntes.pdf) (Coello, computación evolutiva), [algoritmosgeneticos.pdf](Material/Tema%202/algoritmosgeneticos.pdf), [genetico.pdf](Material/Tema%202/genetico.pdf), [MOEA.pdf](Material/Tema%202/MOEA.pdf), [TeoriadePortafolios-0408.pdf](Material/Tema%202/TeoriadePortafolios-0408.pdf), [La rentabilidad y el riesgo en las inversiones financieras.pdf](Material/Tema%202/La%20rentabilidad%20y%20el%20riesgo%20en%20las%20inversiones%20financieras.pdf), carpeta `algoritmos Geneticos/` (ejemplo `algoritmoGenetico.py` con PyGAD).
- [PROYECTO FINANZAS PARA INGENIEROS2025.pdf](Material/PROYECTO%20FINANZAS%20PARA%20INGENIEROS2025.pdf): enunciado del proyecto.
- [Algoritmo Genético (informe)](Material/Algoritmo%20Genético%20Douglas%20Aliendres%20&%20Leonardo%20Lobo.pdf): informe entregado.
