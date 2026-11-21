---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 2/P2P.pdf (Abel Santín González, "Sistemas Operativos Distribuidos")
---
# Sistemas Distribuidos - 05 Peer-to-peer

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 04 Multiprocesadores y objetos distribuidos]]
Siguiente: [[Sistemas Distribuidos - 06 SOA y servicios web]]

## Contexto y objetivo
El documento P2P.pdf (3767 palabras) explica las redes entre iguales: elementos, arquitecturas (híbrida, pura, mixta), búsqueda de recursos, tablas hash distribuidas (DHT) y la plataforma JXTA. Objetivo: entender cómo se organiza un SD **sin servidores fijos**.

## 1. Definición y elementos
"P2P" significa de igual a igual. Una red P2P **no tiene clientes y servidores fijos**: cada nodo actúa a la vez como cliente y servidor. Todos pueden realizar las mismas operaciones aunque difieran en velocidad, ancho de banda y almacenamiento.

- **Par (peer):** unidad básica; entidad capaz de hacer trabajo útil y comunicar resultados.
  - *Pares simples:* sirven a un usuario final; dinámicos y heterogéneos (conexión intermitente).
  - *Superpares:* ayudan a otros a encontrar pares o recursos; relativamente estáticos y siempre conectados.
- **Grupo de pares:** conjunto formado por un interés común; ofrece servicios no accesibles a pares externos y sirve para dividir el espacio de red.
- **Servicios:** de par (si el par cae, el servicio cae) o de grupo de pares (varios miembros dan acceso redundante; si uno cae el servicio sigue).

## 2. Arquitecturas
| Modelo | Generación/ejemplo | Funcionamiento | Pros / contras |
|---|---|---|---|
| **Híbrido o centralizado** | 1.ª, Napster | Un servidor central indexa qué archivos tiene cada par; el cliente consulta al servidor y luego descarga directo del par | Búsqueda muy rápida si el servidor está bien dimensionado; **costoso** y punto único de fallo |
| **P2P puro (descentralizado)** | 2.ª, Gnutella | Sin servidor; cada nodo mantiene conexiones con otros; las búsquedas se **inundan** (flooding) con un **TTL** que baja en cada salto y descarta la petición al llegar a 0; las respuestas vuelven por el mismo camino | Robusto y económico; búsquedas costosas en tiempo y ancho de banda; un recurso existente puede no encontrarse (TTL) |
| **Mixto (semicentralizado)** | 3.ª | Algunos pares son **superpares** que gestionan el tráfico; cada cliente se conecta solo a unos pocos superpares; los superpares se interconectan | Escalable, velocidad comparable al centralizado |

## 3. Búsqueda de pares y contenidos
No hay conocimiento global, así que la búsqueda es el gran problema. Tres niveles:
1. **En caché (sin descubrimiento):** cada par guarda recursos descubiertos con tiempo de vida (cola FIFO); reduce el tráfico. Típico para hallar superpares al conectarse.
2. **Directa:** preguntar a pares vecinos por broadcast/multicast (P2P puro).
3. **Indirecta:** los superpares buscan en nombre del par (arquitecturas mixtas).

## 4. Tablas hash distribuidas (DHT)
Una DHT distribuye el almacenamiento y la búsqueda de una tabla hash entre muchas máquinas; todos los nodos son iguales y pueden entrar y salir libremente. Operaciones: `store(clave, valor)` y `lookup(clave)`.

**Diseño base del documento**
1. Cada nodo recibe un identificador aleatorio y único de $k$ bits (típicamente $k=64$). Los nodos forman un **anillo**: el siguiente es el de ID inmediatamente superior (el mayor apunta al menor).
2. Distancia (con aritmética módulo $2^k$): si $a=b$, 0; si $a<b$, $b-a$; si no, $2^k+(b-a)$.
3. La clave (p. ej. el nombre del recurso) se pasa por una función hash a $k$ bits y se trata como un ID; el nodo responsable es su **sucesor** en el anillo. El hash debe repartir uniformemente.
4. Pseudocódigo del material:
```
findNode(start, key):
    current = start
    while distance(current.id, key) > distance(current.next.id, key):
        current = current.next
    return current
lookup(start, key):      return findNode(start, key).data[key]
store(start, key, v):    findNode(start, key).data[key] = v
```
5. **Unión (join):** el nuevo nodo busca su sucesor, se inserta entre sucesor y antecesor y asume las claves que le corresponden; los punteros no cambian hasta copiar las claves. **Salida (leave):** copia sus datos al predecesor, que actualiza su puntero. **Caída:** los datos del nodo quedan temporalmente no disponibles; los protocolos reasignan/replican; el antecesor reinicia un proceso de unión para recomponer el anillo.
6. **Optimización:** con solo el puntero al siguiente hacen falta hasta $n$ saltos (media $n/2$). Si cada nodo guarda una **tabla de $k$ punteros** a distancias que crecen exponencialmente (el puntero $x$ apunta cerca de $\text{ID}+2^{x-1}$), la búsqueda es **logarítmica**, $O(\log n)$ (idea de Chord). La tabla desactualizada no rompe la búsqueda mientras los punteros "siguiente" sean correctos, pero se pierde la ventaja logarítmica.

## 5. JXTA
Proyecto de protocolos abiertos P2P: define pares, grupos, servicios y una pila de protocolos independiente de la red de transporte (los identificadores no se basan en IP:puerto, que es inflexible). *(El documento solo introduce JXTA; detalle: no se pudo extraer más contenido.)*

## 6. Ejemplo resuelto: DHT con IDs pequeños
$k=4$ (IDs 0-15), nodos 1, 6, 10, 14. Clave con hash 8: ¿qué nodo la guarda? Es el sucesor: el primer ID mayor o igual a 8, o sea **10**. Clave con hash 15: no hay ID mayor, se da la vuelta: nodo **1**. Si llega el nodo 8: asume del sucesor (10) las claves en (6,8], por ejemplo la clave 8. Distancia(14,1) $=16+(1-14)=3$.

## Errores comunes
- Creer que P2P es solo compartir archivos: sirve para cómputo, mensajería, almacenamiento.
- Olvidar que el flooding sin TTL satura la red.
- Usar el hash de la clave sin normalizar a $k$ bits.

## Ejercicios propuestos
1. ¿Por qué el modelo mixto escala mejor que el puro? *R: menos nodos intervienen en el encaminamiento; solo superpares enrutan.*
2. Con $n=1024$ nodos y tablas de punteros, ¿saltos esperados? *R: del orden de $\log_2 1024=10$, frente a ~512 en anillo simple.*
3. ¿Qué sucede con las claves de un nodo que cae? *R: quedan temporalmente inaccesibles salvo réplica.*

## Conexiones
[[Sistemas Distribuidos - 03 Modelo cliente-servidor y arquitecturas por capas]] (contraste), [[Estructura de Datos]] (tablas hash), [[Comunicaciones II]].

## Fuente
P2P.pdf.
