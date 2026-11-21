---
tags: [clase, electiva]
materia: Gestión Tecnológica
fuente: "conocimiento general"
---
# GT 06 - Evaluación de proyectos tecnológicos, incubadoras y políticas CyT

Materia: [[Gestión Tecnológica]]
Anterior: [[GT 05 - Propiedad intelectual]]
Siguiente: —

## Contexto y objetivo
Cerramos la serie con tres temas: cómo evaluar proyectos tecnológicos con alta incertidumbre, qué instituciones apoyan la creación de empresas basadas en tecnología (incubadoras, parques tecnológicos) y cómo se organizan las políticas de ciencia y tecnología, con atención a Venezuela. El objetivo es aplicar VAN con riesgo y una matriz de puntuación, y describir el ecosistema de innovación.

## Teoría

### Evaluación de proyectos tecnológicos
Dimensiones: **técnica** (viabilidad, madurez), **comercial** (mercado), **económica** (VAN, TIR), **legal/PI** (libertad de operación), **organizacional** y **riesgo**.
- **Nivel de madurez tecnológica (TRL)**: escala de 1 (principios básicos) a 9 (sistema probado en entorno real).
- **Modelos de puntuación (scoring)**: $S=\sum w_j c_j$.
- **VAN ajustado por riesgo**: aumentar la tasa de descuento o usar valores esperados por escenario.
- **VAN esperado por escenarios**: $E[VAN]=\sum_k p_k\,VAN_k$.
- **Opciones reales**: el valor de poder expandir, posponer o abandonar; un proyecto con VAN ligeramente negativo puede valer la pena si abre opciones futuras (idea cualitativa aquí).
- **Compuertas de etapa (Stage-Gate)**: el proyecto avanza por fases con revisiones; se invierte poco al inicio y más conforme baja la incertidumbre.

### Ecosistema de innovación
- **Incubadoras**: apoyan empresas en etapa inicial con espacio, mentoría, redes y servicios (a menudo universitarias).
- **Aceleradoras**: programas intensivos de pocos meses, usualmente a cambio de participación.
- **Parques científicos y tecnológicos**: áreas que agrupan empresas, centros de I+D y universidades.
- **Oficinas de transferencia de resultados de investigación (OTRI/OTT)**: gestionan PI y licencias universitarias.
- **Clústeres**: concentración geográfica de empresas interrelacionadas (Porter).
- **Triple hélice** (Etzkowitz): universidad, industria y gobierno.

### Políticas de ciencia y tecnología
Instrumentos: financiamiento de I+D, incentivos fiscales, becas, protección de PI, compras públicas de innovación, formación de capital humano. Indicadores nacionales: gasto en I+D/PIB, investigadores por millón de habitantes, publicaciones y patentes.

**Venezuela** (verificar con el programa oficial y la normativa vigente): existe un marco legal en materia de ciencia, tecnología e innovación (Ley Orgánica de Ciencia, Tecnología e Innovación, LOCTI) con aportes de empresas a actividades de I+D, y organismos como el ministerio con competencia en ciencia y tecnología, el antiguo CONICIT/FONACIT, el IVIC y las universidades. Los detalles actuales de aportes, programas y estructura institucional **deben verificarse** en fuentes oficiales; esta nota no los asume.

## Ejemplo resuelto 1: VAN esperado por escenarios
Proyecto: desarrollo de una plataforma IoT para riego (hipotético). Inversión inicial 80 000 USD. Flujos en caso base: 10 000, 25 000, 35 000, 40 000, 30 000; $i=15\,\%$.

| Año | Flujo | Valor actual (15 %) |
|---|---|---|
| 0 | -80 000 | -80 000,0 |
| 1 | 10 000 | 8 695,7 |
| 2 | 25 000 | 18 903,6 |
| 3 | 35 000 | 23 013,1 |
| 4 | 40 000 | 22 870,1 |
| 5 | 30 000 | 14 915,3 |

$VAN_{base}\approx 8\,398$ USD; TIR $\approx 18{,}69\,\%>15\,\%$.

Escenarios: optimista ($VAN=+40\,000$, prob. 0,25), base ($+8\,398$, prob. 0,45), pesimista ($-30\,000$, prob. 0,30):
$$E[VAN]=0{,}25(40\,000)+0{,}45(8\,398)+0{,}30(-30\,000)=10\,000+3\,779-9\,000=4\,779 \text{ USD}$$
Positivo, pero con 30 % de probabilidad de perder 30 000: se recomienda dividir en etapas (Stage-Gate): fase 1 de 20 000 USD (prototipo y pruebas de campo) con la decisión de continuar solo si el TRL alcanza 6 y hay 3 clientes piloto.

## Ejemplo resuelto 2: scoring con TRL
| Criterio | Peso | Proyecto X | Proyecto Y |
|---|---|---|---|
| Madurez (TRL) | 0,25 | 5 | 3 |
| Mercado | 0,30 | 3 | 5 |
| Ventaja protegible (PI) | 0,20 | 4 | 4 |
| Capacidad del equipo | 0,25 | 4 | 3 |

$S_X=1{,}25+0{,}9+0{,}8+1{,}0=3{,}95$; $S_Y=0{,}75+1{,}5+0{,}8+0{,}75=3{,}80$. X ligeramente mejor; Y tiene más mercado: podría reforzarse con una alianza tecnológica.

## Errores comunes
- Aplicar VAN determinista a proyectos de alta incertidumbre sin escenarios ni etapas.
- Confundir TRL (madurez técnica) con viabilidad comercial.
- Esperar que la incubadora aporte el negocio: aporta entorno, no producto-mercado.
- Evaluar solo la tecnología y no el equipo y el modelo de negocio.
- Citar datos de políticas públicas sin comprobar su vigencia.

## Ejercicios propuestos
1. Probabilidades 0,3/0,5/0,2 con VAN de 60, 10 y -40 (miles): calcule $E[VAN]$. *Respuesta: 18+5-8 = 15 mil.*
2. Defina TRL 4 y TRL 7. *Respuesta: TRL 4: validación de componentes en laboratorio; TRL 7: prototipo del sistema demostrado en entorno operativo.*
3. Diferencie incubadora y aceleradora. *Respuesta: la incubadora acompaña a largo plazo con espacio y servicios; la aceleradora es un programa corto e intenso, con capital por participación.*

## Conexiones con otras materias
[[Ingeniería Económica]], [[Finanzas para Ingenieros]], [[Economía]], [[Ciencia y Sociedad I]], [[Legislación, Valores y Proyecto de País]], [[Formación de Emprendedores]], [[Gerencia de Proyectos]].

## Fuente
Escorsa y Valls; Manual de Oslo; Etzkowitz; NASA (escala TRL). Marco venezolano a verificar con el programa oficial. Cifras ilustrativas.
