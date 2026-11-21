---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: ~/Documentos/UNET/Comunicaciones 2/parcial 3 (README.md, server/gbn.py, server_v2.py)
---
# Comunicaciones II - 11 SFTP-U Go-Back-N adversario y resultados

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 10 SFTP-U Diseno del protocolo y trama]]

## Contexto y objetivo
Segunda mitad del Parcial III: (Fase 2) medir el protocolo ingenuo v1 bajo un **adversario** que inyecta fallas de red; (Fase 3-4) robustecerlo con CRC32, SHA-256, ACK/NACK, temporizadores con retroceso exponencial y **Go-Back-N**, y validar que sobrevive. Aquí se explica la implementación del ARQ, el proxy adversario, la batería de experimentos y la tabla de resultados. Teoría general en [[Comunicaciones II - 04 Confiabilidad ARQ y ventana deslizante]].

## Implementación Go-Back-N de v2 (`gbn.py`)
El ARQ está en dos clases **sin E/S ni reloj del sistema**: el tiempo entra como `now_ms` y el envío como función `send`. Así se verifican propiedades exactas con un reloj falso ("cinco expiraciones consecutivas aplican 300, 600, 1200, 2400 y 2400 ms") sin esperar.

### Emisor `GbnSender`
- Estado: `base`, `next_seq`, `rto`, `retries`, `timer_deadline`, `buffer` (bloques en vuelo).
- `llenar_ventana`: emite mientras `next_seq < base + window`; marca `LAST_BLOCK` en el último bloque; arranca el temporizador si está parado.
- `on_ack(ack)`: la base indicada es `0` si `ack == 0xFFFFFFFF`, o `ack+1`. Si no avanza, el ACK es **obsoleto/duplicado** y se ignora sin tocar temporizador ni reintentos. Si avanza: se reinician `retries` y `rto` (el canal demostró funcionar), se libera el búfer y se rearma o detiene el temporizador.
- `on_nack(ack)`: es un ACK acumulativo implícito; avanza la base y **retransmite la ventana** sin esperar, pero **sin incrementar `retries`** (el desorden no es canal caído) y con **supresión de ráfagas** (una retransmisión por base y por RTO).
- `on_timeout`: `retries += 1`; si supera `max_retries` (8) devuelve `None` y la transferencia aborta con ERR_MAX_RETRIES; si no, retransmite la ventana completa **y luego** duplica el RTO (tope 2400 ms).

### Receptor `GbnReceiver`
```python
def on_data(self, seq, payload):
    if seq == self.expected_seq:            # exactamente el esperado
        self.write_block(seq, payload)      # escribe en offset seq*512
        self.expected_seq += 1
        return "ack", self.ack_actual
    if seq < self.expected_seq:             # duplicado / reinyección
        self.contadores["duplicate_frames"] += 1
        return "ack", self.ack_actual       # reconfirma: recupera ACK perdidos
    self.contadores["out_of_order_frames"] += 1   # llegó adelantado
    return "nack", self.ack_actual          # GBN no almacena fuera de orden
```
Responder siempre (ACK o NACK) evita esperar al temporizador cuando el receptor ya sabe qué falta.

### Ejemplo con valores
Archivo de 6 bloques (0-5), ventana 4, se corrompe el bloque 2. Emisor envía 0-3. Receptor: 0 ->ack0, 1 ->ack1, 2 con CRC malo -> NACK(ack=1), 3 adelantado -> NACK(ack=1). El emisor recibe el primer NACK: base = 2, retransmite 2,3 (con flag RETRANSMIT), supresión de ráfaga ignora el segundo NACK. El receptor acepta 2, 3, luego 4, 5 y FIN. Resultado: 2 retransmisiones, 0 reintentos contados.

## El adversario (`adversary/proxy.py`, `scenarios.yaml`)
Proxy UDP **entre** cliente y servidor: el cliente apunta al proxy (puerto 9000) y el proxy al servidor (9001). Aplica *perfiles de falla* (pérdida, corrupción de payload o cabecera, latencia con jitter, desorden dirigido, duplicación, reinyección, canal caído) según un escenario con semilla reproducible y registra una bitácora CSV. Escenarios `E0` a `E11`.

