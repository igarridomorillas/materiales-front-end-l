# Obtener registros de una base de datos: `SELECT`

## Operaciones en una base de datos

Para trabajar con una base de datos podemos hacer 4 operaciones básicas:

- Leer uno o varios registros.
- Añadir un nuevo registro.
- Modificar un registro existente.
- Borrar un registro existente.

A estas operaciones se le llama **CRUD**: create, read, update and delete.

### Consideraciones sobre las operaciones de una base de datos

- La operación de lectura no modifica la base de datos. El resto de operaciones sí.
- **Todas estas operaciones se realizan sobre una única tabla.** Por ahora, si queremos hacer operaciones sobre varias tablas lo tenemos que hacer accediendo de una en una a cada tabla.
- Existen operaciones más complejas pero son combinaciones de estas 4 operaciones básicas.
- Cada vez que accedemos a una base de datos decimos que hacemos una **query o consulta a la base de datos**.

Durante las siguientes lecciones os vamos a enseñar la sintaxis para hacer queries a una base de datos. Os vamos a enseñar la sintaxis de SQL y la sintaxis de SQLite. Hay mínimas diferencias entre ambas sintaxis. La sintaxis de SQL es igual para todas las bases de datos SQL. La sintaxis de SQLite es la que han elegido las programadoras que han creado SQLite.

## Sintaxis de `SELECT`


´SELECT` nos permite seleccionar uno o varios registros de una tabla de la base de datos.




- Explicar sintaxis de SELECT
- Explicar que las consultas las podemos hacer desde SQLite Browser
- Explicar que las consultas las podemos hacer desde Node
  - Instalar SQLiteBetter
  - Configurar la base de datos
- SELECT
  - Hacer una consulta pidiendo todos los registros
- WHERE
- ORDER BY
- LIMIT
- Sintaxis de SQLiteBetter

   1. Ejecutamos la consulta con:
      1. Get: devuelve una fila en un objeto
      1. All: devuelve varias filas en un array de objetos
      1. Run: ejecuta consultas que no devuelven datos, que los añaden o borran


      A esto se le llama query