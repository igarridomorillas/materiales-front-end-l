# Instalación de SQLite

- Ya sabemos que hay muchos subtipos de SQL. En Adalab vamos a usar SQLite que está pensado para bases de datos pequeñas.
- Te pedimos que te descargues e instales SQLite para que puedas practicar mientras explicamos las siguientes lecciones.
- Lo primero que tenemos que hacer es descargar (poner las instrucciones para descargar desde Ubuntu).

# Nuestra primera base de datos

- Partiendo del ejercicio intro a SQL vamos a ver cómo funciona
- Ya tenemos instalado SQLite Browser
- Tengo aquí preparado un ejercicio
   - Con este ejercicio vamos a gestionar una base de datos de usuarios registrados
   - Creo una base de datos
      - Creo la tabla
      - Creo los campos
         - Añadimos el id, más tarde explicaremos lo que es, más tarde explicaremos los que son el resto de campos de la configuración
         - Añadimos los campos y el tipo
      - Aquí puedo ver los registros que tiene la base de datos
      - Puedo añadir uno
      - Después de hacer cualquier cambio tengo que guardar
   - Por cierto la tabla sqlite_sequence es una tabla especial que necesita la base de datos para hacer sus cosas.
      - Debemos ignorarla y no modificarla nunca.
   - Navegador
      - Con este formulario enviamos un email y contraseña al servidor
   - Servidor
      - Así se configura la base de datos
         - Indicamos el fichero donde está la base de datos
         - Indicamos `verbose: console.log para que todas las llamadas que se hagan a la base de datos se muestren en consola
      - Con el endpoint
         - Obtenemos la fecha actual
         - Obtenemos los datos de la petición
         - Insertamos un nuevo registro en base de datos con la fecha, el email y el password
   - Hacemos una prueba
      - Vemos que se ha creado
- Como véis las tablas de SQL son como tablas de Excel
- En seguida veremos que se pueden crear muchas tablas dentro de una base de datos