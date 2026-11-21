---
tags: [clase, semestre-VII]
materia: Comunicaciones II
fuente: ~/Documentos/UNET/Comunicaciones 2/parcial 2/Informe_OSINT_UNET.md
---
# Comunicaciones II - 09 OSINT reconocimiento pasivo y Google Hacking

Materia: [[Comunicaciones II]]
Anterior: [[Comunicaciones II - 08 Seguridad en redes criptografía y TLS]]
Siguiente: [[Comunicaciones II - 10 SFTP-U Diseno del protocolo y trama]]

## Contexto y objetivo
El **Parcial 2** es una "Auditoría pasiva de infraestructura mediante OSINT (Google Hacking)" sobre el dominio `unet.edu.ve`, con alcance ampliado de control (`edu.ve`, `gob.ve`, búsquedas globales). Objetivo: demostrar que se puede mapear la superficie de exposición de una organización **sin enviar un solo paquete** a su infraestructura, y explicar el impacto de cada hallazgo desde la óptica de telecomunicaciones. El informe existe en .md, .pdf y .html, con capturas numeradas (algunas "censuradas"). En la versión leída varios campos de evidencia y "resultados aproximados" están como plantillas sin completar (`[INSERTAR CAPTURA ...]`); no se reproducen datos de resultados reales.

## Marco ético
- **No interferencia**: sin escáneres de puertos ni herramientas activas; solo el motor de búsqueda y lo ya indexado.
- **Confidencialidad**: datos sensibles (credenciales, correos, IP internas) se censuran, no se almacenan ni usan.
- **Divulgación responsable**: no se accede ni prueba ningún sistema; los hallazgos graves se reportan.
- Nota metodológica: que un dork no devuelva resultados en el dominio objetivo es **un hallazgo positivo**; se documenta y se usa un dork de ampliación para ilustrar el patrón.

## Metodología (4 pasos)
1. **Modelado** de qué recurso se busca. 2. **Construcción del dork** con operadores. 3. **Verificación pasiva** (solo título, URL, fragmento; caché de Google o Wayback Machine, nunca el servidor). 4. **Documentación** (dork, nº aproximado de resultados, captura censurada, impacto).

### Operadores
| Operador | Función |
|---|---|
| `site:` | restringe a un dominio |
| `filetype:` / `ext:` | por extensión |
| `intitle:` / `inurl:` / `intext:` | título, URL, cuerpo |
| `intitle:"index of"` | listados de directorio abiertos (autoindex) |
| `\|` u `OR`, `-` | alternativa, exclusión |

## Los cinco puntos del análisis
### 1. Paneles de administración de routers
Dork UNET: `site:unet.edu.ve (intitle:"RouterOS" | intitle:"router" | inurl:webfig | inurl:"level/15")`. Ampliación: `intitle:"RouterOS router configuration page"`, `intitle:"Cisco" inurl:"level/15/exec"`.
Impacto: el **plano de gestión** publicado hacia la WAN (HTTP 80, HTTPS 443, Winbox 8291) sin ACL, a veces con credenciales por defecto -> control de enrutamiento, NAT, firewall y DNS. Mitigación: gestión solo por SSH (22) con ACL, VLAN de administración, `ip firewall filter` que descarte gestión desde WAN.

### 2. Archivos de captura .pcap/.cap
Dork: `site:unet.edu.ve (ext:pcap | ext:cap | ext:pcapng)`; ampliación con `intitle:"index of" (".pcap" | ".cap") -site:wireshark.org`.
Impacto doble: autoindex activo (mod_autoindex / `autoindex on`) y contenido capa 2-7 con protocolos sin cifrar: FTP (21), Telnet (23), HTTP Basic (credenciales en Base64), POP3/IMAP/SMTP sin STARTTLS, SNMP (161) con *community strings*. Mitigación: desactivar autoindex, sacar capturas del docroot, usar SFTP/SSH/HTTPS/SNMPv3.

