# Cebolla

- Hemos refactorizado el código para enseñar cómo se debe organizar
- Enseñar el código
- Está index.js
   - Que se comunican hacia el interior para configurar el servidor
- Están las capas de lógica de negocio:
   - Que se comunican hacia el interior para pedir datos
- Están las capas de datos:
   - Que se comunican para pedir y modificar los datos
   - Ellos saben cómo son los datos, dónde están guardados...

# SQL

1. Qué es un base de datos
   1. Dónde se ejecuta
   1. Dónde guarda los datos
1. Hay dos grandes tipos de bases de datos
   1. MongoDb: que guarda JSON.
   1. SQL: donde se guardan tablas.
   1. Nosotras vamos a aprender SQL.
   1. Todo lo que huela a SQL es lo mismo: mySQL, SQLite

# SQLite browser

1. Dentro de SQL hay varios tipos de datos, y todas tienen su interfaz gráfico y su forma de acceder desde Node.
1. Todas las bases de datos se gestionan de dos formas: a través de un programa con una interfaz gráfica y a través de programación.
   1. Nosotras seguimos estos pasos, primero creamos y configuramos la base de datos a través de SQLite Browser y luego modificamos los datos desde Node.
1. Descargo e instalo SQLite browser
   1. Hay programas para gestionar la base con un interfaz gráfica
   1. Y también se gestionar desde Node JS.
   1. Abro el programa
1. Abro la base de datos del ejercicio
   1. Las pestañas importantes son Estructura y Hojas de estilo
   1. Estas son mis tablas. sqlite_sequence es una tabla interna, no la debemos tocar.
   1. En estructura puedo configurar los campos de las tablas y los tipos de datos.
   1. En Hoja de datos están los datos que hay ahora mismo en la base de datos.
   1. Si cambio un dato de productos, se cambia en la web.
   1. Tengo que pulsar Guardar cambios.
   1. Compararlo con el JSON
1. Vanos a ver el ejemplo de productos
   1. Creo la tabla products
      1. Creo la estructura
      1. Añado los primeros datos
1. Explicar la configuración de las tablas
   1. Autoincrement
   1. Primary key

# SQLite en el código

1. Ahora vamos a programar
   1. Busco un npm que me encaje, encuentro better-sqlite3
   1. Instalo better-sqlite3 en el proyecto
   1. Miro la documentación
   1. Puede haber muchas bases de datos, a Node le tengo que decir cómo conectarse con una de ellas
   1. Veo que para conectar la base de datos con Node tengo que poner esto
1. SELECT * FROM products: selecciono todos los productos
   1. Como son más de una línea llamo a all. Esto lo explicaremos más adelante.
   1. Esto me devuelve un array
   1. Ya tengo los datos y hago con ellos lo que quiero
   1. Cambiar orden de los productos


# SQL 2

Repetir el tema de: primary key, autoincrement, unique

1. Estructura cebolla:
   1. Como el ejercicio está organizado así se puede cambiar una capa sin que las demás se enteren
   1. Solo vamos a cambiar ficheros de la capa data/
1. Sintaxis de SQL:
   1. SELECT
   1. DELETE
   1. INSERT INTO
   1. UPDATE table SET column1 = value1
   1. WHERE
   1. ORDER BY
   1. LIMIT
1. Sintaxis de Better SQLite 3
   1. A esto se le llama query
   1. La sintaxis de prepare: significa que vamos a hacer una consulta a base de datos
   1. Ejecutamos la consulta con:
      1. Get: devuelve una fila en un objeto
      1. All: devuelve varias filas en un array de objetos
      1. Run: ejecuta consultas que no devuelven datos, que los añaden o borran
1. Puedo borrar los JSON porque ya no se usan
1. SQLite se utiliza para proyectos pequeños
   1. Normalmente se utiliza mySQL
   1. La forma de conectarnos es diferente
   1. La forma de leer y escribir datos es igual
