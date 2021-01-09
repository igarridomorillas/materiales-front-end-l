# Express: servidor de ficheros estáticos

## Qué es un servidor de estáticos

Un servidor de ficheros estáticos es un servidor que devuelve al navegador que los solicita **ficheros sin modificar, independientemente de quién los pida o desde dónde o cuándo se pidan**.

Por ejemplo si una usuaria entra en la página https://adalab.es/contacto.html el servidor devolverá el fichero **contacto.html**, independientemente de si la usuaria está logada o no, independientemente de si la usuaria está en Sevilla o Pekín, independientemente de si se accede desde un ordenador o un móvil...

Las páginas web que desarrollamos como programadoras front end las subimos a los servidores de estáticos para que las usuarias puedan entrar a ellas. Por ello, normalmente, en un servidor tenemos la programación de back end dentro de la carpeta `src/` y la programación de front end dentro de la carpeta `public/`. Por cierto un **GitHub Pages es un servidor de ficheros estáticos.**

La diferencia con un servidor de ficheros dinámicos, es que el servidor de dinámicos devolverá los **ficheros modificados al vuelo**, es decir, el servidor cogerá el fichero, lo modificará añadiendo información y después lo devolverá al navegador.

Por ejemplo, si yo entro en https://amazon.com/pedidos.html, el servidor cogerá el fichero **pedidos.html**, le añadirá mis pedidos en tiempo real y lo devolverá a mi navegador. Si entras tú el servidor hará lo mismo pero añadiendo tus pedidos. Si entra una usuaria que no esté logada, el servidor añadirá un mensaje del tipo "Por favor identifícate para ver tus pedidos".

Vamos a crear un servidor de ficheros estáticos usando [express.static()](http://expressjs.com/en/4x/api.html#express.static).

{% embed url="https://www.youtube.com/watch?v=uEr3B_F8eaE" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-static-server)

## Ficheros por defecto: index.html

Si desde el navegador se hace una petición **sin indicar el fichero**, el servidor de estáticos buscará el fichero `index.html`, **que es el fichero por defecto**, y si existe lo devolverá. En el vídeo hemos visto:

- Que cuando se entra en la página http://localhost:3000, no estamos indicando ningún fichero. Por ello el servidor de estáticos busca en `public/` si existe el fichero `index.html`, lo encuentra y lo devuelve.
- Que cuando se entra en la página http://localhost:3000/blog, tampoco estamos indicando ningún fichero. Por ello el servidor de estáticos busca en la carpeta `public/blog/` si existe el fichero `index.html`, lo encuentra y lo devuelve.
- Que cuando se entra en la página http://localhost:3000/contact.html **sí estamos indicando el fichero que queremos**. Por ello el servidor busca exactamente el fichero `contact.html` dentro de la carpeta `public/`. Lo encuentra y lo devuelve.

Esto es útil para poder hacer rutas más amigables, es decir, para la usuaria es más fácil entrar en http://localhost/blog/ que en http://localhost:3000/blog/index.html o en http://localhost:3000/blog.html.

En el fichero `public/index.html` hemos puesto el enlace `<a href="./blog/">Ir al blog</a>` para que cuando la usuaria acceda a la página del blog vea en la barra de direcciones del navegador la ruta amigable http://localhost:3000/blog/.

## Barra al final del las rutas `/`

A los servidores les da igual si en el navegador ponemos la dirección https://localhost:3000/blog o https://localhost:3000/blog/.

Los servidores interpretan en los dos casos que `blog` es una carpeta y queremos obtener el fichero por defecto `index.html` que está dentro de esta carpeta.

## Gestión de ficheros que no existen: error 404

El servidor de estáticos intenta gestionar la petición hecha desde el navegador. Si no encuentra el fichero buscado, Express JS intenta gestionarlo con los endpoints que estén declarados más abajo en el código.

Puesto que más abajo hemos puesto `app.get('*', (req, res) => { ... })` el servidor intenta gestionarlo con este endpoint. Este endpoint tiene la ruta `'*'`. El `'*'` significa exactamente **cualquier ruta**, por ello el servidor gestionará todas las rutas que no hayan sido gestionadas por un endpoint anterior.

Si la petición es gestionada por `app.get('*', (req, res) => { ... })` significa que el servidor de estáticos no ha encontrado el fichero, es decir, el fichero no existe. Por ello este endpoint devuelve el fichero `404-not-found.html` con un status 404.

> **Nota:** más info sobre el [status 404](https://developer.mozilla.org/es/docs/Web/HTTP/Status/404).

## Ejercicios

### 1. Añade una de tus páginas al servidor de estáticos

Ahora que ya sabemos montar un servidor de estáticos qué mejor forma de celebrarlo que creando con tus propias páginas:

1. Crea un servidor de estáticos. Si quieres utiliza el [ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-static-server).
1. Elije una de las páginas que hayas hecho durante el curso:
   - Si elijes una página hecha con el starter kit de Adalab tienes que copiar dentro de `public/` los ficheros generados en la carpeta `docs/` con `npm run docs`.
   - Si elijes una página hecha con React abre el proyecto, ejecuta `npm run build` y copia en `public/` el contenido de la carpeta `build/`.

### 2. Rutas amigables

Partiendo del [ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-static-server) cambia el código que necesites en `src/index.js` y `public/index.html` para que las usuarias puedan entrar la dirección http://localhost:3000/contact y así hacerles la vida más cómoda.

### 3. Dos servidores de estáticos en un solo servidor

Es poco común pero nos puede interesar tener dos servidores de estáticos en el mismo servidor. Por ejemplo uno para servir las páginas públicas y otro para servir las páginas del área de administración.

Partiendo del [ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-static-server):

1. Añade una carpeta hermana de `public/` que se llame `admin/`.
1. Añade dentro de `admin/` dos ficheros, un `index.html` y un `admin.html`.
1. Añade en `src/index.js` el siguente código después del servidor de estáticos que ya tenemos:
   ```js
   const staticServerPath = './admin';
   app.use(express.static(staticServerPath));
   ```
1. Arranca el servidor y
   1. Entra en http://localhost:3000. ¿Qué fichero te está devolviendo el servidor, el `public/index.html` o el `admin/index.html`? ¿Por qué?
   1. Entra en http://localhost:3000/admin.html y mira qué fichero está devolviendo.
