---
tags: [clase, electiva]
materia: Introducción a las Telecomunicaciones
fuente: "conocimiento general"
---
# ITC 04 - Medios de transmisión guiados

Materia: [[Introducción a las Telecomunicaciones]]
Anterior: [[ITC 03 - Modulación digital y capacidad del canal]]
Siguiente: [[ITC 05 - Radioenlaces y balance de enlace]]

## Contexto y objetivo
El medio de transmisión limita la distancia, el ancho de banda y el costo de un enlace. Objetivo: comparar par trenzado, cable coaxial y fibra óptica, y calcular atenuación y presupuesto de potencia de un enlace guiado.

## Teoría

### Par trenzado
Pares de cobre trenzados para reducir diafonía e interferencia. UTP, FTP, STP. Categorías (referencia): Cat5e hasta 1 Gb/s a 100 m, Cat6 hasta 10 Gb/s en tramos cortos (55 m), Cat6a 10 Gb/s a 100 m. Longitud máxima de segmento Ethernet: 100 m. Estándares de conexión T568A/B. Se usa en LAN y en la última milla (xDSL).

### Cable coaxial
Conductor central, dieléctrico, malla y cubierta; mayor ancho de banda y blindaje que el par trenzado. Usos: televisión por cable (HFC), DOCSIS, enlaces de radiofrecuencia. Impedancia característica 50 Ω (RF) o 75 Ω (video).

### Fibra óptica
Guía de luz por **reflexión interna total** (índice del núcleo mayor que el del revestimiento). Tipos:
| Tipo | Núcleo | Fuente | Alcance típico |
|---|---|---|---|
| Multimodo (OM3/OM4) | 50 µm | LED/VCSEL 850 nm | cientos de metros |
| Monomodo (OS2) | 9 µm | Láser 1310/1550 nm | decenas de km |
Ventajas: gran ancho de banda, baja atenuación, inmunidad electromagnética. Ventajas de montaje: conectores y empalmes por fusión. Ventanas de baja pérdida: 850, 1310 y 1550 nm. Atenuación típica monomodo: 0,35 dB/km en 1310 nm y 0,2 dB/km en 1550 nm. Dispersión modal (multimodo) y cromática limitan la velocidad.

### Atenuación y ruido
Atenuación en dB: $A=10\log_{10}(P_{ent}/P_{sal})$. Para un cable de coeficiente $\alpha$ (dB/km) y longitud $L$: $A=\alpha L$ (en cobre crece con $\sqrt{f}$). Diafonía NEXT/FEXT, ruido térmico $N=kTB$ con $k=1{,}38\times10^{-23}$ J/K.

### Arquitecturas de acceso
FTTx (FTTH, FTTC), redes ópticas pasivas **PON** con divisores ópticos (1:32, 1:64): cada división 1:2 aporta unos 3,5 dB de pérdida.

## Ejemplo resuelto
Presupuesto de potencia de un enlace monomodo de 25 km en 1550 nm entre dos edificios.

Datos: transmisor $+0$ dBm, sensibilidad del receptor $-28$ dBm, $\alpha=0{,}25$ dB/km, 4 empalmes de 0,1 dB, 2 conectores de 0,5 dB, margen de seguridad 3 dB.

1. Fibra: $0{,}25\times25=6{,}25$ dB.
2. Empalmes: $4\times0{,}1=0{,}4$ dB. Conectores: $2\times0{,}5=1{,}0$ dB.
3. Pérdida total: $6{,}25+0{,}4+1{,}0=7{,}65$ dB; con margen: 10,65 dB.
4. Potencia recibida: $0-7{,}65=-7{,}65$ dBm.
5. Presupuesto disponible: $0-(-28)=28$ dB. Holgura: $28-10{,}65=17{,}35$ dB. El enlace es viable; incluso permitiría unos $17/0{,}25\approx 69$ km adicionales (limitados luego por dispersión).
6. Cuidado: si se supera la potencia máxima del receptor (saturación) puede ser necesario un atenuador.

Cobre: Ethernet Cat5e a 100 MHz, atenuación 22 dB/100 m; si el cable mide 90 m, $22\times0{,}9=19{,}8$ dB.

Cálculo en Python:
```python
def presupuesto(ptx_dbm, sens_dbm, km, alfa=0.25, empalmes=0, conectores=2,
                p_emp=0.1, p_con=0.5, margen=3):
    perdidas = alfa*km + empalmes*p_emp + conectores*p_con
    prx = ptx_dbm - perdidas
    holgura = (ptx_dbm - sens_dbm) - perdidas - margen
    return round(perdidas, 2), round(prx, 2), round(holgura, 2)

print(presupuesto(0, -28, 25, empalmes=4))   # (7.65, -7.65, 17.35)
```
Pruebas de campo: OTDR (reflectometría óptica, localiza empalmes y cortes), medidor de potencia y fuente de luz, certificador de cableado UTP (mapa de cableado, atenuación, NEXT). En Linux: `ethtool eth0` muestra velocidad negociada; `ethtool -S eth0` errores del enlace.

## Errores comunes
- Pasar de 100 m en UTP sin repetidor o conmutador.
- Mezclar fibra monomodo y multimodo.
- Curvas pronunciadas (radio mínimo) que causan macrocurvaturas.
- Conectores sucios (primera causa de pérdidas en fibra).
- Cables UTP paralelos a líneas eléctricas.

## Ejercicios propuestos
1. Fibra de 40 km a 0,2 dB/km con 2 conectores de 0,5 dB: pérdida total. *Respuesta: $8+1=9$ dB.*
2. Divisor PON 1:32: ¿pérdida teórica mínima? *Respuesta: $10\log_{10}32=15$ dB (más pérdidas de exceso).*
3. ¿Por qué se trenzan los pares? *Respuesta: para cancelar interferencia electromagnética y reducir diafonía.*

## Conexiones
[[Comunicaciones I]] (medios y ruido), [[Física II]] (óptica, reflexión interna total, campos), [[Administración de Redes]] (cableado estructurado, VLAN y enlaces), [[Organización del Computador]] (interfaces y buses seriales).

## Fuente
Conocimiento general: Tomasi; Stallings; normas TIA/EIA-568 e ITU-T G.652. Los valores de atenuación son típicos; verificar hojas técnicas del fabricante.
