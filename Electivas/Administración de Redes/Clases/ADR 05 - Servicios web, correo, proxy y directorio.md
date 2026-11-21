---
tags: [clase, electiva]
materia: Administración de Redes
fuente: "conocimiento general"
---
# ADR 05 - Servicios web, correo, proxy y directorio

Materia: [[Administración de Redes]]
Anterior: [[ADR 04 - Servicios DNS y DHCP]]
Siguiente: [[ADR 06 - Gestión, monitoreo y FCAPS]]

## Contexto y objetivo
Sobre DNS y DHCP se montan los servicios que usa la organización: sitios web, correo, acceso controlado a Internet y autenticación centralizada. Objetivo: configurar un servidor web con HTTPS y proxy inverso, entender el flujo del correo (SMTP, IMAP, SPF, DKIM, DMARC), un proxy de salida y un directorio LDAP.

## Teoría

### Servidor web y proxy inverso
Apache o Nginx sirven contenido estático y delegan en aplicaciones. Un **proxy inverso** recibe las conexiones externas, termina TLS y reenvía a servidores internos; permite balanceo, caché y ocultar la topología. HTTPS: certificado X.509 firmado por una CA (Let's Encrypt, protocolo ACME). Hosts virtuales: varios sitios en una IP según el nombre (cabecera `Host`/SNI).

### Correo electrónico
- **SMTP** (25 entre servidores; 587 envío autenticado con STARTTLS; 465 TLS implícito).
- **IMAP** (143/993) y POP3 (110/995) para leer.
- Componentes: MUA (cliente), MSA, MTA (Postfix), MDA (Dovecot).
- Anti-suplantación: **SPF** (qué IP pueden enviar por el dominio, registro TXT), **DKIM** (firma criptográfica del mensaje), **DMARC** (política si fallan SPF/DKIM). Registros MX y PTR coherentes con el nombre del servidor.

### Proxy de salida
Squid: controla y registra la navegación, caché, listas de acceso por red, usuario o dominio; puede ser *transparente* (redirección de puerto 80) o explícito.

### Directorio
**LDAP** (389, 636 LDAPS): árbol jerárquico de entradas con DN, p. ej. `uid=ana,ou=personas,dc=lab,dc=local`. **Active Directory** combina LDAP, Kerberos y DNS para autenticación y políticas de grupo (GPO) en entornos Windows. Beneficio: una sola cuenta para correo, VPN, Wi-Fi y servidores.

## Ejemplo resuelto
Sitio `web.lab.local` con proxy inverso Nginx hacia una app en el puerto 3000, más comprobación del correo.

1. Nginx como proxy inverso con TLS (`/etc/nginx/sites-available/web`):
```
server {
    listen 80;
    server_name web.lab.local;
    return 301 https://$host$request_uri;
}
server {
    listen 443 ssl http2;
    server_name web.lab.local;
    ssl_certificate     /etc/ssl/certs/web.crt;
    ssl_certificate_key /etc/ssl/private/web.key;
    ssl_protocols TLSv1.2 TLSv1.3;
    add_header Strict-Transport-Security "max-age=31536000" always;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
```bash
sudo nginx -t && sudo systemctl reload nginx      # validar y recargar
curl -I https://web.lab.local --cacert ca.crt
openssl s_client -connect web.lab.local:443 -servername web.lab.local </dev/null | openssl x509 -noout -dates
# Certificado público automatizado (si el dominio es público)
sudo certbot --nginx -d web.example.org
```
2. Registros DNS de correo para `example.org` (ejemplo):
```
example.org.          IN MX  10 mail.example.org.
example.org.          IN TXT "v=spf1 mx ip4:203.0.113.25 -all"
_dmarc.example.org.   IN TXT "v=DMARC1; p=quarantine; rua=mailto:dmarc@example.org"
```
Pruebas:
```bash
dig example.org MX +short
dig example.org TXT +short
swaks --to ana@example.org --server mail.example.org --port 587 --tls --auth LOGIN
```
Lectura: `-all` en SPF rechaza todo remitente no listado; DMARC `p=quarantine` envía a spam los fallos; `rua` recibe reportes agregados.

3. Squid mínimo (`/etc/squid/squid.conf`):
```
acl lan src 192.168.20.0/24
acl bloqueados dstdomain .redsocial.example
http_access deny bloqueados
http_access allow lan
http_access deny all
http_port 3128
```
Cliente: `curl -x http://192.168.20.2:3128 http://example.org`; bitácora en `/var/log/squid/access.log`.

4. Consulta LDAP:
```bash
ldapsearch -x -H ldap://192.168.20.2 -D "cn=admin,dc=lab,dc=local" -W \
  -b "ou=personas,dc=lab,dc=local" "(uid=ana)" cn mail
```
Entrada LDIF de ejemplo:
```
dn: uid=ana,ou=personas,dc=lab,dc=local
objectClass: inetOrgPerson
cn: Ana Pérez
sn: Pérez
uid: ana
mail: ana@lab.local
```

## Errores comunes
- Permitir retransmisión abierta (*open relay*) en el MTA.
- Certificados vencidos o con nombre distinto al del sitio.
- Olvidar `X-Forwarded-For`: la aplicación solo ve la IP del proxy.
- Publicar LDAP sin TLS ni autenticación.
- PTR del servidor de correo que no coincide con su nombre: los correos terminan en spam.

## Ejercicios propuestos
1. ¿Qué puerto usar para que un cliente envíe correo autenticado? *Respuesta: 587 con STARTTLS (o 465).*
2. ¿Qué protege DKIM que SPF no? *Respuesta: la integridad del mensaje (firma), y funciona aunque el correo sea reenviado.*
3. ¿Ventaja de terminar TLS en el proxy inverso? *Respuesta: certificados centralizados y servidores internos más simples.*

## Conexiones
[[Comunicaciones II]] (capa de aplicación), [[Sistemas Operativos]] (servicios, systemd, permisos), [[Sistemas Distribuidos]] (balanceo, servicios), [[Administración de Redes]] (nota principal).

## Fuente
Conocimiento general: RFC 5321 (SMTP), 7208 (SPF), 6376 (DKIM), 7489 (DMARC), 4511 (LDAP); documentación de Nginx, Postfix y Squid.
