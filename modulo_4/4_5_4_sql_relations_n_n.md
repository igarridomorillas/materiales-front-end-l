# Relaciones N a N

Las relaciones N a N relacionan varios registros de una tabla de base de datos con varios registros de otra tabla.

Una relación N a N se produce cuando un registro de la tabla A puede estar relacionado con varios registros de la tabla B, y a su vez un registro de la tabla B puede estar relacionado con varios registros de la tabla A.

Si pensamos en una tienda virtual la relación entre productos y pedidos es la siguiente:

- ¿Un producto puede estar en varios pedidos? Sí, muchas personas pueden comprar el mismo producto. Esto es una relación 1 a N.
- ¿Un pedido puede tener varios productos? Sí, una persona en un solo pedido puede comprar varios productos. Esto es otra relación 1 a N.

**Como los pedidos y los productos están relacionados por dos relaciones 1 a N, significa que su relación es N a N.**

Vamos a verlo con un ejercicio de verdad:

{% embed url="https://www.youtube.com/watch?v=j_8GJLentuQ" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-5-4-sql-relations-n-n)

## Ejercicios

### 1. Multi-categorías de libros

En el ejercicio 1 de la lección **Relaciones 1 a N** hemos creado una tabla para categorías de los libros. Hemos puesto la condición de que un libro solo puede pertenecer a una categoría. Ahora vamos a hacer el mismo ejercicio pero:

- Haciendo que un libro tenga una categoría principal.
- Permitiendo que un libro pertenezca a varias categorías secundarias.

Si un libro puede pertenecer a muchas categorías secundarias y una categoría secundaria puede tener muchos libros significa que ahora la relación entre los libros y las categorías es de N a N.

Partiendo del ejericio 1 de la lección **Relaciones 1 a N** vamos a empezar por crear la categoría principal:

1. Seguramente en la tabla `books` habías puesto una columna llamada `categoryId` o algo por el estilo. Cambia el nombre de esta columna por `mainCategoryId`.
   - Con este simple cambio estamos diciendo que la relación entre un libro y su categoría principal es 1 a N.

Ahora vamos a crear las multicategorías secundarias:

1. Crea una nueva tabla llamada `secondaryCategories`:
   - Debe tener una columna para indicar el id del libro.
   - Debe tener otra columna para indicar el id de la categoría, el que hemos puesto en la tabla `categories`.
1. Añade datos a mano a través de SQLite a la tabla `secondaryCategories` para que el libro con `id` pertenezca a las categorías secundarias **Novela** e **Historia**.

Ahora vamos a crear un endpoint que devuelva la información de un libro con sus datos, su categoría principal y sus categorías secundarias.

1. Crea un endpoint en tu API para devolver toda la info de un libro. Este endpoint debe:
   - Set de tipo `GET`.
   - Recibir el `id` del libro por URL params.
   - Devolver un objeto del tipo:
   ```json
   {
     "title": "Don Quijote de la Mancha",
     "author": "Miguel de Cervantes",
     "price": 10,
     "mainCategoryId": 2,
     "mainCategoryName": "Novela",
     "secondaryCategories" [
       {
         "name": "Historia"
       },
       {
         "name": "Novela"
       }
     ]
   }
   ```

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.