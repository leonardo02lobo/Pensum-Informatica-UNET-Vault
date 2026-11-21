---
tags: [materia, semestre-II]
semestre: II
---
# Física I

**Semestre:** [[Semestre II]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Matemática I]]

## Correquisito
- [[Laboratorio de Física I]]

## Desbloquea
- [[Física II]]

## Apuntes

### Descripción general y objetivos
Física I es la **mecánica clásica**: cinemática, dinámica, trabajo y energía, momento lineal y dinámica rotacional. Prelación: [[Matemática I]]; correquisito: [[Laboratorio de Física I]]; desbloquea [[Física II]]. Objetivos: modelar movimientos con vectores y derivadas, aplicar las leyes de Newton y las leyes de conservación a problemas de ingeniería. Programa oficial: verificar.

### Contenido programático (según el Material, Parcial 1 y Parcial 3; verificar con el programa oficial)
**I parcial**: conceptos básicos y unidades (conversión), vectores (suma, componentes, producto escalar y vectorial), cinemática en 1D, 2D y 3D (posición, desplazamiento, velocidad, aceleración), movimiento rectilíneo uniforme y uniformemente variado, caída libre, proyectiles, movimiento circular.
**II parcial (típico)**: leyes de Newton, fuerzas (peso, normal, tensión, roce), diagramas de cuerpo libre, trabajo, energía cinética y potencial, conservación de la energía, potencia.
**III parcial**: movimiento circular y rotación del cuerpo rígido, torque, momento angular, momento de inercia, condiciones de equilibrio, y colisiones/momento lineal (según el lapso).

### Fórmulas clave
```
v = dr/dt;  a = dv/dt
MRUV:  v = v0 + a t;  x = x0 + v0 t + a t²/2;  v² = v0² + 2a Δx
Proyectil: x = v0 cosθ t;  y = v0 senθ t - g t²/2;  alcance R = v0² sen2θ / g
Circular: a_c = v²/r;  v = ω r;  ω = ω0 + α t;  θ = θ0 + ω0 t + α t²/2
Newton: ΣF = m a;   roce f = μ N
Trabajo: W = F·d = F d cosθ;  Ec = m v²/2;  Ep = m g h;  teorema trabajo-energía W = ΔEc
Momento lineal: p = m v;  Impulso J = F Δt = Δp
Torque: τ = r x F;  τ = I α;  L = I ω;  I(masa puntual) = m r²
```

### Ejemplos resueltos
1. Un carro parte del reposo con a = 2 m/s². Tras 5 s: v = 10 m/s, x = 25 m.
2. Bloque de 10 kg en plano inclinado 30° sin roce: a = g sen30° = 4,9 m/s².
3. Colisión perfectamente inelástica de m1 = m2 con v2 = 0: v_final = v1/2.

### Relación con otras materias
Usa derivadas de [[Matemática I]] e integrales de [[Matemática II]]; se practica en [[Laboratorio de Física I]]; continúa en [[Física II]] (electricidad y magnetismo) y apoya [[Organización del Computador]] y [[Simulación de Sistemas]].

### Evaluación y consejos
Parciales con problemas y teoría; se permite formulario según el parcial (hay formularios del I y III parcial en el Material). Dibuja siempre el diagrama, verifica unidades y signos, y resuelve las prácticas (PP/PR) y las guías (CT) de cada tema.

### Bibliografía recomendada
Sears, Zemansky, Young y Freedman, *Física universitaria*; Serway y Jewett, *Física para ciencias e ingeniería*; Halliday, Resnick y Krane, *Física*.

### Recursos del Material/
- Carpeta `Parcial 1/`: guías de clase CT11 a CT14 (pdf y pps), prácticas PR y PP, [Conceptos Básicos](Material/Parcial%201/Conceptos_Basicos-1%20imprimir.pdf), [Vectores](Material/Parcial%201/CT1(00)1-2021-2%20Vectores.pdf), [Formulario I Parcial](Material/Parcial%201/Formulario%20I%20Parcial%20de%20Física%20I.pdf) y un examen diferido resuelto.
- Carpeta `Parcial 3/`: guías CT39 y CT310 (rotación, torque, momento angular), prácticas PR39/PR310/PP39 y [Formulario III parcial 2022-1](Material/Parcial%203/Formulario%20III%20parcial%202022-1%20(1).pdf).
