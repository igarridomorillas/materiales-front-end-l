# Actualizar registros de una base de datos: UPDATE

`UPDATE` nos permite **modificar uno varios registros de una tabla** de la base de datos a través de una query.

Así como leer registros de una tabla no modifica la base de datos, actualizar uno o varios registros sí que la modifica.

## Sintaxis de UPDATE en SQL y SQLite browser

La sintaxis de un `UPDATE` es:

```sql
UPDATE nombre_de_la_tabla
SET nombre_de_una_columna = valor_de_una_columna, nombre_de_otra_columna = valor_de_otra_columna
WHERE condicion_que_cumplen_los_registros_a_modificar
```

Supongamos que tenemos esta tabla llamada `users`:

| id  | email              | password     | name  |
| --- | ------------------ | ------------ | ----- |
| 1   | maria@gmail.com    | 987widJYVxyh | María |
| 2   | lucia@hotmail.com  | qwertyui     | Lucía |
| 3   | sofia@yahoo.com    | mnbvcdfgu    | Sofía |

Con la query:

```sql
-- Actualizar el email de la usuaria que tiene el id = 3
UPDATE users SET email = 'sofia.garcia@yahoo.com' WHERE id = 3
```

La tabla quedará así:

| id  | email                      | password     | name  |
| --- | -------------------------- | ------------ | ----- |
| 1   | maria@gmail.com            | 987widJYVxyh | María |
| 2   | lucia@hotmail.com          | qwertyui     | Lucía |
| 3   | **sofia.garcia@yahoo.com** | mnbvcdfgu    | Sofía |

Por otro lado, con la query:

```sql
-- Actualizar el email y la contraseña de la usuaria que tiene el id = 3
UPDATE users SET email = 'sofia.garcia@yahoo.com', password = 'abcdefgh' WHERE id = 3
```

La tabla quedará así:

| id  | email                      | password     | name  |
| --- | -------------------------- | ------------ | ----- |
| 1   | maria@gmail.com            | 987widJYVxyh | María |
| 2   | lucia@hotmail.com          | qwertyui     | Lucía |
| 3   | **sofia.garcia@yahoo.com** | **abcdefgh** | Sofía |

### UPDATE sin WHERE igual a muerte, destrucción y caos!!!

Si hacemos una query para modificar registros de una tabla y no indicamos la condición `WHERE` **se modificarán todos los registros de la tabla**. Todos!!! Esto es porque todos los registros cumplen la condición vacía.

La condición `WHERE` no es obligatoria. Pocas veces vamos a querer cambiar todos los registros de una tabla, así que cuando hagas un `UPDATE` piensa dos veces si debes o no poner `WHERE`.

Con `UPDATE` y `WHERE` podemos actualizar uno o varios registros en una sola query. Todo depende de la condición que pongamos en el `WHERE`.

### No debemos modificar el campo id

Anteriormente hemos hablado que el campo `id` es como el DNI del registro. Por ello, aunque se puede, no debemos modificarlo, nos puede dar muchos problemas.

{% embed url="https://www.youtube.com/watch?v=Gofz_fiOqHw" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-4-4-sql-update)

## Sintaxis de UPDATE en Node JS y Better SQLite 3

Antes de modificar uno o varios registros desde Node JS, deberíamos seguir los pasos que hemos aprendido para trabajar con **Better SQLite 3**:

1. **Instalar Better SQLite 3** en el proyecto con `npm install better-sqlite3`.
1. **Importar Better SQLite 3** en el proyecto con `const Database = require('better-sqlite3');`.
1. **Iniciar y configurar la base de datos** con `const db = new Database('./src/database.db' });`.

Una vez hecho esto ya podemos añadir nuevos registros. La forma de trabajar es igual que con `SELECT`:

```js
// preparamos la query
const query = db.prepare(`UPDATE users SET email = ?, password = ? WHERE id = ?`);
// ejecutamos la query
const result = query.run('sofia.garcia@yahoo.com', 'abcdefgh', 3);
```

Normalmente nuestras queries las haremos desde dentro de un endpoint de Express JS. Por ello el código sería:

```js
app.post('/users', (req, res) => {
  const query = db.prepare(`UPDATE users SET email = ?, password = ? WHERE id = ?`);
  const result = query.run('sofia.garcia@yahoo.com', 'abcdefgh', 3);
  res.json(result);
});
```

Normalmente el email y contraseña nos lo van a enviar desde el navegador con un `fetch` por ello el código sería algo como:

```js
app.post('/users', (req, res) => {
  const query = db.prepare(`UPDATE users SET email = ?, password = ? WHERE id = ?`);
  const result = query.run(req.body.email, req.body.password, req.body.id);
  console.log(result);
  res.json(result);
});
```

### query.run()

En estas queries no estamos leyendo datos de la tabla, por ello no utilizamos `query.all()` ni `query.get()`. En esta query utilizamos `query.run()` porque lo que queremos es modificar registros. Los creadores de Better SQLite 3 han elegido esta forma de trabajar porque les ha apetecido, pero si lo piensas tiene bastante sentido.

### Información retornada por query.run()

Cuando ejecutamos una query de actualización, a veces nos interesa saber cuántos registros se han modificado.

La información retornada por `query.run()` en el código anterior la estamos consoleando. Por ello el console mostrará:

```json
{
  "changes": 1, // se ha cambiado o añadido un registro
  "lastInsertRowid": 0 // no se ha añadido ningún registro nuevo
}
```

{% embed url="https://www.youtube.com/watch?v=jQH3j5huZSY" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-4-4-sql-update)