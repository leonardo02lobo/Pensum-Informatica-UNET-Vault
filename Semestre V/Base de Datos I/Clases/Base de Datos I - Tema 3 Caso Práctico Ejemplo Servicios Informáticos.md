---
tags: [clase, semestre-V]
materia: Base de Datos I
fuente: Material/baseDatosI/temaIII/materialApoyo/Caso Practico Ejemplo Tema 3 v1.pdf
---
# Tema 3 - Caso práctico ejemplo: modelo relacional de "Servicios Informáticos"

Materia: [[Base de Datos I]]
Anterior: [[Base de Datos I - Tema 3 Curso de Diseño Físico]]
Siguiente: [[Base de Datos I - Tema 3 Caso de Estudio Diseño Físico]]

## Contexto y objetivo
Documento de 8 diapositivas que ilustra cómo se redacta la parte "matemática" del diseño físico: el **esquema relacional** de una base de datos y las **operaciones de álgebra relacional** sobre ella. Es el modelo de respuesta para la sección 8b del caso de estudio del Tema 3. Teoría previa: [[Base de Datos I - Tema 3 Curso de Modelo Relacional]].

## 1. Definición formal usada
Una base de datos relacional es una colección de relaciones que forman un esquema $R(r_1, r_2, \dots, r_n)$; cada relación es una tabla de valores y cada fila una colección de valores relacionados. Formalmente, una relación $r(R)$ del esquema $R(A_1,\dots,A_n)$ es un conjunto de n-tuplas $r=\{t_1,\dots,t_m\}$ donde cada tupla $t=\langle v_1,\dots,v_n\rangle$ cumple $v_i \in Dom(A_i)$ (o NULL). Nombre de relación = tabla, tupla = fila, atributo = columna.
Notación del esquema de una relación, con PK y FK marcadas:
`EMPLEADO(Nro_Emp:PK, Nombre, Dirección, Fecha_Nacim, Nro_Dept:FK)`.

## 2. Esquema del caso "Servicios Informáticos"
Una empresa elabora presupuestos para clientes; consultores ejecutan actividades con tarifa por hora.
```
Clientes     (Rif:PK, Nombre, Dirección, Sucursal)
Consultores  (Cedula:PK, Nombre)
Actividades  (Codigo_act:PK, Nombre, Tarifa_hora)
Presupuestos (Nro_presup:PK, Fecha, Rif:FK1, Cedula:FK2)
Servicios    (fechaInicio, fechaFin, Horas_servicio,
              Nro_presup:PK-FK1, Codigo_act:PK-FK2, Cedula:PK-FK3)
```
Análisis: `Presupuestos` es 1:M respecto de Clientes (un cliente, varios presupuestos) y respecto de Consultores. `Servicios` es una **relación asociativa ternaria** entre presupuesto, actividad y consultor: su PK es la combinación de las tres FK (`PK-FK1, PK-FK2, PK-FK3`), y los atributos propios son fechas y horas. Observe el patrón de mapeo del curso de diseño físico: M:M (o ternaria) -> tabla de intersección con PK compuesta de FK.

## 3. Operaciones de álgebra relacional con explicación
1. **Selección de todas las tuplas**: $\sigma(Clientes)$ (sin condición; equivale a `SELECT * FROM clientes`).
2. **Selección con condición**: $\sigma_{Rif='J-234096-7'}(Clientes)$: todas las columnas de un cliente. SQL: `WHERE rif = 'J-234096-7'`.
3. **Proyección**: $\pi_{Clientes.Rif,\ Clientes.Nombre}(Clientes)$: solo dos columnas de todas las filas.
4. **Proyección con join** (cliente + presupuestos):
$$\pi_{C.Rif,\,C.Nombre,\,P.Nro\_presup,\,P.fecha}\big(\sigma_{C.Rif=P.Rif}(C \times P)\big)$$
Explicación del documento: el join verifica que la PK `Clientes.Rif` exista como FK en `Presupuestos.Rif`; **un cliente sin presupuestos no aparece** (es un join interno). Para incluirlo se necesitaría un outer join, que no está en el álgebra básica.
5. **Join de tres tablas con filtro de fecha**:
$$\pi_{C.Nombre,\,P.fecha,\,K.Nombre}\big(\sigma_{C.Rif=P.Rif \wedge P.cedula=K.cedula \wedge P.fecha>'01/01/2023'}(C \times P \times K)\big)$$
Muestra el nombre del cliente, la fecha del presupuesto y el nombre del consultor para presupuestos posteriores a enero de 2023. Tres condiciones: dos de unión y una de filtro.

## 4. Traducción a SQL (complemento)
```sql
-- consulta 5
SELECT c.nombre, p.fecha, k.nombre
FROM   clientes c
JOIN   presupuestos p ON c.rif = p.rif
JOIN   consultores  k ON p.cedula = k.cedula
WHERE  p.fecha > DATE '2023-01-01';
```

## 5. Cómo usar este modelo de respuesta
- Declarar primero el esquema con PK y FK.
- Para cada requerimiento: identificar tablas involucradas, escribir el producto/join con sus condiciones PK = FK, agregar la selección con filtros y cerrar con la proyección de las columnas pedidas.
- Explicar el **tipo de operación**: selección, proyección, combinación (derivada de producto + selección).

## Errores comunes
- Aplicar proyección antes de la selección usando columnas que la proyección eliminó.
- Olvidar una de las condiciones de join en un join de tres tablas (resulta un producto parcial).
- Escribir la FK compuesta de `Servicios` como una sola.

## Ejercicios propuestos
1. Escriba el álgebra para "nombres de consultores que han realizado la actividad de código A10". ($\pi_{K.Nombre}(\sigma_{K.cedula=S.cedula \wedge S.Codigo\_act='A10'}(K \times S))$)
2. Calcule el costo de un servicio. ($Horas\_servicio \cdot Tarifa\_hora$, uniendo Servicios y Actividades.)
3. Clientes sin presupuestos: $\pi_{Rif}(Clientes) - \pi_{Rif}(Presupuestos)$.

## Conexiones
[[Base de Datos I - Tema 3 Caso de Estudio Diseño Físico]], [[Base de Datos I - Tema 5 Consultas avanzadas SQL]].

## Fuente
`Material/baseDatosI/temaIII/materialApoyo/Caso Practico Ejemplo Tema 3 v1.pdf`. Traducción a SQL y ejercicios son complemento.
