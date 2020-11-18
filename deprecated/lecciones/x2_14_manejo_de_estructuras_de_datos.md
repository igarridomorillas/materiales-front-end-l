# Manejo de estructuras de datos
<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)

<!-- /TOC -->

## Introducción

Hasta ahora hemos trabajado con dos estructuras de datos, los arrays y los objetos, y hemos visto diferentes formas de trabajar con ellas. Vamos a ver dos más, una para extraer valores y otra para construir estructuras: **Destructuring** y **Spread operator**.


## _Destructuring_

La sintaxis _destructuring_ de ES6 nos facilita recoger valores de una estructura de datos, como los arrays o los objetos. Simulando la sintaxis de un array o de un objeto, en cada caso, podemos declarar varias variables a la vez, ¡y en una sola línea! Vemos unos ejemplos a continuación:


### _Destructuring_ de arrays

Vamos a ver un par de ejemplos con arrays. Tenemos un array de tres valores, y queremos coger los dos primeros en las variables `x` e `y`:

```js
const coordinates = [150, 35, 12]; // x = 150, y = 35, z = 12

// hasta ahora lo habríamos hecho así
const x = coordinates[0];
const y = coordinates[1];
console.log(`The point is at (${x}, ${y})`); // The point is at (150, 35)

// usando destructuring de array
const [x, y] = coordinates;
console.log(`The point is at (${x}, ${y})`); // The point is at (150, 35)
```

Como vemos, es más sencillo de escribir que manejar los índices. Ahora supongamos que del array solo nos interesa la tercera coordenada, la que sería la coordenada `z`, pero no nos interesan los valores de antes. Sencillo: dejamos las posiciones vacías y le damos nombre solo a la tercera posición:

```js
const coordinates = [150, 35, 12];

// hasta ahora lo habríamos hecho así
const z = coordinates[2];
console.log(`The z-index is ${z}`); // The z-index is 12

// usando destructuring de array
const [, , z] = coordinates;
console.log(`The z-index is ${z}`); // The z-index is 12
```

* * *

#### EJERCICIO 1

**La carrera de escobas**

Partiendo de este array con los resultados de una carrera de escobas ya ordenados, vamos a sacar del array e imprimir en la consola el podium, es decir, los nombres y tiempos del primero, segundo y tercer clasificado usando destructuring del array.

```js
const users = [
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

const {name} = person;
console.log(`Hello ${name}`); // Hello Marie
```

> Este caso es típico: si guardamos el nombre como `name` en este contexto (`window`), estaríamos sobrescribiendo `window.name`, que es una propiedad existente del objeto `window` en los navegadores.

Como no queremos sobreescrituras ¿Y si quisiéramos cambiarle el nombre a la variable porque el nombre de la propiedad no es apropiado?

```js
const {name: personName} = person;
console.log(`Hello ${personName}`); // Hello Marie
```

Ahora un _destructuring_ dentro de otro. Si queremos el segundo valor del array que está en una propiedad, el segundo idioma de Marie, haríamos:

```js
const person = {
  name: 'Marie',
  lastName: 'Smith',
  age: 39,
  languages: ['English', 'French']
};

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
#### EJERCICIO 2

**De nuevo la carrera de escobas**

Revisa el ejercicio 1 para acceder al nombre y tiempo de los ganadores usando destructuring de array y de objeto para imprimirlos en la consola.

```js
const users = [
  {name: 'Nymphadora Tonks', time: 9},
  {name: 'Cedric Diggory', time: 28},
  {name: 'Cho Chang', time: 35},
  {name: 'Luna Lovegood', time: 45},
  {name: 'Gregory Goyle', time: 56}
];

```
* * *

## Bonus: intercambiando variables

Si queremos pasar el valor de una variable `a` a la variable `b`, y el valor de la variable `b` a la variable `a`, ¿cómo lo haríamos?

```js
let a = 'Quiero llamarme b';
let b = 'Quiero llamarme a';

// no hay más código de ejemplo
// ¡intenta resolverlo tú! ;)
```

¿Ya lo has resuelto? Si le has dedicado un poquito de tiempo, verás que es un tanto complicado. [**SPOILER ALERT**] Necesitamos una variable auxiliar que nos sirva de puente. Sin embargo podemos usar _destructuring_ para no tener que pasar por ninguna variable intermedia.

```js
let a = 'Quiero llamarme b';
let b = 'Quiero llamarme a';

