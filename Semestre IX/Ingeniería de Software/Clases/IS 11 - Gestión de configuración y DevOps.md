---
tags: [clase, semestre-IX]
materia: Ingeniería de Software
fuente: "conocimiento general"
---
# IS 11 - Gestión de configuración y DevOps

Materia: [[Ingeniería de Software]]
Anterior: [[IS 10 - Gestión de proyectos y estimación]]

## Contexto y objetivo
Un sistema cambia constantemente: código, dependencias, configuraciones, documentación. La **gestión de configuración del software (SCM)** controla esos cambios; **DevOps** integra desarrollo y operaciones para entregar valor de forma rápida y confiable mediante automatización. Objetivo: manejar Git con flujos de trabajo, entender CI/CD, contenedores, infraestructura como código y observabilidad, con un pipeline de ejemplo.

## Gestión de configuración (SCM)
Actividades (IEEE 828): **identificación** de elementos de configuración (CI), **control de cambios**, **contabilidad de estado**, **auditorías**, gestión de versiones y de *builds/releases*.
- **Línea base (baseline)**: versión aprobada que sirve de punto de referencia.
- **Versionado semántico (SemVer)** `MAYOR.MENOR.PARCHE`: MAYOR cambios incompatibles; MENOR funcionalidad compatible; PARCHE correcciones. Ejemplo: 2.4.1 a 2.5.0 (nueva función).
- **Gestión de cambios**: solicitud, evaluación de impacto (trazabilidad, ver [[IS 02 - Ingeniería de requisitos]]), aprobación (comité CCB en entornos formales), implementación, verificación.

## Control de versiones con Git
Sistema distribuido: cada clon es un repositorio completo. Objetos: *blob*, *tree*, *commit*, *tag*. Áreas: directorio de trabajo, *staging area* (índice), repositorio local, remoto.

Comandos esenciales:
```bash
git init / git clone URL
git status ; git diff
git add archivo ; git commit -m "feat: registrar prestamo"
git log --oneline --graph
git branch rama ; git switch -c feature/prestamos
git merge feature/prestamos        # integra (puede generar commit de merge)
git rebase main                    # reaplica tus commits sobre main (historia lineal)
git stash ; git stash pop
git revert <commit>                # deshace con un nuevo commit (seguro en ramas compartidas)
git reset --hard <commit>          # peligroso: descarta cambios
git push origin rama ; git pull --rebase
git tag -a v1.2.0 -m "release"
```
**Conflictos de merge**: Git marca `<<<<<<<`, `=======`, `>>>>>>>`; se edita, se hace `git add` y se continúa. **Regla**: no reescribas historia ya publicada (rebase/force push en ramas compartidas).

