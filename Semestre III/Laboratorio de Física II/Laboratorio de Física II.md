---
tags: [materia, semestre-III]
semestre: III
---
# Laboratorio de Física II

**Semestre:** [[Semestre III]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- _Ninguna_

## Correquisito
- [[Física II]]

## Desbloquea
- _Ninguna_

## Apuntes

### Descripción general y objetivos

Laboratorio correlativo de [[Física II]]. Su propósito es verificar experimentalmente los fenómenos de electricidad y magnetismo vistos en teoría, y desarrollar destrezas de **medición, tratamiento de datos e informe técnico**. No hay Material propio de esta materia en el vault; el contenido siguiente es referencial. Verificar con el programa oficial las prácticas exactas y la ponderación.

### Contenido programático típico de las prácticas

1. Instrumentos de medición: multímetro, fuente de poder, protoboard, generador de funciones y osciloscopio; incertidumbre y cifras significativas.
2. Electrostática: carga por frotamiento e inducción, electroscopio, líneas de campo y superficies equipotenciales.
3. Ley de Ohm: resistencias óhmicas y no óhmicas (curva V-I).
4. Circuitos serie, paralelo y mixtos; verificación de las leyes de Kirchhoff.
5. Capacitores: carga y descarga de un circuito RC, constante de tiempo.
6. Campo magnético: líneas de campo de imanes y solenoides; fuerza sobre una corriente.
7. Inducción electromagnética: ley de Faraday y ley de Lenz.

### Conceptos clave y fórmulas

- **Error absoluto y relativo**: `ε = |valor medido - valor real|`, `ε_r = ε / valor real`.
- **Incertidumbre estándar**: `σ = sqrt( Σ(xi - x̄)² / (n-1) )`; media `x̄ = Σxi / n`.
- **Propagación**: para `z = x + y`, `Δz = Δx + Δy`; para `z = x·y`, `Δz/z = Δx/x + Δy/y`.
- **Ajuste lineal (mínimos cuadrados)**: pendiente de la gráfica V vs. I = R (ley de Ohm).
- **Constante RC**: `V_c(t) = V0 (1 - e^(-t/RC))`; en `t = RC` el capacitor alcanza el 63,2 %.

```
Resistencia equivalente medida:  R = V / I   (pendiente de la recta V-I)
Potencia disipada:               P = V · I
```

### Ejemplo resuelto breve

Se miden V = 1,0; 2,0; 3,0 V con I = 0,10; 0,21; 0,29 A. La pendiente aproximada es 10,2 Ω; si la resistencia nominal es 10 Ω el error relativo es 2 %.

### Relación con otras materias

Complementa [[Física II]] (correquisito) y se apoya en [[Física I]] y [[Laboratorio de Física I]] para el manejo de datos. Las destrezas con protoboard y multímetro se reutilizan en [[Fundamentos de Lógica Digital]].

### Evaluación y consejos

- Llegar con la guía leída y el procedimiento claro; llevar calculadora y papel milimetrado.
- Registrar datos en tabla con unidades e incertidumbre; graficar siempre.
- El informe suele incluir: objetivo, marco teórico, procedimiento, datos, cálculos, análisis de error y conclusiones.
- Cuidado con la seguridad: no exceder los valores de corriente/tensión de los componentes.

### Bibliografía recomendada

- Guías de laboratorio del Departamento de Matemática y Física de la UNET (verificar).
- Sears, Zemansky, Young, Freedman. *Física Universitaria*, Vol. 2.
- Taylor, J. *Introducción al análisis de errores*.

### Recursos del Material/

Esta materia no tiene carpeta `Material/` en el vault.
