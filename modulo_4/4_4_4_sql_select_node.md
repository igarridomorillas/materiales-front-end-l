# Leer registros de una base de datos: SELECT

## Sintaxis de SELECT en Node JS y Better SQLite 3

Ya sabemos leer de una tabla de base de datos usando el programa SQLite browser. Como hemos dicho este es el DevTools de SQLite. **Nos sirve para hacer pruebas mientras estamos programando.**

A partir de ahora, cuando tengamos que hacer una query, **primero la probaremos en SQLite browser** y cuando encontremos la sintaxis que queremos, la escribiremos en Node JS para que **Node JS haga la query por nosotras**.

Vamos a seguir los pasos para usar bases de datos en un proyecto de Node JS que ya tenemos creado. Tenemos que:

### 1º Instalar Better SQLite 3

En [NPM](https://www.npmjs.com/) hay muchos módulos para acceder a todo tipo bases de datos. También hay muchos módulos para a SQLite. En Adalab vamos a aprender a utilizar uno de ellos que se llama [**Better SQLite 3**](https://www.npmjs.com/package/better-sqlite3).


Para instalar **Better SQLite 3** escribiremos en la terminal:

```bash
npm install better-sqlite3
```

Lo que nos añadirá esta dependencia a nuestro `package.json`.

### 2º Indicar la base de datos que vamos a usar

A continuación tenemos que crear con SQLite browser una base de datos y guardar el fichero dentro de nuestro proyecto, por ejemplo en `./src/database.db` y luego escribir el siguiente código en `src/index.js`:

```js
// importar el módulo better-sqlite3
const Database = require('better-sqlite3');

// indicar qué base de datos vamos a usar con la ruta relativa a la raíz del proyecto
const db = new Database('./src/database.db', {
   // con verbose le decimos que todas las queries que se ejecuten las muestre en la consola
   verbose: console.log
   // así podemos comprobar qué queries estamos haciendo en todo momento
});
```

### 3º Hacer una query

Una query está compuesta de dos líneas de código:

```js
// preparamos la query
const query = db.prepare(`SELECT * FROM users`);
// ejecutamos la query
const users = query.all();
```

Normalmente nuestras queries las haremos desde dentro de un endpoint de Express JS. Por ello el código sería:

```js
app.get('/users', (req, res) => {
  const query = db.prepare(`SELECT * FROM users`);
  const users = query.all();
  res.json(users);
});
```

### 4º Leer uno o varios registros: query.all() vs query.get()

Con este código:

```js
// preparo la query
const query = db.prepare(`SELECT * FROM users`);
// ejecuto la query para obtener todos los registros en un array
const users = query.all();
// ejecuto la query para obtener el primer registro en un objeto
const user = query.get();
```

`const users = query.all()` devuelve varios registros, por ello `users` será un **array de objetos**. Si no hay registros en tabla, `query.all()` devolverá un **array vacío**.

`const user = query.get()` devuelve un registro, por ello `user` será un **objeto**. Si no hay registros en la tabla `query.get()` devolvera un *`undefined`*.

En resumen, cada vez que queramos leer registros de una tabla, debemos pensar si queremos un listado y ejecutar `query.all()` o un único registro y ejecutar `query.get()`

### 5º Leer uno o varios registros pasando datos

Con este código:

```js
// preparo la query
const query = db.prepare(`SELECT * FROM users WHERE id >= ?`);
// la ejecuta indicando: WHERE id >= 2
const users = query.all(2);
```

Estamos indicando que **Better SQLite 3** debe sustituir la `?` por un `2` al ejecutar la query.

Con este código:

```js
// preparo la query
const query = db.prepare(`SELECT * FROM users WHERE email = ? AND password = ?`);
// la ejecuta indicando: WHERE email = 'lucia@hotmail.com' AND password = 'qwertyui'
const users = query.get('lucia@hotmail.com', 'qwertyui');
```

Estamos indicando que **Better SQLite 3** debe sustituir la primera `?` por `'lucia@hotmail.com'` y la segunda `?` por `'qwertyui'` al ejecutar la query.

> **Por cierto:** con esta query obtenemos un objeto con la usuaria que tenga ese email y esa contraseña. Esta es la típica consulta que se usa en un login y comprobar si la usuaria existe en nuestra base de datos.

Los motivos por el cual una query se hace en dos pasos (primero preparar la query y después ejecutar la query) son:

- Para que podamos separar:
  - por un lado la sintaxis de la query
  - por otro lado los datos que pasamos a la query
- Para poder crear una query una única vez y ejecutarla muchas veces con muchos datos diferentes.
- Para que sea más difícil equivocarnos al hacer una query ya que es fácil olvidarse de unas comillas, una coma...

## La sintaxis de SQL es muy amplia

En este curso te estamos enseñando la sintaxis de SQL más usada y la más importante. SQL tiene muchísimas opciones. Cada vez que estés programando en Node JS tengas que hacer una query y no sepas cómo, tienes dos opciones:

- Pedir muchos datos a la base de datos y luego buscar / filtrar en Node JS. Esto **no es recomendable** ya que:
   - Estás haciendo tú algo en Node JS que SQL sabe hacer bien, y para lo cual ha sido diseñado.
   - Estás manejando una cantidad de datos grande cuando no es necesario.
   - Requiere más líneas de código.
   - Siempre va a ser un proceso más lento.
- O también **puedes buscar en Internet la solución**. Seguramente SQL tenga opciones para hacer lo que quieres. Usar las opciones que nos da SQL nos permite:
   - Hacer queries más rápidas, que ya SQL está pensado para ello.
   - Aprender una cosa nueva sobre SQL.
   - Reducir el código Node JS de nuestro servidor.