---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: conocimiento general; parcial 3 (server/gbn.py)
---
# Comunicaciones II - 04 Confiabilidad ARQ y ventana deslizante

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 03 TCP conexión flujo y congestión]]
Siguiente: [[Comunicaciones II - 05 Capa de red IP y enrutamiento]]

## Contexto y objetivo
Un canal real pierde, duplica, reordena y corrompe datagramas. Un **protocolo de transferencia fiable** debe ocultar esto con **ARQ** (*Automatic Repeat reQuest*): detección de errores + confirmaciones + temporizadores + retransmisión. Esta nota formaliza los tres esquemas clásicos y sus eficiencias; es la teoría que se implementa en SFTP-U v2.

## Ingredientes del ARQ
1. **Detección de errores**: checksum, CRC (ver [[Comunicaciones I - 09 Detección y corrección de errores]]).
2. **Retroalimentación**: ACK (positivo), NACK (negativo), ACK acumulativo.
3. **Números de secuencia**: distinguen datos nuevos de duplicados y detectan huecos.
4. **Temporizador y retransmisión**: la ausencia de ACK se interpreta como pérdida.
5. **Ventana**: cantidad de tramas en vuelo sin confirmar.

## Stop-and-Wait
Envía una trama, espera ACK, repite. Con 1 bit de secuencia (0/1) basta. Utilización:
$$U = \frac{L/R}{RTT + L/R}$$
donde L es el tamaño de la trama, R la tasa del enlace. **Ejemplo**: R = 1 Mbps, L = 8000 bits (1000 B), RTT = 40 ms: L/R = 8 ms, U = 8/48 = 16.7 %. Con R = 1 Gbps, L/R = 8 μs y U = 0.02 %: terrible.

## Ventana deslizante (pipelining)
Se permite N tramas en vuelo:
$$U = \min\left(1,\ \frac{N\,L/R}{RTT + L/R}\right)$$
Ventana que llena la tubería: $N \ge 1 + \dfrac{RTT}{L/R}$ (producto ancho de banda × retardo). Del ejemplo: N ≥ 1 + 40/8 = 6.
Para numeración de n bits: Go-Back-N admite $N \le 2^n - 1$; Selective Repeat $N \le 2^{n-1}$.

## Go-Back-N (GBN)
- **Emisor**: mantiene `base` (más antigua sin confirmar) y `next_seq`; un **único temporizador** asociado a `base`. Si expira, retransmite **toda la ventana** base..next_seq-1.
- **Receptor**: solo acepta la trama exactamente esperada (`expected_seq`); descarta las fuera de orden y reenvía el ACK de la última correcta. No tiene búfer de reordenamiento.
- **ACK acumulativo**: ack = k confirma todas las tramas ≤ k.
- Simple, pero ante una pérdida desperdicia ancho de banda reenviando tramas buenas.

### Ejemplo paso a paso (N = 4, tramas 0-7, se pierde la 2)
1. El emisor envía 0,1,2,3. Llegan 0,1,3.
2. Receptor: acepta 0 (ack0), 1 (ack1), descarta 3 (reenvía ack1).
3. El emisor desliza base a 2 al recibir ack1; el temporizador de la trama 2 expira.
4. Reenvía 2,3,4,5 (toda la ventana). Receptor acepta 2,3,4,5 en orden.
Se enviaron 4 + 4 = 8 tramas para entregar 6: la 3 se transmitió dos veces.

## Selective Repeat (SR)
- El receptor **acepta y almacena** tramas dentro de su ventana aunque lleguen fuera de orden; ACK **individual**.
- El emisor tiene un temporizador por trama y retransmite solo la perdida.
- Menos retransmisiones, más complejidad (búfer y temporizadores). TCP real es un híbrido: ACK acumulativo + SACK opcional + un temporizador.

| Esquema | Ventana emisor | Ventana receptor | Retransmite al fallar |
|---|---|---|---|
| Stop-and-Wait | 1 | 1 | la trama |
| Go-Back-N | N | 1 | toda la ventana |
| Selective Repeat | N | N | solo la perdida |

## Temporizadores y retroceso exponencial
Si el RTO es muy corto hay retransmisiones espurias; si es muy largo, la recuperación es lenta. Tras cada expiración consecutiva el RTO se duplica hasta un máximo: **retroceso exponencial** (*exponential backoff*), que evita agravar una congestión. SFTP-U usa RTO inicial 300 ms, máximo 2400 ms, secuencia 300, 600, 1200, 2400, 2400.

## Idempotencia
Con retransmisiones aparecen **duplicados**; el receptor debe tratarlos sin efectos secundarios (descartar y reconfirmar). Esto incluye mensajes de control (p. ej. un `PUT_INIT` repetido no debe reiniciar la transferencia).

## Código real: emisor GBN (resumen de `gbn.py`)
```python
def llenar_ventana(self, now_ms):
    while self.next_seq < self.base + self.window and self.next_seq < self.total:
        ...                       # emite los bloques que caben en la ventana
    if emitidos and self.timer_deadline is None:
        self._arrancar_timer(now_ms)   # un solo temporizador, ligado a 'base'

def on_timeout(self, now_ms):
    self.retries += 1
    if self.retries > self.max_retries: return None   # abortar: canal caído
    reenviados = self._retransmitir_ventana(now_ms)   # GBN: toda la ventana
    self.rto = min(self.rto * 2, self.rto_max)        # retroceso exponencial
```
Observación de diseño: el reloj entra como parámetro `now_ms`, lo que permite pruebas deterministas con un reloj falso.

## Errores comunes
- Usar el mismo número de secuencia para tramas distintas dentro de la ventana (ventana > límite).
- Contar un NACK o ACK duplicado como "reintento": el desorden no es un canal caído.
- Reiniciar el temporizador con cada ACK duplicado y así retrasar la retransmisión necesaria.
- Medir RTT con tramas retransmitidas (ambigüedad; algoritmo de Karn).

## Ejercicios propuestos
1. R = 10 Mbps, L = 1250 B, RTT = 100 ms. ¿Ventana mínima para U = 100 %? *Resp.: L/R = 1 ms, N = 101.*
2. Con SR y 3 bits de secuencia, ¿ventana máxima? *Resp.: 4.*
3. GBN con N = 5; se pierde una trama aislada. ¿Cuántas retransmisiones? *Resp.: hasta 5 (la perdida y las siguientes en ventana).*

## Conexiones
[[Comunicaciones II - 03 TCP conexión flujo y congestión]], [[Comunicaciones II - 11 SFTP-U Go-Back-N adversario y resultados]], [[Comunicaciones I - 10 Control de enlace flujo y ARQ]], [[Sistemas Distribuidos]] (fallos y reintentos).

## Fuente
Conocimiento general (Kurose-Ross cap. 3) y `~/Documentos/UNET/Comunicaciones 2/parcial 3/server/gbn.py` (parámetros: ventana 4, RTO 300-2400 ms, 8 reintentos).
