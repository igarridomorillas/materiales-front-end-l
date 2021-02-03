# Express: query params

Ya sabemos que básicamente nuestro trabajo cuando programamos un servidor es enviar datos desde el navegador, recibirlos en el servidor y responder con otros datos.

En esta mini lección nos vamos a centrar en enviar datos desde el navegador al servidor. Lo que responda el servidor es un problema que abordaremos en otra lección.

Hay 4 formas de enviar datos desde el navegador al servidor:

- Query params
- Body params
- URL params
- Header params

Con este vídeo vamos a aprender cómo se envían datos a través de **query params**.

{% embed url="https://www.youtube.com/watch?v=D7brnaBc6hM" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-request-query-params)

## Características de los query params

- Desde el navegador:
   - Se añaden al final de la URL.
   - Empiezan con el símbolo `?`: http://localhost:3000/user?userName=maricarmen
   - Si queremos enviar varios query params los separamos con `&`: http://localhost:3000/user?userName=maricarmen&userEmail=mari@gmail.com
   - Se pueden utilizar con cualquier verbo (GET, POST, PUT, PATCH...) ya que todas las peticiones tienen URL.
- En el servidor:
   - Recibimos los datos en `req.query`.
   - Todos los datos enviados por query param se reciben en el servidor como **string**.

## URL compartible

Puesto que las query params van al final de la URL, podemos crear una URL con query params y compartirla con quien queramos. Por ejemplo si envías por Slack o Whatsapp la URL https://twitter.com/search?q=oidoEnAdalab la persona que la reciba puede acceder directamente a Twitter con la búsqueda ya hecha.

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

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.