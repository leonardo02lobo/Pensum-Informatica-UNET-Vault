---
tags: [moc, drive, recursos, guia]
---
# Recursos Drive UNET · Índice y Guía de Contribución

Mapa central de consulta para el material universitario recopilado desde Google Drive (`loboleonardo75@gmail.com` y `leonardo.lobo@unet.edu.ve`) en la rama `investigacion-drive`, junto con la guía práctica para mantener y ampliar este vault de **[[Pensum Ingeniería Informática UNET]]**. Ver también [[Fuentes Oficiales UNET]] para códigos, UC, reglamentos y enlaces de RIUNET.

---

## 1. Estructura de esta Red (Vault de Obsidian)

El repositorio está organizado en torno al pensum oficial de **Ingeniería en Informática (UNET)**:

- **`Pensum Ingeniería Informática UNET.md`**: Mapa de contenido (MOC) principal con los 10 semestres y las 13 electivas.
- **`Semestre I/` a `Semestre X/`**: Carpetas por semestre; dentro, una carpeta por asignatura.
- **`Electivas/`**: Asignaturas electivas del pensum.
- **Dentro de cada asignatura**:
  - `<Materia>.md`: Ficha principal (prelaciones, materias que desbloquea, contenido programático, conceptos clave, ejemplos, bibliografía y recursos).
  - `Clases/`: Notas detalladas por tema, encadenadas con `Anterior:` / `Siguiente:`, ejemplos resueltos, errores comunes y sección `## Conexiones` (`[[...]]`).
  - Notas de proyecto/caso de estudio en la raíz de la materia (ej. `[[Tiny++ Compilador e IDE]]`, `[[Proyecto HIDRA - Arquitectura n8n y Ciberseguridad]]`, `[[Sistema Comedor Universitario UNET (CSC-P 2026)]]`).
  - `Material/` *(excluido en `.gitignore`)*: PDFs, videos, zips y ejecutables locales pesados.

---

## 2. Cómo Agregar Nuevo Conocimiento (Ejemplo y Plantilla)

Para que el **Grafo de Obsidian** (`Ctrl + G`) siga conectado y uniforme:

1. **Ubica la materia** en `Semestre X/<Materia>/` o `Electivas/<Materia>/`.
2. **Si es un tema de clase nuevo**, créalo en `Clases/<Materia> - <Tema>.md` usando esta plantilla:

```markdown
---
tags: [clase, semestre-VI]
materia: Sistemas Operativos
---
# Sistemas Operativos - <Título del Tema>

Materia: [[Sistemas Operativos]]
Anterior: [[<Nota anterior o _Ninguna_>]]
Siguiente: [[<Nota siguiente o _Ninguna_>]]

## Contexto y objetivo
Breve explicación del tema y su relación con el programa de la UNET.

## Desarrollo / Conceptos clave
- Punto 1
- Punto 2

## Ejemplo práctico o código
```c
// Código o procedimiento reproducible
```

## Errores comunes
- Error frecuente y cómo evitarlo.

## Conexiones
- Se apoya en [[Otra Materia]] y se aplica en [[Materia Siguiente]].
```

3. **Enlaza la nota nueva** desde `<Materia>.md` (en `## Notas en el vault` o en el tema correspondiente) y, si aplica, actualiza `Anterior:` / `Siguiente:` de las notas vecinas.
4. **Si el archivo fuente es pesado** (PDF, MP4, ZIP), guárdalo en `Material/` (ignorado por Git) o referencia su enlace en Google Drive dentro de la sección `### Recursos`.

---

## 3. Herramientas y Stack Tecnológico a la Mano

