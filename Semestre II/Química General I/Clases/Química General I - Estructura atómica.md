---
tags: [clase, semestre-II]
materia: Química General I
fuente: conocimiento general
---
# Química General I - Estructura atómica

Materia: [[Química General I]]
Anterior: [[Química General I - Conversión de unidades y análisis dimensional]]
Siguiente: [[Química General I - Tabla periódica y propiedades periódicas]]

## Contexto y objetivo
Todas las propiedades químicas (enlace, reactividad, periodicidad) se explican por cómo están organizados los electrones del átomo. Esta nota recorre las partículas subatómicas, los modelos atómicos, los números cuánticos y la configuración electrónica. Objetivo: escribir la configuración de cualquier elemento y deducir sus electrones de valencia. (Programa UNET: verificar.)

## 1. Partículas subatómicas
| Partícula | Carga (C) | Carga relativa | Masa (u) |
|---|---|---|---|
| Protón | +1,602×10^-19 | +1 | 1,0073 |
| Neutrón | 0 | 0 | 1,0087 |
| Electrón | -1,602×10^-19 | -1 | 5,49×10^-4 |

1 u (unidad de masa atómica) = 1/12 de la masa del átomo de ¹²C = 1,6605×10^-27 kg. El núcleo (protones y neutrones, ~10^-15 m) concentra casi toda la masa; los electrones ocupan una nube de ~10^-10 m. (La misma estructura se usa en [[Física II]] al estudiar la carga eléctrica.)

- **Número atómico Z** = número de protones (identifica el elemento).
- **Número másico A** = protones + neutrones; neutrones $N = A - Z$.
- Notación: ${}^{A}_{Z}X$.
- **Isótopos**: mismo Z, distinto A (¹H, ²H, ³H; ¹²C, ¹³C, ¹⁴C).
- **Iones**: catión (pierde e⁻, carga +), anión (gana e⁻, carga -). El número de protones no cambia.
- **Masa atómica promedio**: $\bar{M} = \sum f_i M_i$ con $f_i$ la abundancia fraccionaria.

### Ejemplo 1: masa atómica promedio
Cloro: ³⁵Cl (34,969 u; 75,78 %) y ³⁷Cl (36,966 u; 24,22 %).
$\bar M = 0{,}7578(34{,}969)+0{,}2422(36{,}966) = 26{,}50+8{,}95 = 35{,}45$ u.

### Ejemplo 2: partículas
${}^{56}_{26}\text{Fe}^{3+}$: p = 26; n = 56 - 26 = 30; e = 26 - 3 = 23.

## 2. Evolución de los modelos atómicos
1. **Dalton (1808)**: átomos indivisibles, esferas macizas; compuestos por combinación en proporciones enteras.
2. **Thomson (1897)**: descubre el electrón; modelo del "pudín de pasas".
3. **Rutherford (1911)**: dispersión de partículas α en lámina de oro; la mayoría atraviesa, pocas rebotan: existe un núcleo pequeño, denso y positivo.
4. **Bohr (1913)**: electrones en órbitas circulares con energía cuantizada; los saltos entre niveles emiten o absorben fotones. Para el hidrógeno: $E_n = -\dfrac{13{,}6\ \text{eV}}{n^2}$.
5. **Modelo mecano-cuántico (Schrödinger, 1926)**: el electrón se describe por una función de onda; $|\psi|^2$ da la probabilidad de encontrarlo (orbital). Principio de incertidumbre de Heisenberg: no se pueden conocer simultáneamente posición y momento con precisión arbitraria.

### Radiación y espectros
Relación entre luz y energía: $c = \lambda\nu$, $E = h\nu = hc/\lambda$ con $h = 6{,}626\times10^{-34}$ J·s y $c = 3{,}00\times10^{8}$ m/s. Un salto de $n_i$ a $n_f$ en el H libera $\Delta E = 13{,}6\left(\dfrac1{n_f^2}-\dfrac1{n_i^2}\right)$ eV.

