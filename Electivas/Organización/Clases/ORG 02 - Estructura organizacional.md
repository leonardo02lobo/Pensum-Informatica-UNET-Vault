---
tags: [clase, electiva]
materia: Organización
fuente: "conocimiento general"
---
# ORG 02 - Estructura organizacional

Materia: [[Organización]]
Anterior: [[ORG 01 - Teorías de la organización]]
Siguiente: [[ORG 03 - Procesos y BPM]]

## Contexto y objetivo
La **estructura** es el patrón formal de división del trabajo y coordinación: quién hace qué, quién reporta a quién y cómo se decide. El objetivo es dominar los criterios de departamentalización, calcular amplitud de control, leer y elaborar organigramas, y elegir una configuración según Mintzberg.

## Teoría

### Elementos de diseño
1. **Especialización del trabajo**.
2. **Departamentalización**: agrupar puestos por función, producto, cliente, geografía o proceso.
3. **Cadena de mando**: autoridad (derecho de mandar) y responsabilidad; unidad de mando.
4. **Amplitud de control**: número de subordinados por jefe. Estructura **alta** (muchos niveles, amplitud pequeña) vs. **plana** (pocos niveles, amplitud grande).
5. **Centralización vs. descentralización** de decisiones.
6. **Formalización**: grado de reglas y procedimientos escritos.

### Tipos de estructura
- **Funcional**: áreas por especialidad (TI, finanzas, comercial). Eficiencia técnica; poca visión de conjunto.
- **Divisional**: por producto, región o cliente; autonomía, duplicación de recursos.
- **Matricial**: doble reporte (función y proyecto); flexible, pero conflicto de autoridad. Tipos: débil, equilibrada, fuerte (según el poder del gerente de proyecto).
- **Por proyectos / en red / virtual**.
- **Por equipos**; **orgánica ágil** (squads y tribus).

### Configuraciones de Mintzberg
Cinco partes: ápice estratégico, línea media, núcleo operativo, tecnoestructura, staff de apoyo. Mecanismos de coordinación y configuraciones:
- **Estructura simple** (supervisión directa): startups.
- **Burocracia maquinal** (normalización de procesos): producción masiva.
- **Burocracia profesional** (normalización de destrezas): hospitales, universidades.
- **Forma divisional** (normalización de resultados).
- **Adhocracia** (ajuste mutuo): innovación y proyectos.

### Organigramas
Representación gráfica: **vertical**, **horizontal**, **circular**. Contenido: unidades, niveles, líneas de autoridad (continuas), de asesoría o staff (discontinuas). Reglas: claridad, no sobrecargar, fecha de vigencia.
Descripción de cargos: nombre, objetivo, funciones, relaciones, perfil (formación, experiencia, competencias).

### Dimensionamiento
Número de niveles $N$ para $E$ empleados operativos con amplitud de control $a$: $E\approx a^{N}$ (aprox.), así $N\approx\dfrac{\ln E}{\ln a}$. 
Número total de directivos en una estructura con amplitud $a$ y $N$ niveles: $\sum_{k=0}^{N-1} a^{k}=\dfrac{a^{N}-1}{a-1}$.

## Ejemplo resuelto 1: niveles y directivos
Empresa de 400 personas en el nivel operativo. Se comparan dos amplitudes:
- $a=5$: $N=\dfrac{\ln 400}{\ln 5}=\dfrac{5{,}991}{1{,}609}=3{,}72\Rightarrow$ 4 niveles de supervisión. Directivos aproximados: $\dfrac{5^{4}-1}{4}=156$.
- $a=10$: $N=\dfrac{5{,}991}{2{,}303}=2{,}60\Rightarrow$ 3 niveles. Directivos aproximados: $\dfrac{10^{3}-1}{9}=111$.

Estructura plana: 45 jefes menos y comunicación más corta, pero cada jefe carga más gente; adecuada si las tareas son rutinarias y los equipos maduros. Para trabajo creativo o complejo (desarrollo de software) una amplitud de 6 a 8 suele ser razonable (referencia práctica).

## Ejemplo resuelto 2: organigrama de una empresa de software (texto)
```
Gerencia General
├── Gerencia de Tecnología (TI)
│   ├── Desarrollo (2 equipos)
│   ├── Infraestructura y Seguridad
│   └── Soporte
├── Gerencia Comercial
│   ├── Ventas
│   └── Marketing
├── Gerencia de Administración y Finanzas
└── (Staff) Asesoría Legal / Calidad
```
Análisis: estructura funcional. Si la empresa pasa de producto único a tres líneas (banca, salud, educación), conviene migrar a **divisional por producto** con servicios compartidos (finanzas, infraestructura), o a **matricial** con jefaturas de producto y especialidad técnica. Se debe definir quién prioriza los recursos para evitar el conflicto "dos jefes".

### Matriz de responsabilidades (RACI) para el cambio de estructura
| Actividad | Gerente general | Gerente TI | Jefe de producto |
|---|---|---|---|
| Aprobar nueva estructura | A | C | I |
| Definir cargos | C | A | R |
| Comunicar al personal | A/R | R | I |
(R: responsable, A: aprueba, C: consultado, I: informado.)

## Errores comunes
- Dibujar el organigrama de "cómo quisiéramos" y no el real, o dejarlo desactualizado.
- Matricial sin reglas claras de arbitraje.
- Amplitud de control excesiva en trabajo complejo, o mínima por desconfianza.
- Departamentalizar solo por función cuando el cliente exige procesos transversales.

## Ejercicios propuestos
1. Con 200 operativos y amplitud 6, ¿cuántos niveles aproximadamente? *Respuesta: $\ln200/\ln6=5{,}30/1{,}79=2{,}96\approx3$ niveles.*
2. ¿Qué configuración de Mintzberg corresponde a un hospital? *Respuesta: burocracia profesional.*
3. Proponga la departamentalización para un banco con presencia en 5 estados y 3 tipos de cliente. *Respuesta: respuesta libre; justificar mezcla geográfica y por cliente, con funciones de apoyo centralizadas.*

## Conexiones con otras materias
[[Sistema de Información II]], [[Gerencia de Proyectos]] (matriz de proyectos), [[Teoría General de Sistemas]], [[Efectividad Personal]].

## Fuente
Mintzberg, *La estructuración de las organizaciones*; Chiavenato; Robbins. Fórmulas de dimensionamiento son aproximaciones didácticas.
