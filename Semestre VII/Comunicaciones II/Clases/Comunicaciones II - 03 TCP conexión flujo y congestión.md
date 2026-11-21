---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: conocimiento general
---
# Comunicaciones II - 03 TCP conexión flujo y congestión

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 02 Capa de transporte y UDP]]
Siguiente: [[Comunicaciones II - 04 Confiabilidad ARQ y ventana deslizante]]

## Contexto y objetivo
TCP (RFC 9293, antes RFC 793) convierte el servicio de datagramas de IP en un **flujo de bytes fiable, ordenado y con control de flujo y congestión**. Esta nota explica el segmento TCP, el establecimiento y cierre de conexión, la estimación de RTT, el control de flujo y el control de congestión.

## Características
- Orientado a conexión, **full duplex**, punto a punto (no hay multidifusión).
- Flujo de **bytes** (no conserva límites de mensaje).
- Fiabilidad mediante números de secuencia, ACK acumulativos, temporizador y retransmisión.
- Control de flujo (ventana del receptor) y control de congestión (ventana del emisor).

## Segmento TCP
Cabecera mínima de 20 B: puerto origen (16), puerto destino (16), **número de secuencia** (32, índice del primer byte del segmento), **número de acuse** (32, siguiente byte esperado), longitud de cabecera, banderas (URG, ACK, PSH, RST, SYN, FIN), **ventana** (16), checksum (16), puntero urgente, opciones (MSS, escala de ventana, SACK, marcas de tiempo).

## Establecimiento: saludo de tres vías
1. Cliente -> servidor: **SYN**, seq = x.
2. Servidor -> cliente: **SYN+ACK**, seq = y, ack = x+1.
3. Cliente -> servidor: **ACK**, seq = x+1, ack = y+1.
Estados: CLOSED -> SYN_SENT -> ESTABLISHED (cliente); LISTEN -> SYN_RCVD -> ESTABLISHED (servidor). Los números iniciales son aleatorios para evitar confusiones con segmentos viejos y ataques de predicción. Un servidor que acumula conexiones en SYN_RCVD es vulnerable a **SYN flood**; la defensa son las *SYN cookies*.

## Cierre
Cada sentido se cierra por separado: FIN -> ACK, luego el otro FIN -> ACK (cuatro segmentos). El que cierra primero entra a TIME_WAIT (2·MSL) para absorber segmentos retrasados. RST aborta inmediatamente.

## Fiabilidad
- El ACK es **acumulativo**: ack = n confirma todos los bytes hasta n-1.
- **Retransmisión rápida**: tres ACK duplicados del mismo número disparan retransmisión sin esperar al temporizador.
- SACK permite informar bloques recibidos fuera de orden.

### Estimación del temporizador
$$EstimatedRTT = (1-\alpha)\,EstimatedRTT + \alpha\,SampleRTT,\quad \alpha = 0.125$$
$$DevRTT = (1-\beta)\,DevRTT + \beta\,|SampleRTT - EstimatedRTT|,\quad \beta = 0.25$$
$$RTO = EstimatedRTT + 4\,DevRTT$$
Si expira el temporizador, RTO se **duplica** (retroceso exponencial); la misma idea se usa en SFTP-U.

**Ejemplo.** EstimatedRTT = 100 ms, DevRTT = 10 ms, SampleRTT = 140 ms. EstimatedRTT = 0.875·100 + 0.125·140 = 105 ms. DevRTT = 0.75·10 + 0.25·35 = 16.25 ms. RTO = 105 + 65 = 170 ms.

## Control de flujo
El receptor anuncia en cada ACK `rwnd = tamaño de búfer - datos no leídos`. El emisor mantiene $LastByteSent - LastByteAcked \le rwnd$. Si rwnd = 0, el emisor envía sondas de 1 byte para no quedar bloqueado. El *flujo* protege al receptor, no a la red.

## Control de congestión
El emisor mantiene `cwnd`; la ventana efectiva es $\min(cwnd, rwnd)$.
- **Slow start**: cwnd = 1 MSS y se duplica cada RTT (crece 1 MSS por ACK) hasta alcanzar `ssthresh`.
- **Evitación de congestión (AIMD)**: aumento aditivo de 1 MSS por RTT; ante pérdida, disminución multiplicativa (cwnd/2).
- Ante **3 ACK duplicados** (Reno): ssthresh = cwnd/2, cwnd = ssthresh + 3 (recuperación rápida). Ante **timeout**: ssthresh = cwnd/2, cwnd = 1 MSS y vuelve a slow start.
- CUBIC (Linux) y BBR son variantes modernas.

### Ejemplo resuelto
MSS = 1 KB, ssthresh = 8. Rondas: cwnd = 1, 2, 4, 8 (slow start, 4 RTT), luego 9, 10, 11 (lineal). En la ronda con cwnd = 12 hay timeout: ssthresh = 6, cwnd = 1; siguen 1, 2, 4, 6 y luego 7, 8...

### Rendimiento aproximado
Con pérdida p, RTT y MSS: $Throughput \approx \dfrac{1.22\,MSS}{RTT\sqrt{p}}$. Para MSS = 1460 B, RTT = 50 ms, p = 0.01 %: ≈ 1.22·11680 bits/(0.05·0.01) ≈ 28.5 Mbps.

## Errores comunes
- Confundir flujo (receptor) con congestión (red).
- Creer que el handshake transporta datos útiles en condiciones normales (solo opciones; TCP Fast Open es excepción).
- Pensar que TCP preserva "mensajes": una lectura puede devolver parte de un mensaje o varios; la aplicación debe delimitar (longitud, separador).
- Ignorar TIME_WAIT al reiniciar un servidor (`SO_REUSEADDR`).

## Ejercicios propuestos
1. El cliente envía SYN con seq=1000. ¿Qué ack lleva el SYN+ACK? *Resp.: 1001.*
2. Un enlace de 100 Mbps y RTT 80 ms: ¿qué ventana llena el canal? *Resp.: 100e6·0.08/8 = 1 MB.*
3. cwnd = 20 MSS y llegan 3 ACK duplicados (Reno): valores nuevos. *Resp.: ssthresh = 10, cwnd = 13 (10+3).*

## Conexiones
Comparación con confiabilidad propia sobre UDP: [[Comunicaciones II - 04 Confiabilidad ARQ y ventana deslizante]] y [[Comunicaciones II - 11 SFTP-U Go-Back-N adversario y resultados]]. TLS se apoya en TCP ([[Comunicaciones II - 08 Seguridad en redes criptografía y TLS]]).

## Fuente
Conocimiento general (RFC 9293, RFC 5681, Kurose-Ross cap. 3).
