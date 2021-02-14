# Leer registros de una base de datos: SELECT

## Sintaxis de SELECT en Node JS y Better SQLite 3

Ya sabemos leer de una tabla de base de datos usando el programa SQLite browser. Como hemos dicho este es el DevTools de SQLite. **Nos sirve para hacer pruebas mientras estamos programando.**

A partir de ahora, cuando tengamos que hacer una query, **primero la probaremos en SQLite browser** y cuando encontremos la sintaxis que queremos, la escribiremos en Node JS para que **Node JS haga la query por nosotras**.

Vamos a seguir los pasos para usar bases de datos en un proyecto de Node JS que ya tengamos creado. Tenemos que:

### 1º Instalar Better SQLite 3

En [NPM](https://www.npmjs.com/) hay muchos módulos para acceder a todo tipo bases de datos. También hay muchos módulos para a SQLite. En Adalab vamos a aprender a utilizar uno de ellos que se llama [**Better SQLite 3**](https://www.npmjs.com/package/better-sqlite3).


Para instalar **Better SQLite 3** escribiremos en la terminal:

```bash
npm install better-sqlite3
```

### 2º Indicar la base de datos que vamos a usar

A continuación tenemos que crear con SQLite browser una base de datos dentro de nuestro proyecto, por ejemplo en `./src/database.db` y luego escribir el siguiente código en `src/index.js`:

```js
// importar el módulo better-sqlite3
const Database = require('better-sqlite3');

// indicar qué base de datos vamos a usar con la ruta relativa a la raíz del proyecto
const db = new Database('./src/database.db', {
  verbose: console.log // con verbose le decimos que toda las queries que se ejecuten las muestre en la consola
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
const query = db.prepare(`SELECT * FROM users`);
const users = query.all();
const user = query.get();
```

`const users = query.all()` devuelve varios registros, por ello `users` será un **array de objetos**. Si no hay registros en tabla, `query.all()` devolverá un **array vacío**.

`const user = query.get()` devuelve un registro, por ello `user` será un **objeto**. Si no hay registros en la tabla `query.get()` devolvera un *`undefined`*.

### 5º Leer uno o varios registros pasando datos

Con este código:

```js
const query = db.prepare(`SELECT * FROM users WHERE id >= ?`);
const users = query.all(2);
```

Estamos indicando que **Better SQLite 3** debe sustituir la `?` por un `2` al ejecutar la query.

Esto está hecho así por dos motivos:

- Para que podamos separar la sintaxis de la query de los datos que pasamos a la query.
- Para poder crear una query y ejecutarla muchas veces con muchos datos diferentes.

Con este código:

```js
const query = db.prepare(`SELECT * FROM users WHERE email = ? AND password = ?`);
const users = query.get('lucia@hotmail.com', 'qwertyui');
```

Obtenemos un objeto con la usuaria que tenga ese email y esa contraseña. Esta es la típica consulta que se usa en un login y comprobar si la usuaria existe en nuestra base de datos.