[b, a] = [a, b];

console.log(a); // 'Quiero llamarme a'
console.log(b); // 'Quiero llamarme b'
```


## _Spread operator_

El operador _spread_ (`...`) convierte un array o un objeto en el conjunto de valores que contiene, por lo que nos permite usarlos como si estuvieran escritos en el propio código. Una de las ventajas que nos ofrece el operador _spread_ es que no tenemos por qué saber qué hay en el array u objeto en cada momento.

### _Spreading_ de array

Veamos un par de ejemplos con arrays. Tenemos un array y queremos añadirle un nuevo valor:

```js
const names = ['Smith', 'White', 'Black', 'Pinkman'];

const newNames = [...names, 'Williams'];

console.log(newNames)); // ['Smith', 'White', 'Black', 'Pinkman', 'Williams']
```

Ahora pongamos que queremos mezclar dos arrays distintos que tenemos:

```js
const myBooks = ['1984', 'Brave New World'];
const myBrotherBooks = ['We', 'Fahrenheit 451'];

const books = [...myBooks, ...myBrotherBooks];

console.log(books); // [`1984`, 'Brave New World', 'We', 'Fahrenheit 451']
```

El operador _spread_ también nos puede ser útil para pasar todos los valores de un array como parámetros a una función:

```js
const vowels = ['a', 'e', 'i', 'o', 'u'];

console.log(...vowels);
```

Esto sería equivalente a: 

```js
// 
console.log(vowels[0], vowels[1], vowels[2], vowels[3], vowels[4]);
```

### _Rest parameters_

Pero cuando declaramos una función propia también nos sirve para almacenar los parámetros sobrantes (_rest parameters_) en una sola variable:

```js
function showFavoriteFruits(first, ...rest) {
  const restOfFruits = rest.join(' and ');
  console.log(`My favourite fruit is the ${first}, although I like ${restOfFruits} also.`);
}

const myFavoriteFruits = ['orange', 'banana', 'pear'];
showFavoriteFruits(...myFavoriteFruits); // 'My favourite fruit is the orange, although I like banana and pear also.'
```

### _Spreading_ de objeto

Podemos usar el operador _spread_ también con las propiedades de los objetos. Por ejemplo, para añadir una propiedad nueva o sobreescribirla si ya existe. En este ejemplo copiamos el objeto `person` y lo guardamos en `twinSister`. El objeto `person` sigue existiendo y los dos son independientes:

```js
const person = {
  name: 'Marie',
  lastName: 'Smith',
  age: 39
};

const twinSister = {...person, name: 'Juliette'};

console.log(twinSister); // { name: 'Juliette', lastName: 'Smith', age: 39 }
```

> **¡Cuidado!**: si alguna de las propiedades del objeto original es un array u otro objeto, esa propiedad no se clonaría, sino que se compartiría. Para evitar errores, solo copiaremos de esta manera objetos "planos".


* * *

**Vuelve la carrera de escobas**

Partiendo del listado de participantes de la carrera de escobas del ejercicio 1, vamos a realizar varios ejercicios:  

#### EJERCICIO 3

**Un nuevo participante**

Añadir un último participante que ha llegado tarde: el señor Argus Filch ha hecho un tiempo de 78. Crea un array nuevo con todos los resultados usando el `spreading` de array.

***
#### EJERCICIO 4

**Marcando el primer puesto**

Sacamos el objeto del ganador de la carrera usando destructuring del array, y creamos un nuevo objeto añadiendo una nueva propiedad `win` con valor 1. Lo hacemos usando `spreading` del objeto.

```js
const users = [
  {name: 'Nymphadora Tonks', time: 9},
  {name: 'Cedric Diggory', time: 28},
  {name: 'Cho Chang', time: 35},
  {name: 'Luna Lovegood', time: 45},
  {name: 'Gregory Goyle', time: 56}
];
```

* * *

## Recursos externos

### Mozilla Developer Network

Páginas donde se explica en más profundidad las diferentes características de ES6 (en inglés)

- [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

### Mozilla Hacks: ES6 in Depth

Lista de artículos de colaboradores de Mozilla explicando las novedades de ECMAScript 6

- [ES6 in Depth - Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)
