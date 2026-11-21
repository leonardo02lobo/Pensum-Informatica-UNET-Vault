---
tags: [clase, electiva]
materia: Desarrollo de Aplicaciones Web
fuente: "conocimiento general"
---
# DAW 03 - JavaScript, DOM y consumo de APIs

Materia: [[Desarrollo de Aplicaciones Web]]
Anterior: [[DAW 02 - HTML5, CSS3 y diseño responsivo]]
Siguiente: [[DAW 04 - Back-end con Node.js, Express y FastAPI]]

## Contexto y objetivo
JavaScript es el lenguaje del navegador (y de Node.js en el servidor). Objetivo: dominar variables, funciones, asincronía, manipulación del DOM y consumo de una API REST con `fetch`, y conocer el papel de los frameworks (React, Vue).

## Teoría

### Fundamentos
- `let` y `const` (bloque) frente a `var` (función); preferir `const`.
- Tipos primitivos: number, string, boolean, null, undefined, symbol, bigint; objetos y arreglos son referencias.
- Igualdad: usar `===`.
- Funciones flecha: `const f = (x) => x * 2;`. Cierres (closures): una función recuerda su ámbito léxico.
- Métodos funcionales de arreglos: `map`, `filter`, `reduce`, `find`.
- Módulos: `import`/`export`.

### Asincronía
JavaScript es monohilo con **bucle de eventos**: las operaciones lentas (red, temporizadores) se delegan y su callback entra a la cola. `Promise` representa un valor futuro (pending, fulfilled, rejected); `async/await` es azúcar sintáctica sobre promesas. Orden: código síncrono, luego microtareas (promesas), luego macrotareas (`setTimeout`).

### DOM
Árbol de objetos que representa el documento. Seleccionar con `querySelector`, modificar con `textContent`, `classList`, `append`, escuchar con `addEventListener`. Usar `textContent` y no `innerHTML` para texto de usuario (previene XSS).

### Frameworks
React (componentes, estado, JSX, DOM virtual) y Vue (reactividad, plantillas). Justificación: estado complejo, reutilización de componentes. No sustituyen entender el DOM y HTTP.

## Ejemplo resuelto
Lista de libros que se carga desde la API del DAW 01, con formulario para crear y manejo de errores.

```html
<ul id="lista"></ul>
<form id="form">
  <input id="titulo" placeholder="Título" required>
  <button>Agregar</button>
</form>
<p id="estado" role="status"></p>
<script type="module" src="app.js"></script>
```
```js
// app.js
const API = "/api/v1/libros";
const lista = document.querySelector("#lista");
const estado = document.querySelector("#estado");

async function pedir(url, opciones = {}) {
  const resp = await fetch(url, {
    headers: { "Content-Type": "application/json" },
    ...opciones,
  });
  if (!resp.ok) throw new Error(`HTTP ${resp.status}`);
  return resp.status === 204 ? null : resp.json();
}

function pintar(libros) {
  lista.replaceChildren(); // vaciar
  for (const libro of libros) {
    const li = document.createElement("li");
    li.textContent = `${libro.titulo} (${libro.anio ?? "s/f"})`; // seguro ante XSS
    const borrar = document.createElement("button");
    borrar.textContent = "Borrar";
    borrar.addEventListener("click", () => eliminar(libro.id));
    li.append(" ", borrar);
    lista.append(li);
  }
}

async function cargar() {
  try {
    estado.textContent = "Cargando...";
    pintar(await pedir(API));
    estado.textContent = "";
  } catch (e) {
    estado.textContent = "No se pudo cargar: " + e.message;
  }
}

async function eliminar(id) {
  await pedir(`${API}/${id}`, { method: "DELETE" });
  await cargar();
}

document.querySelector("#form").addEventListener("submit", async (ev) => {
  ev.preventDefault();
  const titulo = document.querySelector("#titulo").value.trim();
  await pedir(API, { method: "POST", body: JSON.stringify({ titulo }) });
  ev.target.reset();
  await cargar();
});

cargar();
```
Paso a paso: `pedir` centraliza `fetch` y convierte códigos no 2xx en excepción (`fetch` solo rechaza ante fallos de red); `pintar` usa `textContent`; el `submit` evita el envío nativo con `preventDefault`; `async/await` serializa pedir, luego recargar.

Operaciones en paralelo:
```js
const [libros, autores] = await Promise.all([pedir("/api/v1/libros"), pedir("/api/v1/autores")]);
```
Pseudocódigo de un componente React equivalente: estado con `useState`, carga con `useEffect`, lista renderizada con `libros.map(...)`.

## Errores comunes
- Olvidar `await` (se obtiene una Promise, no el dato).
- Suponer que `fetch` lanza error en 404/500.
- `innerHTML` con datos del usuario.
- Comparar con `==`.
- Mutar el estado directamente en frameworks.
- Olvidar `preventDefault` en formularios.

## Ejercicios propuestos
1. ¿Qué imprime `console.log(1); setTimeout(()=>console.log(2),0); Promise.resolve().then(()=>console.log(3)); console.log(4)`? *Respuesta: 1, 4, 3, 2.*
2. Dado `const n=[1,2,3,4]`, obtén la suma de los cuadrados de los pares. *Respuesta: `n.filter(x=>x%2===0).map(x=>x*x).reduce((a,b)=>a+b,0)` = 20.*
3. ¿Por qué `textContent` es más seguro que `innerHTML`? *Respuesta: no interpreta el texto como HTML, así que no ejecuta scripts inyectados.*

## Conexiones
[[Programación II]] (funciones, estructuras), [[Multimedia]] (interfaces), [[Sistemas Distribuidos]] (comunicación asíncrona), [[Sistemas Operativos]] (hilos y bucles de eventos).

## Fuente
Conocimiento general: MDN Web Docs; Flanagan, *JavaScript: The Definitive Guide*.
