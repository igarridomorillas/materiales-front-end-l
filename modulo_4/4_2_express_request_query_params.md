# Express: body params

En esta lección vamos a explicar cómo enviar datos a través de body params. Es exactamente lo mismo que enviar datos con query params, pero por otro sitio.

- Vídeo:
   - Ya sabemos cómo enviar datos al servidor a través de query params
   - Los body params son otra forma de enviar datos al servidor
   - Por qué hay varias formas
   - Porque ya sabéis que los lenguajes de programación nos dan muchas formas de hacer lo mismo y nosotras debemos saber cuál usar en cada momento
   - La diferencia principal es que los body params van en el cuerpo de la petición, no en la URL
   - Por ello las usuarias no pueden ver la información que estamos enviando
   - Por ejemplo es muy útil cuando hacemos un login y no queremos que en la URL aparezca el email o la contraseña que estamos enviando al servidor.
   - Se pueden hacer con cualquier verbo o método como por ejemplo POST, pero no se pueden hacer con GET
   - Por cierto esto solo aplica al API

{% embed url="https://www.youtube.com/watch?v=D7brnaBc6hM" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-request-query-params)


## Características de los body params

- Desde el navegador:
   - Se añaden en el cuerpo del fetch.
   - Se envían en formato JSON pero en string, es decir, con:
      ```js
         fetch('http://localhost:3000/user', {
           method: 'POST',
           body: JSON.stringify(bodyParams)
         })
      ```
   - Se pueden utilizar con cualquier verbo (POST, PUT, PATCH...) excepto GET.
- En el servidor:
   - Recibimos los datos en `req.body`.
   - Tenemos que acordarnos de poner `server.use(express.json());`. Si no, el objeto `req.body` estará vacío.

## Ejercicios

### 1. Filtrar usuarias por nombre

Vamos a partir del [ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-request-query-params) y a añadir una nueva funcionalidad. Ya sabemos que cuando pulsamos en el segundo botón del ejercicio, se llama al endpoint http://localhost:3000/users y el servidor nos devuelve el listado completo de usuarias.

Pues bien, queremos añadir un filtro a la web y al servidor para que el servidor nos devuelva las usuarias filtradas por nombre. Para ello:

1. Añade un campo de filtro a la web:
   1. Edita `public/index.html` para añadir un input de texto en el segundo rectángulo.
   1. Edita `public/js/main.js` para que cuando ejecutamos `fetch('http://localhost:3000/users')` se envíe por query params un nuevo dato con el nombre `filterByName`.
   1. Comprueba desde devtools > network qué la llamada que estás haciendo tiene el formato correcto, es decir la URL concatendada con el query param. Si este formato es correcto ya puedes empezar a editar el servidor.
1. Añade el filtro al servidor:
   1. Edita `src/index.js`.
   1. En el endpoint `server.get('/users', (req, res) => {...})` debes recoger el query param `filterByName` y guardarlo en una constante.
   1. En el ejercicio del vídeo estamos devolviendo todo el array de usuarias, que lo hacemos con el código:
      ```js
      res.json({
        result: users
      });
      ```
      Cambia este código para que no devuelva todo el array sino un array con solo aquellas usuarias cuyo nombre contenga el texto escrito en el input de filtrado.

Recuerda que para que el array `users` tenga usuarias hay que añadir usuarias a través del primer formulario de la web.

### 2. Filrar usuarias por nombre e email

Partiendo del ejercicio anterior:

1. Añade un segundo campo de texto a la web para filtrar por email y envíalo también por query params al servidor.
1. Añade un segundo filtro en el servidor en la función `server.get('/users', (req, res) => {...})` para que el servidor solo devuelva aquellas usuarias cuyo nombre contenga el texto del filtro de nombre y cuyo email contenga el texto del filtro de email.
