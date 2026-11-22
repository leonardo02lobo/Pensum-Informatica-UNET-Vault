---
tags: [proyecto, semestre-VI, servicio-comunitario, fastapi, react]
materia: Servicio Comunitario
---
# Sistema Comedor Universitario UNET (CSC-P 2026)

Materia: [[Servicio Comunitario]] · [[Proyecto Servicio Comunitario]]

## Resumen del proyecto

**CSC-P 1/2026: Sistema de Gestión e Información para el Comedor Universitario UNET** (Decanato de Desarrollo Estudiantil), ejecutado entre el **12/05/2026 y el 07/08/2026** (30 sesiones × 4 h = 120 horas) por Leonardo Lobo y Frankly Bautista bajo la tutoría de la Prof. Hedry Fortoul.

## 1. Stack Tecnológico y Arquitectura

| Capa | Tecnologías Utilizadas | Detalles Clave |
|---|---|---|
| **Backend** | Python 3.12, **FastAPI**, SQLAlchemy 2, Pydantic, **Alembic** (34 migraciones), `uv` | 22 routers, 120–135 rutas REST (`/auth`, `/students`, `/lunch-sessions`, `/consumptions`, `/sanctions`, `/inventory`, `/lunches`, `/audit-logs`) |
| **Base de datos** | **PostgreSQL 16** (26 tablas en esquema `public`) | Índice único parcial `uq_lunch_sessions_open_sede`; importación CSV de **8.545 estudiantes** (18 carreras) |
| **Frontend / Escritorio** | **React 19**, TypeScript, Vite, Tailwind CSS, **Tauri 2** | 26–29 pantallas (25 protegidas por RBAC); hook `useBarcodeScanner` para lector USB HID ($<60\text{ ms}$) |
| **Seguridad** | JWT HS256 en cookies `HttpOnly` (`unet_access_token`, `unet_refresh_token`), `bcrypt` | 4 roles: `SUPER_ADMIN`, `ADMIN`, `TAQUILLERO`, `ACCESO_DIRECTO` / `BENEFICIARIO` |
| **Calidad / Pruebas** | `pytest` (servidor), suite cliente | **429** pruebas en servidor y **289** en cliente |

## 2. Documentación y Formatos UNET Utilizados

- **Planificación y control:** `CSC-04` (Control de tutorías — 7 sesiones), `CSC-06` (Control de actividades — 30 sesiones / 120 h), `CSC-10` (Acta de comunidad).
- **Evaluación:** Instrumentos de Impacto Social (RED Táchira: estudiante y comunidad), Manual de Usuario y Documentación Técnica (`v0.1.0`), e Informe Final.

## Recursos en Google Drive

- [Carpeta Cartas de Servicio Comunitario](https://drive.google.com/drive/folders/18cDnPQMG4WmIkl1pscMLvl4nRUhwDBye)
- [Manual y Documentación Técnica (PDF)](https://drive.google.com/file/d/1efyX74Bt7ulDlPC2udoOMLj3gJkvmQkt/view?usp=drivesdk)
- [Informe Final (DOCX)](https://docs.google.com/document/d/1WeYTBzbHXIfH1o9iCsU17wk-sfkgg1bu/edit?usp=drivesdk)

## Conexiones

- Caso de estudio reutilizado en [[Sistema de Información I - Casos de Uso, PIECES y DFD (Comedor UNET)]] y [[Administración de Base de Datos - Prácticas Oracle 18c XE (DBCA, Arranque, Redo Logs y Seguridad)]].
- Se apoya en [[Base de Datos I]], [[Desarrollo de Aplicaciones Web]] e [[Ingeniería de Software]].
