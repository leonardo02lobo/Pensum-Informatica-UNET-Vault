---
tags: [clase, semestre-VII]
materia: Base de Datos II
fuente: ~/Documentos/UNET/Base de datos 2 (etl/*.py, scheduler/*, MANUAL.md)
---
# BD2 - 09 ETL: carga inicial, carga diaria y programación

Materia: [[Base de Datos II]]
Anterior: [[BD2 - 08 SCD Tipo 2 y claves subrogadas]]
Siguiente: [[BD2 - 10 Consultas analiticas vistas y control de calidad]]

## Contexto y objetivo
El ETL (Extract, Transform, Load) alimenta el DWH. El proyecto implementa dos rutinas en Python (pandas + psycopg) sobre PostgreSQL: **carga inicial** y **carga incremental diaria**, más programación con cron/systemd. Objetivo: entender el diseño de un ETL robusto: idempotente, trazable, auditable.

## Módulos (`etl/`)
| Archivo | Responsabilidad |
|---|---|
| `config.py` | credenciales (variables de entorno/`.env`), rutas, mapeo de columnas, hojas de dimensión |
| `db.py` | conexión, bitácora (`abrir_ejecucion`, `cerrar_ejecucion`), marca de agua, `upsert`, `insertar_hechos`, `sincronizar_secuencia`, resolución, staging |
| `extract.py` | lectura de Excel/CSV (`leer_dimensiones`, `leer_hechos`) y `validar_hechos` |
| `resolver.py` | clave de negocio a clave subrogada |
| `carga_inicial.py` | rutina 1 |
| `carga_diaria.py` | rutina 2 |
| `generar_variante_prueba.py` | genera datos desplazados/duplicados para probar el ETL (existe el Excel `..._desplazado_duplicados.xlsx`) |

## Flujo de la carga inicial
Orden por dependencias de FK: **dimensiones → staging crudo → control de calidad → resolución de claves → hechos → marca de agua**.
1. `db.asegurar_miembros_desconocidos`: crea el miembro -1.
2. Para cada hoja de dimensión: `extract.normalizar_dimension` y `db.upsert`.
3. Como se insertaron ids explícitos (el maestro es autoridad del histórico), se llama `sincronizar_secuencia` para que IDENTITY continúe tras el máximo.
4. Hechos: `extract.leer_hechos` (omite las filas decorativas de encabezado `FILAS_ENCABEZADO_HECHO` y columnas "Unnamed"), `cargar_staging(... vaciar=True)` guarda la copia cruda.
5. `validar_hechos` separa válidas y rechazadas (con columna `motivo_rechazo`); solo valida contra dimensiones cuyas claves posee el origen (asesor, apoyo).
6. `resolver.resolver` asigna `id_tiempo` (creando días faltantes con `obtener_id_tiempo`) e `id_estudiante` (versión vigente en la fecha del hecho).
7. Los rechazos se guardan en `data/rechazos/` con el motivo; se registra todo en `etl.log_ejecucion`.
Opciones: `--reiniciar` vacía y recarga.

## Carga diaria
```bash
python etl/carga_diaria.py                    # del día
python etl/carga_diaria.py --simulacion       # valida sin escribir
python etl/carga_diaria.py --fecha 2026-07-01 # reproceso
python etl/carga_diaria.py --desde 2026-06-01 --hasta 2026-06-30
python etl/carga_diaria.py --archivo ruta.csv
```
**Origen** por prioridad: `--archivo`; archivos `.xlsx/.csv` en `data/entrada` (luego pasan a `data/procesados`, copiados con `shutil`); hoja de respaldo `hecho_atenciones_dia` del Excel maestro (`localizar_origenes`).

Propiedades de diseño:
- **Marca de agua** (`etl.control_carga`, `leer_watermark/actualizar_watermark`): solo procesa lo posterior a la última fecha cargada.
- **Idempotencia**: `INSERT ... ON CONFLICT (id_atencion) DO NOTHING`; reejecutar no duplica.
- **Trazabilidad**: cada corrida deja filas leídas/insertadas/omitidas/rechazadas y estado en `etl.log_ejecucion`.
- **Auditoría**: filas rechazadas con motivo exacto.
- **Sincronización de dimensiones**: `sincronizar_dimensiones` se llama con el maestro y con cada archivo del día; estables por UPSERT (SCD1) y `dim_estudiante` por SCD2 con cédula, sin copiar ids del origen. Un estudiante con cédula nueva se crea.
- **Calendario que crece solo**: una fecha ausente de `dim_tiempo` se crea en vez de rechazarse.
- **Miembro desconocido**: estudiante irresoluble se carga con id -1 y queda contado (control 10).

Patrón de `UPSERT`:
```sql
INSERT INTO tabla (cols) VALUES (...) ON CONFLICT (pk) DO UPDATE SET col = EXCLUDED.col;
```

## Programación (`scheduler/`)
- cron: `30 23 * * * "<ruta>/scheduler/ejecutar_carga_diaria.sh"` (todos los días a las 23:30); instalar con `crontab scheduler/crontab.txt`, verificar con `crontab -l`.
- systemd timer: `dwh-carga-diaria.timer` con `OnCalendar=*-*-* 23:30:00` y `Persistent=true` (si el equipo estaba apagado, ejecuta al encender; ventaja sobre cron).
- Windows: Programador de tareas (en MANUAL.md, sección 7).
- Verificar corrida: logs en `logs/carga_diaria.log` y tabla `etl.log_ejecucion`.

## Ejemplo resuelto: reproceso sin duplicados
El 2026-07-01 se cargan 21 hechos. Se vuelve a ejecutar con `--fecha 2026-07-01`: la marca de agua se ignora para esa fecha, pero el `ON CONFLICT DO NOTHING` omite los 21 ya existentes; la bitácora registra 0 insertadas, 21 omitidas. Si el archivo trae 3 filas con asesor inexistente, se rechazan con motivo "asesor no existe" y se escriben a `data/rechazos/`.

## Errores comunes
- Cargar hechos antes de dimensiones.
- No sincronizar la secuencia tras ids explícitos.
- Confiar en claves subrogadas del origen.
- Eliminar el staging y perder la posibilidad de auditar.
- Credenciales en el repositorio: el proyecto usa `.env` (ignorado por git) y `.env.ejemplo`.
- Un ETL no transaccional que deja cargas a medias: use transacciones por etapa.

## Ejercicios propuestos
1. ¿Qué diferencia hay entre marca de agua e idempotencia? *Resp.: la marca limita lo que se lee; la idempotencia protege si se relee.*
2. ¿Por qué `Persistent=true`? *Resp.: recupera ejecuciones perdidas por apagado.*
3. Diseñe el tratamiento de una fila con satisfacción 7. *Resp.: rechazar con motivo "fuera de rango 1-5" y guardarla en rechazos.*

## Conexiones
[[BD2 - 03 Transacciones ACID y control de concurrencia]], [[BD2 - 08 SCD Tipo 2 y claves subrogadas]], [[Administración de Base de Datos]].

## Fuente
`etl/carga_inicial.py`, `etl/carga_diaria.py`, `etl/db.py` (nombres de funciones), `etl/extract.py`, `etl/resolver.py`, `scheduler/`. No se leyó completo `generar_variante_prueba.py` ni `config.py` (solo su uso).
