---
tags: [clase, semestre-III]
materia: Inglés II
---
# Inglés II - Verbos Modales en Contextos Técnicos

Materia: [[Inglés II]]
Anterior: [[Inglés II - Repaso de Tiempos Verbales y Presente Perfecto]]
Siguiente: [[Inglés II - Voz Pasiva y Descripción de Procesos]]

## Contexto y objetivo

Los manuales de usuario, especificaciones RFC y guías de seguridad informática dependen de los **verbos modales** (*modal verbs*) para expresar obligación, prohibición, recomendación, capacidad y probabilidad. Esta clase sistematiza el uso de *can, could, must, have to, should, may* y *might* en inglés técnico.

## 1. Reglas gramaticales de los modales

1. Son invariables: no llevan *-s* en 3.ª persona (*"The user must enter a password"*, nunca ~~musts~~).
2. Van seguidos del verbo principal en **forma base sin *to*** (*"You should back up your files"*). Excepción semimodal: *have to*.
3. Niegan y preguntan por sí mismos, sin *do/does* (*"Must we restart?"*, *"You shouldn't ignore warnings"*).

## 2. Clasificación por función comunicativa

| Modal | Función principal | Ejemplo técnico |
|---|---|---|
| **can / could** | Capacidad, posibilidad, petición | *"This algorithm can sort 10,000 items in milliseconds."* |
| **must** | Obligación fuerte / deducción lógica | *"Passwords must contain at least 8 characters."* |
| **mustn't** | **Prohibición** estricta | *"You mustn't share your private key."* |
| **don't have to** | **Falta de obligación** (no hace falta) | *"You don't have to compile the script manually."* |
| **should / shouldn't** | Recomendación o buena práctica | *"Developers should comment complex functions."* |
| **may / might** | Posibilidad o permiso formal (*may*) | *"The update may require a reboot. / It might fail on older CPUs."* |

## 3. Contraste crítico: *mustn't* vs. *don't have to*

En documentación técnica es vital no confundir ambos significados:
- *"You **mustn't** delete `/etc/fstab`"* = está prohibido; causará un fallo grave.
- *"You **don't have to** install Python again"* = ya está instalado; es opcional hacerlo.

## Errores comunes

- Añadir *to* después de un modal: ~~It might to crash~~ $\rightarrow$ **It might crash**.
- Usar *mustn't* cuando se quiere decir "no es necesario": usar **don't have to** o **needn't**.
- Confundir *can* con *may* en textos formales de especificaciones (*may* indica permiso u opcionalidad; *must*, requisito obligatorio).

## Ejercicios propuestos

1. Elige el modal adecuado: *"The database is corrupted; we (should / mustn't) restore the backup immediately."*
2. Distingue el sentido: *"You (mustn't / don't have to) turn off the server during a firmware update."*
3. Reescribe como recomendación: *"It is a good idea to use version control."* (usa *should*).

**Respuestas:**
1. *should*.
2. *mustn't* (prohibición por riesgo de daño).
3. *"You should use version control."*

## Conexiones

- Amplía los modales básicos de [[Inglés I - Pasado Simple y Verbos Modales Básicos]].
- Se combina con [[Inglés II - Voz Pasiva y Descripción de Procesos]] en especificaciones técnicas (*"The file must be encrypted"*).

## Fuente

Elaborado siguiendo el programa referencial de [[Inglés II]] (Unidad 2: Verbos modales).
