---
tags: [tema, semestre-IX]
---
# Delitos informáticos y firma electrónica

Tema 4 de [[Legislación, Valores y Proyecto de País]].

## Delito informático
Elementos del delito: acto humano (acción u omisión), típico, antijurídico, culpable (dolo o culpa) y punible. Se distinguen los casos en que el computador es el **medio** del delito y aquellos en que es el **objeto** (software, datos). Las normas penales tradicionales cubren el hardware como bien mueble; el software y los datos requirieron tipificación específica.

Categorías de la Ley Especial contra los Delitos Informáticos (2001; verificar articulado vigente): contra sistemas que utilizan tecnologías de información (acceso indebido, sabotaje o daño, espionaje informático, falsificación de documentos), contra la propiedad, contra la privacidad de las personas y las comunicaciones, contra niños y adolescentes, y contra el orden económico.

## Documento y firma electrónica
- **Documento electrónico:** representación informática que da testimonio de un hecho.
- **Firma electrónica:** código que permite determinar la autenticidad e integridad de un documento y evita el repudio.
- **Firma digital:** especie de firma electrónica basada en criptografía asimétrica (claves pública y privada).
- **Certificado de firma digital:** vincula una clave pública con su titular (en Venezuela SUSCERTE acredita a los proveedores de servicios de certificación).
- **Integridad:** el documento no ha sido alterado tras la firma.

## Esquema técnico
```
Firma:    h = SHA-256(doc);  s = Cifrar_clave_privada(h)
Verifica: h' = SHA-256(doc); Descifrar_clave_publica(s) == h'
```
Garantiza autenticidad, integridad y no repudio; la confidencialidad exige cifrar con la clave pública del receptor.

## Relación
[[Comunicaciones II]], [[Sistemas Distribuidos]], [[Ingeniería de Software]] (requisitos de seguridad).

Material: [delitos informáticos](<Material/Tema 4/DELITOS INFORMATICOS.pdf>), [firma electrónica](<Material/Tema 4/FIRMA ELECTRONICA.pdf>).
