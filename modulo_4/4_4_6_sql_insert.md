# Añadir registros de una base de datos: INSERT INTO

`INSERT INTO` nos permite **añadir un registro a una tabla** de la base de datos a través de una query.

Así como leer registros de una tabla no modifica la base de datos, añadir un registro sí que la modifica.

## Sintaxis de INSERT INTO en SQL y SQLite browser

La sintaxis de un `INSERT INTO` es:

```sql
INSERT INTO nombre_de_la_tabla (nombre_de_una_columna, nombre_de_otra_columna)
VALUES (valor_de_una_columna, valor_de_otra_columna)
```

Supongamos que tenemos esta tabla llamada `users`:

| id  | email              | password     | name  |
| --- | ------------------ | ------------ | ----- |
| 1   | maria@gmail.com    | 987widJYVxyh | María |
| 2   | lucia@hotmail.com  | qwertyui     | Lucía |
| 3   | sofia@yahoo.com    | mnbvcdfgu    | Sofía |

### INSERT INTO indicando solo algunas columnas

Con la query:

```sql
-- Añadir un nuevo registro indicando algunas columnas y el valor de cada columna
INSERT INTO users (email, password) VALUES ('celia@gmail.com', 'fas09fn32');
```

La tabla quedará así:

| id  | email               | password      | name  |
| --- | ------------------- | ------------- | ----- |
| 1   | maria@gmail.com     | 987widJYVxyh  | María |
| 2   | lucia@hotmail.com   | qwertyui      | Lucía |
| 3   | sofia@yahoo.com     | mnbvcdfgu     | Sofía |
| 4   | **celia@gmail.com** | **fas09fn32** |       |

Al no haber añadido la columna `name` en la query, la usuaria 4 no tiene nombre.

### INSERT INTO indicando todas las columnas

Si a continuación añadimos otro registro con la query:

```sql
-- Añadir un nuevo registro indicando todas columnas y el valor de cada columna
INSERT INTO users (email, password, name) VALUES ('tania@gmail.com', '09df34D43', 'Tania');
```

| id  | email               | password      | name  |
| --- | ------------------- | ------------- | ----- |
| 1   | maria@gmail.com     | 987widJYVxyh  | María |
| 2   | lucia@hotmail.com   | qwertyui      | Lucía |
| 3   | sofia@yahoo.com     | mnbvcdfgu     | Sofía |
| 4   | celia@gmail.com     | fas09fn32     |       |
| 5   | **tania@gmail.com** | **09df34D43** | Tania |

### Orden de las columnas

Al hacer estas queries nos tenemos que preocupar de que el orden de las columnas coincide con el orden de los valores. Esta query:

```sql
INSERT INTO users (email, password, name) VALUES ('tania@gmail.com', '09df34D43', 'Tania');
```

Es igual que esta:

```sql
INSERT INTO users (name, password, email) VALUES ('Tania', '09df34D43', 'tania@gmail.com');
```

### Valor de la columna id

La columna `id` es una columna especial que no rellenamos nosotras si no que va a ser rellenado por SQL. Esto lo explicaremos más adelante.

Lo importante es que **nunca debemos indicar el valor de la columna `id`**.

### Añadir varios registros

Si queremos añadir varios registros lo tendremos que hacer en varias queries. Para ello tendremos que hacer un `for` en Node JS ejecutando varias veces la query.

<!-- - Vídeo -->

## Sintaxis de INSERT INTO en Node JS y Better SQLite 3

Antes de añadir un nuevo registro desde Node JS, deberíamos seguir los pasos que hemos aprendido para trabajar con **Better SQLite 3**:

1. **Instalar Better SQLite 3** en el proyecto con `npm install better-sqlite3`.
1. **Importar Better SQLite 3** en el proyecto con `const Database = require('better-sqlite3');`.
1. **Iniciar y configurar la base de datos** con `const db = new Database('./src/database.db' });`.

Una vez hecho esto ya podemos añadir nuevos registros. La forma de trabajar es igual que con `SELECT`:

```js
// preparamos la query
const query = db.prepare(`INSERT INTO users (email, password) VALUES (?, ?)`);
// ejecutamos la query
const result = query.run('celia@gmail.com', 'fas09fn32');
```

Normalmente nuestras queries las haremos desde dentro de un endpoint de Express JS. Por ello el código sería:

```js
app.post('/users', (req, res) => {
  const query = db.prepare(`INSERT INTO users (email, password) VALUES (?, ?)`);
  const result = query.run('celia@gmail.com', 'fas09fn32');
  res.json(result);
});
```

Normalmente el email y contraseña nos lo van a enviar desde el navegador con un `fetch` por ello el código sería algo como:

```js
app.post('/users', (req, res) => {
  const query = db.prepare(`INSERT INTO users (email, password) VALUES (?, ?)`);
  const result = query.run(req.body.email, req.body.password);
  console.log(result);
  res.json(result);
});
```

### query.run()

En estas queries no estamos leyendo datos de la tabla, por ello no utilizamos `query.all()` ni `query.get()`. En esta query utilizamos `query.run()` porque lo que queremos es añadir registros. Los creadores de Better SQLite 3 han elegido esta forma de trabajar porque les ha apetecido, pero si lo piensas tiene bastante sentido.

### Información retornada por query.run()

Al añadir un nuevo registro nos interesa saber el `id` que SQL le ha asignado. Lo normal es responder a la petición hecha desde el navegador con el `id` de la usuaria creada. Así el navegador podrá hacer nuevas peticiones al servidor indicando qué usuaria está haciendo las peticiones.

Este `id` es retornado por `query.run()`. Por ello el console del código anterior mostrará:

```json
{
  "changes": 1, // se ha cambiado o añadido un registro
  "lastInsertRowid": 6 // el id del registro añadido es 6, porque hasta ahora había 5 registros en la tabla
}
```