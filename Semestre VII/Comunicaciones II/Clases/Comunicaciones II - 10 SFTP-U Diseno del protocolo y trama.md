---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: ~/Documentos/UNET/Comunicaciones 2/parcial 3 (README.md, server/protocol.py, frame.py, payloads.py, filestore.py, server_v2.py)
---
# Comunicaciones II - 10 SFTP-U Diseno del protocolo y trama

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 09 OSINT reconocimiento pasivo y Google Hacking]]
Siguiente: [[Comunicaciones II - 11 SFTP-U Go-Back-N adversario y resultados]]

## Contexto y objetivo
El **Parcial III** pide diseñar, atacar y robustecer un protocolo de capa de aplicación para transferir archivos sobre UDP ([[SFTP-U Protocolo sobre UDP]] es el resumen). Esta nota documenta el **contrato binario**: formatos de trama v1 y v2, catálogo de mensajes, errores, sesiones y la cadena de validación. La siguiente nota trata la confiabilidad (Go-Back-N), el adversario y los resultados.

El proyecto se reparte por roles: servidor en **Python 3.11+** (estándar), cliente en **Node.js 18+**, adversario (proxy MITM) en Python con PyYAML, más `shared/` (catálogo y vectores de prueba), `experiments/` y `docs/`. Exigir lenguajes distintos obliga a que el formato binario sea un **contrato de bytes** verificado con 23 vectores comunes (`python3 shared/check_catalog.py`, `test_vectors.py`, `test_vectors.js`).

## Dos versiones deliberadas
- **v1 (ingenua, deliberadamente vulnerable)**: cabecera de 8 bytes: `magic(2) version(1) msg_type(1) payload_len(4)`. Sin CRC, sin secuencia, sin ACK, sin sesión. Sirve como línea base que **debe fallar**.
- **v2 (robusta)**: cabecera de 24 bytes con sesión, secuencia, ack, banderas y CRC32.

### Cabecera v2 (formato `!HBBIIIHHI`, big-endian)
| Campo | Tamaño | Función |
|---|---|---|
| magic | 2 B | 0x5346 ("SF"), identifica el protocolo |
| version | 1 B | 0x02 |
| msg_type | 1 B | tipo de mensaje |
| session_id | 4 B | identificador aleatorio de sesión |
| seq | 4 B | número de bloque (DATA) |
| ack | 4 B | último bloque aceptado en orden (0xFFFFFFFF = ninguno) |
| flags | 2 B | 0x0001 LAST_BLOCK, 0x0002 RETRANSMIT |
| payload_len | 2 B | longitud del payload (<= 512) |
| crc32 | 4 B | CRC32 IEEE de la trama con este campo en 0 |

Parámetros: bloque 512 B, datagrama máximo 536 B (24+512, evita fragmentación IP), ventana N = 4, RTO inicial 300 ms, máximo 2400 ms, 8 reintentos, inactividad de sesión 30 s, tope de 5 ERR/s por origen, archivo máximo 16 MiB.

**Orden de red**: todos los campos en big-endian (`!` en `struct`). Un tamaño total fijo permite calcular la eficiencia: 512/536 = 95.5 % de carga útil por datagrama DATA.

## Catálogo de mensajes (15)
| Código | Mensaje | Dirección / uso |
|---|---|---|
| 0x01/0x02 | HELLO / HELLO_ACK | abre sesión; el servidor responde versión, max_payload, ventana |
| 0x10 | PUT_INIT | nombre, tamaño (u64), SHA-256 (32 B) del archivo a subir |
| 0x11 | GET_INIT | nombre del archivo a bajar |
| 0x12/0x40 | LIST_REQ / LIST_RESP | listado: cuenta y (nombre, tamaño) |
| 0x13/0x41 | STAT_REQ / STAT_RESP | tamaño, mtime, SHA-256 |
| 0x20 | DATA | bloque con `seq` |
| 0x21 | FIN | SHA-256 final del archivo |
| 0x30/0x31 | ACK / NACK | confirmación acumulativa / negativa |
| 0x32 | FIN_ACK | código de resultado u16 (0 = OK) |
| 0x50 | ERR | código u16 + mensaje UTF-8 (<=200 B) |
| 0x60 | QUIT | cierra sesión |

Los payloads se serializan con `struct` (por ejemplo PUT_INIT: `name_len u16 + nombre + size u64 + sha256`). Cada decodificador valida su propia longitud y lanza `PayloadInvalido`: la cabecera garantiza que el payload llegó íntegro, no que su estructura tenga sentido.

## Códigos de error (16)
Agrupados: **transitorios** (se detectan antes de superar el CRC: BAD_MAGIC, BAD_VERSION, TRUNCATED, BAD_CRC, LEN_OVERFLOW, UNKNOWN_TYPE; la reacción correcta es retransmitir) y **definitivos** (NO_SESSION, SEQ_OUT_OF_WINDOW, FILE_NOT_FOUND 0x10, FILE_EXISTS 0x11, FILE_TOO_LARGE 0x12, CHECKSUM_MISMATCH 0x13, TIMEOUT, MAX_RETRIES 0x21, BAD_PAYLOAD, INTERNAL). Distinguirlos evita abortar transferencias recuperables.

