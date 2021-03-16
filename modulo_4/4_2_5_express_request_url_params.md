# Express: URL params

En esta lección vamos a explicar cómo enviar datos a través de URL params. Es exactamente lo mismo que enviar datos con query params o body params, pero por otro sitio.

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre URL params](https://www.youtube.com/watch?v=1VbJqdFYk6Y).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-request-url-params)

## Características de los URL params

- Desde el navegador:
   - Como van en la URL y todas las peticiones tienen URL se pueden utilizar con cualquier verbo (GET, POST, PUT, PATCH...).
   - Se pueden usar para hacer peticiones desde la barra de direcciones del navegador o a través de un `fetch`.
- En el servidor:
   - Recibimos los datos en `req.params`.
   - Todos los datos enviados por URL param se reciben en el servidor como **string**.

## Múltiples URL params

Crees que un endpoint puede tener varios URL params. Claro que sí guapi.

Si creáramos una tienda online lo normal sería crear los siguientes endpoints:

- http://localhost:3000/users/123: que devolvería un **objeto con la información del usuario** que tenga el id **123**.
- http://localhost:3000/users/123/orders: que devolvería un **array con los pedidos del usuario** que tenga el id **123**.
- http://localhost:3000/users/123/orders/456: que devolvería un **objeto con la información del pedido** que tenga el id **456** del usuario que tenga el id **123**.
- Y lo mismo para otros endpoints que devuelvan el listado de direcciones postales, el listado de métodos de pago...

Pues bien, si en el servidor creamos un endpoint que sea:

- http://localhost:3000/users/:userId/orders/:orderId

En `req.params` Express JS nos metería el objeto:

```js
{
  userId: 123,
  orderId: 456
}
```

## Ejercicios

### 1. Endpoint para devolver un pedido

Vamos a hacer un servidor que cuando se le haga una petición a la URL http://localhost:3000/users/123/orders/456 la gestione y devuelva algo ¿el qué? da igual, porque lo que nos interesa aquí es la parte de la petición, no la de la respuesta.

1. Crea un index.js con un servidor.
1. Crea un endpoint de tipo GET que sea capaz de atender la petición http://localhost:3000/users/123/orders/456 y consolear en la terminal los parámetros de la URL.

> **Nota:** Usa Postman y así no perderás tiempo en montar una web.

### 2. Troceando a Rick & Morty

Vamos a crear un API que devuelva los datos de Rick y Morty que ya conocemos pero separados en varios endpoints diferentes

1. Crea un `index.js` en un servidor.
1. Crea un fichero `data.json` y copia dentro los datos de Rick y Morty (https://raw.githubusercontent.com/Adalab/rick-y-morty/master/data/rick-y-morty.json)
1. Crea un endpoint para recuperar los datos de un personaje:
   - El endpoint debe ser GET y con la ruta `http://localhost:3000/users/1/` y tiene que devolver:
   ```json
   {
     "id": 1,
     "name": "Rick Sanchez",
     "status": "Alive"
     ...
   }
   ```
1. Crea otro endpoint para recuperar el listado de episodios de un personaje:
   - También debe ser de tipo GET y con la URL `http://localhost:3000/users/1/episodes` y tiene que devolver:
     ```json
     [
       "https://rickandmortyapi.com/api/episode/1",
       "https://rickandmortyapi.com/api/episode/2",
       "https://rickandmortyapi.com/api/episode/3",
       ...
     ]
     ```

> **Nota:** Usa Postman y así no perderás tiempo en montar una web.

Si vemos la [documentación del API de Rick y Morty](https://rickandmortyapi.com/) nos podemos imaginar cómo están programados cada uno de los endpoints:

- [Obtener un personaje](https://rickandmortyapi.com/documentation/#get-a-single-character)
- [Obtener un episodio](https://rickandmortyapi.com/documentation/#get-a-single-episode)
- [Obtener una localización](https://rickandmortyapi.com/documentation/#get-a-single-location)

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.