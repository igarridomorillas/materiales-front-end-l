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
