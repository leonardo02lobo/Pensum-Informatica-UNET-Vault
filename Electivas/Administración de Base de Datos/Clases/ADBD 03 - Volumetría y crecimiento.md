---
tags: [clase, electiva]
materia: Administración de Base de Datos
fuente: "~/Documentos/UNET/administracion DB (estimacion_volumetria.py, punto3_crecimiento_dml.md, reglas_de_negocio.md) y conocimiento general"
---
# ADBD 03 - Volumetría y crecimiento

Materia: [[Administración de Base de Datos]]
Anterior: [[ADBD 02 - Tablespaces y almacenamiento]]
Siguiente: [[ADBD 04 - Segmentos Undo, Temp y constraints]]

## Contexto y objetivo
Antes de crear un tablespace hay que saber cuánto espacio ocupará cada tabla en 1 a 3 años. La **volumetría** es la estimación del tamaño de filas, tablas e índices; el **análisis de crecimiento** proyecta ese tamaño con las reglas del negocio. Objetivo: realizar una estimación defendible y traducirla en tamaños de datafile.

## Teoría

### Tamaño de una fila
$$T_{fila} = \sum_{i} L_i + H_{fila} + 2\ \text{(entrada del directorio de filas)}$$
donde $L_i$ es la longitud media de cada columna (NUMBER ≈ 1 byte por cada 2 dígitos + 1; `VARCHAR2` = longitud media real; `DATE` = 7 bytes; `TIMESTAMP WITH TIME ZONE` = 13 bytes) y $H_{fila}$ ≈ 3 bytes de cabecera por fila más 1 por columna nula intermedia (aproximación; verificar con la documentación del motor).

### Filas por bloque y bloques por tabla
Con bloque de $B$ bytes, cabecera de bloque $H_B \approx 100$ bytes y fracción reservada `PCTFREE` $p$:
$$U = (B - H_B)\cdot (1 - p)\qquad F_{bloque} = \left\lfloor \frac{U}{T_{fila}} \right\rfloor$$
$$N_{bloques} = \left\lceil \frac{N_{filas}}{F_{bloque}} \right\rceil,\qquad \text{Tamaño} = N_{bloques}\cdot B$$

### Proyección de crecimiento
- **Lineal**: $V(t) = V_0 + g\cdot t$ (el caso del comedor: depende de platos servidos por día).
- **Compuesto**: $V(t) = V_0 (1+r)^t$.
Se añade un **margen de seguridad** (p. ej. 20-30 %) por fragmentación y crecimiento imprevisto. El material del proyecto aplica un margen explícito y calcula el neto a 3 años por tabla.

### Perfiles de acceso
Según el patrón DML, cada tabla es: de solo lectura (catálogos), solo inserción (bitácoras), actualización intensiva (transaccionales) o de crecimiento masivo. Determina `PCTFREE`: bajo (0-5) si solo se inserta; alto (15-25) si las filas crecen por `UPDATE`.

### Hallazgos del proyecto del comedor
Según `punto3_crecimiento_dml.md`/`punto4_tablespaces.md`: cinco tablas concentran el 97,3 % del volumen; los índices ocupan el 63,2 %, más que los datos; el crecimiento ilimitado se localiza en tres tablas (`consumptions`, `audit_logs` y otra); las demás son estables. De ahí salieron seis tablespaces funcionales (estático, maestro, transaccional, auditoría, índices, índices de auditoría).

## Ejemplo resuelto
Tabla `consumptions`: 1.500 inserciones diarias (dato del proyecto), 3 años, fila media de 80 bytes, bloque de 8192, `PCTFREE` 10.

1. Filas: $N = 1500 \times 365 \times 3 = 1\,642\,500$.
2. Útil por bloque: $U = (8192-100)\times 0{,}9 = 7282{,}8$ bytes.
3. Filas por bloque: $\lfloor 7282{,}8 / 80 \rfloor = 91$.
4. Bloques: $\lceil 1\,642\,500/91 \rceil = 18\,049$.
5. Tamaño: $18\,049 \times 8192 \approx 147{,}9$ MB.
6. Con margen 25 %: $\approx 184{,}8$ MB; de ahí el `MAXSIZE` del datafile.

Verificación en una base real tras cargar datos de prueba:
```sql
-- Recolectar estadísticas y medir
EXEC DBMS_STATS.GATHER_TABLE_STATS('COMEDOR','CONSUMPTIONS');
SELECT table_name, num_rows, avg_row_len, blocks
  FROM dba_tables WHERE owner = 'COMEDOR' AND table_name = 'CONSUMPTIONS';

-- Tamaño real del segmento
SELECT segment_name, segment_type, ROUND(bytes/1048576,2) mb
  FROM dba_segments WHERE owner = 'COMEDOR'
 ORDER BY bytes DESC FETCH FIRST 5 ROWS ONLY;
```
Un cálculo parecido en Python (el material usa `estimacion_volumetria.py`):
```python
def filas_por_bloque(bloque=8192, cab=100, pctfree=0.10, fila=80):
    utiles = (bloque - cab) * (1 - pctfree)
    return int(utiles // fila)

def tamano_mb(filas, **kw):
    fpb = filas_por_bloque(**kw)
    bloques = -(-filas // fpb)          # techo
    return bloques * kw.get("bloque", 8192) / 1048576

print(round(tamano_mb(1_500*365*3), 1))   # ~147.9
```

## Errores comunes
- Estimar solo datos y olvidar índices (en el proyecto superan a los datos).
- Ignorar `PCTFREE`, undo y temporales.
- Proyectar sin las reglas del negocio (p. ej. altas "al vuelo" que aumentan una tabla maestra en la operación diaria).
- No contar la sobrecarga de LOB; por eso el proyecto prefirió `VARCHAR2(1000)` a `CLOB` para un detalle corto.

## Ejercicios propuestos
1. Fila de 200 bytes, bloque 8 KB, `PCTFREE` 20, cabecera 100: ¿filas por bloque? *Respuesta: $\lfloor 8092\cdot0{,}8/200\rfloor = 32$.*
2. ¿Cuántos MB para 1.000.000 filas con 32 filas/bloque? *Respuesta: 31.250 bloques x 8 KB ≈ 244 MB.*
3. Si una tabla crece 15 % anual desde 100 MB, ¿tamaño al tercer año? *Respuesta: $100\cdot1{,}15^3 \approx 152{,}1$ MB.*

## Conexiones
[[Base de Datos I]] (modelo y normalización), [[Base de Datos II]] (índices), [[Ingeniería de Software]] (requisitos no funcionales).

## Fuente
`~/Documentos/UNET/administracion DB/estimacion_volumetria.py`, `punto3_crecimiento_dml.md`, `punto4_tablespaces.md`, `reglas_de_negocio.md`. Las constantes de tamaño de tipos son aproximaciones generales; verificar contra la documentación de la versión usada.
