---
tags: [clase, electiva]
materia: Interfaces Digitales Biomédicas
---
# Interfaces Digitales Biomédicas - Estándares Clínicos y Seguridad Eléctrica

Materia: [[Interfaces Digitales Biomédicas]]  
Anterior: [[Interfaces Digitales Biomédicas - Procesamiento Digital de Bioseñales]]  
Siguiente: —

## Contexto y objetivo

Conocer los **estándares de interoperabilidad clínica** (**HL7 / FHIR, DICOM**) para integrar dispositivos con historias clínicas electrónicas y sistemas de imágenes, así como los principios fundamentales de **seguridad eléctrica del paciente** bajo la norma **IEC 60601** (macroshock, microshock, corrientes de fuga y aislamiento galvánico).

## 1. Seguridad eléctrica del paciente (IEC 60601-1)

Cuando conectamos electrodos de baja impedancia directamente sobre la piel (o catéteres cerca del corazón), eliminamos la resistencia natural de la piel seca, exponiendo al paciente a dos riesgos críticos:

- **Macroshock**: corriente eléctrica que entra por la superficie corporal externa (ej. contacto accidental con fase de $120\text{ V}$). A partir de $10\text{ – }20\text{ mA}$ provoca contracción muscular sostenida (*let-go threshold*) y por encima de $75\text{ – }100\text{ mA}$ puede inducir fibrilación ventricular.
- **Microshock**: corriente diminuta aplicada directamente al miocardio (por ejemplo, a través de un catéter intracardíaco o marcapasos temporal). **Corrientes tan pequeñas como $10\text{ – }100\;\mu\text{A}$** pueden causar fibrilación ventricular mortal.

### Clasificación de partes aplicadas (IEC 60601)
- **Tipo B (*Body*)**: contacto externo sin conexión directa al corazón (límite corriente de fuga normal $\le 100\;\mu\text{A}$).
- **Tipo BF (*Body Floating*)**: parte aplicada aislada galvánicamente (flotante) del resto del equipo y tierra.
- **Tipo CF (*Cardiac Floating*)**: máxima protección, apta para contacto cardíaco directo (límite corriente de fuga normal $\le 10\;\mu\text{A}$).

### Técnicas de protección en el diseño de hardware
1. **Aislamiento galvánico**: separar la etapa conectada al paciente de la etapa conectada a la red eléctrica/PC usando **aisladores digitales** (ej. ADuM1401, optoacopladores) y **convertidores DC-DC aislados** con tensión de ruptura de $2.5\text{ – }5\text{ kV}$.
2. **Alimentación por batería**: elimina la conexión galvánica con la red eléctrica; combinada con transmisión **BLE/Wi-Fi**, ofrece aislamiento natural ideal para prototipos seguros.
3. **Protección contra desfibrilación**: diodos TVS y resistencias limitadoras de alta tensión en la entrada del amplificador para soportar pulsos de varios kV sin dañar el equipo ni desviar corriente.

## 2. Estándares de interoperabilidad en salud

Para que una interfaz biomédica se integre en un hospital moderno, los datos deben seguir formatos estandarizados:

- **HL7 (Health Level Seven) y FHIR**: estándares para intercambio de datos clínicos administrativos y médicos (observaciones, signos vitales, resultados de laboratorio) entre equipos, servidores y Expedientes Clínicos Electrónicos (EHR). **FHIR** (*Fast Healthcare Interoperability Resources*) utiliza APIs RESTful modernas con JSON/XML.
- **DICOM (*Digital Imaging and Communications in Medicine*)**: estándar universal para almacenamiento, visualización y transmisión de imágenes médicas (rayos X, tomografía, resonancia magnética, ultrasonido) y formas de onda asociadas, encapsulando metadatos del paciente junto a la imagen.

## Errores comunes

- Conectar un prototipo alimentado por el puerto USB de una laptop enchufada a la toma de pared directamente a electrodos en el pecho de una persona sin **aislamiento galvánico**: cualquier falla en el cargador puede exponer al usuario a la tensión de red.
- Tratar el almacenamiento de bioseñales con archivos CSV ad-hoc sin considerar metadatos estándar (frecuencia de muestreo, unidades, calibración, identificación HL7/DICOM).

## Ejercicios propuestos

1. ¿Por qué un equipo conectado a un catéter cardíaco debe ser Tipo **CF** y no Tipo **B**?
   - *Respuesta:* Porque en contacto directo con el miocardio el umbral de **microshock** es del orden de decenas de $\mu\text{A}$; el tipo CF garantiza aislamiento flotante y limita la corriente de fuga normal a $\le 10\;\mu\text{A}$, muy por debajo del umbral de fibrilación.

## Conexiones

- Anterior: [[Interfaces Digitales Biomédicas - Procesamiento Digital de Bioseñales]]
- Materia: [[Interfaces Digitales Biomédicas]]
- Materias relacionadas: [[Física II]], [[Organización del Computador]], [[Introducción a las Telecomunicaciones]]

## Fuente

- Temario de [[Interfaces Digitales Biomédicas]] (Webster, Cap. 14 *Electrical Safety*; norma IEC 60601; HL7 FHIR y DICOM).
