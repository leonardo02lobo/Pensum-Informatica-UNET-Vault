---
tags: [clase, electiva]
materia: Gestión Tecnológica
fuente: "conocimiento general"
---
# GT 01 - Tecnología, innovación y curva S

Materia: [[Gestión Tecnológica]]
Anterior: —
Siguiente: [[GT 02 - Estrategia tecnológica]]

## Contexto y objetivo
Antes de gestionar la tecnología hay que precisar qué es, cómo se relaciona con la ciencia y la innovación y cómo evoluciona en el tiempo. El objetivo es distinguir los conceptos, clasificar tipos de innovación y usar la curva S y el modelo de adopción para ubicar una tecnología en su ciclo de vida. (Temario a verificar con el programa oficial.)

## Teoría

### Ciencia, tecnología e innovación
- **Ciencia**: conocimiento sistemático sobre la naturaleza; busca explicar.
- **Tecnología**: conocimiento aplicado (técnicas, procesos, herramientas, saber hacer) para resolver problemas; puede incorporarse en productos, procesos o personas.
- **Invención**: idea o artefacto nuevo; **innovación**: invención introducida con éxito en el mercado o la sociedad (aporta valor).
- **I+D**: investigación básica, aplicada y desarrollo experimental (definiciones del Manual de Frascati/OCDE).
- Modelos: **lineal** (ciencia empuja la tecnología) vs. **interactivo/enlaces en cadena** (el mercado y la tecnología se retroalimentan) y **sistemas de innovación** (universidades, empresas, estado).

### Tipos de innovación (Manual de Oslo, OCDE)
- De **producto** y de **proceso**; de **mercadotecnia** y de **organización** (en la tercera edición); la edición reciente agrupa en producto y de procesos de negocio.
- Por magnitud: **incremental**, **radical**, y **disruptiva** (Christensen: una tecnología inicialmente inferior en las dimensiones valoradas por el mercado dominante, pero más simple, barata o conveniente, que mejora hasta desplazar a los líderes).
- **Innovación abierta** (Chesbrough): usar ideas internas y externas.

### Ciclo de vida tecnológico: curva S
El desempeño $P$ de una tecnología frente al esfuerzo acumulado (o el tiempo) sigue una forma de S:
1. **Emergente**: progreso lento, alta incertidumbre.
2. **Crecimiento**: mejoras rápidas, estándares, entrada de competidores.
3. **Madurez**: rendimientos decrecientes, límite físico.
4. **Declive**: sustitución por otra tecnología (nueva curva S).

Modelo logístico: 
$$P(t)=\frac{L}{1+e^{-k(t-t_0)}}$$
donde $L$ es el límite de desempeño, $k$ la tasa de crecimiento y $t_0$ el punto de inflexión (50 % de $L$). La pendiente máxima ocurre en $t_0$ con valor $kL/4$.

### Adopción: modelo de Rogers
Innovadores (2,5 %), adoptantes tempranos (13,5 %), mayoría temprana (34 %), mayoría tardía (34 %), rezagados (16 %). **Abismo** (Moore) entre tempranos y mayoría temprana.

### Indicadores
Patentes, publicaciones, gasto en I+D como % del PIB, personal en I+D, productos nuevos en ventas.

## Ejemplo resuelto: ajuste de la curva S
Una tecnología tiene límite estimado $L=100$ (unidades de desempeño), inflexión en $t_0=6$ años y $k=0{,}5$.
- $P(6)=100/(1+1)=50$.
- $P(2)=\dfrac{100}{1+e^{2}}=\dfrac{100}{1+7{,}389}=11{,}9$.
- $P(10)=\dfrac{100}{1+e^{-2}}=\dfrac{100}{1+0{,}1353}=88{,}1$.
- Pendiente máxima: $kL/4=0{,}5\cdot100/4=12{,}5$ unidades/año (en $t=6$).

Lectura: a los 10 años ya se alcanzó 88 % del límite; invertir más en mejorar esa tecnología rinde cada vez menos y conviene explorar la siguiente curva S (por ejemplo, nuevo paradigma). Este análisis es aproximado: estimar $L$ es lo difícil.

Caso cualitativo: discos duros magnéticos vs. memorias flash (SSD). Los discos mejoraron durante décadas en densidad; los SSD entraron como nicho (portátiles, costosos), mejoraron y desplazaron a los discos en la mayoría de usos de cómputo personal.

## Errores comunes
- Equiparar innovación con invención o con "tecnología nueva".
- Creer que solo la innovación radical vale; la incremental sostiene la mayoría de las ganancias de productividad.
- Cambiar de tecnología demasiado pronto (en el abismo) o demasiado tarde (declive).
- Confundir disruptiva con "muy radical": disrupción es sobre trayectoria y modelo de negocio.

## Ejercicios propuestos
1. Clasifique: (a) un nuevo algoritmo de compresión que mejora 5 % el anterior; (b) la fotografía digital frente a la química. *Respuesta: (a) incremental de producto/proceso; (b) disruptiva/radical.*
2. Con $L=200$, $k=0{,}8$, $t_0=5$, calcule $P(5)$ y la pendiente máxima. *Respuesta: 100; $0{,}8\cdot200/4=40$.*
3. Explique por qué el modelo lineal es insuficiente. *Respuesta: ignora el aprendizaje por uso, la retroalimentación del mercado y el papel de otros actores del sistema de innovación.*

## Conexiones con otras materias
[[Ciencia y Sociedad I]], [[Economía]], [[Formación de Emprendedores]], [[Ingeniería Económica]].

## Fuente
Escorsa y Valls, *Tecnología e Innovación en la Empresa*; Manual de Oslo (OCDE); Christensen; Rogers. Conocimiento general.
