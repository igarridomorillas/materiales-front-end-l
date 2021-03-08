# Leer registros de una base de datos: SELECT

## Operaciones en una base de datos

Para trabajar con una base de datos podemos hacer 4 operaciones básicas:

- Añadir un nuevo registro.
- Borrar un registro existente.
- Modificar un registro existente.
- Leer uno o varios registros, que es la que vamos a aprender en esta lección.

A estas operaciones se le llama **CRUD**: create, read, update and delete.

### Consideraciones sobre las operaciones de una base de datos

- **La operación de lectura no modifica la base de datos.** El resto de operaciones sí.
- **Todas estas operaciones se realizan sobre una única tabla.** Por ahora, si queremos hacer operaciones sobre varias tablas tenemos que hacer varias consultas o queries por separado.
- Existen operaciones más complejas pero son combinaciones de estas 4 operaciones básicas.
- Cada vez que accedemos a una base de datos decimos que hacemos una **query o consulta a la base de datos**.

## Sintaxis de SELECT en SQL y SQLite browser

`SELECT` nos permite **seleccionar o leer uno o varios registros de una tabla** de la base de datos.

Supongamos que tenemos esta tabla llamada `users`:

| id  | email              | password     | name  |
| --- | ------------------ | ------------ | ----- |
| 1   | maria@gmail.com    | 987widJYVxyh | María |
| 2   | lucia@hotmail.com  | qwertyui     | Lucía |
| 3   | sofia@yahoo.com    | mnbvcdfgu    | Sofía |

### SELECT

Con `SELECT` seleccionamos las columnas que queremos leer y con `FROM` elegimos el nombre de la tabla de donde queremos leer. Por ello:

```sql
-- Seleccionar el id y el email de todas las usuarias
SELECT id, email FROM users
```

```sql
-- Seleccionar todas las columnas o datos de todas las usuarias
SELECT * FROM users
-- El símbolo `*` indica que quiero seleccionar todas las columnas de una tabla.
```

`SELECT` y `FROM` son palabras obligatorias al hacer una query de lectura.

### WHERE

Con `WHERE` indicamos una condición que debe cumplir el registro (o fila) para poder leerlo. Sería como hacer `filter` o un `if` de JavaScript. Es decir quiero leer una fila **si** cumple la **condición** indicada:

```sql
-- Seleccionar todas las columnas de todas las usuarias cuyo id sea mayor o igual que 2
SELECT * FROM users WHERE id >= 2
-- Esto nos devolverá 0, 1 o varios registros
```

```sql
-- Seleccionar todas las columnas de la usuaria cuyo id sea igual a 2, esto nos devolverá solo un registro
SELECT * FROM users WHERE id = 2
-- Esto nos devolverá 0 o 1 registro.
```

```sql
-- Seleccionar todas las columnas de la usuaria cuyo email sea lucia@hotmail.com
SELECT * FROM users WHERE email = 'lucia@hotmail.com'
```

```sql
-- Seleccionar todas las columnas de la usuaria cuyo email sea lucia@hotmail.com y el password sea qwertyui
SELECT * FROM users WHERE email = 'lucia@hotmail.com' AND password = 'qwertyui'
```

`WHERE` no es obligatorio al hacer una query de lectura. Si una consulta no tiene `WHERE` nos devolverá todos los registros de una tabla.

> **Nota:** `WHERE` también es muy usado en operaciones de modificación y borrado de registros en tablas. Lo veremos más adelante.

### ORDER BY

Con `ORDER BY` podemos indicar el orden en el que queremos leer los registros:

```sql
-- Seleccionar todas las columnas de todas las usuarias ordenadas por nombre de forma ascendente: A-Z
SELECT * FROM users ORDER BY name ASC
```

```sql
-- ASC es el orden por defecto, así que lo podemos omitir. Esta query es igual que la anterior
SELECT * FROM users ORDER BY name
```

```sql
-- Seleccionar todas las columnas de todas las usuarias ordenadas por nombre de forma descendente: Z-A
SELECT * FROM users ORDER BY name DESC
```

```sql
-- Seleccionar todas las columnas de todas las usuarias ordenadas por nombre de forma descendente y a continuación por email de forma descendente
SELECT * FROM users ORDER BY name ASC, email DESC
```

`ORDER BY` no es obligatorio al hacer una query de lectura.

### LIMIT y OFFSET

Con `LIMIT` indicamos el **número máximo de registros** que queremos leer:

```sql
-- Seleccionar todas las columnas hasta un máximo de 2 usuarias
SELECT * FROM users LIMIT 2
```

Con `OFFSET` indicamos el primer registro a partir del cual queremos leer:

```sql
-- Seleccionar todas las columnas hasta un máximo de 2 usuarias empezando en la posición 5
SELECT * FROM users LIMIT 2 OFFSET 5
-- Esta consulta nos devolverá los registros 6º y 7º.
```

Ni `LIMIT` ni `OFFSET` son obligatorio al hacer una query de lectura.

`LIMIT` y `OFFSET` son muy útiles para cuando tenemos muchos registros en una tabla. Por ejemplo, cuando entramos en nuestro Twitter, la web solo nos muestra los primeros 50 tweets. Si bajamos hasta abajo del todo nos muestra los siguientes 50 tweets. Esto se haría con las siguientes consultas:

```sql
-- Query de los primeros 50 tweets: seleccionar todos los tweets hasta un máximo de 50 tweets
SELECT * FROM tweets ORDER BY id LIMIT 50
-- Esta consulta nos devolverá los registros desde el id 1 hasta el id 49
```

