# Borrar registros de una base de datos: DELETE

`DELETE` nos permite **borrar uno o varios registros de una tabla** de la base de datos a través de una query.

Así como leer registros de una tabla no modifica la base de datos, borrar uno o varios registros sí que la modifica.

## Sintaxis de DELETE en SQL y SQLite browser

La sintaxis de un `DELETE` es:

```sql
DELETE FROM nombre_de_la_tabla WHERE condicion_que_cumplen_los_registros_a_borrar
```

Supongamos que tenemos esta tabla llamada `users`:

| id  | email              | password     | name  |
| --- | ------------------ | ------------ | ----- |
| 1   | maria@gmail.com    | 987widJYVxyh | María |
| 2   | lucia@hotmail.com  | qwertyui     | Lucía |
| 3   | sofia@yahoo.com    | mnbvcdfgu    | Sofía |

Con la query:

```sql
-- Borrar un registro indicando indicando el id del registro a borrar
DELETE FROM users WHERE id = 2;
```

La tabla quedará así:

| id  | email              | password     | name  |
| --- | ------------------ | ------------ | ----- |
| 1   | maria@gmail.com    | 987widJYVxyh | María |
| 3   | sofia@yahoo.com    | mnbvcdfgu    | Sofía |

### DELETE sin WHERE igual a muerte, destrucción y caos!!!

Si hacemos una query para borrar registros de una tabla y no indicamos la condición `WHERE` **se borrarán todos los registros de la tabla**. Todos!!! Esto es porque todos los registros cumplen la condición vacía.

La condición `WHERE` no es obligatoria, pero no se nos debe olvidar nunca a no ser que lo que queramos sea vaciar una tabla.

Con `DELETE` y `WHERE` podemos borrar uno o varios registros en una sola query. Todo depende de la condición que pongamos en el `WHERE`.

{% embed url="https://www.youtube.com/watch?v=14qK-nAaMlE" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-4-6-sql-delete)

## Sintaxis de DELETE en Node JS y Better SQLite 3

Antes de borrar un nuevo registro desde Node JS, deberíamos seguir los pasos que hemos aprendido para trabajar con **Better SQLite 3**:

1. **Instalar Better SQLite 3** en el proyecto con `npm install better-sqlite3`.
1. **Importar Better SQLite 3** en el proyecto con `const Database = require('better-sqlite3');`.
1. **Iniciar y configurar la base de datos** con `const db = new Database('./src/database.db' });`.

Una vez hecho esto ya podemos borrar registros. La forma de trabajar es igual que con `SELECT`:

```js
// preparamos la query
const query = db.prepare(`DELETE FROM users WHERE id = ?`);
// ejecutamos la query
const result = query.run(2);
```

Normalmente nuestras queries las haremos desde dentro de un endpoint de Express JS. Por ello el código sería:

```js
app.delete('/users', (req, res) => {
  const query = db.prepare(`DELETE FROM users WHERE id = ?`);
  const result = query.run(2);
  res.json(result);
});
```

Normalmente el `id` nos lo van a enviar desde el navegador con un `fetch` por ello el código sería algo como:

```js
app.delete('/users', (req, res) => {
  const query = db.prepare(`DELETE FROM users WHERE id = ?`);
  const result = query.run(req.body.id);
  console.log(result);
  res.json(result);
});
```

### query.run()

En estas queries no estamos leyendo datos de la tabla, por ello no utilizamos `query.all()` ni `query.get()`. En esta query utilizamos `query.run()` porque lo que queremos es borrar registros. Los creadores de Better SQLite 3 han elegido esta forma de trabajar porque les ha apetecido, pero si lo piensas tiene bastante sentido.

### Información retornada por query.run()

Cuando ejecutamos una query de borrado, a veces nos interesa saber cuántos registros se han borrado.

La información retornada por `query.run()` en el código anterior la estamos consoleando. Por ello el console mostrará:

```json
{
  "changes": 1, // se han modificado o borrado un registro
  "lastInsertRowid": 0 // no se ha añadido ningún registro nuevo
}
```

Si en la tabla no hubiese ningún registro con el `id` 2, `query.run()` nos retornaría:

```json
{
  "changes": 0, // no se ha modificado o borrado ningún registro
  "lastInsertRowid": 0 // no se ha añadido ningún registro nuevo
}
```

Lo que significa que no hemos modificado la tabla de la base de datos.

{% embed url="https://www.youtube.com/watch?v=92F1D59UeB0" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-4-6-sql-delete)
