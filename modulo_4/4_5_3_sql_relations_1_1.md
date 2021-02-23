# Relaciones 1 a 1

SQL es una base de datos relacional. Lo que nos permite relacionar registros de una tabla con los registros de otra tabla.

Supongamos en una tienda virtual tenemos una tabla de usuarios donde guardamos la siguiente información:

- Datos de identificación o acceso de los usuarios:
   - Nombre: texto
   - Email: texto
   - Contraseña: texto
   - Avatar: texto (donde guardamos la URL de la imagen del usuario)
   - Fecha en la que el usuario se registró en la tienda virtual: fecha
- Datos relativos a si el usuario es premium:
   - Usuario premium: booleano
   - Cuota que ha pagado el usuario por ser premium: número
   - Fecha en la que el usuario se dió de alta en la versión premium: fecha
   - Fecha en la que al usuario se le acaba la versión premium: fecha
   - La versión premium se debe autorenovar: booleano
- Datos relativos al tipo de usuario por su volumen de compras
   - Usuario que ha comprado al menos una vez: booleano
   - Usuario recurrente (que compra al menos una vez al mes): booleano
   - Fecha de la última compra: fecha
- Notificaciones:
   - Usuario que quiere recibir avisos por las notificaciones del móvil: booleano
   - Usuario que quiere recibir avisos por email: booleano
- Datos relativos a la newsletter:
   - El usuario está subscrito a la newsletter de productos: booleano
   - El usuario está subscrito a la newsletter de novedades: booleano
   - El usuario está subscrito a la newsletter de nuevas zonas de reparto: booleano
   - Fecha en la que el usuario se dió de alta en la newsletter: fecha
   - Fecha en de la última newsletter que le enviamos al usuario: fecha
   - Otros tipos de newsletters...

Todos estos datos y muchos más podrían estar en la tabla `users` de nuestra base de datos.

Aquí nos surge un problema. Tendríamos la tabla `users` con muchísimas columnas por lo tanto tendríamos una **tabla muy grande**, lo que produce que tengamos más problemas a la hora de trabajar con ella.

Ya sabes que cuando tenemos un fichero de código con muchísimas líneas lo intentamos dividir en ficheros más pequeños, para mejorar la legibilidad, reducir errores, separar responabilidades...

Pues con las tablas vamos a hacer lo mismo, vamos a dividir una tabla grande en otras tablas más pequeñas. Normalmente solemos trabajar en una única tabla y cuando vemos que crece mucho es cuando tomamos la decisión de dividirla en tablas más pequeñas.

Siguiendo el ejemplo de la tabla `users` de la tienda virtual de arriba podríamos dividirla en las siguientes tablas:

- `users`: con datos de identificación o acceso de los usuarios.
- `usersPremium`: Datos relativos a si el usuario es premium.
- `usersType`: Datos relativos al tipo de usuario por su volumen de compras.
- `usersNotifications`: Notificaciones.
- `usersNewsletters`: Datos relativos a la newsletter.

Y ahora que tenemos tablas separadas tenemos que relacionarlas unas con otras. Así que vamos a explicar lo que son las relaciones 1 a 1.

<!-- - Vídeo
  - Ahora que ya sabemos cómo hacer relaciones 1 a N vamos a explicar las relaciones 1 a 1
  - Si yo quiero guardar en la base de datos mucha información sobre un usuario lo lógico sería añadir muchos campos a la tabla
  - Por ejemplo si quiero saber si un usuario es premium, cuánto ha pagado por ser premium, desde cuándo lo es y hasta cuando lo va a ser lo que puedo hacer es añadir más campos o columnas a la tabla users.
  - Si además quiero guardar si un usuario quiere recibir nuestra newsletter, si quiere recibir info sobre nuevos productos y / o nuevas promociones, y cada cuanto tiempo quiere recibir la newsletter lo que también haré será añadir más campos a la base de datos users.
  - El problema es que cuando tenemos muchas cosas que guardar, la tabla users puede crecer hasta el infinito.
  - La solución es separar la tabla users en otras tablas.
  - Las llamo userYLoQueSea
  - Las relaciono con el userId, y así sé que el usuario X ha decicido recibir notificaciones y si es un usuario premium
  - Las ventajas de dividir una tabla grande en varias tablas pequeñas es que guardamos menos info, porque si un usuario no es premium no va a tener su correspondiente registro en la tabla premium
  - Para SQL es más fácil escribir, leer y buscar si las tablas son pequeñas a si son grandes. -->