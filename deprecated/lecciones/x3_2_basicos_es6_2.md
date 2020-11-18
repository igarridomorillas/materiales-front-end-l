# Básicos de ES2015 - 2 (ES6)

[sección-módulos]: #módulos-de-js

## Contenidos
- [Introducción](#introducción)
- [_Spread operator_](#spread-operator)
- [_Arrow functions_ y el `this` léxico](#arrow-functions-y-el-this-léxico)
- [Módulos de JS][sección-módulos]

## Introducción

Hasta el momento hemos visto algunas de las características de la nueva sintaxis de ES2015 (ES6). Ahora veamos el resto.

En la [última sección][sección-módulos], veremos cómo reutilizar nuestro código entre distintos proyectos, o importar código ajeno.


## _Spread operator_

El operador _spread_ (`...`) de ES6 convierte un array o un objeto en el conjunto de valores que contiene, por lo que nos permite usarlos como si estuvieran escritos en el propio código. Una de las ventajas que nos ofrece el operador _spread_ es que no tenemos por qué saber qué hay en el array u objeto en cada momento.

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

#### _Rest parameters_

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

> Cuidado: si alguna de las propiedades del objeto original es un array u otro objeto, esa propiedad no se clonaría, sino que se compartiría. Para evitar errores, solo copiaremos de esta manera objetos "planos".


* * *

**EJERCICIO 1**

Partiendo del listado de participantes de la carrera de escobas del ejercicio 6 de ayer. Vamos a realizar varios ejercicios:  

1. Añadir un último participante que ha llegado tarde: el señor Argus Filch ha hecho un tiempo de 78. Crea un array nuevo con todos los resultados usando el `spreading` de array.
1. Sacamos el objeto del ganador de la carrera usando destructuring del array, y creamos un nuevo objeto añadiendo una nueva propiedad `win` con valor 1. Lo hacemos usando `spreading` del objeto.

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


## _Arrow functions_ y el `this` léxico

Las _arrow functions_ ("funciones flecha") de ES6 son una notación simplificada para declarar funciones. En especial, vienen muy bien cuando queremos declarar funciones anónimas dentro de una expresión, como puede ser en _callbacks_ de acceso al DOM o a una API. La sintaxis básica es la siguiente:

```js
// ES5
const button = document.querySelector('.btn-submit');
button.addEventListener('click', function() {
  console.log('Hello from an anonymous function');
});

// ES6
const button = document.querySelector('.btn-submit');
button.addEventListener('click', () => {
  console.log('Hello from an anonymous function');
});
```

También podemos asignar esas funciones a variables que declaremos:

```js
// ES5
const printSomething = function() {
  console.log('Hmmm... something!');
}

// ES6
const printSomething = () => {
  console.log('Hmmm... something!');
};
```

### Paréntesis opcionales

No podemos quitar los paréntesis si no se especifican parámetros o si son múltiples, pero sí cuando la función solo tenga un parámetro:

```js
const printWaitingTime = minutes => {
  console.log(`Please, wait ${minutes} minutes`);
};

// equivale a
const printWaitingTime = (minutes) => {
  console.log(`Please, wait ${minutes} minutes`);
};
```

### Llaves y _return_ implícito

Escribir o no las llaves (`{}`) significa dos cosas distintas. Solo podremos no escribirlas cuando la función tenga una sola sentencia; es decir, cuando se ejecute una sola orden dentro (un `console.log()`, un cambio en un elemento HTML, un incremento en un contador, etc.). Cuando no escribimos las llaves, el valor que devuelve esa sentencia será el _return_ de la función. Eso nos permite escribir en menos líneas funciones muy sencillas:

```js
// ES5
function rectArea(x, y) {
  return x * y;
}

// ES6
const rectArea = (x, y) => {
  return x * y;
};

const rectArea = (x, y) => x * y;
```

En el caso de que quisiéramos devolver un objeto, entonces tendríamos que rodearlo con paréntesis para que las llaves no se malinterpreten:

```js
const makePersonObject = (name, lastName, currentAge) => ({
  name,
  lastName,
  birthDate: new Date().getFullYear() - currentAge,
});

makePersonObject('Emma', 'Watson', 27); // { name: "Emma", lastName: "Watson", birthDate: 1990 }
```

### El `this` léxico

En todas las funciones se define automáticamente una variable `this` que puede resultar un poco problemática, porque lo entendemos traducido del inglés como "esto que está aquí". `this`, sin embargo, tiene distinto valor según desde qué contexto **se ejecute** la función. Existe una inconveniencia con esto en los _callbacks_, una función que pasas a otra parte del código (_aquello_) para que se ejecute en asíncrono (_allá_). Al declarar una función que use `this`, puede parecer que estemos usando el `this` del contexto (_esto_) desde el que escribimos (_aquí_) la función, pero en realidad no es así:

```js
function Person() {
  this.age = 0;
  this.growUp = function() {
    this.age++;
  };
}

var person = new Person();
console.log(person.age); // 0, la edad inicial

person.growUp(); // ejecutamos la función sobre el objeto "person": "this" === "person"
console.log(person.age); // 1, creció después de ejecutar "growUp"

setInterval(person.growUp, 1000); // callback que ejecuta *el navegador* por mí: "this" !== "person", "this" === "window"
setTimeout(function() {
  console.log(person.age) // 1, ¡no creció! (!)
}, 3000);
```

Una solución a esto en ES5 es guardar la referencia en una variable antes (el ejemplo lo ilustra). En ES6 se resuelve este problema: en las _arrow functions_, el `this` tiene un valor léxico, que quiere decir que el valor de `this` no depende de dónde se ejecute, sino de dónde se escriba (_aquí_).

```js
// ES5, sin this léxico
function Person() {
  var _this = this; // declaramos una variable que podremos usar (ámbito) dentro de las funciones que declaremos
  this.age = 0;
  this.growUp = function() {
    _this.age++;
    // "this" aquí referenciaría al contexto desde el que *se ejecuta* la función
    // Como la ejecuta el navegador por nosotros (es un callback), el contexto es el contexto global, "window"
  }

  setInterval(this.growUp, 1000);
}

// ES6 con this léxico
function Person() {
  this.age = 0;
  this.growUp = () => {
    this.age++;
    // Como es una arrow function, "this" referencia al contexto desde el que **declaramos** la función,
    // no importa que la ejecute luego el navegador por nosotros como callback
  }

  setInterval(this.growUp, 1000);
}

const person = new Person();
setTimeout(() => {
  console.log(person.age); // 2, creció, :)
}, 3000);
```

Así ES6 resuelve un problema y nos ahorra más de un dolor de cabeza.


* * *

**EJERCICIO 2: A STORY `of` ADALABERS RELOADED**:

Vamos a rehacer las funciones del ejercicio 5 de la sesión anterior usando arrow functions. __¡Al lío!__

* * *

## Módulos de JS

Los módulos nos facilitan dividir nuestro código en pequeñas partes reutilizables. Podemos dividir nuestro código en partes tanto para **organizar** un proyecto, **compartir** código entre distintos proyectos nuestros o para **usar librerías** de terceros.

**dog.js**:
```js
class Dog {
  bark() {
    console.log('Wan, wan!');
  }
}

const FAMOUS_DOGS = ['Hachiko', 'Laika', '101 Dalmatians'];

export { Dog, FAMOUS_DOGS };
```

**main.js**:
```js
import { Dog, FAMOUS_DOGS } from './dog.js';

const hachiko = new Dog();

console.log(`Some famous dogs in history: ${FAMOUS_DOGS.join(', ')}...`); // 'Some famous dogs in history: Hachiko, Laika, 101 Dalmatians...'
hachiko.bark(); // 'Wan, wan!'
```

### `export`

Todo lo que hay dentro de un módulo de JavaScript pertenece exclusivamente al módulo por defecto. Nada se puede acceder desde fuera excepto si se **exporta**. La palabra clave `export` nos permite exportar una variable (`var`, `let` o `const`), función o clase que podrá ser **importada** por otro código más tarde.

Podemos exportar de varias maneras. Podemos exportar individualmente valores que ya hayamos declarado:

**module.js**:
```js
export const aConstant = 'constant';

export function aFunction() { /* function body */ }
```

También podemos exportar todo de una sola vez (como un objeto envoltorio), que mejora la legibilidad del código cuando es extenso:

**module.js**:
```js
const aConstant = 'constant';

function aFunction() { /* function body */ }

export { aConstant, aFunction };
```

Por último, podemos declarar un valor exportado por defecto, si queremos. Solo puede haber un valor exportado por defecto en cada módulo, y puede o no tener nombre:

**module_default-unnamed.js**:
```js
export default function() { /* function body */ };
```

**module_default-named.js**:
```js
export default aFunction;
```


### `import`

Para usar código de un módulo, primero tendremos que importarlo en nuestro código. Como es normal en JavaScript, tenemos varias maneras distintas de importar módulos.

Podemos seleccionar, por su nombre, qué valores exportados importar. Importaremos solo uno de la siguiente manera:

**main.js**:
```js
import { aConstant } from './module.js';

console.log(aConstant); // 'constant'
```

E importaremos varios valores así:

**main.js**:
```js
import { aConstant, aFunction } from './module.js';

aFunction(); // do things as declared in module.js
console.log(aConstant); // 'constant'
```

Si queremos cambiarle el nombre a algún valor, lo podemos hacer con `as`:

**main.js**:
```js
import { aFunction as functionFromModule } from './module.js';

functionFromModule(); // do things as declared in module.js
```
```js
import {
  aConstant,
  aFunction as functionFromModule
} from './module.js';

functionFromModule(); // do things as declared in module.js
console.log(aConstant); // 'constant'
```
```js
import {
  aConstant as constantFromModule,
  aFunction as functionFromModule
} from './module.js';

functionFromModule(); // do things as declared in module.js
console.log(constantFromModule); // 'constant'
```

También podemos importar todo el contenido de un módulo con `*`. Esto nos importa todos los valores dentro de un objeto envoltorio al que debemos darle nombre con `as`:

**main.js**:
```js
import * as module from './module.js';

module.aFunction(); // do things as declared in module.js
console.log(module.aConstant); // 'constant'
```

### Declarar módulos

Podemos declarar archivos de JavaScript como módulos en el HTML de la siguiente manera:

**index.html**:
```html
<script type="module" src="route/to/module.js"></script>
```

Sin embargo, esta manera [no está muy soportada aún](https://caniuse.com/#feat=es6-module) por los navegadores: solo un 62.81% de las últimas versiones de los navegadores lo soporta. Sin embargo, no tendremos ningún problema cuando usemos _module bundlers_ o [Babel](http://babeljs.io/) para compilar nuestro código, y en estos casos no será necesario declarar los módulos en el HTML.

* * *

**EJERCICIO 3**:

Prueba los ejemplos anteriores exportando datos desde un fichero e importándolos desde otros. Asegúrate de entender bien cómo funcionan las rutas para importar/exportar adecuadamente.

* * *

## Recursos externos

### Mozilla Developer Network

Páginas donde se explica en más profundidad las diferentes características de ES6 (en inglés)
- [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)
- [Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

### Mozilla Hacks: ES6 in Depth

Lista de artículos de colaboradores de Mozilla explicando las novedades de ECMAScript 6

- [ES6 in Depth - Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)