| Área / Materias | Herramientas, Lenguajes y Plataformas Utilizadas |
|---|---|
| **Algoritmia y Programación** ([[Computación I]], [[Programación I]], [[Programación II]], [[Estructura de Datos]]) | PSeInt (`.psc`), C / C++ (`gcc`, `g++`, `template`, punteros, bits, archivos binarios), Java (JDK 8, NetBeans, AWT/Swing), PHP + MySQL (MVC), Python |
| **Bases de Datos** ([[Base de Datos I]], [[Administración de Base de Datos]]) | Oracle Database 18c XE (Docker `gvenzl/oracle-xe:18-slim`), SQL*Plus, Oracle SQL Developer & Data Modeler, PL/SQL, marco DAMA-DMBOK |
| **Sistemas y Redes** ([[Sistemas Operativos]], [[Comunicaciones I]], [[Introducción a las Telecomunicaciones]]) | Linux (`/proc`, `ps`, `pstree`, `bash`), C (`fork`, `execv`, `wait`, `pipe`, `mmap`, semáforos), multisim (`.ms14`), GPON, 5G SBA |
| **Compiladores** ([[Compiladores e Intérpretes]]) | Java, JFlex, CUP, Tiny++ / Tiny Machine (`TM.C`) |
| **Ingeniería Web y Proyecto** ([[Servicio Comunitario]], [[Desarrollo de Aplicaciones Web]], [[Automatización]]) | FastAPI (Python 3.12), SQLAlchemy, Alembic, PostgreSQL 16, React 19 + TypeScript + Vite + Tailwind, Tauri 2, n8n, Vercel, OWASP ZAP v2.17.0 |
| **Matemática, Física y Simulación** ([[Laboratorio de Física II]], [[Análisis Numérico]], [[Investigación de Operaciones II]], [[Simulación de Sistemas]], [[Finanzas para Ingenieros]]) | Python 3.11 + NumPy, PhET *Cargas y Campos*, MATLAB / Octave (`.m`), Algoritmo Genético (Java/Python), Simulación de Eventos Discretos (LEF) |

---

## 4. Inventario Organizado de Google Drive

> Cuentas consultadas: **Personal** (`loboleonardo75@gmail.com`) y **UNET** (`leonardo.lobo@unet.edu.ve`).

