---
tags: [clase, electiva]
materia: Organización
fuente: "conocimiento general"
---
# ORG 04 - Cultura, liderazgo y comunicación

Materia: [[Organización]]
Anterior: [[ORG 03 - Procesos y BPM]]
Siguiente: [[ORG 05 - Gestión del cambio y mejora continua]]

## Contexto y objetivo
Las estructuras y los procesos son el "esqueleto" de la organización; la cultura, el liderazgo y la comunicación son su comportamiento real. El objetivo es diagnosticar la cultura, distinguir estilos de liderazgo, analizar redes de comunicación y calcular métricas sencillas de clima y de comunicación en equipos de TI.

## Teoría

### Comportamiento organizacional (CO)
Estudia cómo individuos, grupos y estructura afectan la conducta en la organización (Robbins). Niveles: individual (percepción, motivación, personalidad), grupal (equipos, conflicto, comunicación) y organizacional (cultura, cambio).

### Cultura organizacional
- **Definición** (Schein): patrón de supuestos básicos compartidos que el grupo aprendió al resolver problemas y que se enseña a los nuevos miembros.
- **Tres niveles de Schein**: artefactos (visibles: oficina, vestimenta, rituales), valores declarados, supuestos básicos (inconscientes).
- **Tipologías**: Cameron y Quinn (clan, adhocracia, mercado, jerarquía); Hofstede (distancia al poder, individualismo, evitación de incertidumbre, masculinidad, orientación a largo plazo, indulgencia).
- **Cultura fuerte** no es sinónimo de buena: puede resistir el cambio.
- Relación con TI: la cultura DevOps (colaboración, automatización, medición, compartir) es un caso de cultura que condiciona la adopción tecnológica.

### Motivación
- **Maslow**, **Herzberg** (higiene vs. motivación), **McClelland** (logro, poder, afiliación).
- **Teoría de la expectativa (Vroom)**: $\text{Motivación}=E\times I\times V$ (expectativa de que el esfuerzo produzca desempeño, instrumentalidad de que el desempeño produzca recompensa, valencia de la recompensa). Si algún factor es cero, la motivación es cero.
- **Equidad (Adams)**: se compara la relación aportes/resultados propia con la de otros.

### Liderazgo
- **Liderazgo vs. gerencia**: el líder inspira dirección; el gerente planifica y controla.
- **Teorías de rasgos**, **conductuales** (Ohio, Michigan; rejilla gerencial de Blake y Mouton), **situacionales** (Hersey y Blanchard: dirigir, persuadir, participar, delegar según la madurez del seguidor; Fiedler).
- **Transformacional** vs. **transaccional** (Bass). **Liderazgo servicial**. En equipos ágiles, el *servant leadership* es habitual.
- **Poder**: legítimo, de recompensa, coercitivo, de experto, referente.

### Equipos
Etapas de Tuckman: formación, tormenta, normalización, desempeño (y disolución). Roles de Belbin. Tamaño: con $n$ miembros hay $\dfrac{n(n-1)}{2}$ canales de comunicación.

### Comunicación
- Proceso: emisor, mensaje, canal, receptor, retroalimentación, ruido.
- **Formal e informal**; **descendente, ascendente, horizontal**.
- Redes de comunicación: cadena, rueda, todos los canales.
- Barreras: filtrado, percepción selectiva, sobrecarga, jerga técnica.
- **Escucha activa**, retroalimentación, asertividad. Ver [[Efectividad Personal]].
- **Conflicto**: estilos de Thomas-Kilmann (competir, colaborar, comprometer, evitar, acomodar).

## Ejemplo resuelto 1: canales de comunicación y tamaño del equipo
- Equipo de 5: $\dfrac{5\cdot4}{2}=10$ canales.
- Equipo de 9: $\dfrac{9\cdot8}{2}=36$ canales.
- Equipo de 15: $105$ canales.
Al pasar de 5 a 9 personas (80 % más gente) los canales crecen 260 %. Por eso Scrum recomienda equipos de unas 3 a 9 personas (la Guía Scrum habla de 10 o menos) y se divide en subequipos al crecer. (Brooks: añadir personas a un proyecto atrasado lo atrasa más.)

## Ejemplo resuelto 2: expectativa de Vroom en un equipo de desarrollo
Un programador evalúa si esforzarse en una entrega difícil (escala de 0 a 1 para E e I; valencia de -10 a 10):
- $E=0{,}8$ (cree que con esfuerzo cumplirá).
- $I=0{,}3$ (cree que la gerencia casi no premia el buen desempeño).
- $V=8$ (valora mucho un bono).
$M=0{,}8\times0{,}3\times8=1{,}92$.
Si la empresa establece un sistema claro de reconocimiento ($I=0{,}9$): $M=0{,}8\times0{,}9\times8=5{,}76$, tres veces mayor. Lección: el problema no era la valencia ni la capacidad, sino la credibilidad de la recompensa.

## Ejemplo resuelto 3: diagnóstico de clima con encuesta
Cinco ítems en escala 1 a 5, promedios de 20 empleados de TI (hipotéticos): comunicación 2,8; reconocimiento 2,5; autonomía 4,1; liderazgo 3,4; claridad de metas 3,9. Promedio general: $\dfrac{2{,}8+2{,}5+4{,}1+3{,}4+3{,}9}{5}=3{,}34$.
Brechas: reconocimiento y comunicación bajo 3. Plan: reunión semanal de equipo, tablero visible de logros y reconocimiento mensual. Reevaluar en seis meses con el mismo cuestionario para comparar.

## Errores comunes
- Creer que la cultura se cambia con un cartel de valores.
- Confundir clima (percepción actual) con cultura (supuestos profundos).
- Liderar con un solo estilo para todos los seguidores y tareas.
- Comunicar solo por correo o chat sin confirmar la comprensión.
- Interpretar silencio como acuerdo.

## Ejercicios propuestos
1. ¿Cuántos canales de comunicación hay en un equipo de 12? *Respuesta: 66.*
2. Vroom: $E=0{,}6$, $I=0{,}5$, $V=6$. *Respuesta: 1,8.*
3. Un equipo recién formado discute mucho sobre roles: ¿en qué etapa de Tuckman está y qué estilo situacional conviene? *Respuesta: tormenta; dirigir o persuadir con claridad de reglas y metas.*

## Conexiones con otras materias
[[Efectividad Personal]], [[Teoría General de Sistemas]], [[Gerencia de Proyectos]], [[IS 01 - Ciclo de vida y modelos de proceso]], [[Economía]].

## Fuente
Robbins, *Comportamiento Organizacional*; Chiavenato; Schein; Hofstede; Tuckman. Cifras de los ejemplos hipotéticas.
