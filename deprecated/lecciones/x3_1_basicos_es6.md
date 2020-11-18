# Básicos de ES2015 (ES6)

[codepen-string-interpolation]: https://codepen.io/adalab/pen/wpPZvN?editors=0010
[codepen-const]: https://codepen.io/adalab/pen/QaOPwe?editors=0010
[codepen-let-and-scope]: https://codepen.io/adalab/pen/vpWMLr?editors=0010

## Contenidos
- [Introducción](#introducción)
- [¿Para qué sirve lo que vamos a ver en esta sesión?](#¿para-qué-sirve-lo-que-vamos-a-ver-en-esta-sesión)
- [¿Cómo podemos utilizar las novedades de ES2015](#¿cómo-podemos-utilizar-las-novedades-de-es2015)
- [¿En qué casos se utiliza lo que vamos a aprender?](#¿en-qué-casos-se-utiliza-lo-que-vamos-a-aprender)
- [Interpolación de cadenas](#interpolación-de-cadenas)
- [Las variables `let` y `const` y su _scope_](#las-variables-let-y-const-y-su-scope)
- [Bucle `for...of`](#bucle-forof)
- [_Destructuring_](#destructuring)


## Introducción

Hasta el momento hemos visto las bases del lenguaje JavaScript. En esta sesión veremos cómo se escribe JavaScript actualmente, la nueva sintaxis de ES2015 (ES6) y cómo nos permite escribir código más claro y escueto.


## ¿Para qué sirve lo que vamos a ver en esta sesión?

JavaScript se basa en un estándar que se llama ECMAScript. Este estándar reúne las reglas acerca de la sintaxis y el funcionamiento del lenguaje. Hasta ahora todo el código que hemos utilizado, a excepción de las promesas y `fetch`, está recogido en la quinta versión de este estándar, que se conoce como ES5. Hoy veremos algunas de las novedades en la sintaxis y el funcionamiento de la nueva versión, la sexta, llamada ES2015 por el año en que se publicó; también se conoce informalmente con el nombre de ES6, que era el nombre que tenía antes de publicarse.

Entre algunas de las mejoras que ofrece esta nueva versión, destacan la facilidad a la hora de iterar sobre los elementos de un array o un objeto y obtener una propiedad o índice determinado; la mejora a la hora de trabajar con variables y operaciones dentro de cadenas/`string`s; o la posibilidad de crear variables que estén solo disponibles dentro de un bucle `for` o un `if`.

[Harold Abelson](https://es.wikipedia.org/wiki/Hal_Abelson), autor de uno de los libros más famosos de programación, decía: _“Programs must be written for people to read, and only incidentally for machines to execute.”_, que viene a significar algo así como que el código debe escribirse para que las personas puedan leerlo y ya de paso que las máquinas lo ejecuten. Aprendiendo ES6 buscamos en parte esto: esta sintaxis en muchos casos no nos va a permitir hacer nada que no pudiésemos hacer usando otra alternativa, pero la clave aquí es que nos permitirá hacerlo de forma sencilla y que hará que la persona que lee el código pueda entenderlo con facilidad y rapidez.


## ¿Cómo podemos utilizar las novedades de ES2015?

Las últimas versiones de los navegadores web como Chrome incluyen estas funcionalidades, así que se pueden usar desde ya para desarrollar. Sin embargo, cuando hagamos una web para el público, generalmente no debemos dar por hecho que tendrán la última versión de Chrome o Firefox instalada, porque pueden usar otro navegador como Internet Explorer 11, por ejemplo, que no soporta la mayoría de las características de ES6.

Para estos casos, utilizaremos un programa que, al igual que hace Koala para convertir SCSS a CSS, convertirá ES6 a ES5. Este programa se llama [Babel](https://babeljs.io/). De esta forma podremos utilizar las mejoras de ES6 en nuestro código sin preocuparnos de que no funcione en navegadores antiguos.


## ¿En qué casos se utiliza lo que vamos a aprender?

La máxima a la hora de sacar nuevas versiones de JavaScript es _"don't break the Web"_, que significa que no se elimina ni se rompe nada anterior. Por tanto, las distintas versiones de JavaScript son **retrocompatibles** y todo lo que funcionaba con la versión ES5 funciona también con ES2015.

Aunque ES5 sigue funcionando perfectamente, actualmente se escribe en ES6 prácticamente todo el JavaScript nuevo. Hay una gran apuesta por esta versión: lo usan empresas como Cabify, Wallapop, JobandTalent, GitHub, Slack, etc., y una gran variedad de recursos como librerías también se desarrollan así.

En las clases **a partir de ahora escribiremos todo con la nueva sintaxis** y la utilizaremos siempre que sea posible. Cuando salgáis al mercado laboral, muchas de vosotras trabajaréis con esta versión. Como a otras os tocará trabajar con la anterior porque los requisitos del proyecto lo piden, os hemos enseñado ES5 antes de ES6 para que sepáis manejaros con ambas sintaxis, la nueva y la ya existente.


A continuación, vamos a ver algunas de las novedades y posibilidades de la sintaxis. ¡Manos a la obra!


## Interpolación de cadenas

ES6 nos facilita insertar variables y operaciones dentro de cadenas de texto. Para eso escribiremos las cadenas entre acentos graves o _backticks_ (`` `This is a string` ``), en vez de entre comillas, y las expresiones o variables entre `${` y `}` (`${expressionOrVariable}`).

```js
var name = 'Ada';
var surname = 'Lovelace';

console.log(`My name is ${name} ${surname}.`):
// 'My name is Ada Lovelace.'
```

También podemos evaluar operaciones directamente:

```js
var firstItemPrice = 5;
var secondItemPrice = 3;

console.log(`Total amount: ${firstItemPrice + secondItemPrice}€`);
// Total amount: 8€
```

O incluso llamar a funciones:

```js
function sumPrices(price1, price2) {
  return price1 + price2;
}

var firstItemPrice = 5;
var secondItemPrice = 3;

console.log(`Total amount: ${sumPrices(firstItemPrice, secondItemPrice)}€`);
// Total amount: 8€
```

La interpolación de cadenas también nos permite escribir cadenas de varias líneas sin escapar los saltos de línea, como era necesario en ES5:

```js
var element = document.querySelector('#element');
var textToShow = 'Hey, this is important.';

// ES5
element.innerHTML = '\
<div class="popup">\
  <span>' + textToShow + '</span>\
</div>';

// ES6
element.innerHTML = `
<div class="popup">
  <span>${textToShow}</span>
</div>`;
```

[&blacktriangleright; Interpolación de cadenas en Codepen][codepen-string-interpolation]


* * *

**EJERCICIO 1: SALUDOS CON ES2015**

Vamos a familiarizarnos con ES2015 para conocernos mutuamente. Crearemos un programa que nos pregunte nuestro nombre usando `prompt()` y que muestre la siguiente frase: _"Hola, NOMBRE, encantado de conocerte"_. `NOMBRE` será el nombre introducido por el usuario y usaremos la interpolación de cadenas para ello.

* * *

**EJERCICIO 2: INTERPOLACIÓN USANDO INNERHTML**

El objetivo de este ejercicio es pintar tres elementos dentro de una lista. Cada uno de ellos contendrá una imagen. Los datos de las imágenes y del texto los obtendremos a partir del siguiente array:

```js
var dogs = [
  {
    image: 'https://dog.ceo/api/img/schipperke/n02104365_8156.jpg',
    name: 'Dina'
  },
  {
    image: 'https://dog.ceo/api/img/collie-border/n02106166_355.jpg',
    name: 'Bobby'
  },
  {
    image: 'https://dog.ceo/api/img/schipperke/n02104365_8156.jpg',
    name: 'Lana'
  }
];
```
En este caso para añadir cada uno de los elementos utilizaremos la propiedad `innerHTML` y la interpolación de cadenas.

* * *


## Las variables `let` y `const` y su _scope_

ES6 tiene nuevas maneras de declarar variables que mantienen mejor el control sobre dónde se pueden usar.

Cuando declaramos una variable con `var`, la variable está disponible en todo el ámbito (_scope_) de la función, o en el ámbito global si no está dentro de una función. Eso significa que, aunque la declaremos dentro de una estructura de control, por ejemplo, podemos usarla después, como se puede ver en el siguiente ejemplo:

```js
var healthyPerson = true;

if (healthyPerson) {
  var dailyFruits = 5;
  console.log(`Como ${dailyFruits} piezas de fruta al día.`);
}

// Podemos usarla después
dailyFruits += 1;
console.log(dailyFruits); // 6
```

Esto puede causar conflictos de nombres de variables. Nos puede pasar, por ejemplo, que declaremos más abajo en el código una variable `var` con el mismo nombre y que ya contenga valor que no hemos previsto, por haberse usado más arriba o en una librería externa que usemos.

Cuando declaramos variables con `let` o `const`, las variables solo están disponibles **dentro** del ámbito de bloque (entre `{` y `}`) donde se hayan declarado:

```js
let healthyPerson = true;

if (healthyPerson) {
  let dailyFruits = 5;
  console.log(`Como ${dailyFruits} piezas de fruta al día.`);
}

// Si intentamos usarla después...
dailyFruits += 1; // ReferenceError: dailyFruits no está definida.
console.log(dailyFruits); // (esta línea no se ejecutará)
```

Si intentamos usar una variable declarada con `let` o `const` fuera del bloque donde se ha declarado, entonces nos dará un error y nos avisará de que esa variable no existe en ese contexto.

Por otra parte, `const` nos permite declarar una variable cuyo valor nunca cambia una vez lo asignemos. Una "variable" que nunca varía recibe el nombre de **constante**.

```js
const DAYS_PER_WEEK = 7; // Es común escribir las constantes en mayúscula
const HOURS_PER_DAY = 24;

const hoursPerWeek = HOURS_PER_DAY * DAYS_PER_WEEK;

console.log(`Una semana tiene ${hoursPerWeek} horas.`); // 'Una semana tiene 168 horas.'

// Si intentamos modificar su valor...
hoursPerWeek = 151; // TypeError: Asignación no válida a la constante "hoursPerWeek"
```

> Es una convención entre programadores utilizar nombres en UPPER_SNAKE_CASE para [valores constantes](https://eslint.org/docs/developer-guide/code-conventions#naming), que normalmente se declaran en la parte superior del fichero.


Sin embargo, hay que tener en cuenta que si el valor asignado a una constante es un array o un objeto, sus miembros o propiedades **internas** sí pueden cambiar.

```js
const person = {
  name: 'Augusta Ada',
  surname: 'Lovelace'
};

// Podemos cambiar las propiedades de un objeto
person.name = 'Ada';
console.log(`${person.name} ${person.surname}`); // 'Ada Lovelace'

// Pero no podemos cambiar el objeto asignado
person = {
  name: 'Grace',
  surname: 'Hopper'
}
// TypeError: Asignación no válida a la constante `person'
```

[&blacktriangleright; Constantes `const` en Codepen][codepen-const]

[&blacktriangleright; Variables `let` y ámbitos en Codepen][codepen-let-and-scope]


* * *

**EJERCICIO 3: DEJAMOS DE USAR VAR**

Vamos a re-hacer los ejercicios 1 y 2 usando `const` y `let` en vez de `var`. Y todos los ejercicios a partir de ahora los vamos a hacer de esta forma. __Siempre__.

* * *


## Bucle `for...of`

El bucle `for...of` de ES6 nos permite recorrer un objeto iterable, como son los arrays, por ejemplo, sin tener que escribir las condiciones de un `for` normal. Además, nos permite usar nombres mucho más reconocibles para los valores dentro del array.


```js
const bestAnimatedFeature2016Nominees = ['Zootopia', 'Kubo and the Two Strings', 'La tortue rouge', 'Ma vie de Courgette', 'Moana'];

// bucle for en ES5
for (let index = 0; index < bestAnimatedFeature2016Nominees.length; index++) {
  console.log (`"${bestAnimatedFeature2016Nominees[index]}" was nominated to 89th Academy Awards`);  
}

// bucle for...of en ES6
for (const movie of bestAnimatedFeature2016Nominees) {
  console.log (`"${movie}" was nominated to 89th Academy Awards`);
}
```

> **Nota**: si quisiéramos modificar los valores del array, tendríamos que hacer un bucle `for` como ya sabíamos. Esta nueva manera solo nos permite leer los datos.

* * *

**EJERCICIO 4: TENEMOS MUCHO EN COMÚN**

Vamos a hacer un pequeño programa que le pregunte al usuario cuáles son sus dos películas o libros favoritos. Una vez tengamos esa información guardada en un array, lo recorreremos y mostraremos este mensaje por cada obra: "¡A mí también me encantó "OBRA"! Tenemos mucho en común, humano.", donde OBRA será el nombre de la obra.

* * *

**EJERCICIO 5: A STORY `of` ADALABERS**

Estamos en una clase de Adalab, y queremos conocer algunas estadísticas sobre las adalabers de esa clase. Estos son sus datos:

- María, 29 años, diseñadora
- Lucía, 31 años, ingeniera química
- Susana, 34 años, periodista
- Rocío, 25 años, actriz
- Inmaculada, 21 años, diseñadora

En primer lugar, vamos a crear una estructura de datos en JavaScript para manejar estos datos. Usaremos arrays y objetos para crearla.

Después, vamos a crear varias funciones en JavaScript que nos permitan calcular de forma automática estadísticas sobre las adalabers. Todas ellas toman como parámetro un listado de adalabers similar a nuestra estructura de datos anterior.

1. Una función `countAdalabers` que devuelve el número de adalabers en el listado
2. Una función `averageAge` que devuelve la media de edad de listado
3. Una función `theYoungest` que devuelve el nombre de la adalaber más joven
4. Una función `countDesigners` que devuelve el número de adalabers que son diseñadoras

Según vayáis creando las funciones, debéis ir probando que funcionan invocándolas con nuestra estrucutra de datos como argumento. Al final, modificad la estructura de datos para añadir, modificar o quitar adalabers. Y probad que las funciones siguen devolviendo el valor correcto.

* * *


## _Destructuring_

La sintaxis _destructuring_ de ES6 nos facilita recoger valores de una estructura de datos, como los arrays o los objetos. Simulando la sintaxis de un array o de un objeto, en cada caso, podemos declarar varias variables a la vez, ¡y en una sola línea! Vemos unos ejemplos a continuación:


### _Destructuring_ de arrays

Vamos a ver un par de ejemplos con arrays. Tenemos un array de tres valores, y queremos coger los dos primeros en las variables `x` e `y`:

```js
const coordinates = [150, 35, 12]; // x = 150, y = 35, z = 12

// cómo lo habríamos hecho en ES5
const x = coordinates[0];
const y = coordinates[1];
console.log(`The point is at (${x}, ${y})`); // The point is at (150, 35)

// cómo mejora con ES6
const [x, y] = coordinates;
console.log(`The point is at (${x}, ${y})`); // The point is at (150, 35)
```

Como vemos, es más sencillo de escribir que manejar los índices como en ES5. Ahora supongamos que del array solo nos interesa la tercera coordenada, la que sería la coordenada `z`, pero no nos interesan los valores de antes. Sencillo: dejamos las posiciones vacías y le damos nombre solo a la tercera posición:

```js
const coordinates = [150, 35, 12];

// cómo lo habríamos hecho en ES5
const z = coordinates[2];
console.log(`The z-index is ${z}`); // The z-index is 12

// cómo mejora con ES6
const [, , z] = coordinates;
console.log(`The z-index is ${z}`); // The z-index is 12
```

* * *

**EJERCICIO 6: Otra vez la carrera de escobas**

Partiendo de este array con los resultados de una carrera de escobas ya ordenados, vamos a sacar del array e imprimir en la consola el podium, es decir, los tiempos del primero, segundo y tercer clasificado usando destructuring del array.

```js
var users = [
  {name: 'Nymphadora Tonks', time: 9},
  {name: 'Cedric Diggory', time: 28},
  {name: 'Cho Chang', time: 35},
  {name: 'Luna Lovegood', time: 45},
  {name: 'Gregory Goyle', time: 56}
];
```
* * *

### _Destructuring_ de objetos

Vamos ahora con los objetos. En los objetos, los valores no se identifican por su posición, sino que las propiedades tienen su propio nombre, así que tendremos que tener en cuenta esto al asignar los valores con _destructuring_.

Queremos coger el valor de una propiedad de un objeto y guardarla en una variable con el mismo nombre:

```js
const person = {
  name: 'Marie',
  lastName: 'Smith',
  age: 39,
  languages: ['English', 'French']
};

const {lastName} = person;
console.log(`Hello Mrs. ${lastName}`); // Hello Mrs. Smith
```

¿Y si quisiéramos cambiarle el nombre a la variable porque el nombre de la propiedad no es apropiado?

```js
const {name: personName} = person;
console.log(`Hello ${personName}`); // Hello Marie
```

> Este caso es típico: si guardamos el nombre como `name` en este contexto (`window`), estaríamos sobrescribiendo `window.name`, que es una propiedad existente del objeto `window` en los navegadores.


Ahora un _destructuring_ dentro de otro. Si queremos el segundo valor del array que está en una propiedad, haríamos:

```js
const {languages} = person;
const [, secondLanguage] = languages;
console.log(`${secondLanguage} is my second language`); // French is my second language
```

Pero también podemos hacerlo todo en uno sin pasar por el paso intermedio de definir `languages` primero, aunque pueda parecer un lío:

```js
const {languages: [, secondLanguage]} = person;
console.log(`${secondLanguage} is my second language`); // French is my second language
```


* * *

**EJERCICIO 7**

Revisa el ejercicio 6 para acceder al tiempo de los ganadores usando destructuring de array y de objeto. Ahora vamos a imprimir en la consola el nombre del ganador y su tiempo.

* * *

#### Bonus: intercambiando variables

En ES5, si queremos pasar el valor de una variable `a` a la variable `b`, y el valor de la variable `b` a la variable `a`, ¿cómo lo haríamos?

```js
let a = 'Quiero llamarme b';
let b = 'Quiero llamarme a';

// no hay más código de ejemplo
// ¡intenta resolverlo tú! ;)
```

¿Ya lo has resuelto? Si le has dedicado un poquito de tiempo, verás que es un tanto complicado. [**SPOILER ALERT**] Necesitamos una variable auxiliar que nos sirva de puente. En ES6 podemos usar _destructuring_ para no tener que pasar por ninguna variable intermedia.

```js
let a = 'Quiero llamarme b';
let b = 'Quiero llamarme a';

[b, a] = [a, b];

console.log(a); // 'Quiero llamarme a'
console.log(b); // 'Quiero llamarme b'
```


## Recursos externos

### Mozilla Developer Network

Páginas donde se explica en más profundidad las diferentes características de ES6 (en inglés)

- [Template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) (interpolación de cadenas)
- [`let` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
- [`const` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
- [`for...of` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

### You Don't Know JS

Una serie de libros para entender JavaScript en profundidad (en inglés)

- [You Don't Know JS: ES6 & Beyond](https://github.com/getify/You-Dont-Know-JS/blob/master/es6 & beyond/README.md)

### Mozilla Hacks: ES6 in Depth

Lista de artículos de colaboradores de Mozilla explicando las novedades de ECMAScript 6

- [ES6 in Depth](https://hacks.mozilla.org/category/es6-in-depth/)

### Compatibilidad de ES6

Para comprobar la compatibilidad de las características de ES2015/ES6 en los diferentes navegadores

- [Can I Use](http://caniuse.com/)
- También, aunque más engorrosa, la [ECMAScript 6 Compatibility Table](https://kangax.github.io/compat-table/es6/), que incluye distintos motores de JavaScript
