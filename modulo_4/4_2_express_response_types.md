# Express: tipos de respuestas

Hasta ahora hemos visto cómo puede un servidor de Express JS recoger los datos de una petición. **En esta lección vamos a ver cómo puede Express JS responder a una petición.**

En la [documentación de Express JS](https://expressjs.com/en/4x/api.html#res) podemos ver las diferentes formas de responder a una petición. En el siguiente vídeo vamos a ver las formas más importantes y más usadas.

> **Nota:** hasta ahora hemos utilizado `const server = express();` para que sepáis que lo que devuelve la función `express();` es un servidor. Pero normalmente todo el mundo llama a esta constante **app**. Para que os acostumbréis a verlo así, a partir de este vídeo vamos a utilizar `const app = express();`, `app.listen(...)`, `app.get()`...

{% embed url="https://www.youtube.com/watch?v=yxZfpmOURtQ" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-response-types/examples)

Los tipos de respuestas que hemos visto en este vídeo son:

- [res.json](https://expressjs.com/en/4x/api.html#res.json)
- [res.redirect](https://expressjs.com/en/4x/api.html#res.redirect)
- [res.sendFile](https://expressjs.com/en/4x/api.html#res.sendFile)
- [res.download](https://expressjs.com/en/4x/api.html#res.download)
- [res.send](https://expressjs.com/en/4x/api.html#res.send)

Y para cambiar el código de estado de la respuesta usamos:

- [res.status](https://expressjs.com/en/4x/api.html#res.status)

También te recomendamos leer más información sobre [los códigos HTTP de respuesta](https://developer.mozilla.org/es/docs/Web/HTTP/Status).

## Errores comunes

Responder dos veces a la misma petición:

{% embed url="https://www.youtube.com/watch?v=Tqtn4B4J1YE" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-response-types/error-headers-sent)

Más información sobre [res.headerSent](https://expressjs.com/en/4x/api.html#res.headersSent).

## Ejercicios

### 1. Responder muchas cosas

Vamos a crear un servidor para diferentes tipos de respuesta:

- Cuando la usuaria haga un GET a `/response-a` debemos responder `{ result: 'ok' }`.
- Cuando la usuaria haga un GET a `/response-b` debemos responder con una página HTML en la que el `h1` ponga **Esta es una página de prueba**.
- Cuando la usuaria haga un GET a `/response-c` debemos calcular un número aleatorio entre 0 y 10 y redireccionar a:
   - Youtube si el número es par.
   - Instagram si el número es impar.
- Cuando la usuaria haga un GET a `/response-d`
   - con un query param `user=1` o `user=2` debe responder con un json con status 200 y respuesta `{ result: 'ok' }`.
   - si se llama a este endpoint sin query param o con un query param diferente de `user=1` o `user=2` debe responder un json `{ result: 'error: invalid query param' }` con el status **404**.

### 2. Todo el mundo usa códigos HTTP para informar sobre errores

Entra en esta [página que no existe](https://www.google.es/pagina-que-no-existe) y:

- Mira qué información nos muestra la página
- Abre devtools > network, refresca la página y mira qué código de respuesta está devolviendo el servidor de Google.

Entra en esta [otra página que tampoco existe](https://github.com/otra-pagina-que-no-existe) y repite los pasos anteriores.