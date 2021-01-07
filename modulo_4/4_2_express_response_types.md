# Express: tipos de respuestas

Hasta ahora hemos visto cómo puede un servidor de Express JS recoger los datos de una petición. En **esta lección vamos a ver cómo puede Express JS responder a una petición.**

En la [documentación de Express JS](https://expressjs.com/en/4x/api.html#res) podemos ver las diferentes formas de responder a una petición. En el siguiente vídeo vamos a ver las formas más importantes y más usadas:

{% embed url="https://www.youtube.com/watch?v=yxZfpmOURtQ" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-response-types)

- Vídeo
   - En este vídeo vamos a ver las diferentes formas con las que un servidor puede responder a una petición
   - Debemos conocer un poco todas las formas que hay para luego saber cuál elegir en cada momento
   - En este vídeo tenemos un montón de peticiones GET a varios endpoints
   - Aquí no nos importa con qué verbo se realiza la petición ni con qué datos
   - En el ejercicio están los principales tipos
   - JSON
      - Está pensado para responder a una llamada a un API desde un fetch
   - Redirect
      - A veces nos interesa que cuando una usuaria entra en una página la podamos redireccionar a otra página de nuestro servidor o de otro servidor
   - sendFile
      - A veces nos interesa enviar un fichero que no sea un html, que sea por ejemplo un PDF
   - download
      - A veces nos interesa en vez de enviar un fichero que este se descargue automáticamente
      - Tenemos que indicar la ruta del fichero a enviar y el nombre del fichero con el que queremos que se descargue
   - send
      - Otras veces nos interesa
   - status
      - Todas estas peticiones las está respondiendo con el código de respuesta HTTP 200
      - Si no sabes lo que son los códigos HTTP de respuesta no te preocupes ya te lo explicaremos
      - El código 200 es el código de respuesta por defecto
      - Pero si queremos cambiar el código de respuesta no tenemos más que poner status(404) antes de llamar a json, sendFile, send...

https://developer.mozilla.org/es/docs/Web/HTTP/Status