**Ejemplo 3**: Transición $n=3\to n=2$ en H: $\Delta E = 13{,}6(1/4-1/9)=1{,}89$ eV = $3{,}02\times10^{-19}$ J. $\lambda = hc/E = (6{,}626\times10^{-34})(3\times10^8)/3{,}02\times10^{-19} = 6{,}58\times10^{-7}$ m = 658 nm (luz roja, línea H-alfa).

## 3. Números cuánticos
| Símbolo | Nombre | Valores | Describe |
|---|---|---|---|
| $n$ | principal | 1, 2, 3, ... | nivel/tamaño/energía |
| $\ell$ | azimutal | 0 a n-1 (s, p, d, f) | forma del orbital |
| $m_\ell$ | magnético | de -ℓ a +ℓ | orientación |
| $m_s$ | espín | +½, -½ | giro del electrón |

Cada subnivel tiene $2\ell+1$ orbitales: s (1), p (3), d (5), f (7). Cada orbital admite 2 electrones: capacidad por subnivel 2, 6, 10, 14; por nivel $2n^2$.

Formas: orbital s esférico; p con dos lóbulos (px, py, pz); d con cuatro lóbulos en general.

## 4. Configuración electrónica
Reglas:
- **Principio de Aufbau**: se llenan primero los subniveles de menor energía. Orden (regla de Madelung, $n+\ell$ creciente): 1s, 2s, 2p, 3s, 3p, 4s, 3d, 4p, 5s, 4d, 5p, 6s, 4f, 5d, 6p, 7s, 5f, 6d, 7p.
- **Principio de exclusión de Pauli**: no hay dos electrones con los cuatro números cuánticos iguales (máximo 2 por orbital, con espines opuestos).
- **Regla de Hund**: en orbitales degenerados los electrones ocupan orbitales distintos con espines paralelos antes de aparearse.

Notación abreviada con gas noble: Na = [Ne] 3s¹.

### Ejemplos
- O (Z = 8): 1s² 2s² 2p⁴ (dos electrones desapareados).
- Cl (Z = 17): [Ne] 3s² 3p⁵; 7 electrones de valencia.
- Fe (Z = 26): [Ar] 4s² 3d⁶.
- **Excepciones**: Cr = [Ar] 4s¹ 3d⁵ y Cu = [Ar] 4s¹ 3d¹⁰ (estabilidad de subniveles semillenos o llenos).
- Iones: se quitan primero los electrones del nivel más externo (n mayor): Fe²⁺ = [Ar] 3d⁶.

**Propiedades magnéticas**: paramagnético (electrones desapareados, atraído por un imán), diamagnético (todos apareados).

**Electrones de valencia**: los del nivel más externo (n máximo), y d/f incompletos en metales de transición. Determinan el enlace ([[Química General I - Enlace químico]]).

## Errores comunes
- Llenar 3d antes de 4s en neutros (se escribe 4s antes de 3d en el orden de llenado; al formar cationes 4s se pierde primero).
- Olvidar la excepción de Cr y Cu.
- Confundir A con Z, o asignar carga al número de protones.
- Pensar que las órbitas de Bohr son reales en el modelo cuántico.

## Ejercicios propuestos
1. ¿Cuántos neutrones tiene ¹⁴C? (8)
2. Configuración del azufre (Z = 16). (1s² 2s² 2p⁶ 3s² 3p⁴)
3. ¿Posibles valores de ℓ para n = 3? (0, 1, 2)
4. ¿Número máximo de electrones con n = 4? (32)
5. Longitud de onda de un fotón de 2,0 eV. (≈ 620 nm)

## Conexiones
- Continúa en [[Química General I - Tabla periódica y propiedades periódicas]].
- La energía de fotones y niveles cuantizados conecta con el efecto fotoeléctrico y con los semiconductores usados en [[Fundamentos de Lógica Digital]].

## Fuente
Conocimiento general (Chang, Brown-LeMay). Contenido exacto del programa UNET: verificar.
