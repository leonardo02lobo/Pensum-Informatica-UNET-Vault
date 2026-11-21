---
tags: [clase, semestre-III]
materia: Laboratorio de Física II
---
# Laboratorio de Física II - Electrostática y Líneas Equipotenciales

Materia: [[Laboratorio de Física II]]
Anterior: [[Laboratorio de Física II - Instrumentos de Medición y Análisis de Errores]]
Siguiente: [[Laboratorio de Física II - Ley de Ohm y Curvas V-I]]

## Contexto y objetivo

La electrostática estudia las cargas eléctricas en reposo y los campos que generan. Dado que el campo eléctrico $\vec{E}$ no puede medirse directamente con facilidad en el laboratorio básico, esta práctica utiliza la relación entre potencial eléctrico $V$ y campo $\vec{E}$ para trazar **superficies (líneas) equipotenciales** y deducir a partir de ellas la geometría de las líneas de campo.

## 1. Electrización y electroscopio

Los cuerpos pueden adquirir carga neta por tres mecanismos:
1. **Frotamiento**: transferencia de electrones entre materiales con distinta afinidad electrónica (ej. varilla de vidrio con seda, ebonita/plástico con lana).
2. **Contacto**: redistribución de carga al tocar un conductor cargado con otro neutro (ambos quedan con carga del mismo signo).
3. **Inducción**: acercamiento de un cuerpo cargado sin tocar al conductor, seguido de conexión a tierra para dejar una carga neta de signo opuesto.

El **electroscopio** detecta la presencia de carga: al transferir carga a la esfera superior, las laminillas metálicas adquieren igual signo y se repelen formando un ángulo proporcional a la carga.

## 2. Potencial eléctrico, equipotenciales y campo $\vec{E}$

- Una **superficie equipotencial** es el lugar geométrico donde el potencial eléctrico $V$ tiene el mismo valor.
- El trabajo necesario para mover una carga $q$ sobre una equipotencial es nulo: $W = q\,\Delta V = 0$.
- El campo eléctrico $\vec{E}$ es siempre **perpendicular** a las superficies equipotenciales y apunta en el sentido de **potencial decreciente**:
  $$\vec{E} = -\nabla V \implies |\vec{E}| \approx \frac{\Delta V}{\Delta d}$$
  donde $\Delta d$ es la distancia perpendicular entre dos líneas equipotenciales con diferencia de potencial $\Delta V$.

## 3. Procedimiento típico de mapeo en cubeta electrolítica / papel conductor

1. Colocar dos electrodos (ej. placas paralelas o dos electrodos puntuales) sobre la cubeta con agua ligeramente conductora o papel conductor.
2. Alimentar los electrodos con una fuente DC baja (por ejemplo $V_0 = 10\,\text{V}$).
3. Fijar la punta negativa (COM) del voltímetro en el electrodo de referencia ($0\,\text{V}$).
4. Explorar con la punta de prueba los puntos donde el voltímetro marca valores constantes ($2\,\text{V}, 4\,\text{V}, 6\,\text{V}, 8\,\text{V}$) y registrar sus coordenadas $(x, y)$ en papel milimetrado.
5. Trazar las líneas equipotenciales uniendo los puntos de igual voltaje y dibujar las líneas de campo eléctrico perpendiculares a ellas (saliendo del electrodo positivo hacia el negativo).

## Ejemplo resuelto

En la región central entre dos placas paralelas separadas $d = 8{,}0\,\text{cm}$, las equipotenciales de $4{,}0\,\text{V}$ y $6{,}0\,\text{V}$ están separadas por $\Delta d = 1{,}6\,\text{cm} = 0{,}016\,\text{m}$. La magnitud aproximada del campo eléctrico es:
$$E \approx \frac{\Delta V}{\Delta d} = \frac{6{,}0 - 4{,}0}{0{,}016} = 125\,\text{V/m}$$

## Errores comunes

- Trazar líneas de campo eléctrico que se cruzan entre sí (físicamente imposible) o que no son perpendiculares a las equipotenciales.
- Sumergir en exceso o mover los electrodos durante la medición, alterando la geometría del campo.
- Confundir la lectura de potencial $V$ respecto a tierra con la diferencia de potencial entre dos puntos cualesquiera.

## Ejercicios propuestos

1. ¿Por qué el trabajo para desplazar una carga a lo largo de una línea equipotencial es cero?
2. Si dos líneas equipotenciales están muy juntas en una región del plano y muy separadas en otra, ¿dónde es más intenso el campo eléctrico?

**Respuestas:**
1. Porque $W_{AB} = q(V_A - V_B)$ y en una equipotencial $V_A = V_B$.
2. Donde están más juntas ($\Delta d$ menor), ya que $E \approx \Delta V / \Delta d$.

## Conexiones

- Verifica experimentalmente los conceptos de [[Física II]] (campo y potencial eléctrico).
- Continúa con [[Laboratorio de Física II - Ley de Ohm y Curvas V-I]].

## Fuente

Elaborado siguiendo el programa referencial de [[Laboratorio de Física II]] (Práctica 2: Electrostática y superficies equipotenciales).
