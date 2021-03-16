# Express: motores de plantillas

### ¿Qué es un servidor de ficheros dinámicos?

Un servidor de dinámicos es un servidor que devuelve al navegador **el mismo fichero pero personalizado, con pequeñas modificaciones, con diferentes datos** en función de qué usuaria lo está pidiendo o en función de a qué página se está accediendo.

Si entramos en https://www.filmaffinity.com/es/film999902.html y en https://www.filmaffinity.com/es/film942734.html vemos que la página es la misma pero lo único que cambian son los datos e imágenes que se muestran.

No tiene sentido que las maquetadoras de FilmAffinity maqueten una a una todas las películas del mundo. Lo que se hace es maquetar una sola película y convertirla en una plantilla. Cuando el servidor tiene que devolver una película, coge la plantilla, le mete sus datos y la devuelve. Esto es una tarea del motor de plantillas.

## ¿Qué es un motor de plantillas?

Un motor de plantillas, en inglés **template engines**, es la funcionalidad que:

1. Está **esperando** a que desde el navegador se le solicite un fichero. Esto lo hacemos con un endpoint. Cuando esto sucede, el endpoint:
   1. Coge una de plantilla.
   1. Coge los datos, generalmente desde base de datos.
      > **Nota:** En esta lección todavía no sabemos cómo trabajar con bases de datos, así que vamos a coger los datos de un JSON.
   1. Mete los datos en la plantilla. A este proceso se le llama **renderizado**.
   1. Y devuelve la plantilla personalizada al navegador.

## Motores de plantillas en Express JS

Express JS divide la funcionalidad de los motores de plantillas en **dos partes**:

1. Escuchar la petición desde el servidor y responderla:
   - Esta es una tarea de Express JS.
   - Escucha la petición con un endpoint del tipo `app.get('/ruta-del-endpoint, (res, req) => { ... })`.
   - Responde a la petición con `res.render(template, data);`.
