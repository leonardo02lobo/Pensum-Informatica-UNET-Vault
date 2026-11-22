---
tags: [clase, electiva, telecomunicaciones, gpon, 5g]
materia: Introducción a las Telecomunicaciones
---
# Introducción a las Telecomunicaciones - Medios, Radioenlaces, GPON y 5G

Materia: [[Introducción a las Telecomunicaciones]]
Anterior: _Ninguna_
Siguiente: _Ninguna_

## Contexto y objetivo

Resumen de los temas evaluados y documentos desarrollados para **Introducción a las Telecomunicaciones (`0433710T`)** (Diciembre 2025 – Abril 2026) en Google Drive: medios físicos guiados, radioenlaces, redes ópticas pasivas GPON y arquitectura 5G.

## 1. Medios Físicos Guiados y Multiplexación

- **Comparativa de medios:** Par trenzado (bajo costo, susceptible a EMI, distancias cortas), Cable coaxial (mejor blindaje, banda ancha media) y Fibra óptica (inmunidad electromagnética, gran ancho de banda y alcance, mayor costo de terminación).
- **Multiplexación:** **FDM** (división de frecuencia), **TDM** (división de tiempo, usada con modulación **PCM**) y **WDM** (división por longitud de onda en fibra óptica).
- **Nodos de conmutación:** En una malla completa de $n$ nodos se requieren $\frac{n(n-1)}{2}$ enlaces, frente a $n$ enlaces en topología estrella hacia un nodo central.

## 2. Radioenlaces y Antenas

- **Componentes de un radioenlace:** Transmisor (TX) → línea de transmisión → antena transmisora → canal con línea de vista (**LOS**) → antena receptora → receptor (RX).
- **Tipos de antenas:** Omnidireccionales ($360^\circ$ en azimut), direccionales (Yagi-Uda, parabólica de alta ganancia), sectoriales (cobertura por sectores en estaciones base) y planas/microstrip.

## 3. Redes Ópticas Pasivas GPON (ITU-T G.984)

- **Arquitectura P2MP (Punto a Multipunto):**
  - **OLT** (*Optical Line Terminal*) en la central del operador.
  - **ODN** (*Optical Distribution Network*) pasiva mediante *splitters* ópticos.
  - **ONT / ONU** en el cliente final.
- **Longitudes de onda WDM:** $1490\text{ nm}$ (bajada/downstream), $1310\text{ nm}$ (subida/upstream con **TDMA**) y $1550\text{ nm}$ (video/CATV).
- **Seguridad:** Cifrado **AES-128** en el canal descendente.

## 4. Arquitectura 5G

- **Pilares de uso:** **eMBB** (banda ancha móvil mejorada), **URLLC** (comunicaciones ultra confiables de baja latencia) y **mMTC** (comunicaciones masivas tipo máquina / IoT).
- **Arquitectura SBA (*Service-Based Architecture*):** 5G Core virtualizado con **NFV/SDN**, Next-Gen RAN (`gNodeB`), **Massive MIMO**, **Small Cells** y **Network Slicing**.
- **Modos de despliegue:** **NSA** (*Non-Standalone*, apoyado en core 4G) vs **SA** (*Standalone*, core 5G nativo).

## Recursos en Google Drive

- [Parcial 2](https://docs.google.com/document/d/1h6CMo8hD8hx8baqyAC42UksBs7p14eyhFEHC2c85Pao/edit?usp=drivesdk) · [Radio Enlace](https://docs.google.com/document/d/1GBvj6xf2WfWFoWDM-Vy4Rr6DU-xm6aNyupGX-ue8U3E/edit?usp=drivesdk) · [Comparacion de Medios Físicos](https://docs.google.com/document/d/1p9SXKsOEbd4nTSpU0fY69i7NBiklty91hWSv0GS51Jo/edit?usp=drivesdk)
- [Red GPON](https://docs.google.com/document/d/1Am8W1_dhQIcK8Da2hRhQADH_0wS_3ECBtU48p706UT8/edit?usp=drivesdk) · [Red 5G](https://docs.google.com/document/d/11RaOMwsqrCJ7_2HyrJlfIc1T-38j1PANzId5gjCUFIo/edit?usp=drivesdk)

## Conexiones

- Se relaciona con [[Comunicaciones I]], [[Comunicaciones II]] y [[Administración de Redes]].
