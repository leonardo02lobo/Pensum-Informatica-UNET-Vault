---
tags: [materia, semestre-IV]
semestre: IV
---
# Fundamentos de Lógica Digital

**Semestre:** [[Semestre IV]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Programación I]]
- [[Física II]]

## Desbloquea
- [[Organización del Computador]]
- [[Automatización]]

## Apuntes

### Descripción general y objetivos

Fundamentos de Lógica Digital (código 0425404T en el programa analítico; las diapositivas lo citan como 0435406T, **verificar** cuál es el vigente) es el primer curso de **diseño digital**: del álgebra booleana a los bloques MSI, los circuitos aritméticos y la ALU. Prelaciones: [[Programación I]] y [[Física II]]. Desbloquea [[Organización del Computador]] y [[Automatización]]. Dictado por el Departamento de Ingeniería Informática (Prof. Pablo E. Hernández B. en las presentaciones).

Objetivo general por unidades del analítico:
- U-I: estudiar los conceptos básicos de circuitos integrados y las principales tecnologías.
- U-II: diseñar circuitos combinacionales mediante bloques funcionales.
- U-III: estudiar el funcionamiento y aplicaciones de los circuitos lógicos MSI.
- U-IV: estudiar el funcionamiento y aplicaciones de los circuitos aritméticos.
Los parciales del Material siguen incluso contenido posterior (contadores, registros, circuitos secuenciales con CI como el 74LS191), por lo que el curso suele extenderse a lógica secuencial; verificar con el docente.

### Contenido programático

#### Unidad I. Familias lógicas
1. Descripción general de los circuitos integrados (CI): encapsulados, fabricación sobre oblea de silicio.
2. **Niveles de integración**: SSI, MSI, LSI, VLSI, ULSI, GLSI (más de un millón de componentes por chip); ley de Moore.
3. **Familias lógicas**: niveles lógicos, capacidad de carga (fan-out), retardo de propagación y disipación de potencia. TTL (series 74/54, S, LS, AS, ALS, F) y CMOS (4000, HC, LV, LVC...). Compatibilidad de corriente y tensión.

#### Unidad II. Diseño lógico combinacional
1. Compuertas AND, OR, NOT, XOR, XNOR, NAND, NOR; tablas de verdad; funciones lógicas.
2. Descripción algebraica y evaluación de circuitos; implementación a partir de expresiones.
3. **Universalidad** de NAND y NOR.
4. Simplificación: teoremas de Boole y De Morgan; **mapas de Karnaugh**.
5. Diseño de circuitos combinacionales y diseño modular/jerárquico.

#### Unidad III. Circuitos lógicos MSI
Codificadores y decodificadores (incluido codificador de prioridad y decodificador BCD a 7 segmentos), multiplexores y demultiplexores, comparadores de magnitud, implementación de funciones con MUX/decodificadores.

#### Unidad IV. Circuitos aritméticos
Representación con signo (signo-magnitud, complemento a 1 y a 2), semisumador y sumador completo, sumador paralelo (7483), restador, multiplicador, divisor y **ALU**.

### Conceptos clave

- **Nivel lógico**: rangos de tensión que se interpretan como 0 o 1 (VIL, VIH, VOL, VOH).
- **Fan-out**: cuántas entradas puede manejar una salida.
- **Retardo de propagación (tpd)** y **disipación de potencia**: cuenta de velocidad y consumo.
- **Activo en bajo**: la señal es válida con 0 (se dibuja un círculo).
- **Minitérmino/maxtérmino**; forma SOP y POS; condiciones indiferentes (X).
- **MSB / LSB**: bit más y menos significativo.

### Álgebra booleana y fórmulas

```
Identidad:    A + 0 = A      A · 1 = A
Nulo:         A + 1 = 1      A · 0 = 0
Idempotencia: A + A = A      A · A = A
Complemento:  A + A' = 1     A · A' = 0
Absorción:    A + A·B = A    A · (A + B) = A
De Morgan:    (A·B)' = A' + B'      (A+B)' = A'·B'
XOR:          A ⊕ B = A'B + AB'
Compatibilidad TTL/CMOS:  IOH max >= IIH max ; IOL max >= IIL max ; VOH min >= VIH min ; VOL max <= VIL max
Decodificador N a 2^N:    una sola salida activa
Multiplexor 2^N a 1:      Y = Σ mi · Di    (N líneas de selección)
Complemento a 2:          -x = (~x) + 1
Semisumador:      S = A ⊕ B        Cout = A·B
Sumador completo: S = A ⊕ B ⊕ Cin  Cout = AB + Cin(A ⊕ B)
```

