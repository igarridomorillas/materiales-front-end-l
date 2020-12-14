# Express básico

## Qué es Express

- Vídeo
   - Express es un módulo de Node pensado para crear servidores, tanto de estáticos  como GitHub Pages como de dinámicos como puede ser cualquier API
   - Express no viene por defecto con Node, hay que instalarlo
   - Enseñar web
   - Enseñar documentación
   - Puesto que vamos a trabajar con módulos de NPM necesitamos un package.json
   - Explicar que toda petición a servidor está compuesta por una petición y una respuesta
   - Dentro de la petición y la respuesta hay muchas formas de enviar los datos

## Ejemplo de servidor en Express

- Vídeo
   - Explicar ejercicio express-basic
   - Explicar lo que hace el ejercicio con la web
   - Explicar lo que que tenemos una base de datos fake
   - Explicar que como la db es fake, cada vez que reinicio el servidor se reinician los datos
   - Explicar el puertos
   - Explicar cada uno de los endpoints
   - Explicar que es similar a addEventListener
   - Explicar que tenemos la req y la res
   - Explicar que la req que tiene la info del post
   - Explicar que la res tiene métodos para responder la info
   - Explicar que aquí hemos elegidor res.json, pero hay otros como res.send
   - Explicar que el orden de los endpoints es importante como si fuera un if else
   - Enseñar devtools network

## Ejercicios

### Cambio de las rutas

Partiendo del ejercicio express-basic

1. Cambia la ruta `app.post('/new-user', (req, res) => {` por `app.post('/users/add', (req, res) => {`
   - Qué debes cambiar en el front para que la web para sigua funcionando
1. Cambia la ruta `app.get('/users', (req, res) => {` por `app.post('/users', (req, res) => {`
   - Qué debes cambiar en el front para que la web para sigua funcionando
1. Cambia el puerto `const serverPort = 3000;` por `const serverPort = 3500;`
   - Qué debes cambiar en el front para que la web para sigua funcionando

