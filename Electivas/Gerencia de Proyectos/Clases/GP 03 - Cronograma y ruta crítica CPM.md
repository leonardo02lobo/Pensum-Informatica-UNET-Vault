---
tags: [clase, electiva]
materia: Gerencia de Proyectos
fuente: "conocimiento general"
---
# GP 03 - Cronograma y ruta crítica CPM

Materia: [[Gerencia de Proyectos]]
Anterior: [[GP 02 - Alcance y WBS]]
Siguiente: [[GP 04 - PERT y diagrama de Gantt]]

## Contexto y objetivo
Una vez definido el alcance, se planifica el tiempo: actividades, dependencias, duraciones y la **ruta crítica** que determina la duración mínima del proyecto. El objetivo es construir una red de actividades, calcular tiempos tempranos y tardíos, holguras y ruta crítica con el método CPM (Critical Path Method), y comprimir el cronograma. El fundamento de grafos y redes está en [[Investigación de Operaciones I]].

## Teoría

### Pasos del cronograma
1. Definir actividades (desde los paquetes de trabajo de la WBS).
2. Secuenciar (dependencias).
3. Estimar recursos y duraciones.
4. Desarrollar el cronograma (CPM) y controlarlo.

### Dependencias
Tipos de relación: **FS** (fin-inicio, la más común), **SS** (inicio-inicio), **FF** (fin-fin), **SF** (inicio-fin, rara). **Adelanto (lead)** y **retraso (lag)**. Dependencias: obligatorias, discrecionales, externas, internas.

### Redes
- **AON** (actividad en nodo, usada por MS Project y PMBOK) y **AOA** (actividad en flecha, requiere actividades ficticias).
- Una red tiene un inicio y un fin; no debe contener ciclos.

### Cálculos CPM
**Paso hacia adelante** (tiempos tempranos):
$$ES_j=\max_{i\in\text{pred}(j)}EF_i,\qquad EF_j=ES_j+d_j$$
con $ES=0$ para actividades sin predecesoras. La duración del proyecto es $\max EF$.

**Paso hacia atrás** (tiempos tardíos): 
$$LF_i=\min_{j\in\text{suc}(i)}LS_j,\qquad LS_i=LF_i-d_i$$
con $LF$ igual a la duración del proyecto para las actividades finales.

**Holgura total**: $H_T=LS-ES=LF-EF$. **Holgura libre**: $H_L=\min_{j}ES_j-EF_i$ (cuánto puede retrasarse sin afectar el inicio temprano de ningún sucesor).
**Ruta crítica**: secuencia de actividades con $H_T=0$ (la ruta más larga). Puede haber varias.

### Compresión de cronograma
- **Crashing**: agregar recursos para acortar actividades críticas; se elige la de menor **costo de aceleración por unidad de tiempo**: $\dfrac{C_{ac}-C_{n}}{D_n-D_{ac}}$. Se recalcula la ruta crítica tras cada reducción (pueden aparecer rutas críticas paralelas).
- **Fast tracking**: superponer actividades que iban en secuencia (más riesgo y retrabajo).

### Nivelación y asignación de recursos
Si los recursos son limitados, se reprograman actividades dentro de su holgura (**nivelación**) y la ruta crítica puede cambiar (cadena crítica). Se tratará más en [[GP 04 - PERT y diagrama de Gantt]].

## Ejemplo resuelto 1: CPM con seis actividades
| Actividad | Descripción | Duración (días) | Predecesoras |
|---|---|---|---|
| A | Requisitos | 3 | - |
| B | Diseño | 4 | A |
| C | Configurar entorno | 2 | A |
| D | Desarrollo | 5 | B |
| E | Preparar datos de prueba | 3 | C |
| F | Pruebas e implantación | 2 | D, E |

**Paso hacia adelante**
- A: ES 0, EF 3. B: ES 3, EF 7. C: ES 3, EF 5. D: ES 7, EF 12. E: ES 5, EF 8.
- F: ES $=\max(12,8)=12$, EF 14. **Duración del proyecto: 14 días.**

