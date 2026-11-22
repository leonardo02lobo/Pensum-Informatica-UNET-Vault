---
tags: [clase, semestre-III, laboratorio]
materia: Laboratorio de Física II
---
# Laboratorio de Física II - Campo Eléctrico y Superficies Equipotenciales

Materia: [[Laboratorio de Física II]]
Anterior: _Ninguna_
Siguiente: _Ninguna_

## Contexto y objetivo

Basado en el *Prelaboratorio de Campo Eléctrico y Superficies Equipotenciales* (`0842303L`, Noviembre 2026) ubicado en Google Drive (`Laboratorio de Física II`). El objetivo es determinar experimentalmente y mediante simulación numérica la distribución del potencial eléctrico $V(r)$ y el campo eléctrico $\vec{E}(r)$ entre electrodos cilíndricos concéntricos.

## 1. Fundamentos teóricos

- **Intensidad de campo eléctrico:** $\vec{E} = \lim_{q_0 \to 0} \frac{\vec{F}}{q_0}$ (N/C o V/m).
- **Relación campo–potencial:** $\Delta V = -\int \vec{E} \cdot d\vec{s}$, por lo que $\vec{E} = -\nabla V$ (el campo eléctrico es perpendicular a las superficies equipotenciales y apunta hacia donde disminuye el potencial).
- **Ecuación de Laplace ($\nabla^2 V = 0$) en cilindros concéntricos** (radios $R_1 < r < R_2$ con $V(R_1) = V_0$ y $V(R_2) = 0$):
  $$V(r) = V_0 \frac{\ln(R_2 / r)}{\ln(R_2 / R_1)}$$
  Al graficar $V(r)$ frente a $\ln(r)$ se obtiene una relación lineal cuya pendiente permite validar experimentalmente la solución analítica.

## 2. Montaje experimental y protocolo UNET

- **Equipos:** Cuba electrolítica ($55 \times 35 \times 5\text{ cm}$), electrodos cilíndricos concéntricos de acero inoxidable ($R_1 = 1.5\text{ cm}$, $R_2 = 15.0\text{ cm}$), reóstato de $600\ \Omega$, fuente de $110\text{ V AC}$ (ajustada a $V_0 = 60\text{ V}$ AC) y voltímetro digital AC.
- **Seguridad:** Verificar aislamiento de cables y no tocar el electrolito ni los electrodos con la fuente energizada.

## 3. Herramientas digitales y modelado en Python

Además de la simulación interactiva en **PhET «Cargas y Campos»** (HTML5 1.0), se utiliza **Python 3.11 + NumPy** para el modelado coaxial 2D, cálculo de las 7 equipotenciales (de $35\text{ V}$ a $5\text{ V}$) y linealización semi-logarítmica:

```python
import numpy as np

V0 = 60.0   # Voltios AC
R1 = 1.5    # cm (electrodo interno)
R2 = 15.0   # cm (electrodo externo)

def radio_equipotencial(V: float) -> float:
    """Despeja r a partir de V(r) = V0 * ln(R2/r) / ln(R2/R1)."""
    return R2 * np.exp(-(V / V0) * np.log(R2 / R1))

voltajes = [35, 30, 25, 20, 15, 10, 5]
for v in voltajes:
    r = radio_equipotencial(v)
    print(f"V = {v:2d} V -> r = {r:.3f} cm, ln(r) = {np.log(r):.4f}")
```

## Errores comunes

- Confundir la escala lineal de $r$ con la semi-logarítmica $\ln(r)$ al realizar el ajuste por mínimos cuadrados.
- Tocar el fondo o los bordes de la cuba con la punta de prueba, introduciendo lecturas asimétricas.

## Recursos

- [Prelaboratorio_Campo_Electrico_Fisica_II.docx (Google Drive)](https://docs.google.com/document/d/1o5WpJU455aoxNpMLOrjwcjDvJiTMA0y0/edit?usp=drivesdk)

## Conexiones

- Aplica directamente los conceptos de [[Física II]] y las técnicas de propagación de errores de [[Laboratorio de Física I]].
- Complementa la parte de cálculo numérico vista en [[Análisis Numérico]].
