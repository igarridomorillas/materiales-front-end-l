# Express: Middleware and next

## La respuesta

- Hay muchos tipos de respuestas

## La respuesta

- Vídeo
   - Explicar los diferentes tipos de respuestas que tenemos en el ejercicio
   - Explicar qué pasa si respondemos dos veces

## Ejercicios

###

Crear un servidor para devolver un número aletorio entero entre 0 y 100 con los tipos de respuesta:

- `{ result: 13 }`
- Una página HTML en la que el `h1` ponga **El número aleatorio es 13**.
- Una redirección que si el número aleatorio es par redireccione a youtube y si es impar a instagram
- Un endpoint que si recibe por query params el `user=1` o `user=2` o `user=3` devuelva el json con status 200 y respuesta `{ result: 'ok' }`. Si el user es diferente que devuelva un `{result: 'error' }` con el status 404.
- Para qué será `res.headersSent`