1. Renderizado de la plantilla:
   - Este es el proceso que hay entre el escuhado de la petición y la respuesta.
   - Express JS **no** se encarga del renderizado.
   - Existen muchos motores de plantillas que funcionan sobre Express JS, que son los encargados del renderizado.
      - Estos motores de plantillas los crean grupos de desarrolladores y los suben a NPM para que el resto los usemos.
      - Nosotras debemos elegir uno, instalarlo en nuestro proyecto, configurarlo y usarlo.
      - En este módulo vamos a usar [EJS](https://ejs.co/).

## Motores de plantilla

### Ejemplo básico

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre motores de plantillas](https://www.youtube.com/watch?v=6Q2PjHavDYA).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-3-express-template-engine/template-basic)

En el vídeo hemos visto:

- Para instalar EJS: `npm install ejs`.
- Para configurar EJS: `app.set('view engine', 'ejs');`.
- Tenemos que crear nuestras plantillas en la raíz del proyecto, en la carpeta `views/`, porque así nos lo pide EJS.
- Podemos crear las carpetas que queramos dentro de `views/`.
- Es nuestra responsabilidad poner bien la ruta de las carpetas en `res.render('pages/film', filmData)`. No hace falta poner la extensión `.ejs`.
- Es nuestra responsabilidad poner bien la ruta de los partials dentro de las plantillas escribiendo `<%- include('../partials/header'); %>`.
- La sintaxis para añadir un partial es `<%- include('ruta-relativa-del-partial'); %>`. No hace falta poner la extensión `.ejs`.
- La sintaxis para añadir a la plantilla un dato es `<%= nombreDeMiVariableOPropiedad %>`.

### Ejemplo con condicionales

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre motores de plantillas con if](https://www.youtube.com/watch?v=mhu-Wa5oMjY).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-3-express-template-engine/template-if)

En el vídeo hemos visto:

- Que la sintaxis para añadir JS que no sea un partial o pintar en la plantilla es con `<% ... %>`. Por ejemplo:
   ```js
   <% if (country !== "") { %>
   <li>País: <%= country %></li>
   <% } %>
   ```
- Que a EJS no le gustan las comparaciones con `undefined`, por lo que `<% if (country !== undefined) { %>` no le gusta.
- Que es mejor asegurarnos de que existen todas las variables que va a utilizar EJS antes de llamar al renderizado. Por ello en `src/index.js` nos aseguramos de que la variable existe poniendo `filmData.country = filmData.country || '';`

### Ejemplo con bucles

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre motores de plantillas con forEach](https://www.youtube.com/watch?v=V5LoZpgi3Yo).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-3-express-template-engine/template-for)

En el vídeo hemos visto:

- Que la sintaxis para añadir JS que no sea un partial o pintar en la plantilla es con `<% ... %>`. Por ejemplo:
   ```js
   <% awards.forEach(function(award) { %>
   <li><%= award.year %>: <%= award.info %>.</li>
   <% }) %>
   ```
- Que dentro del bucle tenemos disponibles las variables que estamos creando en el bucle. Como en el bucle hemos creado la variable `award` en `<% awards.forEach(function(award) { %>`, dentro podemos usarla poniendo `<%= award.info %>`.
- Que es mejor pasarle los datos limpios a la plantilla para que esta se lo más sencilla posible. Por ejemplo, si queremos pintar el listado de premios, pero filtrándo por los premios Goya, tendríamos dos opciones:
   - Pasar a la plantilla el listado completo de premios y el criterio de filtrado, y que sea la plantilla la que primero filtre y luego itere para pintar o
   - Filtrar en `src/index.js` y pasarle el array de premios ya filtrados a la plantilla. Esto es mucho más limpio y legible. Es lo que preferimos.

## Múltiples plantillas

En un motor de plantillas puede haber muchas plantillas. En FilmAffinity tienen plantillas para las películas, directores, actores, géneros...

Para crear una nueva plantilla, por ejemplo de directoras, en nuestro servidor lo único que habría que hacer es:

1. Crear una plantilla en `views/pages/director.ejs`.
1. Crear un endpoint para escuchar una petición desde el navegador, por ejemplo: `app.get('/es/director/:directorName)` y dentro de este endpoint:
   1. Obtener los datos de la directora, por ejemplo: `const directorData = ...;`.
   1. Renderizar y responder con `res.render('director', directorData);`.

## Ejercicios

### 1. Crea una plantilla para directoras

Partiendo del [ejercicio básico del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-3-express-template-engine/template-basic):

1. Añade un fichero en `src/directors-data.json` con datos sobre dos directoras.
1. Añade a `src/index.js` un nuevo endpoint del tipo `app.get('/es/directora/:directorId', ...)` para gestionar peticiones del tipo http://localhost:3000/es/directora/iciar-bollain.
1. Obten los datos de la directora que nos llega por `req.params`.
1. Crea una plantilla en `views/pages/director.ejs` con el HTML que quieras.
1. Usa los datos de la directora para pintarlos en la plantilla.

### 2. Filtra por el año de los premios

Partiendo del [ejercicio de bucles del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-3-express-template-engine/template-for):

1. Añade un filtro en `src/index.js` para que solo se pinten los premios del año 2004.

Una vez lo hayas conseguido coge de las query params el año de filtrado, es decir:

- Si entras a la página http://localhost:3000/es/film942734.html?adwarsYear=2003 se deben pintar solo los premios de 2003.
- Si entras a la página http://localhost:3000/es/film942734.html?adwarsYear=2004 se deben pintar solo los premios de 2004.

### 3. Plantillas dentro de plantillas

Partiendo del [ejercicio básico del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-3-express-template-engine/template-basic):

1. Crea una nueva plantilla en `views/partials/search.ejs` que sea un formulario de búsqueda. Cualquier código HTML vale, ya que no vamos a crear la funcionalidad del formuario, como si pones un "hola mundo".
1. Añade este partial a los partials de la cabecera y el footer. Para ello elije bien la ruta relativa.

Si consigues que se vea el formulario en la página el ejercicio estará bien.

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.