### Ejemplos resueltos

1. **Simplificación con Karnaugh**: `F(A,B,C) = Σm(1,3,5,7)`. El mapa agrupa los cuatro unos (C = 1) y resulta `F = C`.
2. **Complemento a 2 (4 bits)**: -6 = 1010. Se niega 0110 -> 1001 y se suma 1 -> 1010. Suma (+4) + (-3): 0100 + 1101 = 1 0001 -> se descarta el acarreo, resultado 0001 = +1.
3. **Prioridad de 4 entradas** (tabla del Material): si x3=1 -> y1y0=11; si x3=0,x2=1 -> 10; si x2=0,x1=1 -> 01; si todas 0 -> 00.
4. **Función con MUX 4x1**: para `F = A'B + AB'` se conectan A,B a las selecciones y D0=0, D1=1, D2=1, D3=0 (XOR).

### Cómo se relaciona con otras materias

- Parte de [[Programación I]] (pensamiento algorítmico) y [[Física II]] (corriente, tensión, semiconductores).
- Desbloquea [[Organización del Computador]] (la ALU, registros y memorias son la base de la CPU) y [[Automatización]] (PLC, lógica de control).
- Conecta con [[Matemática Discreta]] (álgebra booleana, conjuntos y lógica).

### Evaluación y consejos de estudio

- Dos parciales principales con problemas aplicados (ej. control de llenado de un depósito con sensores y electroválvulas; contador módulo 150 con el CI 74LS191; diseño de registros con carga paralela y rotación). Hay también una modalidad de **primer proyecto en Multisim** (simulación). Ponderación: verificar con el programa oficial.
- Practicar con exámenes de cursos anteriores (disponibles en el Material, 2007 a 2011).
- Escribir siempre la tabla de verdad primero; simplificar con Karnaugh y comprobar con simulación.
- Usar Multisim (o Logisim/Falstad) para validar cada diseño antes del examen.
- Revisar hojas de datos (datasheet) de los CI: pines, niveles y tiempos.

### Bibliografía recomendada

- Tocci, R. *Sistemas digitales. Principios y aplicaciones*, Prentice Hall.
- Wakerly, J. *Diseño digital. Principios y prácticas*, Prentice Hall.
- Nelson, V. *Análisis y diseño de circuitos lógicos digitales*.
- Mano, M. *Diseño digital*.

### Recursos del Material/

- [Programa Analatico Fundamentos de logica digital.pdf](Material/Programa%20Analatico%20Fundamentos%20de%20logica%20digital.pdf): programa analítico por unidades.
- [Guia Didactica FDL.pdf](Material/Guia%20Didactica%20FDL.pdf): guía didáctica (documento escaneado, sin texto extraíble).
- [Presentación FLD con audio.ppsx](Material/Presentaci%C3%B3n%20FLD%20con%20audio.ppsx): presentación introductoria.
- [Sistemas_Digitales_Principios_y_Aplicaci.pdf](Material/Sistemas_Digitales_Principios_y_Aplicaci.pdf): libro de Tocci.
- Carpeta `1 er Parcial`: [unidad I FLD.pptx](Material/1%20er%20Parcial/unidad%20I%20FLD.pptx), [niveles de integración](Material/1%20er%20Parcial/nivels%20de%20integracion.pdf), [PROBLEMAS unidad I](Material/1%20er%20Parcial/PROBLEMAS%20unidad%20I.pdf) y parciales anteriores 2007-2011 en zip y carpeta.
- Carpeta `2do Parcial`: [unidad III](Material/2do%20Parcial/unidad%20III%20FLD.ppsx) (MSI), [unidad IVa](Material/2do%20Parcial/unidad%20IVa%20FLD.ppsx) y [IVb](Material/2do%20Parcial/unidad%20IVb%20FLD.ppsx) (aritméticos y ALU) y parciales anteriores en zip.
- Carpeta `Primer Proyecto en Multisim`: archivo `.ms14` del circuito, tres imágenes y zip con la entrega.
