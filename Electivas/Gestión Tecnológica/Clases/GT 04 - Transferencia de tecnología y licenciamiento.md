---
tags: [clase, electiva]
materia: Gestión Tecnológica
fuente: "conocimiento general"
---
# GT 04 - Transferencia de tecnología y licenciamiento

Materia: [[Gestión Tecnológica]]
Anterior: [[GT 03 - Vigilancia tecnológica y prospectiva]]
Siguiente: [[GT 05 - Propiedad intelectual]]

## Contexto y objetivo
Una organización puede obtener tecnología fuera: comprándola, licenciándola, formando alianzas o recibiéndola desde universidades. Esta clase describe los mecanismos de transferencia, los contratos de licencia, la valoración de regalías y el proceso de negociación. El objetivo es comparar alternativas y calcular el valor de una licencia.

## Teoría

### Conceptos
- **Transferencia de tecnología**: movimiento de conocimiento, habilidades y derechos desde quien la posee hacia quien la va a usar.
- **Transferencia vertical** (de I+D a producción) y **horizontal** (entre organizaciones o países).
- **Capacidad de absorción** (Cohen y Levinthal): habilidad del receptor para reconocer, asimilar y aplicar conocimiento externo; depende de su I+D previa.
- **Adaptación y aprendizaje**: el receptor debe adaptar la tecnología a su contexto (sin ello hay transferencia "caja negra").

### Mecanismos
| Mecanismo | Descripción |
|---|---|
| Licencia (de patentes, software, know-how) | Derecho de uso a cambio de pago |
| Compra / cesión | Se adquiere la titularidad |
| Franquicia | Marca + sistema de gestión |
| Joint venture / alianza | Empresa o proyecto conjunto |
| Llave en mano ("turnkey") | El proveedor entrega la planta o sistema funcionando |
| Contratos de I+D / consultoría | Desarrollo por encargo |
| Spin-off universitaria | Empresa creada a partir de resultados de investigación |
| Inversión extranjera directa | Transferencia mediante subsidiarias |
| Movilidad de personal, formación | Transferencia de conocimiento tácito |

### Contrato de licencia: cláusulas esenciales
1. **Objeto** (qué patente, software o know-how).
2. **Alcance**: exclusiva, no exclusiva o única; territorio; campo de uso; duración; sublicencias.
3. **Contraprestación**: pago inicial (upfront), regalías (royalty), mínimos garantizados, hitos.
4. **Mejoras** y cesión recíproca (grant-back).
5. **Confidencialidad**, garantías, responsabilidad, soporte y capacitación.
6. **Terminación**, resolución de controversias y ley aplicable.
Para el aspecto legal consulte [[Legislación, Valores y Proyecto de País]] y [[GT 05 - Propiedad intelectual]].

### Valoración de una licencia
- **Regla del 25 %** (heurística): el licenciatario paga alrededor de 25 % de la utilidad operativa que genera la tecnología (referencia, no norma).
- **Regalía sobre ventas**: $R_t = r\, V_t$ con tasa $r$ típica entre 1 % y 10 % según el sector (referencial).
- **Valor actual de regalías**: $VA=\sum_{t=1}^{n}\dfrac{r V_t}{(1+i)^t}$.
- **Enfoque de ingresos incrementales**: flujo con tecnología menos flujo sin ella, descontado.
- Otros enfoques: costo de desarrollo y comparables de mercado.

### Barreras
Costos de transacción, asimetría de información, resistencia al cambio ("no inventado aquí"), diferencias culturales y falta de capacidad de absorción.

## Ejemplo resuelto: licencia de un software de optimización
Una universidad licencia un algoritmo a una empresa (datos hipotéticos). Pago inicial: 20 000 USD. Regalía: 4 % de ventas del producto. Ventas proyectadas: año 1: 200 000; año 2: 350 000; año 3: 500 000. Tasa de descuento 10 %.

Regalías: 8 000; 14 000; 20 000.
$$VA_{reg}=\frac{8000}{1{,}10}+\frac{14000}{1{,}21}+\frac{20000}{1{,}331}=7\,272{,}7+11\,570{,}2+15\,026{,}3=33\,869{,}2$$
Valor total para el licenciante: $20\,000+33\,869{,}2=53\,869{,}2$ USD.

**Comparación con compra de la tecnología** por 70 000 USD: para el receptor, la licencia cuesta 53 869 en valor actual (más barata) y reparte riesgo (si las ventas fallan, paga menos). Pero la compra elimina regalías perpetuas si el producto es exitoso, y da control sobre mejoras. Regla de decisión: si el receptor espera ventas altas y largas, comprar puede ser mejor; si hay incertidumbre, la licencia con regalías reduce el riesgo.

**Regla del 25 %** (control): si la utilidad operativa del producto es 30 % de ventas, el 25 % de esa utilidad equivale a 7,5 % de ventas, así que 4 % es razonable pero queda margen de negociación para el licenciante.

## Errores comunes
- Transferir solo documentos y no entrenar a personas (conocimiento tácito).
- No definir propiedad de las mejoras.
- Licencia exclusiva sin mínimos de explotación (la tecnología queda "dormida").
- Valorar solo por costo de desarrollo, ignorando el valor para el usuario.
- Ignorar la capacidad de absorción del receptor.

## Ejercicios propuestos
1. Regalía 5 %, ventas 100 000 y 200 000 en dos años, tasa 10 %: valor actual. *Respuesta: $5000/1{,}1+10000/1{,}21=4\,545{,}5+8\,264{,}5=12\,810$ USD.*
2. Diferencie licencia exclusiva y no exclusiva. *Respuesta: exclusiva: solo el licenciatario explota (incluso el titular no, si es "única" lo permite); no exclusiva: el titular puede licenciar a varios.*
3. Nombre tres cláusulas imprescindibles y su razón. *Respuesta: alcance (evitar conflictos de uso), regalías (precio), confidencialidad (proteger know-how).*

## Conexiones con otras materias
[[Ingeniería Económica]], [[Finanzas para Ingenieros]], [[Legislación, Valores y Proyecto de País]], [[Formación de Emprendedores]], [[Ingeniería de Software]] (licencias de software).

## Fuente
Escorsa y Valls; Cohen y Levinthal; conocimiento general. Tasas de regalía y la regla del 25 % son heurísticas referenciales; verificar con el programa oficial y con asesoría legal.
