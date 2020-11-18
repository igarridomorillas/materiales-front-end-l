# Peticiones al servidor

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-6)
- [EJERCICIO 8 BONUS](#ejercicio-7-bonus)

<!-- /TOC -->

## Introducción

En esta sesión vamos a aprender a utilizar AJAX que es el puente entre el cliente (navegador) y el servidor, entre el frontend y el backend de nuestra aplicación. Las peticiones AJAX nos permiten acceder y manipular datos en el servidor, pero iniciando el proceso en el frontend.

AJAX viene de Asynchronous JavaScript And XML porque cuando se creó servía para hacer peticiones al servidor desde JS y normalmente el formato de datos que nos devolvía era XML (una forma de escribir los datos para poder enviarlos). Pero actualmente no es así y AJAX ahora utiliza otros tipos de datos, desde texto hasta JSON que veremos más adelante. Pero el hecho de que sea *asíncrono* sí es importante. Aunque sea una palabra que asusta, asíncrono simplemente significa trabajar con eventos (como hemos visto en las sesiones anteriores), es decir, que cuando sucede un evento se ejecuta una función. Se llama asíncrono porque nosotros no ejecutamos el código de forma síncrona (una instrucción detrás de otra) sino que *el código se ejecuta cuando sucede un evento*.

El uso de AJAX, por tanto, nos permite acceder a información en un servidor que normalmente se accede mediante un API. Veremos un API como una URL (dirección de Internet) donde podemos consultar o guardar datos de un servicio. Veremos más detalles sobre APIs en la próxima sesión.


## ¿En qué casos se utiliza?

Algunos ejemplos de uso de AJAX que podemos encontrar en una webApp (aplicación web):

- Cuando realizamos una búsqueda de pisos en Airbnb, hacemos una petición AJAX al servidor, y cuando nos devuelve los datos de los pisos lo pintamos en el HTML
- Cuando en nuestra app de tareas marcamos una tarea como terminada, se envía una petición al servidor para que almacene en base de datos que esa tarea ha sido completada; así, al abrir la app en nuestro móvil aparecerá como completada
- En GMail, el listado de nuestros correos se obtiene de una petición al servidor; cuando marcamos un correo como leído se envía la info al servidor; o cuando enviamos un correo, éste se envía a un servidor para que lo lleve a su destinatario

En esta sesión aprenderemos también cómo trabajar en casos de asincronía compleja, como por ejemplo:
- realizar una acción cuando se hayan completado varios procesos asíncronos que dependen uno del otro (*peticiones encadenadas*)
- realizar una acción cuando se hayan completado varios procesos asíncronos que se ejecutan en paralelo (*peticiones en paralelo*)

Veamos algunos casos de ejemplo donde es necesario ejecutar *peticiones encadenadas*:
- en una web sobre perros, hago una primera petición al servidor sobre las razas disponibles y después hago una segunda petición para pedir información de perros de una raza concreta
- en una web con área privada, cuando la usuaria introduce su email y su contraseña, hago una petición al servidor para *autenticarla*, el servidor me devuelve un `string` que identifica a la usuaria, con él hago una petición para pedir sus datos privados y mostrarlos en el área privada.

Veamos algunos ejemplos en la web de *peticiones que se ejecutan en paralelo*:
- cuando buscamos en una app de transporte cuál es la ruta más rápida entre dos puntos y necesitamos obtener información de distintas APIs web (taxis, EMT, Uber, Cabify...) y esperar a recibir la respuesta de todas para reflejar cual será la opción más rápida entre ellas


## Fetch

A día de hoy la manera estándar de acceder a datos en el servidor desde nuestro frontend es `fetch`, una nueva API del navegador que funciona gracias a una forma moderna de manejar la asincronía de JavaScript llamada *Promesas*. Hasta ahora el estándar había sido usar el objeto `XMLHttpRequest` que trabaja con *callbacks* y que veremos al final de esta sesión como bonus.

[Tutorial de MDN sobre el uso de fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch).

### Promesas

Trabajar con *callbacks* para gestionar la asincronía hacía el código bastante complejo y poco intuitivo cuando necesitábamos encadenarlos.

Las promesas nos ofrecen una alternativa a los *callbacks* para intentar escribir código más claro y limpio. Es decir, podemos hacer las mismas cosas que con *callbacks* pero de una forma más elegante.

### Usando fetch

Vamos a realizar un ejemplo de petición usando `fetch` un API para obtener un *emoji* (piedra, papel, tijera, lagarto o spok) aleatorio en [https://rand.fun/](https://rand.fun/). Vamos a ver cómo queda un ejemplo de petición a este API con `fetch`:

```js
fetch('https://api.rand.fun/games/rockpaperscissorslizardspock')
  .then(function(response) {
    return response.json();
  })
  .then(function(data) {
    document.body.innerHTML = data.result;
  });
```

Lo mismo pero con `arrow functions`:

```js
fetch('https://api.rand.fun/games/rockpaperscissorslizardspock')
  .then(response => response.json())
  .then(data => document.body.innerHTML = data.result);
```


En primer lugar, vemos que a la función `fetch` solo le pasamos un parámetro: la URL a donde queremos hacer la petición, así de sencillo. La URL la hemos construido como se indica [en la documentación](https://rand.fun/), es decir, a la URL base 'https://api.rand.fun' le hemos añadido '/games/rockpaperscissorslizardspock' para pedir un *emoji* aleatorio.

Al ejecutar `fetch(URL)`, este método devuelve una promesa, es decir, algo sobre lo que podemos hacer `.then()`. Una promesa se llama así porque mientras se ejecuta el fetch (se hace la petición al servidor, responde y nos llega la respuesta) podemos trabajar con la respuesta en otra variable `response` donde 'nos prometen' que estará la respuesta del servidor cuando llegue. Es decir, que seguimos trabajando de forma asíncrona (en respuesta a eventos) pero las promesas nos ocultan esa complejidad.

Entonces, sobre una promesa podemos hacer un `.then()` pero ¿para qué? Para poder indicar qué hacer cuando se complete esa promesa. Al método `then()` le tenemos que pasar una función (en este caso es anónima, pero puede ser una normal con nombre) que toma como parámetro el resultado de la promesa cuando esté resuelta. En este caso el parámetro `response` representa a la respuesta del servidor, y sobre él ejecutamos el método `.json()` que devuelve otra promesa. Esto es porque el método `json` trabaja de forma asíncrona y obtiene la respuesta del servidor en formato texto. Como trabaja de forma asíncrona necesitamos otro `then()` para recoger la respuesta. A este segundo `then()` le pasamos como parámetro otra función que toma como parámetro `data` que contiene el objeto que devuelve el servidor. En esta última función lo único que hacemos es, usando `innerHTML` sobre el `body`, añadir un *emoji* a la página.

> NOTA: es **MUY IMPORTANTE** no olvidar hacer un `return` al final de la función que pasamos a `then` para encadenar con el siguiente `then`. En el último no hace falta porque ya no hay más `then` a quien tener que pasarlo.

Prueba este ejercicio con este código:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Ejercicio</title>
  </head>
  <body>
    <button class="js-emoji">Emoji!!!</button>
    <p class="js-result"></p>
    <script src="./js/main.js"></script>
  </body>
</html>
```

```js
function getEmoji() {
  fetch("https://api.rand.fun/games/rockpaperscissorslizardspock")
    .then(response => response.json())
    .then(data => {
      document.querySelector('.js-result').innerHTML = data.result
    });
}
document.querySelector('.js-emoji').addEventListener("click", getEmoji);
```

> **Nota importante:** Cuando los hackers quieren boicotear una web una de las cosas que hacen es lanzar desde muchos ordenadores miles de peticiones AJAX al servidor de dicha web. De esta forma el servidor se satura y no puede funcionar correctamente. Esto se llama [Ataque por denegación de servicio](https://es.wikipedia.org/wiki/Ataque_de_denegaci%C3%B3n_de_servicio). La forma que tienen los servidores de defenderse de estos ataques es rechazando las peticiones que vengan de una IP en concreto, cuando superan un límite. Por ejemplo si desde una misma IP hacemos más de 100 peticiones por minuto, el servidor rechaza desde la petición 101 en adelante. Cuando hagamos los ejercicios en clase vamos a ser 20 alumnas haciendo cada una un montón de peticiones a un servidor en concreto y este nos denegará el servicio porque creerá que lo estamos atacando. Para minimizar el número de peticiones que hagamos, hoy no podemos trabajar desde Codepen. Recordemos que Codepen actualiza el resultado cada vez que escribimos una letra.

#### EJERCICIO 1

**Numero aleatorio**

Vamos a jugar un poco con el código del ejemplo anterior. Mirando la [documentación de 'rand.fun'](https://rand.fun/), vamos a pedir un número entero (`integer`).

Podemos jugar añadiendo parámetros a la URL del tipo `clave=valor`, siempre después de character `?` y separados por `&`, por ejemplo si quisieras pedir un `string` con determinada longitud, la url quedaría así `https://api.rand.fun/text/password?length=20`

\_\_\_\_\_\_\_\_\_\_

## El formato JSON

Es formato muy habitual para el intercambio de información en la web (pronunciado en inglés como *Jason*). Son las siglas de JavaScript Object Notation, es decir, que es muy similar a como se definen los objetos literales en JavaScript... **¡¡¡algo que ya sabemos!!!** Aunque hay pequeñas diferencias:

- Las claves siempre van entre comillas `{"userName": "Paco"}`
- Los valores permitidos son: `string`, `number`, `boolean`, `array`, `null` y `json object`. Esto quiere decir que un `JSON` no podemos almacenar funciones por lo tanto nunca tendrá métodos.

Esto es un ejemplo de JSON sencillo que devuelve el [Dog CEO API](https://dog.ceo/dog-api/):

```js
{
"status": "success",
"message": "https://dog.ceo/api/img/terrier-australian/n02096294_4492.jpg"
}
```

Como vemos, es simplemente un objeto JavaScript que tiene los datos que devuelve el servidor. En este caso, nos da una imagen aleatoria de un perro en la propiedad `message`. Vamos a ver el ejemplo completo de cómo hacer la petición con `fetch`:

```js
fetch('https://dog.ceo/api/breeds/image/random')
  .then(response => response.json())
  .then(data => {
    const img = document.querySelector('img');
    img.src = data.message;
    img.alt = 'Un perro';
  });
```

Vamos a ver los cambios respecto al ejemplo anterior de los emojis.

En primer lugar, la URL en el `fetch` cambia para usar la URL de Dog API que nos da una imagen de perro aleatoria.

El segundo cambio está en la función del segundo `then()`, en el ejemplo de *emojis* el objeto `data` contenía una clave `result` con un `emoji`, y en este caso `data` tiene una clave `message` con la url de la imagen de un perro. Esto ocurre porque el **_schema_ de la respuesta** (cómo es el objeto JSON que nos devuelve el servidor, cómo se llaman sus claves, y qué contienen) lo ha definido y desarrollado una programadora como nosotras, así que debemos asumir que diferentes APIs tendrán diferentes *schemas*. De esta manera, leer la documentación y `loguear` el `JSON` que nos llega del servidor antes de operar con el siempre es una buena idea.

Podéis jugar con este código:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Ejercicio</title>
  </head>
  <body>
    <button class="js-dog">Perretes!!!</button>
    <img />
    <script src="./js/main.js"></script>
  </body>
</html>
```

```js
function getDogImage() {
  fetch("https://dog.ceo/api/breeds/image/random")
    .then(response => response.json())
    .then(data => {
      const img = document.querySelector("img");
      img.src = data.message;
      img.alt = "Un perro";
    });
}
const btn = document.querySelector(".js-dog");
btn.addEventListener("click", getDogImage);
```

> **Nota**: Cuando recogemos un elemento de HTML podemos leer y modificar algunos de sus atributos directamente, como `src` y `alt` de la etiqueta `img` ¡Genial!

#### EJERCICIO 2

**Chihuahas, chihuahas por todas partes**

Sigamos jugando un poco con el [Dog API](https://dog.ceo/dog-api/):

a) Vamos a modificar el ejemplo anterior para que las fotos de nuestra página salgan sólo perros de la raza *Chihuahua*.

b) Vamos a encapsular toda la lógica para crear una petición en una función. Añadimos un botón a la página con el título 'Enséñame otro Chihuahua' de forma que al pulsarlo se haga otra petición al servidor de una imagen aleatoria y aparezca una nueva imagen de Chihuaua.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

Ahora vamos a explorar un nuevo API: [el API de usuarios de GitHub](https://developer.github.com/v3/users/). La URL de este API es `https://api.github.com/users/{username}`, donde `{username}` es el nombre del usuario en GitHub. Por ejemplo, aquí tenéis la URL para obtener información del usuario de Isra `https://api.github.com/users/gootyfer`. Si ponéis esta URL en una nueva pestaña del navegador podréis observar qué datos nos devuelve el API.

Vamos a crear una página en la que haya un input de texto y un botón de buscar. El usuario escribirá en el input un nombre de usuario de GitHub. Prepararemos una función que se ejecute cuando se pulse el botón buscar y que contenga una petición al API para obtener información de ese usuario y así mostrarla en nuestra página:
- nombre
- número de repositorios
- avatar (imagen)

![Screenshot buscador en GitHub](assets/images/2-9/buscador-github.png)

\_\_\_\_\_\_\_\_\_\_

## Peticiones encadenadas

Comenzamos con este ejemplo en el que pedimos al API de Dog CEO el listado de razas de perro usando promesas.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Ejercicio</title>
  </head>
  <body>
    <button class="js-btn">Breeds</button>
    <ul></ul>
  </body>
</html>
```

```js
function getBreeds () {
  fetch('https://dog.ceo/api/breeds/list')
    .then(response => response.json())
    .then(data => {
      console.log('Breeds data response: ', data);

      const ul = document.querySelector('ul');
      const breeds = data.message;
      let ulContent = '';

      for (const breed of breeds) {
        const breedContent = `<li>${breed}</li>`;
        ulContent += breedContent;
      }
      ul.innerHTML = ulContent;
    });
}
const btn = document.querySelector('.js-btn');
btn.addEventListener('click', getBreeds);
```

Ahora vamos a partir del ejemplo anterior para pedir al servidor una foto de una raza concreta de perro. Para ello, por tanto, necesitamos conocer primero el listado de razas (como en el ejemplo anterior) y luego, con esta información, pedir al servidor una foto de una raza concreta. Por tanto son dos callbacks encadenados, es decir, que la segunda petición depende de los datos que llegan en la primera. Vamos a ver un ejemplo:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Ejercicio</title>
  </head>
  <body>
    <button class="js-btn">Breeds</button>
    <img src="" alt="">
  </body>
</html>
```

```js
function getBreedsImage () {
  fetch('https://dog.ceo/api/breeds/list')
    .then(breedsResponse => breedsResponse.json())
    .then(breedsData => {
      const breeds = breedsData.message;
      return fetch('https://dog.ceo/api/breed/' + breeds[0] + '/images/random');
    })
    .then(imageResponse => imageResponse.json())
    .then(imageData => {
      const img = document.querySelector('img');
      img.src = imageData.message;
      img.alt = 'Un perro';
    });
}
const btn = document.querySelector('.js-btn');
btn.addEventListener('click', getBreedsImage);
```

Una de las características principales de las promesas es que nos facilitan encadenar peticiones como en este caso, y el código resultante es muy sencillo. En el código hemos encadenado hasta 4 promesas:
 1. petición al servidor de las razas
 2. convertir a JSON la respuesta
 3. segunda petición de la foto de una raza
 4. convertir la segunda respuesta a JSON

Como hemos indicado antes, es importante que al final de los `then()` devolvamos una promesa para pasar los datos al siguiente `then()`. Así que en el segundo `then()` tenemos que devolver la promesa de `fetch`.

#### EJERCICIO 4

**Listado de repos de una organización en Github**

Vamos a seguir explorando el API de GitHub explorando la parte del [API para acceder a la info sobre organizaciones](https://developer.github.com/v3/orgs/). La URL de este API es `https://api.github.com/orgs/{orgname}`, donde `{orgname}` es el nombre de la organización en GitHub. Por ejemplo, aquí tenéis la URL para obtener información de la organización Adalab `https://api.github.com/orgs/Adalab`. Si ponéis esta URL en una nueva pestaña del navegador podréis observar qué datos nos devuelve el API.

El objetivo de este ejercicio es mostrar en una web el listado completo de los repositorios de una organización que hay creados en GitHub. Por ejemplo, para Adalab, el resultado final debería ser similar a este:

![Resultado del ejercicio](assets/images/2-9/resultado-ejercicio-1-listado-de-repos.png)

Para ello vamos a hacer lo siguiente:

1. Preparar un input  con un botón para que la usuaria introduzca la organización.
2. Cuando la usuaria pulse el botón buscar acceder a la información de la organización como primera petición al servidor.
3. Recoger la información de la URL donde consultar la información de los repositorios de la organización en la respuesta del servidor (en la propiedad `repos_url`) y hacer una nueva petición a esa URL.
4. En el último `then` pintar en nuestra web el nombre de todos los repositorios de la organización en una lista (propiedad `name` de cada objeto repositorio).

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 5

Vamos a entrar en la URL `https://api.github.com/orgs/Adalab` a través de nuestro navegador para obtener la respuesta del API de GitHub. A continuación vamos a analizar de qué tipo es cada una de las propiedades que nos está devolviendo. Por ejemplo, de qué tipo son `login`, `id`, `node_id`, `is_verified`...

Y si entramos en `https://dog.ceo/api/breeds/list` ¿de qué tipo es la propiedad `message`?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

**La raza del perro**

Vamos a realizar un ejercicio con la API de 'https://dog.ceo/dog-api/' y la api de 'https://rand.fun/'. Tenemos que pedir un listado de razas de perros, y con un número aleatorio elegir una raza del listado:
- pintar un mensaje que muestre la raza elegida al azar.
- pedir una imagen aleatoria de un perro de esa raza y pintarla.

Si has llegado hasta aquí te proponemos otro reto, intenta que la última función sea la única que se encargue de interactuar con `html`, y sea esta la que pinte la raza y la imagen.
¡Al turrón!

\_\_\_\_\_\_\_\_\_\_

## Peticiones en paralelo

Ya hemos visto la utilidad de tener peticiones encadenadas, en las que una petición depende de las anteriores. Ahora vamos a ver por qué usar peticiones en paralelo, es decir, peticiones que se ejecutan a la vez para poder realizar alguna acción cuando todas se han completado.

Para trabajar con varias promesas en paralelo usamos el método `Promise.all` que toma como parámetro un array de promesas y devuelve otra promesa que se resuelve cuando todas las del array se han resuelto. Por tanto, sobre el resultado podremos hacer un `then()` que recibe como parámetro un array con todos los resultados de las promesas anteriores, es decir, donde tendremos todos los `JSON` de la respuesta del servidor. Veamos el ejemplo:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Ejercicio</title>
  </head>
  <body>
    <button class="js-btn">Breeds</button>
    <img class="dog1" src="" alt="Dog">
    <img class="dog2" src="" alt="Dog">
    <script src="./js/main.js"></script>
  </body>
</html>
```

```js
const createPromise = () =>
  fetch('https://dog.ceo/api/breeds/image/random')
    .then(response => response.json());

function getBreedImages () {
  const promises = [createPromise(), createPromise()];
  Promise.all(promises)
    .then(responses => {
      for (let i = 0; i < responses.length; i++) {
        const img = document.querySelector('.dog' + (i + 1));
        img.src = responses[i].message;
      }
    });
}
const btn = document.querySelector('.js-btn');
btn.addEventListener('click', getBreedImages);
```

Hemos creado una función `createPromise` que crea las promesas de las peticiones al servidor con `fetch` y parsea a JSON en el `then()`.
Luego creamos el array de promesas ejecutando 2 veces la función anterior.
Después ejecutamos `Promise.all` pasándole como argumento el array de promesas, cuando todas las peticiones al servidor hayan terminado, se ejecutará la función del `then()` a la que le llegan todos los resultados mediante el parámetro  `responses`.
Finalmente recorremos el array que se encuentra en responses para ir pintando las imágenes en los `img` del HTML.

#### EJERCICIO 7

**Pintando varias imágenes a la vez**

Partiendo el ejemplo anterior, vamos a modificarlo para que en lugar de pedir 2 imágenes en paralelo pida 10, y el resultado sólo se pinte en la pantalla cuando las 10 imágenes hayan llegado del servidor. Ahora sí que se nota el efecto de que se pintan todas a la vez, ¿verdad? Vamos a probar también con 25 imágenes, para ver bien este efecto.

\_\_\_\_\_\_\_\_\_\_

## BONUS

### Gestión de errores con promesas

Otra de las ventajas de las promesas es que facilitan la gestión de errores. Este es un tema que no hemos visto hasta ahora con JavaScript, pero vamos a ver cómo se hace con promesas porque facilitan mucho la vida.

```js
fetch('https://dog.ceo/api/breeds/list')
  .then(response => response.json())
  .then(data => {
    console.log('Breeds data response: ', data);

    const ul = document.querySelector('ul');
    const breeds = data.message;
    let ulContent = '';

    for (const breed of breeds) {
      const breedContent = `<li>${breed}</li>`;
      ulContent += breedContent;
    }
    ul.innerHTML = ulContent;
  })
  .catch(error => console.log(`Ha sucedido un error: ${error}`));

```

Cuando usamos promesas podemos encadenar el final de los `then()` un `catch` que también recibe una función, que tiene como parámetro información del error que puede haber sucedido en cualquiera de los `then()` anteriores. En el ejemplo anterior, este error puede deberse, por ejemplo a que la usuaria haya perdido la conexión o que el servidor nos devuelva un JSON con una estructura que no esperábamos y lo parseemos mal.

#### EJERCICIO 8 BONUS

**Cazando errores 1**

Partiendo del ejercicio 1 vamos a modificarlo para en lugar de parsear la respuesta a `JSON` (`response.json()`) lo hagamos a `html` (`response.html()`). Ahora si abrimos la consola del navegador nos encontraremos un mensaje de error, léelo para familiarizarte con él.

Este error nos indica que ha sucedido un error en una de las promesas y que no lo hemos cazado, también nos da algo de información sobre el error. En este caso hemos intentado parsear a `html` la respuesta de la api de `rand.fun` que solo es parseable a `JSON`.

Vamos a ponerle un `catch` a nuestra promesa y a `loguear` el error.

\_\_\_\_\_\_\_\_\_\_

Puede ser que tras este ejercicio no notes mucha diferencia entre el error que mostraba el navegador y nuestro `console.log`. Pero tener nuestros errores controlados es muy importante, aunque a día de hoy no vayamos a hacer nada más que `loguear` el error, ya tenemos el código preparado para en un futuro hacer otras cosas como:
- Mostrar feedback a la usuaria sobre lo que ha ocurrido.
- Intentar realizar la petición de nuevo pasados unos segundos en caso de errores por falta de conexión.
- Mandar información sobre el error a un servicio que lo almacene para después investigarlo.

> **Nota**: los mensajes de error en la consola del navegador no solo nos indican errores en las promesas, aparecen cada vez que hacemos algo que no debemos, aunque a estas alturas ya debes haberte dado cuenta. A partir de ahora **NUNCA** deberías dejar un mensaje de error ignorado, aunque en tu mente sepas que es por una tontería y pienses solucionarlo más tarde. Los errores en JavaScript hacen que nuestro código sea muy frágil, y pueden hacer que toda una lógica se rompa.

#### Otras APIs públicas

Todas las APIs que estamos utilizando en esta lección son APIs públicas. Esto quiere decir que cualquier persona puede acceder a los datos de estas APIs. Las APIs privadas son aquellas que para usarlas tenemos que pedir permiso a los propietarios y estos nos facilitan una clave de acceso secreta para acceder al API.

Por si tenéis curiosidad aquí tenéis otra API: estudio Ghibli https://ghibliapi.herokuapp.com. Podéis acceder a la información de la peli 'Mi vecino Totoro' con esta url https://ghibliapi.herokuapp.com/films/58611129-2dbc-4a81-a72f-77ddfc1b1b49.

### `XMLHttpRequest`

Para ver la diferencia del uso de callbacks y promesas (verás que con promesas el código es mucho más simple y legible), te dejo explorar el primer ejemplo que vimos usando `XMLHttpRequest` en este código:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Ejercicio</title>
  </head>
  <body>
    <button class="js-emoji">Emoji!!!</button>
    <p class="js-result"></p>
    <script src="./js/main.js"></script>
  </body>
</html>
```

```js
let request;

function showPicture() {
  const response = JSON.parse(request.responseText).result;
  document.querySelector('.js-result').innerHTML = response;
}

function sendRequest () {
  request = new XMLHttpRequest();
  request.open('GET', 'https://api.rand.fun/games/rockpaperscissorslizardspock');
  request.addEventListener('load', showPicture);
  request.send();
}

document.querySelector('.js-emoji').addEventListener("click", sendRequest);
```

## Resumen

En esta sesión hemos visto la tecnología asíncrona **AJAX** que nos permite comunicarnos con el servidor usando **`XMLHttpRequest`** basado en **callbacks** o **`fetch`** basado en **promesas**.

Hemos introducido el concepto **API** (URL para consultar datos de un servicio), como comúnmente estas nos devuelven una respuesta que se puede parsear a **JSON**. Y lo importante de leer la documentación.

Hemos profundizado en el uso de `fetch` y la promesa que devuelve, viendo como podemos encadenarle un **`then`** que recibe una función como argumento, esta:
- se ejecutará cuando la promesa se cumpla.
- recibe como argumento la respuesta del servidor
- puede devolver otra promesa, para continuar encadenando `then`s.
- si esta promesa que devuelve no se resuelve y se rechaza por un error, podemos gestionarlo con `catch`

Por lo tanto, gracias al funcionamiento de las promesas podemos **encadenar llamadas al servidor**.

También hemos visto como realizar **llamadas en paralelo** utilizando **`Promise.all`**

Relacionado con los elementos de HTML ya sabemos como leer y modificar los atributos **`src`** y **`alt`** de la etiqueta imagen.


## Recursos externos

- [Exploring JS: promises](http://exploringjs.com/es6/ch_promises.html)
- [MDN: using promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [We have a problem with promises](https://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html)
- [AJAX](https://es.wikipedia.org/wiki/AJAX)
- [JSON](https://es.wikipedia.org/wiki/JSON)
