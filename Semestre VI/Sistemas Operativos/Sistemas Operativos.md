---
tags: [materia, semestre-VI]
semestre: VI
---
# Sistemas Operativos

**Semestre:** [[Semestre VI]] · [[Pensum Ingeniería Informática UNET]]

## Prelaciones (cursar antes)
- [[Organización del Computador]]

## Desbloquea
- [[Compiladores e Intérpretes]]

## Apuntes

### Descripción general y objetivos
Sistemas Operativos estudia el software que administra los recursos del computador (procesador, memoria, almacenamiento y dispositivos) y ofrece servicios a los programas. Objetivo: comprender procesos e hilos, planificación, sincronización, interbloqueos, memoria virtual, sistemas de archivos y protección, con prácticas en Linux (llamadas al sistema, scripts, C). No hay Material del estudiante; el contenido sigue el programa típico (verificar con el programa oficial).

### Contenido programático
1. **Introducción**: funciones, modos usuario/kernel, llamadas al sistema, estructuras (monolítico, microkernel), historia.
2. **Procesos e hilos**: estados, PCB, creación (`fork`), comunicación entre procesos (pipes, memoria compartida, señales), hilos.
3. **Planificación de CPU**: FCFS, SJF, SRTF, prioridades, Round Robin, colas multinivel; métricas.
4. **Sincronización**: condición de carrera, sección crítica, semáforos, monitores, productor-consumidor, lectores-escritores, filósofos.
5. **Interbloqueos**: condiciones de Coffman, grafo de asignación, prevención, evasión (algoritmo del banquero), detección.
6. **Gestión de memoria**: particiones, paginación, segmentación, memoria virtual, reemplazo (FIFO, LRU, óptimo), hiperpaginación.
7. **Sistemas de archivos y E/S**: directorios, asignación (contigua, enlazada, indexada), i-nodos, planificación de disco, RAID.
8. **Seguridad y protección**: permisos, autenticación, control de acceso.

### Conceptos clave
- **Proceso**: programa en ejecución con su espacio de direcciones y contexto.
- **Cambio de contexto**: guardar/restaurar el estado de un proceso.
- **Exclusión mutua**, **inanición**, **interbloqueo**.
- **Fallo de página**: acceso a página no residente en memoria.
- **Tiempo de espera** = tiempo de retorno − ráfaga.

### Algoritmos y código
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
int main(void) {
    pid_t pid = fork();
    if (pid == 0) { printf("hijo %d\n", getpid()); }
    else { wait(NULL); printf("padre termina\n"); }
    return 0;
}
```
```
Semáforo:  wait(S): while (S<=0); S--      signal(S): S++
Dirección física = marco * tamaño_página + desplazamiento
Tiempo de acceso efectivo = (1-p)*t_mem + p*t_fallo     (p = tasa de fallos)
```

### Ejemplo resuelto: Round Robin (quantum 4)
P1 ráfaga 10, P2 ráfaga 5, P3 ráfaga 8, llegada 0. Diagrama de Gantt: P1(0-4) P2(4-8) P3(8-12) P1(12-16) P2(16-17) P3(17-21) P1(21-23). Tiempos de finalización: P1=23, P2=17, P3=21; espera promedio = ((23-10)+(17-5)+(21-8))/3 = 12.67.

### Relación con otras materias
Prelada por [[Organización del Computador]]; desbloquea [[Compiladores e Intérpretes]]. Se relaciona con [[Estructura de Datos]], [[Programación II]], [[Sistemas Distribuidos]], [[Administración de Redes]] y [[Automatización]] (tiempo real).

### Evaluación y consejos
- Parciales con problemas de planificación, memoria y sincronización, más prácticas en C/Linux; verificar con el programa oficial.
- Dibuja siempre el diagrama de Gantt y las tablas de reemplazo de páginas paso a paso.
- Practica con `fork`, pipes, hilos POSIX y semáforos.

### Bibliografía recomendada
- Silberschatz, Galvin y Gagne. *Fundamentos de Sistemas Operativos*.
- Tanenbaum, A. *Sistemas Operativos Modernos*. Pearson.
- Stallings, W. *Sistemas Operativos*. Pearson.

### Recursos del Material/
No hay carpeta `Material/` en esta materia.
