---
tags: [materia, semestre-III]
semestre: III
---
# Física II

**Semestre:** [[Semestre III]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Física I]]

## Correquisito
- [[Laboratorio de Física II]]

## Desbloquea
- [[Fundamentos de Lógica Digital]]

## Apuntes

### Descripción general y objetivos

Física II es el curso de **electricidad y magnetismo** de la carrera. En Informática es la base física de la electrónica digital: sin comprender carga, campo, potencial, corriente y circuitos no se entienden las compuertas ni las familias lógicas de [[Fundamentos de Lógica Digital]]. Se apoya en el cálculo ([[Matemática II]]/[[Matemática III]]: integrales, vectores) y en la mecánica de [[Física I]]. Su laboratorio correlativo es [[Laboratorio de Física II]].

Objetivos: describir la naturaleza de la carga y las interacciones electrostáticas; calcular campos y potenciales; analizar circuitos de corriente continua; y comprender los campos magnéticos y la inducción electromagnética. El texto guía es *Física Universitaria* (Sears, Zemansky, Young, Freedman), Vol. 2, 12.ª ed. Verificar con el programa oficial qué capítulos exactos se cubren en el lapso.

### Contenido programático (referencial, basado en Sears-Zemansky Vol. 2)

1. **Carga eléctrica y campo eléctrico** (cap. 21): carga, conservación y cuantización; conductores y aislantes; carga por frotamiento, contacto e inducción; ley de Coulomb; campo eléctrico, líneas de campo, dipolos.
2. **Ley de Gauss** (cap. 22): flujo eléctrico, aplicaciones a simetrías esférica, cilíndrica y plana; conductores en equilibrio electrostático.
3. **Potencial eléctrico** (cap. 23): energía potencial eléctrica, potencial, superficies equipotenciales, gradiente de potencial.
4. **Capacitancia y dieléctricos** (cap. 24): capacitores, combinaciones serie/paralelo, energía almacenada, dieléctricos.
5. **Corriente, resistencia y fuerza electromotriz** (cap. 25): corriente, resistividad, ley de Ohm, potencia eléctrica.
6. **Circuitos de corriente continua** (cap. 26): resistencias serie/paralelo, leyes de Kirchhoff, circuito RC.
7. **Campo magnético y fuerzas magnéticas** (cap. 27) y **fuentes de campo magnético** (cap. 28): fuerza de Lorentz, ley de Biot-Savart, ley de Ampère.
8. **Inducción electromagnética** (cap. 29) e **inductancia** (cap. 30): ley de Faraday, ley de Lenz, inductores.

### Conceptos clave

- **Carga eléctrica**: propiedad fundamental; hay positiva y negativa; cargas iguales se repelen y opuestas se atraen. Un objeto neutro tiene igual número de protones y electrones; se carga ganando o perdiendo electrones.
- **Conservación y cuantización**: la carga total de un sistema aislado es constante; toda carga es múltiplo de e = 1,602 x 10^-19 C.
- **Campo eléctrico** E: fuerza por unidad de carga de prueba, `E = F/q0`.
- **Potencial** V: energía potencial por unidad de carga, en voltios.
- **Corriente** I = dQ/dt, en amperios.
- **Fuerza electromotriz (fem)**: energía por unidad de carga que entrega una fuente.

### Fórmulas fundamentales

```
Ley de Coulomb:        F = k |q1 q2| / r^2        k = 8,99e9 N·m²/C²  (= 1/(4π ε0))
Campo de carga puntual: E = k q / r^2
Flujo y ley de Gauss:  Φ_E = ∮ E · dA = Q_enc / ε0
Potencial puntual:     V = k q / r        ΔV = -∫ E · dl
Energía potencial:     U = k q1 q2 / r
Capacitancia:          C = Q / V     placas paralelas  C = ε0 A / d
Serie / paralelo:      1/Ceq = Σ 1/Ci    |   Ceq = Σ Ci
Energía en capacitor:  U = ½ C V²
Ohm / potencia:        V = I R           P = V I = I² R
Resistencias:          Rs = Σ Ri         1/Rp = Σ 1/Ri
Kirchhoff:             Σ I(nodo) = 0     Σ ΔV(malla) = 0
Circuito RC:           q(t) = Q(1 - e^(-t/RC))   constante de tiempo τ = RC
Fuerza magnética:      F = q v × B        F = I L × B
Faraday:               ε = -dΦ_B/dt
```

### Ejemplos resueltos

1. **Coulomb**: dos cargas de +2 µC y -3 µC separadas 0,30 m. `F = 8,99e9 · (2e-6)(3e-6)/0,09 = 0,60 N`, atractiva.
2. **Resistencias**: 6 Ω en paralelo con 3 Ω: `Rp = (6·3)/(6+3) = 2 Ω`. Con una fuente de 12 V la corriente total es 6 A.
3. **Capacitores**: 4 µF y 6 µF en serie: `Ceq = 24/10 = 2,4 µF`.

### Relación con otras materias

- Prelación: [[Física I]] (fuerzas, trabajo y energía). Correquisito: [[Laboratorio de Física II]].
- Desbloquea [[Fundamentos de Lógica Digital]] (semiconductores, niveles de tensión, familias TTL/CMOS) y, más adelante, [[Automatización]].
- Usa el cálculo vectorial y las integrales de línea/superficie de [[Matemática III]] y [[Matemática IV]] (teorema de la divergencia ↔ Gauss; Stokes ↔ Ampère/Faraday).

### Evaluación y consejos de estudio

- Resolver muchos problemas del libro; la comprensión conceptual (dibujar líneas de campo, signos de carga) evita errores de signo.
- Mantener unidades SI en cada paso y usar notación científica.
- Antes de usar Gauss, identificar la simetría; si no existe, integrar con Coulomb.
- Los apuntes del Material son "tips" para estudiar con el libro, no sustituyen la lectura del texto.
- Ponderación y fechas de parciales: verificar con el programa oficial.

### Bibliografía recomendada

- Sears, Zemansky, Young, Freedman. *Física Universitaria con Física Moderna*, Vol. 2, 12.ª ed., Pearson.
- Serway, R. *Física para ciencias e ingeniería*, Vol. 2.
- Resnick, Halliday, Krane. *Física*, Vol. 2.

### Recursos del Material/

- [Carga Electrica y Campo Electrico v.9.pdf](Material/Carga%20Electrica%20y%20Campo%20Electrico%20v.9.pdf): "Lección 1, tips del libro", cap. 21 de Sears-Zemansky: carga, formas de cargar un cuerpo, interacciones.
- [Sears_Zemansky_LIBRO-signed.pdf](Material/Sears_Zemansky_LIBRO-signed.pdf): libro completo *Física Universitaria con Física Moderna*, Vol. 2 (900 páginas).
- [Tarea 1.docx](Material/Tarea%201.docx): tarea de noviembre de 2024 sobre valor absoluto (definición, propiedades, ejemplos).
