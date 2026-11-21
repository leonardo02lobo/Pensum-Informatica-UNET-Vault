---
tags: [clase, semestre-VIII]
materia: Sistema de Información II
---
# Sistema de Información II - Seguridad, Control de Acceso y Continuidad Operativa

Materia: [[Sistema de Información II]]
Anterior: [[Sistema de Información II - Inteligencia de Negocios, Data Warehouse y OLAP]]
Siguiente: [[Sistema de Información II - Implantación, Gestión del Cambio y Gobierno de TI]]

## Contexto y objetivo
Diseñar controles de **seguridad de la información** (tríada CIA), mecanismos de **autenticación y autorización**, **pistas de auditoría** y planes de **respaldo y continuidad operativa (BCP/DRP)** para proteger la integridad y disponibilidad de los sistemas empresariales.

## 1. Tríada CIA de la seguridad de la información
Todo control de seguridad en un SI protege al menos una de tres propiedades:
1. **Confidencialidad**: la información solo es accesible a personas o sistemas autorizados (cifrado en tránsito TLS/HTTPS, cifrado en reposo, control de acceso).
2. **Integridad**: los datos se mantienen exactos, completos y sin alteraciones no autorizadas (validaciones, firmas digitales, hashes, transacciones ACID).
3. **Disponibilidad**: los sistemas y datos están accesibles cuando los usuarios autorizados los necesitan (redundancia, balanceo de carga, respaldos).

## 2. Autenticación, Autorización y Auditoría (AAA)
- **Autenticación**: verificar *quién* es el usuario (algo que sabe: contraseña con hash seguro `bcrypt`/`Argon2`; algo que tiene: token MFA/TOTP; algo que es: biometría).
- **Autorización**: verificar *qué puede hacer*. El estándar empresarial es **RBAC** (*Role-Based Access Control*): los permisos se asignan a *roles* (Administrador, Asesor, Auditor) y los usuarios se asocian a roles, aplicando el **principio de mínimo privilegio**.
- **Auditoría y trazabilidad**: registro inmutable (*logs* de auditoría) de quién creó, consultó o modificó registros críticos, cuándo y desde dónde. Es indispensable para detectar fraudes y cumplir normativas.

### Controles contra vulnerabilidades comunes
- Consultas parametrizadas / ORM para prevenir **Inyección SQL**.
- Escape de salida y políticas CSP contra **XSS** (*Cross-Site Scripting*).
- Validación de permisos en cada endpoint del servidor (evitar **IDOR**, acceso directo inseguro a objetos por ID).

## 3. Respaldo (Backup) y Continuidad del Negocio
- **Regla 3-2-1 de respaldos**: mantener **3** copias de los datos, en **2** medios distintos, con **1** copia fuera de sitio (*off-site* o nube inmutable contra ransomware).
- **RPO (*Recovery Point Objective*)**: máxima pérdida de datos tolerable medida en tiempo (ej. si el RPO es 1 hora, los respaldos/logs deben permitir recuperar hasta hace $\le 1$ hora).
- **RTO (*Recovery Time Objective*)**: tiempo máximo tolerable para restablecer el servicio tras una falla grave.
- **BCP (*Business Continuity Plan*)** y **DRP (*Disaster Recovery Plan*)**: procedimientos probados periódicamente mediante simulacros de restauración (un respaldo nunca probado no es garantía de recuperación).

## Errores comunes
- Almacenar contraseñas en texto plano o con hashes rápidos sin sal (como MD5/SHA-1).
- Confiar en que la replicación en tiempo real de bases de datos sustituye a los respaldos: si un usuario o un atacante ejecuta `DELETE` o cifra la BD principal, el error se replica instantáneamente a la réplica.
- Otorgar permisos de superusuario de base de datos (`postgres`, `root`) a la aplicación web diaria.

## Ejercicios propuestos
1. Un sistema de nómina sufrió un ataque de ransomware a las 14:00. Su último respaldo diario se hizo a las 02:00 y tomó 4 horas restaurar el servicio. ¿Cuál fue el RPO real logrado y el RTO real?
   - *Respuesta*: pérdida de 12 horas de datos (RPO real = 12 h) y 4 horas de caída (RTO real = 4 h).
2. Clasifique bajo la tríada CIA: (a) implementar TLS/HTTPS; (b) usar un servidor secundario en *failover*; (c) verificar un hash SHA-256 de un archivo de respaldo.
   - *Respuesta*: (a) confidencialidad e integridad en tránsito; (b) disponibilidad; (c) integridad.

## Conexiones
- Seguridad en redes y protocolos en [[Redes de Computadores]].
- Roles, privilegios y recuperación en SGBD en [[Administración de Base de Datos]].
- Marco de gobernanza y auditoría en [[Sistema de Información II - Implantación, Gestión del Cambio y Gobierno de TI]].

## Fuente
Basado en el programa orientativo de [[Sistema de Información II]] (Laudon & Laudon, *Sistemas de Información Gerencial*; Kendall & Kendall, *Análisis y Diseño de Sistemas*).
