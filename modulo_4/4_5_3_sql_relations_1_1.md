# Relaciones 1 a 1

SQL es una base de datos relacional. Lo que nos permite **relacionar registros de una tabla con los registros de otra tabla**.

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

Pues con las tablas vamos a hacer lo mismo, **vamos a dividir una tabla grande en otras tablas más pequeñas**. Normalmente solemos trabajar en una única tabla y cuando vemos que crece mucho es cuando tomamos la decisión de dividirla en tablas más pequeñas.

Siguiendo el ejemplo de la tabla `users` de la tienda virtual de arriba podríamos dividirla en las siguientes tablas:

- `users`: con datos de identificación o acceso de los usuarios.
- `usersPremium`: Datos relativos a si el usuario es premium.
- `usersType`: Datos relativos al tipo de usuario por su volumen de compras.
- `usersNotifications`: Notificaciones.
- `usersNewsletters`: Datos relativos a la newsletter.

Y ahora que tenemos tablas separadas tenemos que relacionarlas unas con otras. Así que vamos a explicar lo que son las relaciones 1 a 1.

&#10230; &#128250; **Echa un vistazo [a este vídeo sobre cómo hacer relaciones 1 a 1 desde Node JS
](https://www.youtube.com/watch?v=bwA541uhLHI).**

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-5-3-sql-relations-1-1)

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.