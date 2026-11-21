---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 1/Clase 1 Complemento.pdf (Apéndices A y B) y conocimiento general
---
# Sistemas Distribuidos - 09 RPC y RMI

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 08 Comunicación entre procesos]]
Siguiente: [[Sistemas Distribuidos - 10 Relojes y orden de eventos]]

## Contexto y objetivo
Escribir `send`/`receive` a mano es incómodo. **RPC** (*Remote Procedure Call*, desarrollada hacia 1984) permite invocar un procedimiento remoto con la sintaxis de una llamada local; **RMI** hace lo propio con objetos. Los apéndices A y B del capítulo de Lafuente describen el mecanismo. Es la base técnica de los servicios web (nota 06) y de los objetos distribuidos (nota 04).

## 1. Idea y mecanismo de RPC
El cliente llama `res = servicio_rpc(parámetros)`; un **stub** (función sustituta o representante) en el cliente oculta el envío. El servidor tiene su propio stub (esqueleto) que despacha a la función real. Pasos del material (Fig. 1.A1):
1. Identificado el servicio como remoto, el mecanismo RPC del cliente **localiza el servidor** que lo soporta.
2. Se **serializan** (*marshaling*) los argumentos en formato estándar (p. ej. **XDR**, External Data Representation) para formar el cuerpo del mensaje.
3. Se envía el mensaje a la interfaz de red (p. ej. UDP/IP).
4. El cliente queda **bloqueado** esperando respuesta.
5. En el servidor, el mecanismo de RPC está en una función de espera; al llegar el mensaje lo recibe y **deserializa** los parámetros.
6. Ejecuta la función asociada al servicio.
7. Serializa el resultado, lo envía al cliente.
8. En el cliente se desbloquea, deserializa el resultado y lo devuelve al llamador como valor de retorno.

El servidor usa un bucle de espera de peticiones (`registrar servicio` + `esperar`). El nivel semántico de una librería RPC puede ser más o menos alto (paso de punteros, tipos complejos, manejo de excepciones).

```
Cliente            stub cliente        red        stub servidor      Servidor
 res=f(x) --->  marshal(x) ---send---->           unmarshal --->  f(x)
          <---  unmarshal <--reply---  marshal(res) <------------  res
```

## 2. Problemas específicos
- **Transparencia imperfecta:** la llamada puede fallar por razones que no existen en local (red caída, servidor caído). Hay que decidir la **semántica de invocación**:
  - *Quizás (maybe):* sin reintentos ni garantías.
  - *Al menos una vez (at-least-once):* el cliente reintenta; el servicio podría ejecutarse varias veces (aceptable si es idempotente).
  - *A lo sumo una vez (at-most-once):* el servidor detecta duplicados y reenvía la respuesta guardada.
  - *Exactamente una vez:* ideal, inalcanzable sin transacciones.
- **Paso de parámetros:** no se pueden pasar punteros; se copia el valor (copia-restauración) o se pasan referencias remotas.
- **Heterogeneidad:** distinta representación de enteros (orden de bytes) y cadenas: de ahí XDR.
- **Enlace (binding):** cómo se localiza el servidor (servicio de nombres, *portmapper*).
- **Fallos del cliente:** huérfanos (cómputos que nadie espera).
- Uso de una **IDL** (lenguaje de definición de interfaces) para generar stubs automáticamente (rpcgen, protobuf/gRPC hoy).

## 3. RMI (Apéndice B)
RMI es a la programación orientada a objetos lo que RPC a la procedimental: un objeto invoca un método de un **objeto remoto**; hay un **representante local** (proxy) del objeto en el cliente, que serializa la invocación. **Java RMI** extiende el modelo de objetos de Java:
- Las interfaces remotas extienden `java.rmi.Remote` y sus métodos lanzan `RemoteException`.
- Se crean proxies (*stubs*) mediante el compilador `rmic` (versiones antiguas; hoy se generan dinámicamente).
- Los objetos remotos se registran en un **registro de nombres** (`rmiregistry`) y el cliente hace `lookup`.
- Paso de parámetros: objetos serializables **por copia**; objetos remotos **por referencia**.

Esqueleto (conocimiento general):
```java
public interface Saldo extends java.rmi.Remote {
    double consultar(String cuenta) throws java.rmi.RemoteException;
}
// Servidor: exportar e inscribir
Saldo stub = (Saldo) UnicastRemoteObject.exportObject(impl, 0);
Registry reg = LocateRegistry.getRegistry();
reg.rebind("saldo", stub);
// Cliente
Saldo s = (Saldo) LocateRegistry.getRegistry("host").lookup("saldo");
double d = s.consultar("0102-1234");
```

## 4. Ejemplo resuelto: contar duplicados
Un cliente invoca `transferir(A,B,100)` con *at-least-once*; la respuesta se pierde y reintenta: la transferencia se ejecuta dos veces. **Solución:** asociar un identificador único de petición; el servidor guarda `(id -> resultado)` y, al ver el mismo id, devuelve el resultado sin reejecutar (*at-most-once*). Otra opción: diseñar la operación idempotente (`fijarSaldo(A, valor)` en lugar de `restar`).

## Errores comunes
- Tratar una RPC como llamada local sin manejar timeouts.
- Pasar estructuras con punteros.
- Reintentar operaciones no idempotentes.

## Ejercicios propuestos
1. ¿Qué hace el stub del cliente? *R: serializa argumentos, envía, espera y deserializa la respuesta.*
2. ¿Por qué se necesita XDR? *R: máquinas heterogéneas representan los datos distinto.*
3. ¿Qué semántica garantiza reintentar y descartar duplicados? *R: at-most-once.*

## Conexiones
[[Sistemas Distribuidos - 08 Comunicación entre procesos]], [[Sistemas Distribuidos - 06 SOA y servicios web]] (XML-RPC, SOAP), [[Sistemas Distribuidos - 04 Multiprocesadores y objetos distribuidos]].

## Fuente
Apéndices A y B del Complemento (Lafuente, UPV/EHU); ejemplos de código y semánticas: conocimiento general.
