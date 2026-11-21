---
tags: [clase, semestre-VI]
materia: Servicio Comunitario
---
# Servicio Comunitario - Transferencia Tecnológica y Sostenibilidad Comunitaria

Materia: [[Servicio Comunitario]]
Anterior: [[Servicio Comunitario - Seguimiento, Bitácora y Control de Horas]]
Siguiente: [[Servicio Comunitario - Cierre, Informe Final, Evaluación y Acta de Culminación]]

## Contexto y objetivo
Uno de los mayores fracasos en proyectos universitarios de informática ocurre cuando el sistema desarrollado o los equipos recuperados dejan de usarse pocas semanas después de que los estudiantes aprueban la materia. Para evitar ese desperdicio de esfuerzo, la etapa final de ejecución en [[Servicio Comunitario]] debe centrarse en la **transferencia tecnológica** y el aseguramiento de la **sostenibilidad**.

Al finalizar esta clase, el estudiante sabrá preparar la entrega técnica integral (manuales, respaldos, código y credenciales), capacitar a usuarios multiplicadores y verificar que la comunidad pueda operar autónomamente.

## 1. ¿Qué es la transferencia tecnológica comunitaria?
No basta con "instalar" una solución; transferir tecnología implica entregar a la comunidad tanto el **artefacto** (software, red, aula configurada) como el **conocimiento práctico** para operarlo, respaldarlo y resolver fallas cotidianas sin depender permanentemente del estudiante.

## 2. Paquete de entrega técnica (Kit de Sostenibilidad)
Todo proyecto informático comunitario debe dejar en manos de la institución receptora un paquete organizado (en carpeta local y en medio externo como pendrive o repositorio):
1. **Manual de Usuario**: redactado en lenguaje sencillo, con capturas de pantalla paso a paso para las tareas frecuentes (registrar, consultar, imprimir reporte).
2. **Manual Técnico / de Administración**: arquitectura básica, ubicación de la base de datos, instrucciones de arranque/reinicio del servidor local y procedimiento de respaldo y restauración.
3. **Código fuente y scripts de base de datos**: debidamente comentados, con archivo `README.md` y lista de dependencias.
4. **Gestión de credenciales**: entrega formal de usuarios administradores y contraseñas al tutor comunitario (recomendando cambiar las claves iniciales tras la entrega).
5. **Plan de copias de seguridad (Backups)**: automatizado si es posible, o mediante un procedimiento de un solo clic hacia una unidad externa.

## 3. Formación de usuarios clave (Multiplicadores)
En instituciones comunitarias suele haber rotación de personal o voluntarios. Para mitigar este riesgo:
- **Capacitar al menos a 2 o 3 personas** en la operación crítica del sistema, nunca a una sola.
- **Realizar simulacros de falla controlada**: enseñar qué hacer si se va la luz, si el navegador muestra error de conexión local o si se necesita restaurar el respaldo de la semana anterior.
- **Evaluación práctica de autonomía**: observar al usuario comunitario operando la herramienta sin ayuda del estudiante antes de dar por concluida la transferencia.

## 4. Validación de usabilidad y aceptación en campo
Antes del cierre administrativo, se realiza una **entrega formal** mediante un **Acta de Entrega de Productos Tecnológicos**, donde el tutor comunitario verifica que:
- El sistema o laboratorio funciona en las condiciones reales de la sede.
- Los manuales y archivos fuente fueron recibidos.
- El personal designado recibió la capacitación acordada.

## Errores comunes
- **Dejar contraseñas en manos exclusivas del estudiante desarrollador**: bloquea a la comunidad ante cualquier cambio futuro.
- **Entregar manuales llenos de jerga técnica**: un manual que dice *"ejecute `docker-compose up -d`"* no es útil para una secretaria escolar si no se automatiza con un acceso directo claro.
- **No probar la restauración del respaldo**: hacer copias de seguridad sin verificar nunca que realmente se pueden restaurar.

## Ejercicios propuestos
1. Diseña un esquema breve (4 puntos) para el Manual de Usuario de un sistema de registro de citas en un ambulatorio comunitario.
   - *Respuesta esperada:* (1) Cómo encender el equipo e iniciar el sistema; (2) Cómo registrar un nuevo paciente y asignar cita; (3) Cómo buscar, reprogramar o cancelar una cita; (4) Qué hacer ante mensajes de error comunes y cómo hacer el respaldo al final del día.
2. ¿Por qué es riesgoso capacitar únicamente al director de la institución en el uso operativo del software?
   - *Respuesta esperada:* Porque el director suele tener múltiples responsabilidades administrativas y poca disponibilidad diaria; además, si cambia de cargo, el conocimiento se pierde. Es indispensable capacitar al personal operativo cotidiano y al menos a un respaldo.

## Conexiones
- Materia principal: [[Servicio Comunitario]]
- Anterior: [[Servicio Comunitario - Seguimiento, Bitácora y Control de Horas]]
- Siguiente: [[Servicio Comunitario - Cierre, Informe Final, Evaluación y Acta de Culminación]]
- Diseño previo de sostenibilidad: [[Proyecto Servicio Comunitario - Evaluación, Indicadores y Sostenibilidad del Proyecto]]

## Fuente
Basado en el programa típico de la asignatura y en buenas prácticas de entrega y transferencia de software.
