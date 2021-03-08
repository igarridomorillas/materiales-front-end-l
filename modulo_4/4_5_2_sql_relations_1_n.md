# Relaciones 1 a N

## Múltiples tablas de una base de datos

Lo normal es tener **muchas tablas dentro de una base de datos** porque queremos guardar muchos tipos de información.

Por ejemplo en una tienda virtual vamos a tener una base de datos con **una tabla para cada tipo de información**:

- Una tabla para los usuarios registrados.
- Una tabla para los productos.
- Una tabla para los pedidos.
- Una tabla para las direcciones de entrega de los pedidos.
- ...

Cada tipo de información lo creamos en una tabla diferente con sus diferentes campos.

**A estos tipos de información les llamamos entidades o entities.** Una tabla guarda entidades del mismo tipo, por ejemplo usuarios. Y **cada columna define las características de una entidad**, como el nombre, email, password... del usuario.

## Relaciones entre los registros de dos tablas

Una base de datos suele tener muchas tablas. A menudo nos interesa **relacionar unos registros de una tabla con los registros de otra tabla**.

Por ejemplo en una tienda virtual tenemos una tabla para almacenar las diferentes direcciones de entrega donde se deben enviar los pedidos. Pero necesitamos saber qué dirección de entrega pertenece a un usuario concreto. **Por ello en la tabla de direcciones de entrega tendremos un campo llamado `userId` que indicará a qué usuaria pertenece una dirección de entrega.**

Para relacionar los registros vamos a usar los campos `id`, `userId`... ya que son identificadores únicos que nunca van a cambiar.

**Por este motivo SQL se define como una base de datos relacional.**

## Relaciones 1 a N

En siguientes lecciones explicaremos las relaciones 1 a 1 y las relaciones N a N. Ahora vamos a empezar por explicar las relaciones 1 a N que son las más fáciles de entender:

{% embed url="https://www.youtube.com/watch?v=gokEW7ivt1s" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-5-2-sql-relations-1-n)

**Las relaciones 1 a N son aquellas relacionan un registro de una tabla con varios registros de otra tabla.**

En este caso estamos relacionando una usuaria de la tabla `users` con N direcciones de la tabla `addresses`.