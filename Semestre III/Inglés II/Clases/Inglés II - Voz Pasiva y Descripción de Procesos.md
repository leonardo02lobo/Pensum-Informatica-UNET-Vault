---
tags: [clase, semestre-III]
materia: Inglés II
---
# Inglés II - Voz Pasiva y Descripción de Procesos

Materia: [[Inglés II]]
Anterior: [[Inglés II - Verbos Modales en Contextos Técnicos]]
Siguiente: [[Inglés II - Comparativos, Superlativos y Oraciones Condicionales]]

## Contexto y objetivo

En la literatura científica y técnica de la Ingeniería Informática, el foco recae sobre el **objeto, el dato o el proceso**, no sobre la persona que ejecuta la acción. Por ello, la **voz pasiva** (*Passive Voice*) es una de las estructuras más frecuentes en manuales, arquitecturas de software y reportes de laboratorio.

## 1. Transformación de voz activa a voz pasiva

$$\text{Sujeto (paciente)} + \text{verbo } \textit{to be} \text{ (en el tiempo correspondiente)} + \text{participio pasado (V3)} + [\text{by } + \text{agente}]$$

- **Activa:** *"The compiler translates the source code."*
- **Pasiva:** *"The source code **is translated** by the compiler."*

El complemento *by + agente* se omite cuando el agente es obvio, desconocido o irrelevante (*"The data is stored in RAM"*).

## 2. La voz pasiva en distintos tiempos y con modales

| Tiempo / Estructura | Fórmula pasiva | Ejemplo |
|---|---|---|
| Presente simple | `am/is/are + V3` | *Packets **are routed** across the network.* |
| Pasado simple | `was/were + V3` | *The bug **was fixed** in patch 1.2.* |
| Presente continuo | `am/is/are being + V3` | *The database **is being migrated**.* |
| Presente perfecto | `have/has been + V3` | *Three vulnerabilities **have been patched**.* |
| Con modales | `modal + be + V3` | *Passwords **must be hashed** before storage.* |

## 3. Descripción de un proceso técnico paso a paso

Para redactar o comprender cómo funciona un algoritmo o sistema, se combina la voz pasiva en presente simple con conectores secuenciales (*First, Next, Then, After that, Finally*):

> *"First, the user's request **is received** by the web server. Next, the input **is validated** and **sent** to the database. Then, the query **is executed** and the results **are formatted** as JSON. Finally, the response **is returned** to the client."*

## Errores comunes

- Olvidar el verbo *to be* en la pasiva: ~~The file compressed~~ $\rightarrow$ **The file is compressed**.
- Usar el pasado simple en lugar del participio pasado en verbos irregulares: ~~The code was wrote~~ $\rightarrow$ **The code was written**.
- Traducir literalmente la pasiva refleja española ("se almacena") con *itself*: ~~The data stores itself~~ $\rightarrow$ **The data is stored**.

## Ejercicios propuestos

1. Pasa a voz pasiva: *"The system encrypts all messages."*
2. Pasa a voz pasiva (pasado): *"Engineers designed this protocol in 1995."*
3. Completa: *"Before deployment, the application must ___ (test) thoroughly."*

**Respuestas:**
1. *"All messages **are encrypted** (by the system)."*
2. *"This protocol **was designed** in 1995 (by engineers)."*
3. *be tested*.

## Conexiones

- Continúa desde [[Inglés II - Verbos Modales en Contextos Técnicos]].
- Muy útil para redactar procedimientos y resultados en [[Laboratorio de Física II]] y [[Metodología de la Investigación]].

## Fuente

Elaborado siguiendo el programa referencial de [[Inglés II]] (Unidad 3: Voz pasiva en descripciones de procesos).
