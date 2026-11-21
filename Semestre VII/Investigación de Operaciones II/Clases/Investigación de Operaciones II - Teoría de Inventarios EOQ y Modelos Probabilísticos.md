---
tags: [clase, semestre-VII]
materia: Investigación de Operaciones II
---
# Investigación de Operaciones II - Teoría de Inventarios EOQ y Modelos Probabilísticos

Materia: [[Investigación de Operaciones II]]  
Anterior: [[Investigación de Operaciones II - Teoría de Colas y Modelos MM1 y MMc]]  
Siguiente: [[Investigación de Operaciones II - Teoría de Juegos y Solución por PL]]

## Contexto y objetivo

Estudiar la **Unidad III (Teoría de Inventarios)**: identificar los costos relevantes de inventario, deducir el modelo clásico **EOQ** y sus extensiones determinísticas (producción finita, faltantes permitidos, descuentos por cantidad), y resolver modelos **probabilísticos** (punto de reorden con stock de seguridad y modelo de un solo período / vendedor de periódicos).

## 1. Estructura de costos de inventario

1. **Costo de pedido o preparación ($K$)**: costo fijo por emitir una orden o preparar una corrida de producción.
2. **Costo de mantenimiento ($h$)**: costo de almacenar una unidad durante un período (capital inmovilizado, bodega, seguro, obsolescencia).
3. **Costo de adquisición ($C$)**: precio unitario del artículo.
4. **Costo de faltante ($p$)**: penalización por unidad agotada o pérdida de venta.

## 2. Modelos determinísticos (EOQ y variantes)

Sea $D$ la demanda anual (constante).

### A. EOQ Clásico (sin faltantes, reposición instantánea)
$$CT(Q) = \frac{D}{Q}K + \frac{Q}{2}h + D\cdot C$$
Derivando respecto a $Q$ e igualando a cero:
$$Q^* = \sqrt{\frac{2DK}{h}}, \qquad T^* = \frac{Q^*}{D}, \qquad N^* = \frac{D}{Q^*}$$

### B. EOQ con producción finita (tasa de producción $P > D$)
$$Q^* = \sqrt{\frac{2DK}{h\left(1 - \frac{D}{P}\right)}}$$

### C. EOQ con faltantes permitidos (costo de faltante $p$ por unidad-año)
$$Q^* = \sqrt{\frac{2DK}{h}\cdot\frac{h+p}{p}}, \qquad S^* = Q^* \cdot \frac{h}{h+p} \quad (\text{faltante máximo})$$

### D. Descuentos por cantidad
El costo unitario $C_j$ depende del tramo de $Q$. Procedimiento:
1. Calcular $Q_j^* = \sqrt{2DK / h_j}$ desde el tramo de menor precio hacia arriba.
2. Si $Q_j^*$ es factible en su tramo, es candidato; si está por debajo del límite inferior del tramo, ajustar al límite inferior.
3. Comparar el $CT(Q)$ total (incluyendo $D\cdot C_j$) de los candidatos y elegir el mínimo.

### Ejemplo trabajado (EOQ)
$D = 1200$ u/año, $K = 50$ \$/pedido, $h = 6$ \$/u-año:
$$Q^* = \sqrt{\frac{2(1200)(50)}{6}} = \sqrt{20000} \approx 141.4 \text{ unidades}$$
Número de pedidos al año: $1200 / 141.4 \approx 8.5$ pedidos.

## 3. Modelos probabilísticos

1. **Revisión continua con punto de reorden ($R$) y stock de seguridad ($SS$)**:
   Si la demanda durante el tiempo de entrega (*lead time* $L$) es normal con media $\mu_L = d\cdot L$ y desviación estándar $\sigma_L$:
   $$R = \mu_L + z_\alpha \sigma_L, \qquad SS = z_\alpha \sigma_L$$
   donde $z_\alpha$ corresponde al nivel de servicio deseado (ej. $95\% \implies z = 1.645$).

2. **Modelo de un solo período (Vendedor de periódicos)**:
   Se equilibra el costo de subestimar la demanda ($C_u = \text{margen perdido}$) frente al costo de sobreestimar ($C_o = \text{pérdida por unidad sobrante}$):
   $$F(Q^*) = \frac{C_u}{C_u + C_o}$$

## Errores comunes

- Usar $h$ en costo por *mes* y $D$ en unidades por *año* (ambos deben compartir la misma unidad de tiempo).
- Omitir el término $D\cdot C$ al comparar tramos en el modelo de descuentos por cantidad.

## Ejercicios propuestos

1. Una tienda vende $D = 3600$ unidades/año, $K = 40$, $h = 2$. Calcula $Q^*$ y el costo anual de ordenar y mantener.
   - *Respuesta:* $Q^* = \sqrt{2(3600)(40)/2} = \sqrt{144000} \approx 379.5 \approx 380$ unidades. $CT_{\text{inv}} = \frac{3600}{380}(40) + \frac{380}{2}(2) \approx 378.9 + 380 = 758.9$.

## Conexiones

- Anterior: [[Investigación de Operaciones II - Teoría de Colas y Modelos MM1 y MMc]]
- Siguiente: [[Investigación de Operaciones II - Teoría de Juegos y Solución por PL]]
- Nota resumen: [[Investigación de Operaciones II - Teoría de Colas y Modelos MM1 y MMc]]
- Materia: [[Investigación de Operaciones II]]
- Materias relacionadas: [[Estadística II]], [[Ingeniería Económica]], [[Economía]]

## Fuente

- `Material/ProgramaInvOperacionesII.doc` (Unidad III) y Taha (Cap. 11 y 16).
