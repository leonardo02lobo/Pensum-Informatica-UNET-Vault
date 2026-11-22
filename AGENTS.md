# AGENTS.md — Reglas para Agentes

Este repositorio contiene el Vault de Obsidian para **Ingeniería en Informática UNET**. Todo agente que trabaje en este repositorio debe cumplir estrictamente estas reglas.

---

## 1. Flujo de Git y GitHub (Protección de `main`)

La rama `main` está protegida en GitHub mediante un Ruleset activo (sin *bypass*):
- **Prohibido** trabajar, hacer commits, `push`, `merge` o `push --force` directamente sobre `main`.
- **Prohibido** modificar, desactivar o eliminar Rulesets o reglas de protección de ramas en GitHub.
- **Obligatorio** trabajar siempre en una rama nueva o asignada, creada a partir de `main` actualizada.

### Convención de nombres de ramas
Usa siempre prefijos descriptivos en minúsculas y separados por guiones (`kebab-case`):
- `feature/<tema>`: nuevas notas, clases, materias o ampliaciones de contenido del vault.
- `docs/<tema>`: documentación, índices principales (`README.md`, `Recursos Drive UNET.md`, `Fuentes Oficiales UNET.md`, MOCs).
- `fixture/<tema>`: correcciones de estructura, enlaces rotos, metadatos, plantillas o datos del pensum.
- `chore/<tema>`: mantenimiento del repositorio (`.gitignore`, `AGENTS.md`, limpieza).

### Entrega de cambios (Pull Request)
1. Antes de hacer commit, revisa `git status` y `git diff`.
2. **No** subas archivos temporales (ej. `Untitled`), archivos de estado local de Obsidian (`.obsidian/workspace*.json`) ni material binario/pesado dentro de `**/Material/` (excluido en `.gitignore`).
3. Haz commits claros y descriptivos en español.
4. Sube la rama al remoto (`git push -u origin <rama>`) y abre un **Pull Request** hacia `main` (`gh pr create`) con un resumen claro de los cambios.
5. **Nunca hagas merge del PR automáticamente.** El propietario del repositorio revisará y aprobará el merge manualmente en GitHub.

---

## 2. Convenciones del Vault (Obsidian)

- **Idioma:** Todo el contenido, títulos, notas y documentación deben estar en **español**.
- **Wikilinks:** Usa enlaces internos de Obsidian (`[[Nombre de la Nota]]`) para conectar materias, semestres, prelaciones y temas, preservando la navegación en la Vista de Grafo.
- **Estructura de carpetas:**
  - `Semestre I/` a `Semestre X/` y `Electivas/` contienen las carpetas de cada asignatura.
  - Dentro de cada asignatura:
    - `<Materia>.md`: ficha principal (frontmatter YAML con `tags`, prelaciones, materias que desbloquea, contenido programático, conceptos clave, bibliografía y recursos).
    - `Clases/`: notas detalladas por tema, encadenadas con `Anterior:` / `Siguiente:`, ejemplos resueltos, errores comunes, ejercicios propuestos y sección `## Conexiones` con `[[wikilinks]]`.
    - `Material/`: uso exclusivamente local para PDFs, guías y binarios pesados (ignorado por Git).
- **Índices y fuentes:** Si agregas asignaturas, recursos o referencias institucionales, mantén coherencia con:
  - `Pensum Ingeniería Informática UNET.md` (MOC principal)
  - `Recursos Drive UNET.md`
  - `Fuentes Oficiales UNET.md`
- **Higiene:** No dejes notas vacías, duplicadas ni archivos basura sin propósito.