Uso típico (del README):
```bash
python3 server/server_v2.py --port 9001 --dir server/storage
python3 adversary/proxy.py --scenario E4 --listen 9000 --target 9001 --log /tmp/adv.csv
node client/cli.js --version 2 --port 9000 put ./experiments/fixtures/prueba_32k.bin
```
Error clásico: apuntar el cliente al lado equivocado; `proyecto.sh cliente` resuelve solo el puerto vigente.

## Batería de experimentos
`experiments/run_battery.sh 1|2 [escenarios]` levanta servidor, proxy, captura (`tshark`, opcional) y cliente para los 12 escenarios, y acumula métricas en `experiments/metrics.csv`; `summarize.py` resume y compara fases. Opciones: `VENTANA=1` (v2 como Stop-and-Wait), `FIXTURE=...prueba_4096k.bin` para medir *goodput*. Archivo de referencia: 32 KiB = 64 bloques.

## Resultados (según README)
| Escenario | Falla | v1 | v2 |
|---|---|---|---|
| E0 | ninguna | OK | OK |
| E1 / E2 | pérdida 10 % / 30 % | TRUNCATED (0 B) | OK |
| E3 | pérdida 50 % de ACK/NACK | OK (inaplicable) | OK |
| E4 | corrupción de payload | CORRUPT (tamaño exacto, contenido alterado) | OK |
| E5 | corrupción de cabecera | TRUNCATED | OK |
| E6 | latencia 200 ms ± 150 | TRUNCATED | OK |
| E7 | desorden dirigido | CORRUPT (bloques intercambiados) | OK |
| E8 | duplicación 20 % | DUPLICATED (+10 240 B) | OK |
| E9 | reinyección | OK por azar | OK (rechazo activo) |
| E10 | combinado | TRUNCATED | OK |
| E11 | canal caído | TRUNCATED, **reporta éxito** | ABORTED con error explícito |

Conclusión del informe: **9 de 11 escenarios con falla dejaron el archivo inservible en v1 y en ninguno lo informó** (todos los clientes salieron con código 0). v2 recupera los diez escenarios recuperables con SHA-256 coincidente y falla de forma controlada con el canal caído. Lección: *el éxito debe verificarse extremo a extremo*, no suponerse.

## Pruebas del proyecto
`test_gbn.py` / `test_gbn.js` (ARQ con reloj falso), `test_v2_integration.py` (sesiones, replay), `test_profiles.py` (adversario), `test_vectors` (23 vectores binarios). Pendiente declarado: capturas `.pcapng` por falta de `tshark` (30 filas de metrics.csv lo anotan).

## Errores comunes
- Contar NACK/ACK duplicados como reintentos (abortaría transferencias recuperables).
- Reiniciar el temporizador con ACK obsoletos.
- Retransmitir ventana completa por cada NACK de una ráfaga.
- Medir resultados con una sola semilla; los escenarios fijan semilla para reproducir.
- No distinguir "éxito del protocolo" de "éxito verificado por hash".

## Ejercicios propuestos
1. RTO inicial 300 ms, máximo 2400: secuencia tras 5 timeouts. *Resp.: 300, 600, 1200, 2400, 2400.*
2. Tiempo total antes de abortar con 8 reintentos (suma de esperas, tope 2400)? *Resp.: 300+600+1200+2400·5 = 14 100 ms (aprox., según se cuente la primera espera).*
3. Con ventana 1 (`VENTANA=1`), ¿qué esquema es? *Resp.: Stop-and-Wait.*
4. ¿Por qué GBN no necesita búfer en el receptor? *Resp.: solo acepta la trama esperada; descarta las demás.*

## Conexiones
[[Comunicaciones II - 10 SFTP-U Diseno del protocolo y trama]], [[Comunicaciones II - 03 TCP conexión flujo y congestión]] (comparación con TCP), [[SFTP-U Protocolo sobre UDP]], [[Sistemas Distribuidos]] (tolerancia a fallos).

## Fuente
`~/Documentos/UNET/Comunicaciones 2/parcial 3/README.md`, `server/gbn.py`, `server/server_v2.py`. No se leyeron adversary/proxy.py, scenarios.yaml, ni docs/matriz-errores-soluciones.md; la descripción del adversario se basa en el README.
