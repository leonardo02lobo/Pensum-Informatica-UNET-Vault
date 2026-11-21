---
tags: [clase, semestre-VIII]
materia: Sistemas Distribuidos
fuente: ~/Documentos/UNET/Sistema Distribuidos/P1/Clase 2/Clase 2.pdf y CS.pdf (E. Marini, linuxito.com, 2012)
---
# Sistemas Distribuidos - 03 Modelo cliente-servidor y arquitecturas por capas

Materia: [[Sistemas Distribuidos]]
Anterior: [[Sistemas Distribuidos - 02 Hardware, software y propiedades]]
Siguiente: [[Sistemas Distribuidos - 04 Multiprocesadores y objetos distribuidos]]

## Contexto y objetivo
La Clase 2 ("Modelos de sistemas distribuidos") presenta cómo se **divide la responsabilidad** entre componentes y dónde se ubican. Esa arquitectura condiciona prestaciones, fiabilidad y seguridad. Cinco modelos: multiprocesador, cliente/servidor, objetos distribuidos, peer-to-peer y orientado a servicios. Esta nota trata el más extendido: cliente/servidor (CS).

## 1. Capas de un SD
De abajo arriba: *computador y hardware de red* → *plataforma* (SO en cada computador, que da la interfaz de programación del sistema) → **middleware** (capa de software que enmascara la heterogeneidad y ofrece un modelo de programación cómodo) → *aplicaciones y servicios*.

## 2. El modelo cliente/servidor
Definición (Marini): modelo de aplicación distribuida en el que las tareas se reparten entre los **proveedores de recursos o servicios (servidores)** y los **demandantes (clientes)**. Los clientes envían peticiones a uno o varios servidores que deben estar en ejecución. Rasgos:
- Clientes y servidores son **procesos distintos**; pueden estar en la misma o en distintas máquinas. Varios procesos servidores pueden vivir en un solo procesador (no hay relación 1:1 proceso-procesador).
- Los clientes conocen qué servidores existen, pero normalmente **no conocen a otros clientes**.
- La capacidad de proceso se reparte, pero la ventaja principal es **organizativa**: centralización de la gestión de la información y separación de responsabilidades.
- Un servidor puede ser cliente de otro servidor (pero no recibe servicios de clientes).

## 3. Modelo de servicios: tres lógicas
1. **Lógica de presentación:** interacción usuario-aplicación (interfaz). Idealmente solo llama a procesos de las otras lógicas; así es inmune a cambios en reglas de negocio o gestores de datos.
2. **Lógica de negocio:** secuencia de acciones, reglas de la empresa e integridad de transacciones. Aislarla da flexibilidad de ubicación (componente en servidor, procedimiento almacenado o incluso cliente), permite varias interfaces sobre las mismas reglas (macro de Office, VB o página HTML), facilita el mantenimiento y permite sustituir reglas por país manteniendo la interfaz. *Ejemplo del documento:* el cálculo de sueldos: la funcionalidad (calcular sueldo) es estable, pero su codificación cambia con normas legales o políticas de incentivos.
3. **Lógica de datos:** mantenimiento y acceso a los datos (gestor de BD, ficheros). Conecta con [[Base de Datos II]] (procedimientos almacenados, transacciones).

## 4. Arquitecturas CS por capas
### 4.1 Dos capas
- **Cliente ligero (thin):** el cliente solo hace presentación; procesamiento y datos en el servidor. Ventaja: administración centralizada. Desventaja: carga y tráfico en servidor y red.
- **Cliente rico/gordo (fat):** el cliente implementa la lógica de aplicación e interacción; el servidor solo gestiona datos. Ventaja: descarga al servidor. Desventaja: gestión y actualización difíciles de muchos clientes.
*Ejemplo de las diapositivas:* los cajeros automáticos no hablan directamente con la base de datos de clientes sino con un **monitor de teleproceso / gestor de transacciones** (middleware) que serializa las transacciones y permite recuperarse de fallos sin corromper datos.

### 4.2 Tres capas
Presentación, procesamiento de aplicación y gestión de datos son procesos lógicamente separados en procesadores distintos: más **escalable**, y las comunicaciones entre capas pueden usar protocolos de bajo nivel rápidos. *Ejemplo:* un sistema bancario por Internet: BD de clientes (datos), servidor web (aplicación: transferir, estado de cuenta, pagos), navegador (presentación).

### 4.3 Multicapas
Cuando la aplicación accede a **varias bases de datos**, un **servidor de integración** entre el servidor de aplicaciones y las BD presenta los datos distribuidos como si fuesen una sola BD. Reduce el tráfico respecto al cliente ligero de dos capas; la lógica de aplicación (la más volátil) se actualiza en un solo sitio.

## 5. Ejemplo resuelto: elegir arquitectura
*Problema:* aplicación de inventario para 500 usuarios, reglas de negocio que cambian cada trimestre, tres bases de datos en sucursales.
- Reglas cambiantes -> centralizar la lógica de negocio (servidor), descartar cliente rico.
- Tres BD -> servidor de integración (multicapa).
- Muchos usuarios -> separar aplicación y datos en procesadores distintos (tres capas) para escalar.
- **Resultado:** cliente ligero (navegador) + servidores de aplicación + servidor de integración + BD.

## Errores comunes
- Mezclar lógica de negocio en la capa de presentación (rompe la reutilización).
- Creer que cliente/servidor implica máquinas distintas: son roles de proceso.
- Ignorar que el servidor central es **punto único de fallo y cuello de botella**.

## Ejercicios propuestos
1. ¿Qué lógica reside en un procedimiento almacenado? *R: lógica de negocio/datos.*
2. Ventaja de tres capas sobre dos con cliente ligero. *R: separa aplicación y datos en procesadores distintos, escala mejor.*
3. ¿Por qué el cajero usa un gestor de transacciones? *R: serializa transacciones y evita corrupción ante fallos.*

## Conexiones
[[Sistemas Distribuidos - 08 Comunicación entre procesos]] (protocolo solicitud/respuesta), [[Sistemas Distribuidos - 06 SOA y servicios web]], [[Desarrollo de Aplicaciones Web]].

## Fuente
Clase 2.pdf (2010 palabras) y CS.pdf (3585 palabras).
