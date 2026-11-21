---
tags: [clase, semestre-VI]
materia: Comunicaciones I
fuente: conocimiento general
---
# Comunicaciones I - 03 Medios de transmisión

Materia: [[Comunicaciones I]]
Anterior: [[Comunicaciones I - 02 Señales y análisis de Fourier]]
Siguiente: [[Comunicaciones I - 04 Límites del canal Nyquist y Shannon]]

## Contexto y objetivo
El medio es el camino físico (o el espacio) por el que viaja la señal. Sus características (atenuación, ancho de banda, inmunidad al ruido, costo) determinan alcance y tasa. Se estudian medios guiados y no guiados.

## Medios guiados
### Par trenzado
Dos hilos de cobre trenzados reducen interferencia. **UTP** (sin blindaje) y **STP/FTP**. Categorías: Cat5e (100 MHz, 1 Gbps), Cat6 (250 MHz, 1 Gbps/10 Gbps hasta 55 m), Cat6a (500 MHz, 10 Gbps a 100 m), Cat7/8. Alcance típico en Ethernet: **100 m**. Conectores RJ-45; normas de cableado T568A/B. Problemas: **diafonía** (NEXT, FEXT), atenuación por frecuencia.

### Cable coaxial
Conductor central, dieléctrico, malla y cubierta. Mayor ancho de banda y blindaje que el par trenzado; usado en TV por cable, 10BASE2/5 histórico, enlaces de RF. Impedancia típica 50 Ω (datos) o 75 Ω (video).

### Fibra óptica
Transmite luz (reflexión interna total, ley de Snell: $n_1\sin\theta_1 = n_2\sin\theta_2$).
- **Multimodo** (núcleo 50/62.5 μm, LED/VCSEL 850 nm, cientos de metros a pocos km; dispersión modal).
- **Monomodo** (núcleo ≈ 9 μm, láser 1310/1550 nm, decenas a cientos de km).
- Ventanas de baja atenuación: 850, 1310, 1550 nm (≈ 0.2 dB/km en 1550 nm).
- Ventajas: enorme ancho de banda, inmune a EMI, baja atenuación, seguridad. Desventajas: costo de conectores y empalmes, fragilidad.

## Medios no guiados (inalámbricos)
- **Radio** (omnidireccional, 3 kHz-1 GHz), **microondas** terrestres y satelitales (1-40 GHz, línea de vista), **infrarrojo**, **láser**.
- Bandas ISM 2.4/5 GHz (Wi-Fi, Bluetooth), celular (LTE/5G), satélite GEO (retardo ≈ 250 ms de ida), LEO (≈ 20-40 ms).
- Propagación: **espacio libre** $L_{dB} = 20\log_{10}(d) + 20\log_{10}(f) + 32.44$ (d en km, f en MHz), reflexión, refracción, difracción, **multitrayecto**, desvanecimiento.

## Deterioros de la transmisión
1. **Atenuación** (en dB/km; se compensa con amplificadores/repetidores).
2. **Distorsión** (de retardo, de dispersión en fibra).
3. **Ruido**: térmico $N_0 = kT$ ($k = 1.38\times10^{-23}$ J/K), intermodulación, **diafonía**, impulsivo.

### Ejemplo de presupuesto de enlace
Fibra monomodo de 40 km a 1550 nm con 0.25 dB/km: pérdida de fibra 10 dB; 4 conectores de 0.5 dB = 2 dB; 2 empalmes de 0.1 dB. Pérdida total 12.2 dB. Potencia de transmisión 0 dBm, sensibilidad del receptor -28 dBm: margen = 28 - 12.2 = 15.8 dB. Es suficiente.

Otro: enlace Wi-Fi 2.4 GHz a 100 m (0.1 km): $L = 20\log(0.1) + 20\log(2400) + 32.44 = -20 + 67.6 + 32.44 \approx 80$ dB.

## Comparativa
| Medio | Ancho de banda | Alcance | Costo | EMI |
|---|---|---|---|---|
| UTP Cat6 | hasta 250 MHz | 100 m | bajo | sensible |
| Coaxial | cientos de MHz | cientos de m | medio | bajo |
| Fibra | THz | km - cientos de km | alto | inmune |
| Radio/microondas | MHz-GHz | variable | medio | sensible |

## Errores comunes
- Exceder los 100 m en UTP sin repetidor/switch.
- Confundir fibra multimodo y monomodo (módulos ópticos incompatibles).
- Olvidar las pérdidas de conectores y empalmes en el presupuesto.
- Sumar dB como si fueran lineales para potencias absolutas (dBm + dBm no se suma; dBm + dB sí).

## Ejercicios propuestos
1. Atenuación 0.2 dB/km en 60 km: pérdida. *Resp.: 12 dB.*
2. Una señal de 10 mW pasa por 15 dB de pérdida: potencia final. *Resp.: 10 mW/31.6 = 0.316 mW (-5 dBm).*
3. Retardo ida de un satélite GEO a 36 000 km. *Resp.: ≈ 120 ms (≈ 240-270 ms por salto completo tierra-satélite-tierra).*

## Conexiones
[[Comunicaciones I - 04 Límites del canal Nyquist y Shannon]]; [[Introducción a las Telecomunicaciones]]; [[Administración de Redes]] (cableado estructurado).

## Fuente
Conocimiento general (Stallings cap. 4; Tanenbaum cap. 2).