**Mensajes de commit**: convención *Conventional Commits* (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`), mensaje imperativo, un cambio lógico por commit.

### Flujos de ramas
- **Git Flow**: main, develop, feature, release, hotfix (releases planificadas).
- **GitHub Flow**: main siempre desplegable + ramas cortas + *pull request*.
- **Trunk-Based Development**: ramas muy cortas o commits directos a trunk con *feature flags*; base de CD de alto rendimiento.
Pull request: descripción, revisión de pares, CI verde, aprobación, merge (squash, merge commit o rebase).

## Integración y entrega continuas
- **CI (Integración Continua)**: integrar a la rama principal frecuentemente (al menos a diario); cada integración dispara *build* y pruebas automáticas.
- **Entrega continua (CD)**: el software está siempre listo para desplegarse; el despliegue a producción es una decisión (botón).
- **Despliegue continuo**: cada cambio que pasa el pipeline se despliega automáticamente.
Etapas típicas del pipeline: compilar, pruebas unitarias, análisis estático/calidad (SonarQube, linters), pruebas de seguridad (SAST, dependencias), empaquetar (imagen Docker), pruebas de integración, desplegar a staging, pruebas de humo, aprobar, desplegar a producción.

Ejemplo de pipeline en GitHub Actions:
```yaml
name: ci
on:
  push:
    branches: [main]
  pull_request:
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.12"
      - run: pip install -r requirements.txt pytest pytest-cov
      - run: pytest --cov=app --cov-fail-under=80   # falla si cobertura menor a 80%
  docker:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: docker build -t prestamos:${{ github.sha }} .
```
Herramientas: GitHub Actions, GitLab CI, Jenkins, CircleCI.

## Contenedores
**Docker** empaqueta aplicación y dependencias en una imagen reproducible; los contenedores comparten el kernel del anfitrión (más livianos que máquinas virtuales).
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["gunicorn", "-b", "0.0.0.0:8000", "app:app"]
```
`docker compose` orquesta varios servicios (app + base de datos). **Kubernetes** orquesta contenedores a escala (pods, deployments, services, ingress, autoescalado). Ver [[Sistemas Distribuidos]].

## Infraestructura como código (IaC)
Describir la infraestructura en archivos versionados: Terraform (aprovisionamiento declarativo), Ansible (configuración), CloudFormation. Beneficios: reproducibilidad, revisiones, eliminación de "servidores copo de nieve".

## Estrategias de despliegue
- **Rolling**: se reemplazan instancias gradualmente.
- **Blue/Green**: dos entornos; se conmuta el tráfico.
- **Canary**: se expone a un pequeño porcentaje de usuarios.
- **Feature flags**: activar funciones sin desplegar.
- **Rollback** automatizado y migraciones de BD compatibles hacia atrás (expand/contract).

## Observabilidad y operación
Tres pilares: **logs, métricas, trazas** (OpenTelemetry). Herramientas: Prometheus + Grafana, ELK/Loki, Jaeger. Conceptos SRE: SLI (indicador), SLO (objetivo), SLA (acuerdo), presupuesto de error, *post-mortems* sin culpables. Métricas DORA para medir el desempeño de entrega (ver [[IS 09 - Calidad y métricas de software]]).

## DevSecOps
Seguridad desplazada a la izquierda: escaneo de dependencias (SCA), secretos en gestores (nunca en el repositorio), imágenes mínimas, firmas, revisión de configuraciones, SBOM.

## Ejemplo resuelto: del commit a producción
1. Ana crea `feature/vencidos`, commitea con `feat: marcar prestamos vencidos`.
2. Abre un PR; el pipeline ejecuta pytest (cobertura 84%, supera el mínimo del 80%) y linters.
3. Luis revisa y pide un cambio de nombre; Ana añade un commit.
4. Se aprueba y se hace *squash merge* a main.
5. CI construye la imagen `prestamos:abc123`, la sube al registro y despliega a staging.
6. Pruebas de humo pasan; el líder aprueba y se hace canary al 10%, luego 100%.
7. Se etiqueta v1.3.0 y se publican notas de versión; si el error de 5xx sube, rollback.

## Errores comunes
- Commits gigantes y mensajes como "cambios".
- Subir credenciales o archivos `.env` al repositorio (usa `.gitignore` y gestor de secretos; si ocurre, rota la credencial).
- Ramas de larga vida que generan "infierno de merge".
- Pipeline lento y frágil que el equipo aprende a ignorar.
- Considerar DevOps como un puesto en lugar de una cultura.

## Ejercicios propuestos
1. ¿Qué incrementa SemVer al corregir un bug sin cambiar la API? *Resp.: el PARCHE (x.y.Z).*
2. Diferencia entre `merge` y `rebase`. *Resp.: merge preserva la historia con un commit de unión; rebase reescribe los commits para una historia lineal.*
3. ¿Qué diferencia hay entre entrega y despliegue continuo? *Resp.: en la entrega el paso a producción es manual/decisión; en el despliegue es automático.*

## Conexiones
[[Sistemas Distribuidos]], [[Administración de Redes]], [[Desarrollo de Aplicaciones Web]], [[IS 08 - Pruebas de software]], [[IS 01 - Ciclo de vida y modelos de proceso]].

## Fuente
Conocimiento general. Chacon y Straub, *Pro Git*; Humble y Farley, *Continuous Delivery*; Kim et al., *The DevOps Handbook*; Forsgren et al., *Accelerate*.