### 3. Archivos de topología (Packet Tracer / Visio)
Dork: `site:unet.edu.ve (ext:pkt | ext:pka | ext:vsd | ext:vsdx)`; ampliación `(ext:pkt | ext:pka) (site:edu.ve | site:gob.ve)`.
Impacto: fuga de **diseño** (direccionamiento, VLAN, modelos de equipos, protocolos de enrutamiento) que ahorra la fase de descubrimiento al atacante; aunque muchos son ejercicios ficticios. Mitigación: tratar diagramas como confidenciales.

### 4. IoT y CCTV sin autenticación
Dorks por huella de modelo: `inurl:"/view/index.shtml"` (Axis), `intitle:"Live View / - AXIS"`, `inurl:"ViewerFrame?Mode="` (Panasonic), `intitle:"webcamXP" | intitle:"webcam 7"`. No se usa `site:` porque las cámaras rara vez publican dominio; ubicarlas con Shodan/Censys sería activo y queda fuera del alcance pasivo.
Impacto: port forwarding directo, UPnP, RTSP (554) o MJPEG sin credenciales, claves por defecto -> video/audio interceptable. Mitigación: no exponer a WAN, desactivar UPnP, cambiar credenciales, VPN.

### 5. Archivos .env y logs FTP con "password"
Dork: `site:unet.edu.ve (ext:env | ext:sql | ext:log) intext:password`; ampliación `filetype:env "DB_PASSWORD"`, `intitle:"index of" ".env"`, `intext:"ftp" filetype:log intext:password`.
Impacto: `.env` servido como texto estático (credenciales de MySQL 3306 / PostgreSQL 5432, claves API); FTP en claro y logs que guardan contraseñas. Mitigación: `.env` fuera del docroot o bloqueado, no exponer puertos de BD a WAN, usar SFTP/FTPS.

## Conclusiones del informe
1. El reconocimiento pasivo es indetectable y primera fase de una auditoría real. 2. Casi todas las exposiciones se reducen a **servicios de gestión/datos publicados a la WAN sin filtrado** y **protocolos sin cifrar**. 3. La ausencia de resultados en routers, capturas y `.env` bajo `unet.edu.ve` es indicador positivo; los hallazgos ilustrativos vienen de dorks de ampliación, pasivos y censurados.

## Cómo diseñar un dork (ejemplo resuelto)
Meta: encontrar PDFs con "contraseña" en un dominio. Paso 1: dominio -> `site:ejemplo.edu.ve`. Paso 2: tipo -> `filetype:pdf`. Paso 3: texto -> `intext:"contraseña"`. Resultado: `site:ejemplo.edu.ve filetype:pdf intext:"contraseña"`. Paso 4: excluir ruido: `-inurl:instructivo`. Se verifica solo en la página de resultados.

## Errores comunes
- Abrir los enlaces encontrados: deja de ser pasivo y puede ser ilegal.
- No censurar credenciales en las capturas.
- Interpretar "0 resultados" como fallo del trabajo (es hallazgo positivo).
- Mezclar alcance: dorks globales son solo ilustrativos, sin atribuir a la UNET lo hallado fuera de su dominio.

## Ejercicios propuestos
1. Escriba un dork para listados abiertos con archivos `.bak` en `*.gob.ve`. *Resp.: `intitle:"index of" ".bak" site:gob.ve`.*
2. ¿Qué puerto usa Winbox? *Resp.: 8291/TCP.*
3. ¿Por qué un `.pcap` de FTP es más grave que uno de HTTPS? *Resp.: FTP expone credenciales en claro; HTTPS cifra el contenido.*

## Conexiones
[[Comunicaciones II - 08 Seguridad en redes criptografía y TLS]], [[Comunicaciones II - 05 Capa de red IP y enrutamiento]], [[Administración de Redes]].

## Fuente
`~/Documentos/UNET/Comunicaciones 2/parcial 2/Informe_OSINT_UNET.md` (leído completo). No se abrieron las capturas PNG ni el PDF/HTML (versiones del mismo informe).
