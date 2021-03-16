# Express básico

Ya sabemos crear aplicaciones con Node JS pero todavía no sabemos cómo crear un servidor. Podemos ponernos a programar un servidor pero es algo bastante complejo y seguramente tendríamos que escribir varios miles de líneas de código. Uff qué pereza.

Por suerte ya hay alguien que ha creado esa programación, son los creadores de [Express JS](https://expressjs.com/). Así que vamos a aprender a utilizar el módulo de [NPM de Express JS](https://www.npmjs.com/package/express).

## ¿Qué es Express JS?

Express JS es un módulo de NPM que nos facilita la vida a la hora de programar un servidor, nos ayuda a escuchar las peticiones que se hacen desde el navegador al servidor. También nos ayuda a obtener los datos de dichas peticiones, procesarlos y crear una respuesta que le devolvemos al navegador.

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre intro a Express JS](https://www.youtube.com/watch?v=4CRIGOANDMw).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-basic)

> **Nota:** cuando programamos una API a los métodos GET, POST... que utilizamos también les llamamos **verbos**. Y a las rutas `/users`, `/new-user`... les llamamos endpoints.

## Pasos para crear un servidor con Express JS

1. Debemos crear un proyecto o repo.
1. Debemos crear un `package.json` usando `npm init` o creándolo a mano.
1. Debemos instalar el módulo `express` ejecutando en la terminal `npm install express`.
   - Para saber que lo hemos hecho bien, dentro del fichero `package.json` debe aparecer `express` dentro de `dependencies`.
1. Debemos instalar el módulo `cors` ejecutando en la terminal `npm install cors`.
   - Para saber que lo hemos hecho bien, dentro del fichero `package.json` debe aparecer `cors` dentro de `dependencies`.
1. Debemos crear un fichero `index.js` dentro de la carpeta `src` donde programaremos el servidor.
1. Para arrancar debemos hacer una de las siguientes cosas:
   - Ejecutar el comando `node src/index.js` o
   - Añadir al `package.json` el script:
     ```js
     "scripts": {
       "start": "node src/index.js"
     }
     ```
     y ejecutar el comando `npm start` para que en consola se ejecute `node src/index.js`.

## Errores comunes

¿Qué pasa cuando hacemos una petición al servidor y este no responde?

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre errores comunes](https://www.youtube.com/watch?v=H4qwAfzrsL4).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-basic)

## Ejercicios

### 1. Crea un servidor desde cero

1. Sigue los pasos que hemos visto antes en el apartado: **Pasos para crear un servidor con Express JS**
1. Añade al fichero `index.js` las líneas de código:
   ```js
   const express = require('express');
   const cors = require('cors');

   const server = express();

   server.use(cors());
   server.use(express.json());

   const serverPort = 3000;
   server.listen(serverPort, () => {
     console.log(`Server listening at http://localhost:${serverPort}`);
   });

   server.get('/users', (req, res) => {
     const response = {
       users: [{ name: 'Sofía' }, { name: 'María' }]
     };
     res.json(response);
   });
   ```
1. Entra en `http://localhost:3000/users` desde Chrome
1. Verás que el navegador muestra el JSON con la respuesta del servidor `{ users: [...] }`.

> **Nota:** recuerda que cada vez que hagas un cambio en los ficheros de tu servidor, debes parar el servidor con `Ctrl+C` y volverlo a arrancar.

### 2. Cambio de endpoints y verbos

1. Descarga el [ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-basic).
1. Haz `npm install` para que NPM instale Express JS dentro de `node_modules/`.
1. Haz `npm start` para arrancar (o levantar) el servidor.
1. En el fichero `src/index.js`:
   1. Cambia la ruta `app.post('/new-user', (req, res) => {` por `app.post('/users/add', (req, res) => {`
      - ¿Qué debes cambiar en `public/main.js` para que la web para sigua funcionando?
   1. Cambia la ruta `app.get('/users', (req, res) => {` por `app.post('/users', (req, res) => {`
      - ¿Qué debes cambiar en `public/main.js` para que la web para sigua funcionando?
   1. Cambia el puerto `const serverPort = 3000;` por `const serverPort = 3500;`
      - ¿Qué debes cambiar en `public/main.js` para que la web para sigua funcionando?

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.