---
tags: [clase, electiva]
materia: Gestión Tecnológica
fuente: "conocimiento general"
---
# GT 05 - Propiedad intelectual

Materia: [[Gestión Tecnológica]]
Anterior: [[GT 04 - Transferencia de tecnología y licenciamiento]]
Siguiente: [[GT 06 - Evaluación de proyectos tecnológicos, incubadoras y políticas CyT]]

## Contexto y objetivo
La **propiedad intelectual** (PI) otorga derechos exclusivos sobre creaciones del intelecto y signos distintivos. Permite proteger, licenciar y valorar la tecnología. El objetivo es distinguir las figuras (patentes, marcas, derechos de autor, secretos, diseños), conocer los requisitos de patentabilidad y entender los tipos de licencia de software, incluido el software libre.

## Teoría

### Figuras de protección
| Figura | Protege | Requisito clave | Duración (referencia) |
|---|---|---|---|
| **Patente de invención** | Soluciones técnicas (producto o procedimiento) | Novedad, nivel inventivo, aplicación industrial | 20 años desde la solicitud (referencia general, ADPIC/TRIPS) |
| **Modelo de utilidad** | Mejoras técnicas menores | Novedad, utilidad | Variable según el país |
| **Diseño industrial** | Apariencia estética | Novedad, carácter singular | Variable (renovable) |
| **Marca** | Signos que distinguen productos o servicios | Distintividad, registro | 10 años renovables (referencia) |
| **Derecho de autor** | Obras literarias, artísticas, software | Originalidad; nace con la creación | Vida del autor + 50 a 70 años (varía) |
| **Secreto empresarial** | Información confidencial con valor | Medidas razonables de secreto | Indefinida mientras se mantenga secreto |
| **Denominación de origen** | Producto ligado a un lugar | Origen y calidad | Mientras se cumpla |

Los plazos son referenciales: **verificar con la ley vigente y el programa oficial**. Autoridad en Venezuela: el SAPI (Servicio Autónomo de la Propiedad Intelectual); verificar competencias actuales.

### Patentes
- **Reivindicaciones**: delimitan el alcance legal; la descripción debe permitir reproducir la invención.
- **Territorialidad**: la patente rige solo en el país donde se concede; el **PCT** (Tratado de Cooperación en materia de Patentes) permite solicitud internacional unificada.
- **Libertad de operación (FTO)**: análisis de si se puede explotar sin infringir patentes de terceros.
- **Estado de la técnica**: todo lo divulgado antes de la solicitud destruye la novedad (incluidas las propias publicaciones).
- Qué no es patentable (en general): descubrimientos, teorías científicas, métodos matemáticos y, según la legislación, programas de computación "como tales".

### Software: derechos de autor y licencias
El software se protege principalmente por **derecho de autor** (código fuente y objeto). Tipos de licencia:
- **Propietaria**: el código no se entrega; uso limitado por EULA.
- **Software libre (Free Software, FSF)**: cuatro libertades (usar, estudiar, copiar, modificar). **Copyleft** fuerte: GPL (obras derivadas deben mantener la licencia). **Copyleft débil**: LGPL, MPL.
- **Código abierto (Open Source, OSI)**: licencias permisivas como MIT, BSD, Apache 2.0 (permiten uso en software propietario con atribución; Apache incluye cláusula de patentes).
- **Creative Commons** para contenido (CC BY, CC BY-SA, CC BY-NC...).
- **Dominio público**.
Compatibilidad entre licencias es un riesgo de cumplimiento (auditoría de dependencias).

### Estrategia de PI
Patentar vs. mantener en secreto (la patente revela la invención; el secreto no protege contra ingeniería inversa legítima). **Portafolio defensivo**, licenciamiento cruzado, publicación defensiva. Titularidad de resultados de empleados y estudiantes: definir por contrato (ver [[GT 04 - Transferencia de tecnología y licenciamiento]]).

### Valoración
Métodos de costo, mercado e ingresos. Ejemplo de ingresos: $V=\sum_t \dfrac{\Delta FC_t}{(1+i)^t}$ con $\Delta FC$ el flujo atribuible a la protección.

## Ejemplo resuelto: decidir entre patente y secreto
Una startup desarrolla un algoritmo de calibración de sensores (hipotético). Opciones:
- **Patente**: costo estimado 15 000 USD (redacción, tasas y costos de tres países), protección de 20 años; revela el método. Probabilidad de concesión 60 %. Beneficio si se concede: licencias por 80 000 USD en valor actual.
 $VE = 0{,}6 \times 80\,000 - 15\,000 = 33\,000$ USD.
- **Secreto**: costo 2 000 USD (contratos, controles). Riesgo de que un competidor lo replique por ingeniería inversa en 2 años: 50 %; si ocurre, el beneficio cae a 20 000 USD; si no, 60 000 USD.
 $VE = 0{,}5\times 60\,000+0{,}5\times 20\,000-2\,000=38\,000$ USD.

El secreto resulta algo mejor en este caso numérico, pero la decisión debe considerar: si el algoritmo es **observable en el producto** (fácil de invertir) conviene patentar; si es un proceso interno, el secreto es viable. También cuentan los inversionistas (suelen valorar patentes) y la posibilidad de licenciar. El cálculo sirve para ordenar la discusión, no para sustituir la asesoría de un agente de propiedad industrial.

### Lista de verificación para publicar código
1. ¿Hay dependencias GPL? 2. ¿Se eligió licencia y se incluyó el archivo LICENSE? 3. ¿Están los encabezados de autoría? 4. ¿Hay datos sensibles en el repositorio? 5. ¿La institución es titular de lo creado en horas de trabajo?

## Errores comunes
- Divulgar la invención (artículo, demo pública) antes de solicitar la patente.
- Creer que "gratis" significa "sin licencia": el software libre tiene condiciones.
- Registrar una marca sin búsqueda de anterioridad.
- No dejar por escrito la titularidad de lo desarrollado por colaboradores.
- Asumir que una patente nacional protege en el exterior.

## Ejercicios propuestos
1. Clasifique la protección adecuada para (a) el logotipo; (b) el código fuente; (c) un nuevo procedimiento de purificación; (d) la fórmula secreta de una salsa. *Respuesta: (a) marca; (b) derecho de autor; (c) patente; (d) secreto empresarial.*
2. Diferencie GPL y MIT. *Respuesta: GPL exige mantener la licencia en obras derivadas; MIT permite integrarlo en software propietario con atribución.*
3. Con probabilidad de concesión 40 %, beneficio 100 000 y costo 20 000, ¿conviene patentar según el valor esperado? *Respuesta: VE = 40 000-20 000 = 20 000 > 0; sí, con las reservas de riesgo.*

## Conexiones con otras materias
[[Legislación, Valores y Proyecto de País]], [[Delitos informáticos y firma electrónica]], [[Ingeniería de Software]], [[Formación de Emprendedores]], [[Ciencia y Sociedad I]].

## Fuente
ADPIC/TRIPS, Convenio de París, PCT, Convenio de Berna; Escorsa y Valls. Plazos y requisitos a verificar con la legislación vigente y el programa oficial. Cifras ilustrativas.
