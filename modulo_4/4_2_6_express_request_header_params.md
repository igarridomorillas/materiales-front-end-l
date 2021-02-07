# Express: Headers params

La cuarta y última forma de enviar datos al servidor desde nuestro navegador es con **header params**. Si has llegado hasta aquí ya te podrás imaginar que es muy parecido a enviar query, body o URL params...

## Características de los header params

- Desde el navegador:
   - Se pueden enviar en todos los tipos de peticiones (GET, POST, PUT, PATCH...).
   - Al igual que los body params, se tienen que enviar **siempre desde un `fetch`**, no las podemos indicar en la barra de direcciones del navegador como las query o URL params.
   - Se envían añadiendo un objeto `headers` al fetch como se puede ver en el siguiente código:
   ```js
   fetch('http://localhost:3000/ruta-del-endpoint', {
       method: 'POST', // o GET, PUT, PATCH...
       headers: {
         unParametroEnLaCabecera: 'Hola mundo',
         'otro-parametro-de-la-cabecera': 123,
         otroParametroMas: 'Soy un dato'
       }
     })
     .then(response => response.json())
     .then(data => {...});
   ```
- En el servidor:
   - Recibimos los datos en `req.headers` que es un objeto.
   - También podemos acceder a una header param a través del método `req.header('nombre-de-header-param')` que nos devuelve el vamos de un header param.
   - Todos los datos enviados por header param se reciben en el servidor como **string**, aunque desde el `fetch` los hayamos enviado como un número u otro tipo de dato.
   - Todos los nombres de propiedades del objeto `req.headers` nos llegan al servidor en minúsculas.

## Los headers params llegan en minúsculas

Una curiosidad que tienen las headers params es que **los nombres de las header params llegan al servidor en minúsculas**. Insistimos en esto porque es algo poco usual. Vamos que es algo rarito.

Si desde el front envíamos:

```js
fetch('http://localhost:3000/ruta-del-endpoint', {
    method: 'POST', // o GET, PUT, PATCH...
    headers: {
      PARAMETRO_EN_MAYUSCULAS: '1',
      parametro_en_minusculas: '2',
      parametroEnCamelCase: '3',
      'Parametro-Separado-Con-Guiones': '4'
    }
  })
```

En el objeto `req.headers` del servidor recibiremos todos los nombres de propiedad en minúsuculas:
```js
{
  parametro_en_mayusculas: '1',
  parametro_en_minusculas: '2',
  parametroencamelcase: '3',
  'parametro-separado-con-guiones': '4'
}
```

## Header params del navegador

Cuando envías una petición desde el navegador al servidor, ya sea desde un `fetch` o desde la barra de direcciones del navegador, **el navegador siempre envia sus propias headers params**.

El navegador necesita enviar su propia información al servidor para decirle cosas como por ejemplo:

- Qué tipo, versión, modelo... de navegador es.
- Qué lenguajes (español, inglés...) entiende el usuario. Estos son los lenguajes que el usuario ha configurado en su navegador u ordenador.
- Qué tipos de formato de datos entiende, como texto, JSON, datos binarios...
- Cuál es la URL actual del navegador.
- Temas de caché, es decir, por cuanto tiempo va el navegador a almacenar la respuesta del servidor...

### User agent

Por ello cuando nosotras enviamos header params al servidor, en el objeto `req.headers` hay muchos más datos.

Uno de los parámetros más importantes en envía el navegador es el **`user-agent`**, en el que especifica el modelo de navegador (Chrome, Safari, Firefox, Internet Explorer, Edge...). En el servidor utiliza este parámetro para:

- Recoger estadísticas de los usuarios.
- Adaptar la respuesta que debe devolver al navegador.

Por ejemplo si una usuaria entra a una página web desde un Internet Explorer 6 (un navegador del que solo han oido hablar los más viejos del lugar), algún servidor devuelve un HTML en el que pone un mensaje del tipo "Nuestra página es muy moderna y no está preparada para navegadores tan viejunos. Por favor actualícese".

## Ejercicios

### 1. Investiga cómo recibir header params

1. Descarga, instala y arranca este (ejercicio)[https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-request-header-params].
1. Entra en http://localhost:3000 y pulsa en el botón.
1. Comprueba qué datos estás recibiendo en el servidor.
1. Abre el fichero `public/js/main.js` y mira qué datos se están enviando en la cabecera.
   1. Cambia los datos que se están enviando para enviar otro tipo de datos, como números enteros, decimales, booleanos, objetos...

### 2. User agent

1. Partiendo del ejercicio anterior ¿puedes averiguar el modelo de tu navegador?
1. Haz una nueva petición al servidor utilizando Postman y mira qué valo tiene el header param `user-agent`.

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.