```sql
-- Query de los siguientes 50 tweets: seleccionar todos los tweets hasta un máximo de 50 tweets empezando por el número 50
SELECT * FROM tweets ORDER BY id LIMIT 50
-- Esta consulta nos devolverá los registros desde el id 50 hasta el id 99
```

### Conclusiones de la sintaxis de SQL

<!-- - Vídeo
  - Hacer todas estas queries en SQLite Browser -->

Nuestro trabajo cuando leemos datos de una tabla es combinar `SELECT`, `FROM`, `WHERE`, `ORDER BY` y `LIMIT` para obtener los datos que queremos.

**Mayúsculas vs minúsuculas:** normalmente escribimos en **mayúsculas** las palabras `SELECT`, `FROM`, `WHERE`, `ORDER BY`, `LIMIT` y otras que aprenderemos en próximas lecciones **porque son palabras del lenguaje SQL**. Y escribimos en **minúsculas o camelCase las columnas y los nombres de las tablas**. De esta forma es más fácil leer una query.

**Comentarios:** todos los lenguajes de programación tiene caracteres para indicar comentarios. En JS ponemos `// mi comentario` o `/* mi comentario */`. En SQL los comentarios se ponen con dos guiones `--` al principio de la query.

{% embed url="https://www.youtube.com/watch?v=c_phy5dfWAE" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-4-3-sql-select)

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

{% embed url="https://www.youtube.com/watch?v=87KvwNxLWRA" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-4-3-sql-select)

## Otras opciones para hacer un SELECT

Las opciones para leer datos de SQL son infinitas, por ejemplo:

```sql
-- Seleccionar todas las columnas de todas las usuarias que no tengan id = 2
SELECT * FROM users WHERE id <> 2
```

```sql
-- Seleccionar todas las columnas de la usuaria que tenga un id = 2 o un email = lucia@hotmail.com
SELECT * FROM users WHERE id = 1 OR email = 'lucia@hotmail.com'
```

```sql
-- Seleccionar todas las columnas de todas las usuarias cuyo email contenga la palabra: gmail
SELECT * FROM users WHERE email LIKE '%gmail%'
```

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

## Busca en Internet

Como hemos comentado cuando tengas cualquier duda sobre cómo realizar una query de cualquier tipo busca en Internet. Te recomendamos que al buscar escribas **SQL** y lo que estés buscando, por ejemplo:

- SQL WHERE with AND
- SQL filtrar por id
- SQL obtener los primeros 10 registros
- ...

Es decir, no busques por SQLite, sino por SQL, ya que ambos tienen la misma sintaxis pero en Internet hay muchas más páginas que hablan sobre SQL en general que sobre SQLite en particular.

## Ejercicios

### 1. El blog: tabla de artículos

Vamos a suponer que tenemos que crear una base de datos para gestionar un blog. Entre las muchas tablas que tendría la base de datos nos toca crear una para almacenar los artículos escritos por la autora:

1. Crea un proyecto de Node JS, si quieres puedes utilizar el ejercicio del vídeo de esta sección.
1. Instala (si no lo has hecho ya) SQLite browser.
1. Crea una base de datos a través SQLite browser dentro del proyecto.
1. Crea una tabla llamada articles con las siguientes columnas:
   1. Título del artículo.
   1. Cuerpo del artículo.
   1. URL de la imagen principal.
   1. Fecha de publicación.
   1. Borrador o publicado.
   1. Pon cualquier otro campo que te parezca bien.
1. Antes de continuar:
   1. Revisa qué tipos y opciones le has puesto a cada columna.
   1. ¿Has puesto alguna columna para identificar cada artículo?
1. Crea 3 artículos rellenando todas las columnas. Haz que dos de ellos tengan la palabras **bases de datos** en el título.
1. Desde el editor SQL de SQLite browser ejecuta las siguientes queries:
   1. Selecciona todos los artículos.
   1. Selecciona el artículo con el artículo que tiene el `id = 2`.
   1. Selecciona todos los artículos que tengan en el título la palabra **datos**. Te ayudará buscar en Internet [**SQL like**](https://www.google.com/search?q=sql+like&oq=sql+like&aqs=chrome.0.69i59j0l9.3481j0j7&sourceid=chrome&ie=UTF-8).

Después de cada consulta comprueba que los resultados que muestra SQLite browser tienen sentido.

### 2. La tienda online: tabla de libros

Ahora vamos a suponer que tenemos que crear una base de datos para una tienda online de teléfonos libros. Sobre el proyecto del ejercicio anterior o sobre uno nuevo:

1. Crea una nueva tabla para guardar tus libros a la venta para guardar la siguiente información:
   1. Nombre del libro.
   1. Autora del libro.
   1. Resumen del libro.
   1. Precio del libro.
   1. Stock del libro.
   1. ¿Es un libro descargable como un ebook o es un libro físico que debemos enviar por mensajería?
1. Crea 5 libros.
1. Crea un API en Node JS que devuelva la siguiente información en diferentes endpoints:
   1. Un array con todos los libros ordenados de menor a mayor precio.
   1. Un array con los libros con precio superior a 5 €.
   1. Un array con los libros con stock.
   1. Un array con los libros físicos y en stock.
   1. Un objeto con el libro con `id = 1`.
   1. Un array con los 3 primeros libros ordenados alfabéticamente por nombre.
   1. Un array con los 3 siguientes libros ordenados alfabéticamente por nombre.

Todos los endpoints que hagas deben:

- Ser con el método `GET`.
- Recibir la información necesaria para hacer la petición por query params.

Revisa qué la ruta de los endpoints sea coherente con lo que hacen.

> **Nota:** puedes acceder a tu API directamente desde Postman.

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.