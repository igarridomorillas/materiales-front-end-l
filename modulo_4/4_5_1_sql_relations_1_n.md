# 5. SQL: Relaciones 1 a N

## Múltiples tablas de una base de datos

Lo normal es tener muchas tablas dentro de una base de datos porque queremos guardar muchos tipos de datos.

Por ejemplo en una tienda virtual vamos a tener una base de datos para los usuarios registrados, otra para los productos, otra para los pedidos, otra para las direcciones de entrega de los pedidos.

Cada tipo de datos lo creamos en una tabla diferente con sus diferentes campos.

## Relaciones entre los registros de las tablas

Una base de datos suele tener muchas tablas. A menudo nos interesa relacionar unos registros de una tabla con los registros de otra tabla.

Por ejemplo en una tienda virtual tenemos una tabla para almacenar las diferentes direcciones de entrega donde se deben enviar los pedidos. Pero necesitamos saber qué dirección de entrega pertenece a un usuario concreto.

Por ello queremos relacionar cada dirección con su usuario.

Para relacionar los registros vamos a usar los campos `id`.

Por este motivo SQL se define como una base de datos relacional.

## Relaciones 1 a N

Vamos a empezar por explicar las relaciones 1 a N que son las más fáciles de entender:

- SQL es una base de datos relacional
   - Esto significa que vamos a tener muchas tablas dentro de nuestra base de datos
   - Cada registro de una tabla se relaciona con otro registro de otra tabla gracias a los ids
- Esta podría ser la base de datos de una tienda online
   - Abrir la tabla usuarios
   - Si yo quiero guardar en base de datos la dirección de entrega del usuario puedo añadir más campos para el país, provincia...
   - Pero y si quiero guardar dos direcciones del usuario o tres o 30
   - No puedo saber cuantas direcciones va a añadir el usuario
   - Por ello lo que hago es crear otra tabla para las direcciones
   - Con el userId indico a qué usuario pertenece esta dirección
   - Así el usuario puede crear tantas direcciones como quiera
   - Así relaciono unas cosas con otras
- Esto es una relación 1 a N porque cada 1 usuario puede tener N direcciones
- Si nos damos cuenta es como si el usuario tuviese un array de direcciones