---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 2/Soa_WS.pdf
---
# Sistemas Distribuidos - 06 SOA y servicios web

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 05 Peer-to-peer]]
Siguiente: [[Sistemas Distribuidos - 07 Gerencia de procesos y asignación de procesadores]]

## Contexto y objetivo
Último modelo arquitectónico de la Clase 2: la **Arquitectura Orientada a Servicios (SOA)** y los **servicios web (Web Services)** como su implementación más difundida. El documento Soa_WS.pdf (809 palabras) define los conceptos y los estándares SOAP, WSDL y UDDI; esta nota los amplía.

## 1. SOA
- El modelo de referencia fue definido por **OASIS**. Su auge se debe a factores económicos y administrativos: permite el desarrollo distribuido de aplicaciones y la reutilización de componentes, conecta una organización ágil con las tecnologías que la apoyan y permite responder a cambios legales o tecnológicos.
- El desarrollo distribuido permite que distintos proveedores construyan partes sin conocer todo el proceso (más seguridad).
- Impacto organizacional: compartir y reutilizar servicios sustantivos; conviene fijar claramente **acuerdos de nivel de servicio (SLA)** para saber qué esperar de capacidad, habilidades y disponibilidad.
- **Servicio:** tarea de negocio requerida (normalmente de forma repetida) por uno o varios procesos; encapsula una unidad funcional tras una **interfaz bien definida**, independiente de la implementación; puede ser consumido por otros servicios o aplicaciones.
- **Aplicación compuesta:** conjunto de servicios relacionados e integrados que soportan un proceso sustantivo.
- **Orientación a servicios:** método para integrar aplicaciones y procesos como servicios ligados; las diferencias técnicas se superan con capas estándar de abstracción. SOA es un paradigma para organizar y usar capacidades distribuidas que pueden estar bajo distintos dominios de propiedad.

### Principios (conocimiento general)
Contrato de servicio estandarizado, bajo acoplamiento, abstracción, reutilización, autonomía, ausencia de estado (idealmente), descubribilidad y componibilidad.

## 2. Servicios web
Un **Web Service** es una forma de implementar SOA: método de comunicación entre dos dispositivos en una red, colección de protocolos y estándares abiertos para intercambiar datos entre aplicaciones. Gracias a estándares abiertos, programas en Java y Python, o en Windows y Linux, interoperan. La base es **XML + HTTP**.

Historia que cuenta el documento: **XML-RPC** (el protocolo más simple: un RPC codificado en XML sobre HTTP, mezcla de contenido XML y cabeceras HTTP) evolucionó a **SOAP**.

### Componentes
| Estándar | Qué es | Rol |
|---|---|---|
| **SOAP** (Simple Object Access Protocol) | Protocolo en XML para intercambiar información; formato de mensaje que puede extender cabeceras HTTP | Define qué información se envía y cómo; acceso al servicio |
| **WSDL** (Web Services Description Language) | Lenguaje XML para describir servicios y cómo acceder a ellos (diseñado por Microsoft e IBM) | Contrato: operaciones, mensajes, tipos, dirección |
| **UDDI** (Universal Description, Discovery and Integration) | Estándar XML de directorio para registrar, publicar y encontrar servicios web | Descubrimiento |

Flujo típico: el proveedor publica su descripción WSDL en un registro UDDI; el consumidor lo busca, obtiene el WSDL y envía mensajes SOAP sobre HTTP.

### Ejemplo de mensaje SOAP mínimo
```xml
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
  <soap:Body>
    <ObtenerSaldo><cuenta>0102-1234</cuenta></ObtenerSaldo>
  </soap:Body>
</soap:Envelope>
```
La respuesta tiene la misma estructura con `<ObtenerSaldoResponse>`. Es esencialmente una RPC (nota 09) en XML.

## 3. SOAP frente a REST
El material no trata REST; como complemento: REST usa recursos identificados por URL, verbos HTTP (GET, POST, PUT, DELETE) y formatos ligeros como JSON; es más simple y hoy dominante, mientras SOAP aporta contratos estrictos (WSDL), extensiones de seguridad (WS-Security) y transacciones (WS-*). Las arquitecturas de **microservicios** heredan la idea de SOA.

## 4. Ejemplo resuelto
*Una aseguradora quiere que su portal, su app móvil y un corredor externo usen el mismo cálculo de primas.* Se implementa un servicio `CalcularPrima` con contrato WSDL. Cambia la ley de primas: se modifica solo el servicio; portal, app y corredor siguen usando la misma interfaz (bajo acoplamiento). Si el corredor es otro dominio de propiedad, se acuerda un SLA (disponibilidad, tiempo de respuesta).

## Errores comunes
- Confundir SOA (arquitectura/paradigma) con servicios web (una tecnología).
- Diseñar servicios demasiado finos que generan llamadas excesivas por la red.
- Omitir el SLA y la seguridad entre dominios.

## Ejercicios propuestos
1. ¿Para qué sirve UDDI? *R: registro/descubrimiento de servicios.*
2. ¿Por qué SOAP evolucionó de XML-RPC? *R: por necesitar mensajes extensibles, tipos y estándares sobre la simplicidad inicial.*
3. Dé dos ventajas de SOA para una organización. *R: reutilización y agilidad ante cambios.*

## Conexiones
[[Sistemas Distribuidos - 09 RPC y RMI]], [[Sistemas Distribuidos - 03 Modelo cliente-servidor y arquitecturas por capas]], [[Desarrollo de Aplicaciones Web]], [[Ingeniería de Software]].

## Fuente
Soa_WS.pdf (OASIS, SOAP, WSDL, UDDI); REST y microservicios añadidos como conocimiento general.
