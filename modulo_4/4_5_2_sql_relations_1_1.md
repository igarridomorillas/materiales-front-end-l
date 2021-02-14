
# SQL: Relaciones 1 a 1

- Ahora que ya sabemos cómo hacer relaciones 1 a N vamos a explicar las relaciones 1 a 1
- Si yo quiero guardar en la base de datos mucha información sobre un usuario lo lógico sería añadir muchos campos a la tabla
- Por ejemplo si quiero saber si un usuario es premium, cuánto ha pagado por ser premium, desde cuándo lo es y hasta cuando lo va a ser lo que puedo hacer es añadir más campos o columnas a la tabla users.
- Si además quiero guardar si un usuario quiere recibir nuestra newsletter, si quiere recibir info sobre nuevos productos y / o nuevas promociones, y cada cuanto tiempo quiere recibir la newsletter lo que también haré será añadir más campos a la base de datos users.
- El problema es que cuando tenemos muchas cosas que guardar, la tabla users puede crecer hasta el infinito.
- La solución es separar la tabla users en otras tablas.
- Las llamo userYLoQueSea
- Las relaciono con el userId, y así sé que el usuario X ha decicido recibir notificaciones y si es un usuario premium
- Las ventajas de dividir una tabla grande en varias tablas pequeñas es que guardamos menos info, porque si un usuario no es premium no va a tener su correspondiente registro en la tabla premium
- Para SQL es más fácil escribir, leer y buscar si las tablas son pequeñas a si son grandes.