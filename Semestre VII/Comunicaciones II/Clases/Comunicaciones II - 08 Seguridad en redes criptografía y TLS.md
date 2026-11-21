---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: conocimiento general
---
# Comunicaciones II - 08 Seguridad en redes criptografía y TLS

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 07 Contenedores Docker y arquitectura cliente-servidor]]
Siguiente: [[Comunicaciones II - 09 OSINT reconocimiento pasivo y Google Hacking]]

## Contexto y objetivo
Los protocolos originales de Internet (FTP, Telnet, HTTP, SMTP, SNMPv1) no cifran ni autentican. Esta nota presenta las propiedades de seguridad, criptografía simétrica/asimétrica, funciones hash, firmas, TLS, cortafuegos y amenazas comunes, como marco para el informe OSINT y para entender por qué SFTP-U v2 usa CRC32 y SHA-256 (con las salvedades que se explican).

## Propiedades de seguridad (tríada CIA y más)
- **Confidencialidad**: solo los autorizados leen. **Integridad**: los datos no se alteran sin detección. **Disponibilidad**: el servicio responde. Además: **autenticación** (¿quién eres?), **no repudio**, **autorización**.

## Criptografía
### Simétrica
Una sola clave $K$ cifra y descifra. Rápida: AES-128/256 (bloques de 128 bits; modos CBC, CTR, **GCM** que además autentica). Problema: distribuir la clave.

### Asimétrica
Par (pública, privada). RSA (factorización), curvas elípticas (ECDSA, ECDH/X25519). Cifrar con la pública, descifrar con la privada; **firmar** con la privada, verificar con la pública. Más lenta: se usa para intercambiar una clave simétrica de sesión.

**Diffie-Hellman** (ejemplo con números pequeños): $p = 23, g = 5$. A elige a = 6: $A = 5^6 \bmod 23 = 8$. B elige b = 15: $B = 5^{15} \bmod 23 = 19$. Clave: $B^a = 19^6 \bmod 23 = 2$ y $A^b = 8^{15} \bmod 23 = 2$. Un espía ve p, g, 8 y 19 pero no a ni b.

### Funciones hash
$H(m)$ de longitud fija, resistente a preimagen y colisiones: SHA-256 (256 bits). **No cifran**; sirven para integridad y huellas. Para autenticar mensajes se usa **HMAC** (hash con clave).
- Diferencia clave con CRC: el **CRC32** detecta *errores accidentales* con alta probabilidad pero es lineal y trivial de falsificar por un adversario; un hash criptográfico dificulta construir otro mensaje con la misma huella. En SFTP-U el CRC protege cada trama frente al ruido y el SHA-256 verifica el archivo completo; ninguno autentica al emisor, por lo que un atacante activo podría recalcular ambos.

## Certificados y PKI
Un certificado X.509 liga una clave pública a una identidad, firmado por una **autoridad certificadora (CA)**. El navegador valida la cadena hasta una raíz de confianza, el nombre (SAN) y la vigencia.

## TLS 1.3 (resumen del saludo)
1. ClientHello: versiones, suites, parte pública ECDHE.
2. ServerHello + certificado + firma + Finished (ya cifrado con claves derivadas).
3. Cliente verifica, envía Finished. Datos con AEAD (AES-GCM o ChaCha20-Poly1305).
Un solo RTT (0-RTT opcional). Proporciona confidencialidad, integridad y autenticación del servidor y **secreto perfecto hacia adelante**. HTTPS = HTTP+TLS, SFTP usa SSH (equivalente conceptual). DTLS adapta TLS a UDP.

## Cortafuegos y filtrado
- Filtro de paquetes sin estado (ACL por IP/puerto/protocolo).
- **Con estado** (stateful): rastrea conexiones; permite el tráfico de retorno solo de sesiones iniciadas desde dentro.
- Proxy/WAF de aplicación (capa 7). IDS/IPS detectan firmas y anomalías.
- Principio de **mínimo privilegio** y **denegar por defecto**; zona desmilitarizada (DMZ) para servidores públicos.
```
# Ejemplo iptables: permitir SSH solo desde la red de gestión, denegar el resto
iptables -P INPUT DROP
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp -s 10.0.0.0/24 --dport 22 -j ACCEPT
```

## Amenazas frecuentes
| Ataque | Descripción | Mitigación |
|---|---|---|
| Sniffing | captura de tráfico en claro | cifrado (TLS, SSH) |
| Suplantación (ARP/DNS/IP spoofing) | falsear identidad | DNSSEC, DAI, autenticación |
| MITM | intermediario activo | TLS con validación de certificados |
| SYN flood / DDoS | agotar recursos | SYN cookies, limitación de tasa, CDN |
| Replay | reinyección de mensajes válidos | nonces, números de secuencia, marcas de tiempo |
| Inyección (SQL, comando) | datos tratados como código | consultas parametrizadas, validación |
| Fuerza bruta | probar credenciales | bloqueo, MFA, contraseñas fuertes |
| Reconocimiento (OSINT, escaneo) | recolectar información | minimizar exposición |

## Ética y legalidad
Toda prueba debe tener **alcance autorizado**. El reconocimiento pasivo (buscadores, registros públicos) no genera tráfico hacia el objetivo; el escaneo activo sí y puede ser ilegal sin permiso. Divulgación responsable: reportar al propietario.

## Errores comunes
- Pensar que hashear una contraseña con SHA-256 simple es suficiente (usar bcrypt/Argon2 con sal).
- Creer que base64 es cifrado (HTTP Basic Auth es solo codificación).
- Confundir cifrado con integridad: un cifrado sin autenticación (CBC solo) es maleable.
- Reutilizar IV/nonce en modos como CTR/GCM.

## Ejercicios propuestos
1. ¿Cuántas claves simétricas se necesitan para que n personas se comuniquen por pares? *Resp.: n(n-1)/2.*
2. ¿Por qué el CRC32 no sirve contra un atacante activo? *Resp.: es lineal y sin clave; puede recalcularse.*
3. ¿Qué propiedad aporta un HMAC que no da un hash simple? *Resp.: autenticidad (requiere clave secreta).*

## Conexiones
Informe práctico: [[Comunicaciones II - 09 OSINT reconocimiento pasivo y Google Hacking]]. Diseño con integridad: [[Comunicaciones II - 10 SFTP-U Diseno del protocolo y trama]]. Gestión de redes: [[Administración de Redes]].

## Fuente
Conocimiento general (Stallings; Kurose-Ross cap. 8; RFC 8446).
