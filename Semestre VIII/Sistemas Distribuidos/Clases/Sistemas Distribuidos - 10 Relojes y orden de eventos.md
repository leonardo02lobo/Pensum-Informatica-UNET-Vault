---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 4/Sincronizacion.pdf
---
# Sistemas Distribuidos - 10 Relojes y orden de eventos

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 09 RPC y RMI]]
Siguiente: [[Sistemas Distribuidos - 11 Exclusión mutua y elección de líder]]

## Contexto y objetivo
Primera parte de la Clase 4 ("Sincronización de procesos", Parte 6 de las diapositivas). Sin memoria ni reloj común, ¿cómo se ordenan los eventos? Se estudian la **causalidad potencial**, los **relojes lógicos de Lamport** y los **relojes físicos** (Cristian, Berkeley). Resumen previo en [[Sincronización y Tolerancia a Fallos en SD]].

## 1. El problema: causalidad potencial
El material ilustra con el compilador `make`: un archivo `x.c` se compila en una máquina cuyo reloj marca 10 y el editor, en otra, marca 8 cuando lo modifica; como cada máquina tiene su propio reloj, a un evento ocurrido **después** se le puede asignar un tiempo **anterior** (por ejemplo `x.o` parece más viejo que `x.c`, y `make` no recompila). Dos filosofías:
- **Relojes lógicos:** importa la **consistencia interna**, no la cercanía al tiempo real.
- **Relojes físicos:** además deben mantenerse cerca del tiempo real (UTC) dentro de una cota.

## 2. Relación "ocurre antes" y relojes de Lamport
Relación $a \rightarrow b$ ("a ocurre antes de b"):
1. Si $a$ y $b$ son eventos del mismo proceso y $a$ precede a $b$, entonces $a\rightarrow b$.
2. Si $a$ es el envío de un mensaje y $b$ su recepción, $a\rightarrow b$.
3. Transitiva: $a\rightarrow b$ y $b\rightarrow c$ implican $a\rightarrow c$.
Si ni $a\rightarrow b$ ni $b\rightarrow a$, son **concurrentes** ($a\parallel b$): típicamente eventos en procesos distintos sin mensajes entre ellos.

**Algoritmo.** Cada proceso $P_i$ mantiene un contador $C_i$:
- Antes de cada evento: $C_i := C_i + 1$.
- Al enviar un mensaje $m$ se adjunta la marca $t_m = C_i$.
- Al recibir $m$: $C_j := \max(C_j, t_m) + 1$. (El material lo describe así: si el reloj del receptor muestra un valor anterior al tiempo de envío, el receptor "adelanta su reloj" a una unidad más que el tiempo de envío.)

Propiedad: si $a\rightarrow b$ entonces $C(a) < C(b)$. **El recíproco no vale:** $C(a)<C(b)$ no implica causalidad. Para obtener un **orden total** se desempata con el identificador de proceso: $(C, i)$ ordenado lexicográficamente; se necesita para la exclusión mutua de Ricart-Agrawala (nota 11).

### Ejemplo resuelto (Lamport)
Procesos P1 y P2, relojes iniciales 0. P1 ejecuta evento a (C1=1), envía m a P2 (C1=2, marca 2). P2 ejecuta evento b (C2=1). P2 recibe m: $C2=\max(1,2)+1=3$. P2 ejecuta c (C2=4). Orden: a(1) -> envío(2) -> recepción(3) -> c(4); b(1) es concurrente con a y con el envío, aunque su marca sea menor que la del envío.

### Relojes vectoriales (complemento)
Cada proceso mantiene un vector $V$ de $n$ contadores. Al evento local: $V_i[i]{+}{+}$; al enviar se adjunta $V$; al recibir: $V_j[k]=\max(V_j[k],V_m[k])$ para todo $k$ y luego $V_j[j]{+}{+}$. Entonces $a\rightarrow b \iff V(a)<V(b)$ (todas las componentes $\le$ y alguna $<$); si no son comparables, son concurrentes. Es la forma de **distinguir causalidad de concurrencia**.

## 3. Sincronización de relojes físicos
Cada reloj deriva: con tasa de deriva $\rho$ (p. ej. $10^{-6}$ s/s) y cota de desfase $\delta$, hay que resincronizar al menos cada $\delta/(2\rho)$ segundos.

### Algoritmo de Cristian
Un **servidor de tiempo** (con receptor UTC) responde a peticiones. El cliente mide:
- $T_0$: instante local de envío; $T_1$: instante local de recepción de la respuesta; $I$: tiempo de manejo de interrupción del servidor (debe conocerse).
- Tiempo de propagación de ida: $(T_1 - T_0 - I)/2$.
- El cliente fija su reloj en $t_{\text{servidor}} + (T_1-T_0-I)/2$.
Mejoras del material: hacer **varias mediciones**; **descartar** las que superen un umbral de $T_1-T_0$; promediar el resto, o usar la de menor ida y vuelta como la más precisa. El reloj nunca debe **retroceder** (se ralentiza gradualmente).

### Algoritmo de Berkeley
No hay servidor con hora exacta; se calcula un **promedio**. El demonio de tiempo (activo) sondea a todas las máquinas, les indica su hora y ellas responden con la **diferencia** respecto a la del demonio. El demonio calcula el promedio (incluyéndose) y envía a cada máquina **el ajuste** (no la hora, para evitar el retardo de la red). La hora del demonio se fija manualmente de modo periódico.

**Ejemplo del material:** demonio 3:00; máquinas con 3:25 (+25) y 2:50 (-10). Promedio de diferencias: $(0+25-10)/3=+5$. Nuevo tiempo: 3:05. Ajustes: demonio $+5$; máquina de 3:25 recibe $-20$; máquina de 2:50 recibe $+15$. Todas quedan en 3:05.

### NTP (complemento)
*Network Time Protocol*: jerarquía de servidores por *estratos*; estima desfase y retardo con cuatro marcas de tiempo: $\theta=\frac{(t_1-t_0)+(t_2-t_3)}{2}$, $\delta=(t_3-t_0)-(t_2-t_1)$.

## 4. Errores comunes
- Creer que $C(a)<C(b)$ prueba que $a$ causó $b$.
- Poner el reloj hacia atrás (rompe `make`, logs, expiraciones).
- Usar el valor del reloj de un nodo con mensajes sin considerar la latencia.

## 5. Ejercicios propuestos
1. P envía a Q un mensaje con marca 10; $C_Q=4$. ¿Valor tras recibir? *R: $\max(4,10)+1=11$.*
2. Cristian: $T_0=100$, $T_1=120$ ms, $I=2$ ms, servidor devolvió 5000. ¿Hora a fijar? *R: $5000+(20-2)/2=5009$ ms.*
3. Berkeley con diferencias $+10,-20,+4$ (demonio 0): ¿promedio? *R: $(0+10-20+4)/4=-1{,}5$.*

## Conexiones
[[Sistemas Distribuidos - 11 Exclusión mutua y elección de líder]], [[Sistemas Distribuidos - 12 Tolerancia a fallos, transacciones y consenso]] (marcas de tiempo en transacciones), [[Comunicaciones II]].

## Fuente
Sincronizacion.pdf (2438 palabras): causalidad potencial, Lamport, Cristian, Berkeley; relojes vectoriales y NTP añadidos como complemento.
