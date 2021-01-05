# Express básico

Ya sabemos crear aplicaciones con Node JS pero todavía no sabemos cómo crear un servidor. Podemos ponernos a programar un servidor pero es algo bastante complejo y seguramente tendríamos que escribir varios miles de líneas de código. Uff qué pereza.

Por suerte ya hay alguien que ha creado esa programación, son los creadores de [Express JS](https://expressjs.com/). Así que vamos a aprender a utilizar el módulo de [NPM de Express JS](https://www.npmjs.com/package/express).

## ¿Qué es Express JS?

Express JS es un módulo de NPM que nos facilita la vida a la hora de programar un servidor, nos ayuda a escuchar las peticiones que se hacen desde el navegador al servidor. También nos ayuda a obtener los datos de dichas peticiones, procesarlos y crear una respuesta que le devolvemos al navegador.

- Vídeo
   - Ya sabemos trabajar con Node para hacer aplicaciones que se ejecutan en una terminal
   - La idea de este vídeo es que tengáis una idea general de cómo funciona un servidor con Express
   - Cada una de las partes explicadas en este vídeo las explicaremos en detalle en los siguientes vídeos
   - Ahora vamos a utilizar Node para crear un servidor (ver diagrama)
      - Ya sabéis un servidor es un ordenador que está conectado a Internet todo el día
      - Y está esperando peticiones por parte de un navegador
      - Cuando recibe una petición, la recibe, la procesa y la responde
      - Cuando el navegador recibe la respuesta del servidor puede pintar la página
   - Para crear un servidor vamos a utilizar Express JS
      - Express JS es un módulo de NPM (enseñar la página)
      - Es un módulo que facilita que el servidor esté escuchando peticiones desde el navegador y las responda
      - Nosotras podemos programar un servidor sin Express, pero sería mucho trabajo.
      - Express nos ayuda a escuchar peticiones y responderlas
      - Nuestro trabajo es programar qué peticiones se escucha, cómo se procesan y con qué información se responden
   - Veamos un ejemplo (ver código)
      - Yo ya tengo un servidor programado
      - Aquí tengo un servidor que está compuesto de:
         - `package.json` porque necesitamos un módulo de NPM (enseñar express dentro del `package.json`)
      - La carpeta `src` tiene la programación de mi servidor, lo explicamos
         - Importamos Express para poder crear el servidor
         - Al ejecutar la función `express()`, está crea un servidor con un montón de funcionalidad y luego la retorna para que nosotras lo guardemos en esta constante y lo podamos utilizar más adelante.
         - `express.json()` es una cosa avanzada que explicaremos en otro momento
         - Arrancamos el servidor de express en el puerto 3000 (ejecutar npm start)
         - Al arrancar un proyecto que usa Express, Node no se ejecuta y termina, sino que se queda arrancado esperando a que desde el navegador hagamos peticiones al servidor.
         - Un inciso. Qué es un puerto
            - Ponemos una comparación: para poder enviar un paquete desde Pekín a Zaragoza por barco, el paquete tiene que viajar por el mundo y tiene que pasar por el puerto de Barcelona.
            - Es decir el puerto es la puerta de entrada al país, no el destino.
            - Pues bien un ordenador es como si fuera un país.
            - Es decir, para que un ordenador pueda tener dentro muchos servidores, a cada servidor le asignamos un puerto, que es por donde se va a comunicar con otros ordenadores.
            - Por eso si desde la web llamamos a http://localhost:3000/images/logo.png, significa que estamos pidiendo una imagen al servidor local a través del puerto 3000
            - Mientras estamos programando ponemos el puerto que queramos, por ejemplo el 3000, el 3001, el 5500...
            - Cuando subamos nuestro código a un servidor de verdad cambiaremos ese 3000 por otro puerto. Esto nos lo dirá nuestra compañera de devops que se dedica a configurar los servidores.
            - Dos cosas más:
               - El 3000 es el 3000 de la página. Si lo cambiamos aquí por otro número lo tenemos que cambiar también en la web.
               - Todas las peticiones que se hagan por el puerto 3000 las va a gestionar este servidor.
      - Servidor de ficheros estáticos
         - Aquí le estoy diciendo que cuando el navegador solicite un fichero, express debe buscar el fichero en la carpeta `public` y enviarlo al navegador.
         - Enseñar en la página el HTML, CSS, JS y logo en devtools y carpeta public
         - Cuando programamos una web como programadoras front metemos aquí los ficheros
      - API
         - Son las peticiones que hacemos desde el front con `fetch` (enseñar main.js)
         - Cuando hacemos una petición a `localhost:3000/users` se ejecuta esta función porque aquí pone users
            - A esto se le llama ruta
            - La función recibe `req` que es la request, la petición, con información sobre la petición
            - La función también recibe `res` que es la response, que lo usamos para poder responder
            - Con `res.json` le decimos que responda a la petición devolviendo estos datos.
            - Enseñar ejercicio
         - Cuando hacemos una petición a localhost:3000/new-user se ejecuta esta función.
            - Se diferencia de la anterior en que esta es de tipo POST
            - Gracias a que es de tipo POST podemos enviar datos (enseñar devtools)
            - Express nos mete estos datos en `req.body.userName`.
            - Lo explicaremos en detalle más adelante.
            - Lo importante es que la web puede enviar al servidor datos y el servidor puede obtenerlos y hacer con ellos lo que quiera.
            - Esta función ejecuta `res.json` con datos para responder
      - Ya hemos terminado de explicar este ejercicio, ahora unas conclusiones
      - En un API cada una de estas rutas es un endpoint, hablaremos mucho de ellos en el futuro
      - Cuando programemos un servidor vamos a crear un servidor de estáticos y meter ahí los ficheros de la web, es decir, del front
      - Y también vamos a crear muchos endpoints como estos para:
         - Que las usuarias hagan login
         - Que se registren
         - Que hagan un pedido en una tienda online
         - Que añadan un nuevo mensaje en un chat
         - Cada uno de estos endpoint va a ser de tipo GET, POST... y cada uno van a tener una ruta
      - Nuestro trabajo es crear estos endpoints
         - Meter código dentro para crear la respuesta
         - Aquí comprobaremos que los datos que nos envían desde la web son correctos
         - Aquí leeremos y escribiremos datos en las bases de datos
         - Y muchas cosas más
      - En próximos vídeos vamos a ver cada una de estas partes en detalle

> **Nota:** cuando programamos una API a los métodos GET, POST... que utilizamos también les llamamos **verbos**. Y a las rutas `/users`, `/new-user`... les llamamos endpoints.

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-basic)

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

Qué pasa cuando hacemos una petición al servidor y este no responde:

- Vídeo
   - Explicar que si el servidor no responde es que se nos ha olvidado responder

## Ejercicios

### 1. Crea un servidor desde cero

1. Sigue los pasos de que hemos visto antes en el apartado: **Pasos para crear un servidor con Express JS**
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

### 2. Cambio de las rutas y verbos

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