### Semestre I
- **[[Matemática I]]**
  - `GUIAS` (UNET): [Carpeta Matemática I](https://drive.google.com/drive/folders/1VPPi9ZnzS2_a0OqsKc4Rc8APnQvxbgob) — Límites, línea recta, gráficas, aplicaciones de derivadas, cronograma `2023-1`.
- **[[Computación I]]**
  - Carpeta UNET: [Computación I](https://drive.google.com/drive/folders/1RMw-1DP_hX69R7WaNDhdQtsf-OX5fC34) — Parciales en C (`Embajada.c`, `Recursos Humanos.c`, *Juego de barcos*) y pseudocódigo PSeInt en carpeta `Otros` ([Enlace](https://drive.google.com/drive/folders/1e1nXPrZuUNRNqJsxsJyhSrHdvoxA6Dk6): `CITA MEDICA.psc`, `JUBILACIONES.psc`, etc.).
- **[[Matemática Discreta]]**
  - Carpetas UNET: [Matemática Discreta (UNET)](https://drive.google.com/drive/folders/1EGBV-zeu-_uyaqDwfSVX2iXXSgFKY2B7) y [Matemática Discreta (Raíz)](https://drive.google.com/drive/folders/1TP-uEwyo2prXRP-8PpERy85zq-72crRw) — [Guía Didáctica 2022-3](https://drive.google.com/file/d/1_x_LRYL3ixCGD0AYN3DY_0C3kClRDUCB/view?usp=drivesdk), libros de Johnsonbaugh y Murillo Tsijli, relaciones binarias, digrafos, matrices de adyacencia/incidencia y recorridos de árboles.
- **[[Introducción a la Ingeniería Informática]]**
  - Carpeta UNET: [Introducción a la Ing. Informática](https://drive.google.com/drive/folders/1VdArZHg-KARkfttkthRt3TJDrSyrJndA) — Trabajos sobre tecnología en el entorno laboral, Internet y administración de datos.
- **[[Efectividad Personal]]**
  - Carpeta UNET (`ELECTIVIDAD PERSONAL`): `Construyendo significados-Efectividad Personal`.

### Semestre II
- **[[Programación I]]**
  - Sinóptico y analítico `0416202T`, clases PDF completas de **C++** (POO, herencia, polimorfismo, punteros, bits, separación de tokens) y **Java** (POO, herencia, polimorfismo, clases abstractas, interfaces, excepciones, archivos, AWT/Swing): [Carpeta Programación I](https://drive.google.com/drive/folders/1tbIZCc3ZcO7I1k8zfv3Bz17HRBnv1rUs), [Parciales de Programación 1](https://drive.google.com/drive/folders/1jJyq3mZ4Qp4fl1PsLX2pS_jQTB67ilHo).
  - Proyectos finales en Java: *Space Invaders* ([Carpeta](https://drive.google.com/drive/folders/18UdCJ1tY0ykiXGBbwHRQuKAEnJnoL_D2)) y *Sopa de Letras* ([Carpeta](https://drive.google.com/drive/folders/1_2s9f8tpESzedwrwcJe6RSNwX18hIp9E)).
  - **Videos de preparadurías** impartidas por Leonardo Lobo: [videos de prepas](https://drive.google.com/drive/folders/1zZCvN7UnvhkdebF-UWD_QqyGnrNOE-pw) (Vectores/Matrices/Listas, Excepciones/Archivos, POO en Java, Java Swing, Animaciones).
- **[[Física I]] y [[Laboratorio de Física I]]**
  - Parciales 1 y 3 de Física I (vectores, cinemática, dinámica), informes de inercia, choques y proyecto *Molino de Agua*.
- **[[Química General I]]**
  - `quimica.docx` y guías PDF.

### Semestre III
- **[[Estructura de Datos]]**
  - Material completo de C++ (`0416304T`, Prof. David Ortiz): [Carpeta compartida](https://drive.google.com/drive/folders/1hotk7daZnrYEKSdsMCE9NC7yX7MOO-Hu) y [Carpeta UNET](https://drive.google.com/drive/folders/1LfX_oJs06SpDHqouIxj3ODFLw2nLzWz3) — Archivos binarios/texto, ordenamiento interno/externo, búsqueda/hashing, pilas/colas/listas, árboles binarios/AVL (`ArbolAVL.h`), grafos y proyectos 1, 2 y 3.
- **[[Laboratorio de Física II]]**
  - [Carpeta Laboratorio de Física II](https://drive.google.com/drive/folders/13rKv0LjYwlW8cNorYbBrGkAsvhwX1qGA) — [Prelaboratorio_Campo_Electrico_Fisica_II.docx](https://docs.google.com/document/d/1o5WpJU455aoxNpMLOrjwcjDvJiTMA0y0/edit?usp=drivesdk). Nota integrada en [[Laboratorio de Física II - Campo Eléctrico y Superficies Equipotenciales]].
- **[[Física II]]**, **[[Matemática III]]**, **[[Inglés I]]**, **[[Teoría General de Sistemas]]**
  - Guías y parciales de TGS, Sears-Zemansky Vol. 2, ejercicios de Matemática III (velocidad, aceleración, paraboloide hiperbólico).

### Semestre IV
- **[[Programación II]]**
  - Analítico `0425401T`, Guía didáctica SEED UNET 4.0, estilos de programación (K&R, Allman, GNU), backtracking, PHP + MySQL (MVC), parciales `2025-1`.
- **[[Fundamentos de Lógica Digital]]**
  - Analítico, guía didáctica, libro Tocci (*Sistemas Digitales*), presentaciones con audio, 11 exámenes históricos y proyecto en Multisim (`.ms14`).
- **[[Estadística I]]**, **[[Matemática IV]]**, **[[Ciencia y Sociedad I]]**, **[[Inglés II]]**
  - Guías resumen de Estadística I (Descriptiva, Probabilidad, Distribuciones), libros de Matemática IV (Stewart, Larson, Edwards Penney), video de exposición de Inglés II.

### Semestre V
- **[[Base de Datos I]]**
  - Repositorio completo **Equipo 9 (2025-1)** y **Equipo 4 (2025-2)** (Temas I al VI: DAMA-DMBOK, Oracle Data Modeler, DDL/DML 16 tablas DB-GRV, SQL avanzado y PL/SQL con triggers, cursores y paquetes): [Tema 1](https://drive.google.com/drive/folders/1ebrGcGsMoCyq0GKRRwID2dOSPXr9vdUa) · [Tema 2](https://drive.google.com/drive/folders/1kkx3DYHP6aMrcUWpGfnosM3I_OCLu0si) · [Tema 3](https://drive.google.com/drive/folders/1YgO1oe7xu_nwVcOktf73oGOtTpsOl_mO) · [Tema 4](https://drive.google.com/drive/folders/1OHk5oJ7oQ1GL43x6Czmsoy1_GIjePCFf) · [Tema 5](https://drive.google.com/drive/folders/1t-6vGLO0tdvqBTEcQ4-RA-A9bKaI7i-c) · [Tema 6](https://drive.google.com/drive/folders/1ByEhaTCwF8uRLnj27IWvHbdKE43ajGa5). Nota integrada en [[Base de Datos I - Caso Transversal DB-GRV y PL-SQL]].
- **[[Automatización]]**
  - **Proyecto HIDRA** (Grupo 4, 2026): [Informe-Lider-Proyecto-HIDRA.docx](https://docs.google.com/document/d/1s2DUp0DWsFLfGwXQpeVLDCm6vNU1mdxP/edit?usp=drivesdk) y [Auditoria-Ciberseguridad-Hidra](https://docs.google.com/document/d/1VnX8nrE5jgpvMCPlf3uQWgMVRaMXH5c8rRwcMM57yl4/edit?usp=drivesdk). Nota integrada en [[Proyecto HIDRA - Arquitectura n8n y Ciberseguridad]].
- **[[Análisis Numérico]]** (*Métodos Numéricos*)
  - Sinóptico, planificación y scripts `.m` (MATLAB/Octave) para Temas 1–6 (Bisección, Newton-Raphson, Secante, Lagrange, Gauss, LU, Gauss-Seidel, SOR, Trapecio, Simpson).
- **[[Estadística II]]**
  - [Trabajo Estadistica II](https://docs.google.com/document/d/1iaLtNZilHui418MhPms50EE9DPfjBliVJVgqob7cB84/edit?usp=drivesdk) (intervalos de confianza, ANOVA, regresión lineal y correlación) + guías 1P, 2P, 3P y tablas estadísticas.
- **[[Organización del Computador]]**
  - Línea temporal de microprocesadores (Intel `8086` a `Alder Lake`, AMD `K7` a `Zen 4`, Apple `M3`).
- **[[Proyecto Servicio Comunitario]]**
  - [Informe Inicial Comedor UNET](https://docs.google.com/document/d/10qhzh1-KrCy3_7Z8Avtkxk0IKeOzeq3eBiHbyqKvksk/edit?usp=drivesdk) y cartas de autorización/autofinanciamiento.

### Semestre VI
- **[[Sistemas Operativos]]**
  - Práctica 1/2 (Linux/procesos), Práctica 5 ([Memory Monitor](https://drive.google.com/drive/folders/1zX4Uzww_kVJhq2GQV56I0dVVGqMCbVDM)) y Práctica 6 ([Túneles y semáforos en C](https://drive.google.com/drive/folders/1AzZ4QTmk17gGzU6WFYDg9LG_ObX0wUa9)). Nota integrada en [[Sistemas Operativos - Prácticas Linux, Memory Monitor y Túneles IPC en C]].
- **[[Servicio Comunitario]]**
  - Carpeta [Cartas de Servicio Comunitario](https://drive.google.com/drive/folders/18cDnPQMG4WmIkl1pscMLvl4nRUhwDBye): [Manual y Documentación Técnica](https://drive.google.com/file/d/1efyX74Bt7ulDlPC2udoOMLj3gJkvmQkt/view?usp=drivesdk), [Informe Final](https://docs.google.com/document/d/1WeYTBzbHXIfH1o9iCsU17wk-sfkgg1bu/edit?usp=drivesdk), formatos `CSC-04`, `CSC-06`, `CSC-10` e Impacto Social. Nota integrada en [[Sistema Comedor Universitario UNET (CSC-P 2026)]].
- **[[Sistema de Información I]]**
  - [Actores y Casos de Uso (Comedor UNET)](https://docs.google.com/document/d/1yppcSLI5BF4iLSAIksVASMeRn5TUoVAI5D-8OVMT6g8/edit?usp=drivesdk) y [Parcial 2 (PIECES, DER, DFD)](https://docs.google.com/document/d/1eU-sxqSd0wfCNoHyuilu0sls4dPErha0IuasGdO4yjs/edit?usp=drivesdk). Nota integrada en [[Sistema de Información I - Casos de Uso, PIECES y DFD (Comedor UNET)]].
- **[[Investigación de Operaciones I]]**, **[[Economía]]**
  - Ejercicio de transbordo, libro de Programación Lineal y resúmenes de Economía (1er a 3er parcial).

### Semestre VII
- **[[Compiladores e Intérpretes]]**
  - `Classroom/Compiladores Intensivo 2026 1`: Parcial I (JFlex, DFA/NFA, Thompson, traducción dirigida por sintaxis) y Parcial II (conjuntos Primeros, Siguientes y Predicción LL).
- **[[Investigación de Operaciones II]]**
  - [Caso Estudio Teoría de Inventarios (s, S)](https://docs.google.com/document/d/1c1pvWzIaALkcncVXr3Xnku9d_QnvJYHXez0AlLfz1yQ/edit?usp=drivesdk), [Exposición Colas M/M/1](https://docs.google.com/presentation/d/1m6KTgQfj3HUtw9-NlSCpDGPXKaYkqc48bqbUKT0Qkg0/edit?usp=drivesdk) y [IV Parcial Tema 7 (Redes y PERT/CPM)](https://docs.google.com/document/d/1fgZs1HtWV9FR9078xXfApUykrmhBfp2wOnlP6cS2PR4/edit?usp=drivesdk).
- **[[Ingeniería Económica]]**
  - Guías Temas 1 al 7 y video sobre inflación.

### Semestre VIII y IX
- **[[Simulación de Sistemas]]**
  - [Parcial 2: Modelo formal Age of Conquest](https://docs.google.com/document/d/1ph-_pmDts7lQXeuTwxlmkzu5trUcDJAZHlR0w7U5FH0/edit?usp=drivesdk) (eventos discretos, LEF, IA, traza).
- **[[Finanzas para Ingenieros]]**
  - Proyecto de Algoritmo Genético + Markowitz para portafolios de criptomonedas (`algoritmoGenetico.py` / Java) y guías de Tema 1 y 2.
- **[[Legislación, Valores y Proyecto de País]]**
  - Ley de Ejercicio de la Ingeniería, LOTTT, Delitos Informáticos, Firma Electrónica, Registro Mercantil y ensayos.

### Electivas y Actividades Institucionales
- **[[Administración de Base de Datos]]** (`0423805T`): Serie completa de 7 prácticas e informes sobre **Oracle 18c XE** + `Guia_Didáctica_ABD 2026-1`. Nota integrada en [[Administración de Base de Datos - Prácticas Oracle 18c XE (DBCA, Arranque, Redo Logs y Seguridad)]].
- **[[Introducción a las Telecomunicaciones]]**: Parciales 1 y 2, [Red GPON](https://docs.google.com/document/d/1Am8W1_dhQIcK8Da2hRhQADH_0wS_3ECBtU48p706UT8/edit?usp=drivesdk), [Red 5G](https://docs.google.com/document/d/11RaOMwsqrCJ7_2HyrJlfIc1T-38j1PANzId5gjCUFIo/edit?usp=drivesdk), [Radio Enlace](https://docs.google.com/document/d/1GBvj6xf2WfWFoWDM-Vy4Rr6DU-xm6aNyupGX-ue8U3E/edit?usp=drivesdk), [Comparación Medios Físicos](https://docs.google.com/document/d/1p9SXKsOEbd4nTSpU0fY69i7NBiklty91hWSv0GS51Jo/edit?usp=drivesdk). Nota integrada en [[Introducción a las Telecomunicaciones - Medios, Radioenlaces, GPON y 5G]].
- **[[Aprendizaje Automático]]**: Defensa AutoML (`Grupo 5`), carpeta [datos_ensembl](https://drive.google.com/drive/folders/11htu4XMyuUZJP5La9gdRStLXN5Zgo-Pd), libros de Géron (Scikit-Learn/Keras/TF) y Witten (Data Mining).
- **[[Desarrollo de Aplicaciones Web]]**: Carpeta [Documentacion](https://drive.google.com/drive/folders/1t5Mgpq-yato-QvjQdgFQdKEzseY7Cwha) (Tailwind, JavaScript, Flask, Reflex, Electron).
- **[[Formación de Emprendedores]]**: Parcial 2 (*Diseño Espiral*, Lean Startup), entrevista a emprendedor y videos de productividad.
- **Hello World Cup (2025–2026)**: [Carpeta Hello World Cup](https://drive.google.com/drive/folders/1mCJe_tazJghCbCHl6E5S5pe54FXYLwSs) — Reglamentos Básica/Avanzada, baremo de puntaje (Computación I, Programación I, Estructura de Datos), cartas y logística.
