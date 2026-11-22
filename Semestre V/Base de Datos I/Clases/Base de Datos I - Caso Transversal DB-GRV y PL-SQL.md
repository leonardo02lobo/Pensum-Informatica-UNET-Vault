---
tags: [clase, semestre-V, oracle, plsql]
materia: Base de Datos I
---
# Base de Datos I - Caso Transversal DB-GRV y PL/SQL

Materia: [[Base de Datos I]]
Anterior: [[SQL avanzado - ROLLUP CUBE y casos de estudio]]
Siguiente: _Ninguna_

## Contexto y objetivo

Recopilación práctica del proyecto transversal **Gestión de Reservación de Vehículos (DB-GRV)** (Equipo 4, Lapso 2025-2) y del proyecto **DB-GBT** (Bolsa de Trabajo), desarrollados bajo el marco **DAMA-DMBOK** en **Oracle Database** con **Oracle SQL Developer Data Modeler** (Temas 1 al 6 en Google Drive).

## 1. Ciclo de desarrollo (Temas 1 al 6)

1. **Tema 1 (Gobierno y Trazabilidad):** Marco DAMA-DMBOK, justificación y matriz de trazabilidad entre objetivos del negocio y requisitos de la aplicación.
2. **Tema 2 (Diseño Conceptual/Lógico):** Rueda DAMA-DMBOK, requisitos de datos, entidades principales (`CLIENTE`, `VEHICULO`, `AGENCIA`, `RESERVA`, `PROMOCION`, auto-relación `avalado`), cardinalidades.
3. **Tema 3 (Modelo Relacional y Físico):** Transformación en Oracle SQL Developer Data Modeler, normalización (1FN–3FN), claves primarias/foráneas y arcos/supertipos (`AGENCIA_PROPIA`, `AGENCIA_CONVENIO`).
4. **Tema 4 (DDL/DML y Pruebas):** Implementación de **16 tablas**, **8 secuencias (`seq_*`)**, **3 índices (`IDX*`)**, restricciones `CHECK` con `REGEXP_LIKE`, normalización `INITCAP` y planilla de casos de prueba (`CPBD04`).
5. **Tema 5 (SQL Avanzado):** Consultas sobre facturación (`FACTURAS`, `COBRANZAS`, `CANALES`, `CLIENTES`, `SERVICIOS`, `SUCURSALES`, `VENDEDORES`) con `JOIN`, `NOT EXISTS`, `GROUP BY`, `CASE`, `ROUND`, `EXTRACT` y cubos (`ROLLUP` / `CUBE`).
6. **Tema 6 (PL/SQL):** Tabla materializada `RESUMEN_SERVICIOS`, trigger `BEFORE INSERT` con validaciones `RAISE_APPLICATION_ERROR`, cursor con patrón `UPSERT` (`DUP_VAL_ON_INDEX`) y paquete `resumen_servicios_pkg`.

## 2. Ejemplo PL/SQL (Trigger + UPSERT + Paquete)

Patrón utilizado en el Tema 6 (Oracle PL/SQL):

```sql
CREATE OR REPLACE TRIGGER validar_resumen_servicios
BEFORE INSERT ON RESUMEN_SERVICIOS
FOR EACH ROW
BEGIN
    IF :NEW.total_facturado < 0 THEN
        RAISE_APPLICATION_ERROR(-20001, 'El total facturado no puede ser negativo.');
    END IF;
END;
/

-- Patrón UPSERT dentro de un cursor explícito
BEGIN
    INSERT INTO RESUMEN_SERVICIOS (canal_id, servicio_id, total_facturado)
    VALUES (v_canal, v_servicio, v_total);
EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        UPDATE RESUMEN_SERVICIOS
        SET total_facturado = total_facturado + v_total
        WHERE canal_id = v_canal AND servicio_id = v_servicio;
END;
/
```

## Errores comunes

- Olvidar el orden de creación/borrado de tablas por dependencias de claves foráneas (o no incluir `ON DELETE CASCADE` cuando corresponde en tablas de resumen).
- Usar `CHECK` sin validar formatos de cadenas (teléfonos, cédulas, placas) cuando se requiere `REGEXP_LIKE`.

## Recursos en Google Drive (Equipo 4 - 2025-2)

- [Tema 1](https://drive.google.com/drive/folders/1ebrGcGsMoCyq0GKRRwID2dOSPXr9vdUa) · [Tema 2](https://drive.google.com/drive/folders/1kkx3DYHP6aMrcUWpGfnosM3I_OCLu0si) · [Tema 3](https://drive.google.com/drive/folders/1YgO1oe7xu_nwVcOktf73oGOtTpsOl_mO) · [Tema 4](https://drive.google.com/drive/folders/1OHk5oJ7oQ1GL43x6Czmsoy1_GIjePCFf) · [Tema 5](https://drive.google.com/drive/folders/1t-6vGLO0tdvqBTEcQ4-RA-A9bKaI7i-c) · [Tema 6](https://drive.google.com/drive/folders/1ByEhaTCwF8uRLnj27IWvHbdKE43ajGa5)

## Conexiones

- Continúa directamente lo visto en [[SQL avanzado - ROLLUP CUBE y casos de estudio]].
- Prepara la base práctica para [[Administración de Base de Datos]] y [[Sistema de Información I]].
