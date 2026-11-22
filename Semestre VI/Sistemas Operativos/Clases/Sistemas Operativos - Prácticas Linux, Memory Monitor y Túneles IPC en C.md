---
tags: [clase, semestre-VI, linux, c, ipc]
materia: Sistemas Operativos
---
# Sistemas Operativos - Prácticas Linux, Memory Monitor y Túneles IPC en C

Materia: [[Sistemas Operativos]]
Anterior: _Ninguna_
Siguiente: _Ninguna_

## Contexto y objetivo

Síntesis técnica de las prácticas de laboratorio realizadas en **Sistemas Operativos (`0435607T`)** (Noviembre 2025 – Marzo 2026) documentadas en Google Drive, cubriendo manejo de procesos en Linux, monitoreo de RAM mediante `/proc` y comunicación entre procesos (IPC) portable con pipes, memoria compartida y semáforos.

## 1. Práctica 1 y 2: Linux y Gestión de Procesos

- **Terminal y automatización:** Navegación de directorios, edición con `nano`, permisos (`chmod`, `sudo`), scripts Bash y compilación con `gcc`.
- **Árbol y control de procesos:** Uso de `ps`, `pstree`, lectura de `/proc/<pid>/comm`, creación de procesos con `fork()`, reemplazo de imagen con `execv()`, espera con `wait()` y terminación con `kill(..., SIGKILL)`.

## 2. Práctica 5: Memory Monitor

- **Objetivo:** Monitorear el uso global de memoria RAM, identificar el proceso con mayor consumo e inspeccionar su actividad (estado `sleeping`, memoria compartida en `/dev/shm`, bibliotecas cargadas como X11).
- **Repositorio:** `https://github.com/leonardo02lobo/Memory-Monitor`

## 3. Práctica 6: Túneles y Semáforos en C (IPC Portable)

Sistema productor–consumidor portable entre Linux y Windows (`#ifdef _WIN32`):
1. El **Proceso Padre** crea un *pipe* (`pipe()`), un segmento de **memoria compartida** (`mmap()` en POSIX / `CreateFileMapping()` en Windows) y un **semáforo** inicializado en `0`.
2. **Hijo 1 (Productor):** Lee texto del usuario y lo envía por el pipe.
3. **Hijo 2 (Consumidor):** Lee del pipe, transforma el texto a mayúsculas, lo escribe en memoria compartida y hace `post`/`signal` sobre el semáforo.
4. **Hijo 1 y Padre:** Esperan el semáforo (`wait`), leen el resultado desde la memoria compartida y lo imprimen.

```bash
gcc tuneles.c -o tuneles -pthread
./tuneles
```

- **Repositorio:** `https://github.com/leonardo02lobo/tunnels-on-C`

## Errores comunes

- Olvidar cerrar los extremos no utilizados de un `pipe()` en padre e hijos (provoca bloqueos en `read()` porque nunca llega `EOF`).
- Compilar código con semáforos POSIX (`sem_init`, `sem_wait`, `sem_post`) olvidando enlazar `-pthread`.

## Recursos en Google Drive

- [Introduccion a Linux](https://docs.google.com/document/d/1hTZakvIJBzc-ew3nmyBtdc0-Z0J2U3D588GCJbgCmX4/edit?usp=drivesdk)
- [Carpeta Práctica 5 (Memory Monitor)](https://drive.google.com/drive/folders/1zX4Uzww_kVJhq2GQV56I0dVVGqMCbVDM) · [Memory Monitor PDF](https://drive.google.com/file/d/1XQpPzB_uu4Up4BLP7A5uo1pb6O3qjAqz/view?usp=drivesdk)
- [Carpeta Práctica 6 (Túneles y Semáforos)](https://drive.google.com/drive/folders/1AzZ4QTmk17gGzU6WFYDg9LG_ObX0wUa9) · [Túneles y Semáforos PDF](https://drive.google.com/file/d/1fv5pmWjouFxSDNX6KW8wNGdgAnBdvj7q/view?usp=drivesdk)

## Conexiones

- Aplica programación en C vista en [[Programación I]] y [[Estructura de Datos]].
- Sirve de base para sincronización y concurrencia en [[Sistemas Distribuidos]].
