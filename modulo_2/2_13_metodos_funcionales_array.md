# Métodos funcionales de array

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)
- [EJERCICIO 8](#ejercicio-8)
- [EJERCICIO 9](#ejercicio-9)
- [EJERCICIO 10](#ejercicio-10)
- [EJERCICIO 11](#ejercicio-11)
- [EJERCICIO 12](#ejercicio-12)

<!-- /TOC -->

## Introducción

En esta sesión vamos a ver cómo trabajar con arrays de forma eficiente en JavaScript. Hasta ahora hemos trabajado con arrays y conocemos algunos métodos del objeto array, como `push` para meter nuevos elementos en el array
o `join` para unir todos los elementos de un array en una cadena. Y cuando queremos acceder todos los elementos de un array, usamos un bucle para recorrerlo. Pero en esta sesión vamos a aprender a realizar acciones con varios elementos de un array pero sin necesidad de bucles, usando los denominados _métodos funcionales_ de array. Se llaman métodos funcionales porque están alineados con una forma de programar que da mucha importancia a las funciones... ¡nuestras amigas las funciones!

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Usar los métodos funcionales de array nos sirve para poder operar con los valores contenidos en un array de una forma elegante a la vez que fácil de leer.

## ¿En qué casos se utiliza?

Los métodos funcionales de array pueden ser utilizados en cualquier aplicación que trabaje con arrays, y es muy usado en entornos concretos como React, una tecnología que veremos más adelante en el curso.

Con estos métodos funcionales podemos realizar las mismas acciones para las que necesitaríamos un bucle, por ejemplo:

- buscar un elemento en un array
- sumar los elementos de un array
- aplicar una transformación a todos los elementos de un array
- filtrar los elementos de un array, es decir, quedarnos sólo con los que cumplen un criterio
- ordenar los elementos de un array según un criterio

## Métodos funcionales de array

Vamos a ver algunos de estos métodos y descubriremos su utilidad usando ejemplos de ejercicios que ya hemos hecho en el pasado pero ahora con métodos funcionales.

### map

El método `map` nos permite aplicar una función a todos los elementos de un array y devuelve otro array de la misma longitud con los resultados de aplicar esa función sobre cada elemento.

Vamos a ver cómo usarlo. [En este ejemplo en codepen](https://codepen.io/adalab/pen/wppeQx?editors=0011), partimos de un array con nombres `names` y queremos obtener otro array con los nombres en mayúscula `capitalNames`:

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const capitalNames = [];

for (let i = 0; i < names.length; i++) {
  const capitalName = names[i].toUpperCase();
  capitalNames.push(capitalName);
}

console.log(capitalNames);
```

En el bucle, simplemente llamamos a la función `toUpperCase` sobre cada elemento del array de forma que la cadena se convierte en mayúsculas. Después, sólo metemos el resultado en un nuevo array al que hemos llamado `capitalNames`, usando `push`.

Ahora vamos a ver cómo [realizar esto mismo usando `map`](https://codepen.io/adalab/pen/gooREe?editors=0011):

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const capitalNames = names.map(name => name.toUpperCase());

console.log(capitalNames);
```

En este caso ejecutamos el método `map` sobre el array de nombres `names`. A `map` le pasamos un único parámetro que es una función que se va a aplicar sobre cada elemento del array. Esta función (que hemos decidido hacer con una `arrow function`) toma como parámetro el elemento del array, al que hemos llamado `name`. Nosotros no ejecutamos esta función, sino que solo se la pasamos como parámetro a `map`, justo de la misma forma que hacíamos con los callbacks, y será `map` quien la ejecute pasándoles como argumento cada elemento del array. Dentro de la función tenemos el elemento del array (el nombre, por ejemplo, en primer lugar 'María') sobre el que ejecutamos directamente el método `toUppercase` (pasar a mayúscula). Devolvemos (con un `return` implícito) el resultado para que pase al array de resultados `capitalNames`. En este caso nosotros no hemos tenido que crear el array `capitalNames` a mano sino que `map` lo crea directamente porque así es como funciona: devuelve un array del mismo tamaño que el original con el resultado de aplicar una función a cada elemento del array.

> **NOTA**: es importante recordar que el array resultante de aplicar map va a ser siempre de la misma longitud que el array original.

Es importante recordar que el único argumento que recibe la función `map` (al igual que resto de funciones que vamos a ver hoy) es una función. Y para que se entienda perfectamente vamos a rehacer el ejemplo anterior sustiyendo el código `name => name.toUpperCase()` por la función `getUperCaseName`:

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const getUperCaseName = name => name.toUpperCase();
const capitalNames = names.map(getUperCaseName);

console.log(capitalNames);
```

¿Qué argumento recibe `map`?

#### EJERCICIO 1

**Inflar las notas**

¡Ya tenemos las notas del examen! Los profes, como somos así, las hemos metido en un array: `const marks = [5, 4, 6, 7, 9];`. Casi todo el mundo lo ha hecho bastante bien pero... vamos a hacer un poco de trampa de la buena :) Vamos a modificar las notas de todas para añadirles 1 punto, ¿no? Pues usemos nuestro reciente amigo `map` para crear un nuevo array `inflatedMarks` con las notas modificadas. Finalmente, mostraremos en la consola las notas modificadas para ver que funciona correctamente. ¡Al lío!

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

**Saludar es de buena educación**

Estamos creando una aplicación web, y lo primero que queremos hacer es saludar al usuario por su nombre, ¡como es debido! Tenemos un array con el listado de usuarios de nuestra aplicación `const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];` y queremos conseguir otro array con los saludos, por ejemplo, _'Bienvenida Yolanda'_. ¿Podríamos usar `map` para que nos echase una mano?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

**Gracias por confiar en nosotros**

Seguimos desarrollando nuestra aplicación web que romperá el mercado. Pero antes, queremos agradecer a nuestros usuarios premium (de pago) su ayuda en el saludo de la aplicación. Por tanto, a los usuarios premium queremos saludarles así _'Bienvenida Yolanda. Gracias por confiar en nosotros.'_, y mantener el saludo simple _'Bienvenida Yolanda'_ para el resto de usuarios.

Vamos a partir de este array con el listado de usuarios que incluye tanto su nombre como si son usuarios premium o no.

Tenemos que crear un nuevo array con los saludos. ¿Podremos hacerlo con `map`?

```js
const users = [
  { name: 'María', isPremium: false },
  { name: 'Lucía', isPremium: true },
  { name: 'Susana', isPremium: true },
  { name: 'Rocío', isPremium: false },
  { name: 'Inmaculada', isPremium: false }
];
```

\_\_\_\_\_\_\_\_\_\_

### filter

El siguiente método funcional que vamos a ver es `filter`. `filter` nos ayuda a, como su propio nombre indica, filtrar un array y elegir algunos de sus elementos dado un criterio. La forma de uso es muy parecida a `map` ya que toma como único argumento una función que se aplica sobre cada elemento del array. Si al ejecutar la función sobre un elemento esa función devuelve `true` el elemento se mantiene en el array de resultados, pero si es `false`, no se meterá. Por tanto, el array que crea `filter` siempre va a tener una longitud igual o menor que el original: va a tener como máximo los elementos del original y como mínimo estará vacío.

[Partimos de un ejemplo](https://codepen.io/adalab/pen/vppJVQ?editors=0011) en el que, dado un listado de nombres queremos quedarnos solo con los que tienen más de 5 letras, es decir, 6 o más. Primero vamos a solucionarlo con un bucle:

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const longNames = [];

for (const name of names) {
  const nameLength = name.length; // ¡Sí, podemos usar .length con strings para saber su longitud!
  if (nameLength > 5) {
    longNames.push(name);
  }
}

console.log(longNames);
```

Como en el caso del `map` recorremos el array usando un bucle y hemos creado un array `longNames` para almacenar el resultado. Dentro del bucle accedemos a la longitud del nombre con la propiedad `length`. Después lo comparamos con 5: si es mayor lo metemos en el array de resultados, pero si no lo es pues no lo metemos.

Ahora vamos a realizar [este mismo ejemplo con `filter`](https://codepen.io/adalab/pen/PEEKVr?editors=0011):

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const longNames = names.filter(name => name.length > 5);

console.log(longNames);
```

En este caso hemos ejecutado el método `filter` sobre el array `names` y le pasamos como parámetro una función que es la que se ejecuta sobre cada elemento del array. Esta función (anónima) define un parámetro que hemos llamado `name` que representa el elemento del array, por ejemplo, 'María'. Dentro de la función comparamos la longitud (`length`) del nombre con 5, y devolvemos el resultado de esa comparación. Es decir, devolvemos `true` (si la longitud del nombre es mayor que 5) o `false` (si no lo es).

> **NOTA**: El return siempre deberá devolver un booleano o una operación que devuelva un valor de este tipo, por ejemplo, `3 < 4` o `'hola' === 'adios'`.

#### EJERCICIO 4

**Solo los premium**

Seguimos con nuestra app de moda y vamos a utilizar el listado de usuarios del ejercicio 3. Pero ahora queremos tener un listado de usuarios (en un array `premiumUsers`) que solo tenga los usuarios premium. ¿Sabremos hacerlo con `filter`?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 5

**Los pares pueden entrar**

Tenemos un listado de las contraseñas (PIN de 4 números) de los usuarios de nuestra web:

```js
const pins = [2389, 2384, 2837, 5232, 8998];
```

De ese listado de contraseñas, queremos que solo puedan entrar los que han elegido una contraseña que es un número par para hacer [A/B testing](https://es.wikipedia.org/wiki/Test_A/B). ¿Nos ayudas a encontrar las contraseñas usando `filter`?

> PISTA: Recuerda que el resto de la división entera (módulo `%`) de número par es 0.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

**Los usuarios que pueden entrar**

Ya hemos conseguido las contraseñas pertenecientes a cada usuario. ¿Podrías darnos un array con los usuarios que pueden acceder a la aplicación, es decir, los que tienen como PIN un número par?

```js
const users = [
  { name: 'María', isPremium: false, pin: 2389 },
  { name: 'Lucía', isPremium: true, pin: 2384 },
  { name: 'Susana', isPremium: true, pin: 2837 },
  { name: 'Rocío', isPremium: false, pin: 5232 },
  { name: 'Inmaculada', isPremium: false, pin: 8998 }
];
```

\_\_\_\_\_\_\_\_\_\_

### reduce

El método `reduce` es un método funcional complejo que nos permite realizar cálculos o acciones que requieran utilizar varios elementos de un array. A diferencia de `map` o `filter` el resultado de `reduce` no es un array sino un valor del tipo que queramos. Se basa en aplicar una función a todos los elementos de un array (como las anteriores) y se va trabajando con resultados parciales hasta que se llega al resultado final. Se usa cuando queremos obtener un resultado que depende de varios de los elementos del array, por ejemplo, calcular la media de un listado de números.

Vamos a empezar con un ejemplo de la sesión sobre arrays que calcula la suma de un listado de números:

```js
const scores = [4, 2, 7, 8, 6, 7, 9, 1, 2, 6, 7];
let result = 0;

for (let i = 0; i < scores.length; i++) {
  result += scores[i];
}

console.log(result);
```

En la variable `result`, que comienza siendo 0, vamos acumulando la suma de todos los números del array accediendo a cada uno como `scores[i]` dentro del bucle.

Vamos a ver cómo haríamos este mismo ejemplo con `reduce`:

```js
const scores = [4, 2, 7, 8, 6, 7, 9, 1, 2, 6, 7];

const result = scores.reduce((acc, number) => acc + number, 0);

console.log(result);
```

En este caso ejecutamos el método `reduce` sobre el array `scores` y le pasamos como parámetros 1) una función y 2) un valor inicial.

1. La función se ejecuta por cada elemento del array y toma como parámetros: a) un _acumulador_ `acc`, que acumula el resultado de un elemento al siguiente; y b) el elemento del array, por ejemplo, en la primera vuelta será el de índice 0 cuyo valor es 4.

2. El segundo parámetro, en este caso `0`, es el valor inicial del acumulador.

La función lo que hace es sumar al acumulador el valor del número actual y devuelve el resultado y ese mismo resultado se convierte en el acumulador del siguiente paso. Vamos a ver cómo funciona internamente:

1. Se ejecuta la función sobre el primer valor del array (`4`) que tiene como argumentos `acc` con valor 0 (valor inicial que hemos pasado al acumulador) y `number`que es 4, y devuelve la suma `4 + 0` que es 4 y se convierte en el valor del acumulador.
2. Para el segundo valor, los argumentos son `acc` que vale 4 y `number` que es 2, y devuelve la suma que es 6 y será el valor del acumulador en el siguiente paso
3. La función toma como argumentos `acc=6` y `number=7` y devuelve 13
4. Y así sucesivamente hasta llegar al último elemento del array, que sumará al acumulado 7 y devolverá el resultado final, que es la suma de todos los números del array (59).

> NOTA: el segundo parámetro de `reduce` (el valor del acumulador) es opcional y si no lo pasamos se toma como valor inicial el primer elemento del array. En nuestro ejemplo anterior sería válido no indicar segundo parámetro y comenzaríamos a aplicar la función a partir del segundo elemento (en el caso anterior el `2`) que toma como acumulador el primero (en el caso anterior el `4`).

```js
const result = scores.reduce((acc, number) => acc + number);
```

Esta forma de trabajar es bastante compleja y requiere de mucha práctica, así que vamos a practicar realizando unos ejercicios.

#### EJERCICIO 7

**La media de la carrera**

Hemos organizado una carrera de escobas para que podáis exprimir a fondo vuestra flamante Nimbus 2000. Tenemos los tiempos en este array y nos gustaría conocer la media: ¿nos ayudas a calcularla usando `reduce`?

```js
const times = [56, 9, 45, 28, 35];
```

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 8

**El ganador de la carrera**

Ya hemos conseguido los nombres de los competidores y nos gustaría que usases `reduce` para averiguar quién ha ganado.

> PISTA: en este caso el acumulador puede ser no sólo un número sino cualquier valor. Por ejemplo un objeto que sea nuestro candidato a ganador :)

```js
const runners = [
  { name: 'Gregory Goyle', time: 56 },
  { name: 'Nymphadora Tonks', time: 9 },
  { name: 'Luna Lovegood', time: 45 },
  { name: 'Cedric Diggory', time: 28 },
  { name: 'Cho Chang', time: 35 }
];
```

\_\_\_\_\_\_\_\_\_\_

### Estos métodos pueden encadenarse

Dado que el resultado de aplicar `map` y `filter` es un array, querríamos poder encadenar su comportamiento. `reduce` también podemos encadenarlo, pero será normalmente el último ya que su resultado no tiene por qué ser un array. Vamos a ver un [ejemplo en codepen](https://codepen.io/adalab/pen/BqEjzN?editors=0011).

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const longNames = names.filter(name => name.length > 5).map(name => name.toUpperCase());

console.log(longNames);
```

En este caso queremos filtrar los nombres largos pero además obtenerlos en mayúscula. Para eso vamos a, primero filtrar con `filter` por longitud del nombre y luego convertirlos en mayúscula usando `map`.

#### EJERCICIO 9

**El ganador de los estudiantes**

Como en el ejemplo anterior vamos a averiguar quién ha ganado usando `reduce`, pero queremos saber el ganador de los estudiantes, por lo que tendremos que filtrar primero quiénes lo son.

```js
const runners = [
  { name: 'Gregory Goyle', time: 56, student: true },
  { name: 'Nymphadora Tonks', time: 9, student: false },
  { name: 'Luna Lovegood', time: 45, student: true },
  { name: 'Cedric Diggory', time: 28, student: true },
  { name: 'Cho Chang', time: 35, student: true }
];
```

\_\_\_\_\_\_\_\_\_\_

### find y findIndex

`find` nos permite buscar un elemento en un array dada una condición. A diferencia de `filter`, no devuelve un array con los resultados, sino un único elemento: el primero que cumpla la condición que establecemos. Por otro lado, su _compañero_ `findIndex` hace lo mismo pero en vez de devolver el elemento, nos devuelve su índice (posición en el array) que es muy útil si queremos, por ejemplo, borrarlo usando `splice`.

[Partimos de un ejemplo](https://codepen.io/adalab/pen/dLRZBO?editors=0011) en el que, dado un listado de nombres queremos quedarnos con el primero que tenga más de 5 letras, es decir, 6 o más. Primero vamos a solucionarlo con un bucle:

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
let longName;

for (const name of names) {
  const nameLength = name.length;
  if (nameLength > 5 && longName === undefined) {
    longName = name;
  }
}

console.log(longName);
```

Recorremos el array usando un bucle y hemos creado una variable `longName` para almacenar el resultado. Dentro del bucle comparamos la longitud del nombre con 5 y además comprobamos que la variable `longName` no esté aún definida para asegurarnos que es el primer nombre que cumple esta. Si se cumplen ambas condiciones metemos el nombre en la variable de resultados, y así el resto de nombre que sean más largos de 5 letras no se guardarán porque `longName` ya está definido (no es `undefined`).

Ahora vamos a realizar [este mismo ejemplo con `find`](https://codepen.io/adalab/pen/NmgXvo?editors=0011):

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const longName = names.find(name => name.length > 5);

console.log(longName);
```

Igual que en el caso de `map` y `filter`, al método `find` de array le pasamos como parámetro una función que es la que se ejecuta sobre cada elemento del array. En la función comparamos la longitud (`length`) del nombre con 5, y devolvemos el resultado de esa comparación. El primer elemento cuyo resultado de la comparación de como resultado `true` será devuelto por la función y lo recogemos en la variable `longName`.

Ahora vamos a ver [un ejemplo con `findIndex`](https://codepen.io/adalab/pen/WWOdzB?editors=0011):

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];
const index = names.findIndex(name => name.length > 5);

console.log(index);
```

En este caso el resultado es 2 porque es el índice del array del primer nombre con más de 5 letras (Susana).

#### EJERCICIO 10

**Encuentra el usuario**

a) En nuestra aplicación de gestión de usuarios, nos ha llegado una incidencia asociada al PIN 5232. ¿Podrías encontrar el usuario que corresponde a ese PIN para poder contactarle? Usa el método `find` para conseguirlo.

```js
const users = [
  { name: 'María', isPremium: false, pin: 2389 },
  { name: 'Lucía', isPremium: true, pin: 2384 },
  { name: 'Susana', isPremium: true, pin: 2837 },
  { name: 'Rocío', isPremium: false, pin: 5232 },
  { name: 'Inmaculada', isPremium: false, pin: 8998 }
];
```

b) Resulta que el usuario se ha dado de baja por la incidencia :( ¿Podrías borrarlo del array de usuarios? Usa el método `findIndex` para encontrar su posición y bórralo usando `splice`.

\_\_\_\_\_\_\_\_\_\_

### BONUS: sort

Para terminar, vamos a ver un último método que nos permite ordenar los elementos de un array. Es diferente de los anteriores en que, en lugar de devolver un nuevo array, modifica directamente el array original. Vamos a ver [algunos ejemplos](https://codepen.io/adalab/pen/jYYzZe?editors=0011).

Para ordenar valores que son cadenas, no es necesario usar ninguna función de ordenación ya que por defecto `sort` ordena los elementos de un array alfabéticamente.

```js
const names = ['María', 'Lucía', 'Susana', 'Rocío', 'Inmaculada'];

names.sort();
console.log(names);
```

Si queremos indicar otro tipo de orden, tendremos que pasar al método `sort` una función que sepa qué hacer para ordenar 2 elementos. Esta función toma 2 parámetros (`a` y `b`) que son 2 elementos cualquiera del array y tenemos que devolver:

- un número negativo si queremos que `a` se posicione antes que `b` en el array
- un número positivo si queremos que `b` se posicione antes que `a` en el array
- cero si queremos se comporten como valores iguales y en la ordenación aparezcan juntos

Vamos a ver un ejemplo de la función de ordenación para ordenar números:

```js
const times = [56, 9, 45, 28, 35];

times.sort((a, b) => a - b);
console.log(times);
```

De esta forma, si un número `a` es mayor que otro `b` el resultado es positivo y `b` se posiciona antes en el resultado. Lo contrario ocurre cuando `a` es menor que `b`. Si son iguales, el resultado es 0 y se quedan como están.

#### EJERCICIO 11

**Clasificación de la carrera**

Volviendo a nuestra carrera de escobas, queremos tener el array del ejercicio 8 ordenado para poder tener una clasificación de la carrera: ¿nos ayudar a hacerlo usando `sort`?

> PISTA: la función que le pasamos a sort toma como parámetros 2 elementos del array, así que para acceder a una propiedad de un objeto en la función podemos hacerlo con el operador punto (`a.time`), como hemos hecho hasta ahora ;).

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 12

**Poniendo orden en nuestros usuarios**

Vamos a volver al listado de usuarios del ejercicio 6, porque nos ha dado la manía de tenerlos ordenados. ¿Podrías ordenarlos por orden alfabético? ¿Y por su número de PIN?

\_\_\_\_\_\_\_\_\_\_

### Recorriendo las propiedades de un objeto

En algunas ocasiones necesitaremos acceder al listado de propiedades de un objeto, que a priori no sabemos cuáles son. Por ejemplo, nos puede llegar la información de un libro de una petición a un API y queremos pintar en pantalla todas las propiedades que comienzan por 'ds\_'. Para poder hacer esto usamos el método `Object.keys` que nos devuelve el listado de las propiedades de un objeto en un array.

```js
const book = {
  title: 'Harry Potter and the Deathly Hallows',
  ds_title: 'Harry Potter 7',
  author: 'J. K. Rowling',
  ds_author: 'Rowling',
  ...
};

const keys = Object.keys(book);
console.log(keys); //['title', 'ds_title', 'author', 'ds_author', ...]
```

## Recursos externos

- [Array `map` en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [Array `filter` en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [Array `reduce` en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
- [Array `find` en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [Array `findIndex` en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findindex)
- [Array `sort` en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
- [`Object.keys` en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