## Cadena de validación `decode_v2`
Se evalúa en orden y se detiene en la primera falla:
1. longitud >= 24 B; 2. `magic`; 3. `version`; 4. `payload_len <= 512`; 5. longitud real == 24 + payload_len; 6. **CRC32**; 7. `msg_type` en el catálogo cerrado; 8. (fuera del códec) sesión activa.

```python
def crc32_de_trama(cabecera_sin_crc, payload):
    # Cubre la cabecera completa (con crc=0) y el payload
    return zlib.crc32(cabecera_sin_crc + payload) & 0xFFFFFFFF
```
Decisiones de diseño explicadas en el código:
- **Nunca** se usa `payload_len` para reservar memoria antes de comprobar la longitud real del datagrama (evita agotamiento de memoria con longitudes falsas; v1 sí confía en `payload_len`).
- El CRC cubre la **cabecera**, no solo el payload: la corrupción de `msg_type`, `seq` y `payload_len` es la más dañina.
- Si el CRC falla, nada de la trama es confiable (ni su origen): no se contesta con ERR (`respondible=False`). El NACK se construye con `expected_seq`, dato local.

## Sesiones y máquina de estados
- `HELLO` crea una sesión con `session_id` de 32 bits aleatorios criptográficos (`secrets.randbits(32)`): un identificador capturado no permite predecir el siguiente (defensa contra reinyección entre sesiones). Un HELLO duplicado **reutiliza** la misma sesión (idempotencia).
- Estados (resumen): sesión establecida -> TRANSFERRING -> FINALIZING -> DONE/ABORTED, que son terminales **por transferencia**; tras ellos la sesión vuelve a SESSION para no obligar a reiniciar el cliente. Un segador libera sesiones inactivas.
- **PUT**: PUT_INIT (se escribe en archivo *temporal*) -> DATA (ventana GBN) -> FIN con SHA-256 -> el servidor compara tamaño y hash; si todo coincide renombra el temporal al nombre definitivo ("la existencia del archivo definitivo prueba su integridad") y responde FIN_ACK(0); si no, descarta y responde FIN_ACK(0x13).
- **Idempotencia**: PUT_INIT duplicado no trunca el temporal ni reinicia el contador; FIN duplicado repite el mismo FIN_ACK.
- **GET**: el servidor emite con su propio emisor GBN; el cliente ACK/NACK.
- Escritura por **offset** `seq*512`, no por posición actual: el desorden no corrompe el archivo.

## Almacén de archivos (seguridad básica)
`FileStore.resolver` rechaza nombres vacíos, > 255 caracteres, con byte nulo, con `/` o `\`, `.` y `..`, y verifica con `resolve()` + `relative_to(raiz)` que el destino no escape de la raíz (atrapa enlaces simbólicos). Previene *path traversal*. Ambas versiones lo tienen: el objeto de estudio es la tolerancia a fallos del canal, no el sistema de archivos.

## Ejemplo resuelto: armar un datagrama
Un bloque DATA de 3 bytes (`61 62 63`), session_id=0x00000001, seq=0, ack=0xFFFFFFFF, flags=0, payload_len=3. Cabecera de 24 B con el campo CRC=0: `53 46 02 20 | 00 00 00 01 | 00 00 00 00 | FF FF FF FF | 00 00 | 00 03 | 00 00 00 00`. Se calcula `crc = crc32(cabecera + 616263)` y se escribe en los últimos 4 B. Tamaño total 27 B; el receptor verifica `len == 24 + 3`.

## Errores comunes
- Calcular el CRC sin poner antes el campo crc a cero.
- Mezclar endianness entre Python y Node.js (todo big-endian).
- Fiarse de `payload_len` sin cotejarlo.
- Responder con ERR a tramas con CRC inválido (amplificación y confusión).
- Renombrar el archivo antes de verificar el SHA-256.

## Ejercicios propuestos
1. ¿Tamaño máximo de un datagrama v2? *Resp.: 536 B.*
2. ¿Cuántos bloques tiene un archivo de 32 KiB? *Resp.: 64.*
3. ¿Por qué un session_id aleatorio y no incremental? *Resp.: evita que un atacante prediga/reinyecte en otra sesión.*
4. ¿Qué detecta el CRC32 que el SHA-256 final no detecta a tiempo? *Resp.: la corrupción de cada trama individual, permitiendo retransmitir en el acto.*

## Conexiones
[[Comunicaciones II - 02 Capa de transporte y UDP]], [[Comunicaciones II - 04 Confiabilidad ARQ y ventana deslizante]], [[Comunicaciones II - 08 Seguridad en redes criptografía y TLS]], [[Comunicaciones I - 09 Detección y corrección de errores]] (teoría del CRC).

## Fuente
`~/Documentos/UNET/Comunicaciones 2/parcial 3/`: README.md, server/protocol.py, frame.py, payloads.py, filestore.py, server_v2.py (parcial). No se leyeron `client/*.js`, `adversary/*`, `docs/*` ni `shared/protocol.md`.
