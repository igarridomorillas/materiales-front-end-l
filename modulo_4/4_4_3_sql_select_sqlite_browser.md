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
```

`SELECT` y `FROM` son palabras obligatorias al hacer una query de lectura.

### WHERE

Con `WHERE` indicamos una condición que debe cumplir el registro (o fila) para poder leerlo. Sería como hacer `filter` o un `if` de JavaScript:

```sql
-- Seleccionar todas las columnas de todas las usuarias cuyo id sea mayor o igual que 2
SELECT * FROM users WHERE id >= 2
```

```sql
-- Seleccionar todas las columnas de la usuaria cuyo id sea igual a 2, esto nos devolverá solo un registro
SELECT * FROM users WHERE id = 2
```

```sql
-- Seleccionar todas las columnas de la usuaria cuyo email sea lucia@hotmail.com
SELECT * FROM users WHERE email = 'lucia@hotmail.com'
```

```sql
-- Seleccionar todas las columnas de la usuaria cuyo email sea lucia@hotmail.com y el password sea qwertyui
SELECT * FROM users WHERE email = 'lucia@hotmail.com' AND password = 'qwertyui'
```

`WHERE` no es obligatorio al hacer una query de lectura.

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

`ORDER BY` no es obligatorio al hacer una query de lectura.

### LIMIT

Con `LIMIT` indicamos el **número máximo de registros** que queremos leer:

```sql
-- Seleccionar todas las columnas de un máximo de 2 usuarias
SELECT * FROM users LIMIT 2
```

`LIMIT` no es obligatorio al hacer una query de lectura.

### Conclusiones de la sintaxis de SQL

- Vídeo
  - Hacer todas estas queries en SQLite Browser

Nuestro trabajo cuando leemos datos de una tabla es combinar `SELECT`, `FROM`, `WHERE`, `ORDER BY` y `LIMIT` para obtener los datos que queremos.

**Mayúsculas vs minúsuculas:** normalmente escribimos en **mayúsculas** las palabras `SELECT`, `FROM`, `WHERE`, `ORDER BY`, `LIMIT` y otras que aprenderemos en próximas lecciones **porque son palabras del lenguaje SQL**. Y escribimos en **minúsculas (o camelCase) las columnas y los nombres de las tablas**. De esta forma es más fácil leer una query.

**Comentarios:** todos los lenguajes de programación tiene caracteres para indicar comentarios. En JS ponemos `// mi comentario` o `/* mi comentario */`. En SQL los comentarios se ponen con dos guiones `--` al principio de la query.

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
-- Seleccionar todas las columnas de todas las usuarias cuyo email sea de gmail
SELECT * FROM users WHERE email LIKE '%gmail%'
```

Cada vez que tengas que hacer una query y no sepas cómo tienes dos opciones:

- Hacer una query genérica que te devuelva muchos datos y luego filtrar o buscar en Node JS hasta encontrar el dato que buscas. Esto no es recomendable ya que requiere más líneas de código y siempre va a ser un proceso más lento.
- Buscar en Internet cómo hacerlo. Seguramente SQL tenga opciones para hacer lo que quieres. Usar las opciones que nos da SQL nos permite:
   - Hacer queries más rápidas, que ya SQL está pensado para ello.
   - Aprender una cosa nueva sobre SQL.