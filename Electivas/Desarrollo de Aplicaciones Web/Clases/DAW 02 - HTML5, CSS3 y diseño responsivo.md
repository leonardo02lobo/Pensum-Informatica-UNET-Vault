---
tags: [clase, electiva]
materia: Desarrollo de Aplicaciones Web
fuente: "conocimiento general"
---
# DAW 02 - HTML5, CSS3 y diseño responsivo

Materia: [[Desarrollo de Aplicaciones Web]]
Anterior: [[DAW 01 - HTTP, cliente-servidor y REST]]
Siguiente: [[DAW 03 - JavaScript, DOM y consumo de APIs]]

## Contexto y objetivo
El front-end es lo que el usuario ve. HTML estructura, CSS presenta y JavaScript comporta. Objetivo: escribir páginas con marcado semántico, accesibles y que se adapten a distintos tamaños de pantalla.

## Teoría

### HTML5 semántico
Etiquetas con significado: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`, `figure`. Mejoran accesibilidad, SEO y mantenimiento frente a `div` genéricos. Formularios: `input type="email|date|number|password"`, `required`, `pattern`, `label for`.

### CSS3
- **Selectores**: etiqueta, clase `.x`, id `#x`, descendiente, hijo `>`, pseudoclases `:hover`, `:focus`, `:nth-child`.
- **Cascada y especificidad**: gana la regla más específica (id > clase > etiqueta), luego la última. `!important` rompe el orden; evitarlo.
- **Modelo de caja**: contenido + padding + border + margin. `box-sizing: border-box` hace que `width` incluya padding y borde.
- **Layout**: Flexbox (una dimensión) y Grid (dos dimensiones).
- **Variables**: `--color: #0a7;` y `var(--color)`.

### Diseño responsivo
Enfoque *mobile first*: se escribe para móvil y se amplía con `@media (min-width: ...)`. Imprescindible la meta `viewport`. Unidades relativas: `rem`, `%`, `vw`, `fr`, `clamp()`.

### Accesibilidad (WCAG)
Contraste mínimo 4,5:1 para texto normal, textos alternativos `alt`, navegación con teclado, `label` asociados, atributos ARIA solo cuando el HTML nativo no basta, jerarquía correcta de `h1-h6`.

## Ejemplo resuelto
Una tarjeta de cursos que pasa de 1 columna (móvil) a 3 columnas (escritorio).

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Cursos</title>
  <link rel="stylesheet" href="estilos.css">
</head>
<body>
  <header><h1>Catálogo de cursos</h1>
    <nav aria-label="Principal">
      <a href="#web">Web</a> <a href="#datos">Datos</a>
    </nav>
  </header>
  <main>
    <section class="tarjetas" id="web">
      <article class="tarjeta">
        <img src="web.png" alt="Logotipo del curso de desarrollo web">
        <h2>Desarrollo Web</h2>
        <p>HTML, CSS y JavaScript.</p>
        <a class="boton" href="/cursos/web">Ver curso</a>
      </article>
      <!-- repetir tarjetas -->
    </section>
    <form action="/suscribir" method="post">
      <label for="correo">Correo</label>
      <input id="correo" name="correo" type="email" required>
      <button type="submit">Suscribirme</button>
    </form>
  </main>
  <footer><small>Electiva DAW</small></footer>
</body>
</html>
```
```css
:root { --primario: #0b6e4f; --texto: #1c1c1c; --fondo: #fafafa; }
*, *::before, *::after { box-sizing: border-box; }
body { margin: 0; font-family: system-ui, sans-serif;
       color: var(--texto); background: var(--fondo); line-height: 1.5; }
header, main, footer { padding: 1rem; }

/* Mobile first: una columna */
.tarjetas { display: grid; gap: 1rem; grid-template-columns: 1fr; }
.tarjeta { background: #fff; border: 1px solid #ddd; border-radius: .5rem; padding: 1rem; }
.tarjeta img { max-width: 100%; height: auto; }
.boton { display: inline-block; padding: .5rem 1rem; color: #fff;
         background: var(--primario); border-radius: .25rem; text-decoration: none; }
.boton:focus-visible { outline: 3px solid #ffbf47; outline-offset: 2px; }

/* Tablet y escritorio */
@media (min-width: 48rem) { .tarjetas { grid-template-columns: repeat(2, 1fr); } }
@media (min-width: 64rem) { .tarjetas { grid-template-columns: repeat(3, 1fr); } }
```
Paso a paso: (1) `viewport` evita que el móvil simule 980 px; (2) la rejilla comienza con una columna; (3) los `media queries` suben a 2 y 3 columnas; (4) `max-width:100%` en imágenes impide desbordes; (5) `:focus-visible` mantiene el foco visible para teclado. Contraste: blanco sobre `#0b6e4f` supera 4,5:1 (comprobar con una herramienta de contraste).

## Errores comunes
- Maquetar con tablas o `div` sin semántica.
- Olvidar `viewport` y `alt`.
- Anchos fijos en píxeles.
- Quitar el `outline` sin alternativa.
- Selectores demasiado específicos que impiden sobrescribir.

## Ejercicios propuestos
1. ¿Cuál es el ancho real de un div con `width:200px; padding:20px; border:5px` en `content-box`? *Respuesta: 250 px (con `border-box`, 200 px).*
2. ¿Flexbox o Grid para una barra de navegación horizontal? *Respuesta: Flexbox (una dimensión).*
3. Escribe la regla para ocultar un menú en pantallas menores a 600 px. *Respuesta: `@media (max-width: 600px) { .menu { display:none; } }`.*

## Conexiones
[[Multimedia]] (imágenes, color y usabilidad), [[Ingeniería de Software]] (usabilidad y requisitos), [[Programación II]] (estructura de programas).

## Fuente
Conocimiento general: MDN Web Docs, WCAG 2.1 del W3C.