**Paso hacia atrás**
- F: LF 14, LS 12. D: LF 12, LS 7. E: LF 12, LS 9. B: LF 7, LS 3. C: LF 9, LS 7. A: LF $=\min(LS_B,LS_C)=\min(3,7)=3$, LS 0.

| Act. | ES | EF | LS | LF | $H_T$ |
|---|---|---|---|---|---|
| A | 0 | 3 | 0 | 3 | 0 |
| B | 3 | 7 | 3 | 7 | 0 |
| C | 3 | 5 | 7 | 9 | 4 |
| D | 7 | 12 | 7 | 12 | 0 |
| E | 5 | 8 | 9 | 12 | 4 |
| F | 12 | 14 | 12 | 14 | 0 |

**Ruta crítica: A - B - D - F = 3+4+5+2 = 14 días.** La ruta A - C - E - F dura 10 días (holgura 4). Holgura libre de E: $ES_F-EF_E=12-8=4$; de C: $ES_E-EF_C=5-5=0$ (C tiene holgura total 4 pero libre 0: retrasar C mueve a E).

## Ejemplo resuelto 2: compresión
Se quiere terminar en 12 días. Costos de aceleración (USD/día): A=300, B=200, D=250, F=400 (las no críticas no ayudan). Límite de reducción (días): B hasta 1, D hasta 1, A hasta 1, F 0.
- Reducir 1 día en B (el más barato, 200): duración 13; la ruta A-C-E-F sigue en 10; la crítica A-B-D-F es 13.
- Reducir 1 día en D (250): duración 12. Costo total $=200+250=450$ USD. No aparecen rutas críticas nuevas (la otra ruta es de 10 días). Si se quisiera 10 días, se alcanzarían rutas críticas paralelas y habría que acortar en ambas.

## Ejemplo resuelto 3: implementación en Python
```python
act = {
    "A": (3, []), "B": (4, ["A"]), "C": (2, ["A"]),
    "D": (5, ["B"]), "E": (3, ["C"]), "F": (2, ["D", "E"]),
}
ES, EF = {}, {}
for k in act:                      # el orden dado ya es topologico
    d, pred = act[k]
    ES[k] = max([EF[p] for p in pred], default=0)
    EF[k] = ES[k] + d
fin = max(EF.values())
suc = {k: [j for j in act if k in act[j][1]] for k in act}
LS, LF = {}, {}
for k in reversed(list(act)):
    LF[k] = min([LS[s] for s in suc[k]], default=fin)
    LS[k] = LF[k] - act[k][0]
for k in act:
    h = LS[k] - ES[k]
    print(k, ES[k], EF[k], LS[k], LF[k], h, "critica" if h == 0 else "")
print("duracion", fin)
```
Salida: ruta crítica A, B, D, F; duración 14. (Código verificado.)

## Errores comunes
- Olvidar una dependencia y obtener una ruta crítica falsa.
- Calcular la holgura sobre ES y LF mezclados (usar $LS-ES$ o $LF-EF$).
- Suponer que la ruta crítica no cambia al comprimir o al nivelar recursos.
- Duraciones sin buffer, ni calendarios (fines de semana, feriados).
- Poner duraciones sin la participación de quienes ejecutan.

## Ejercicios propuestos
1. Actividades X (4), Y (3, pred X), Z (6, pred X), W (2, pred Y y Z). Duración y ruta crítica. *Respuesta: 12 días; X-Z-W.*
2. Holgura total de Y en el ejercicio anterior. *Respuesta: 3 días (Y ES 4, EF 7, LF 10).*
3. ¿Qué actividad acelerar si X cuesta 100/día, Z 150/día y W 90/día y se quiere ganar un día? *Respuesta: W (90), por ser crítica y la más barata.*

## Conexiones con otras materias
[[Investigación de Operaciones I]], [[Ingeniería de Software]], [[Ingeniería Económica]], [[Organización]].

## Fuente
PMI, *PMBOK*; Kerzner; Kelley y Walker (CPM). Cálculos de esta nota verificados manualmente y por ejecución del código.
