# Buenas prácticas en React

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)

<!-- /TOC -->

## Introducción

Hemos visto ya las funcionalidades más básicas de la librería. En esta sesión nos centraremos en repasar lo ya visto e introducir buenas prácticas en el uso de React.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Para poder escribir un código de React más legible y usando el "React way", es decir, haciéndolo de la forma en que lo hacen los desarrolladores de React.

## Uso de expresiones y programación funcional

Como ya sabemos, en React podemos mezclar código de JSX (nuestro HTML en JS) y código JavaScript metiéndolo entre llaves `{ }`. Pero el código que metemos entre llaves debe ser una expresión, es decir, un trozo de código que devuelve un resultado. Por eso, por ejemplo, no podemos meter código con `if`/`else` o hacer un `for` en JSX. Si necesitamos hacerlo, debemos llevarnos ese código a una nueva función (o método) y ejecutarla entre las llaves `{miFucn()}` ya que ejecutar una función sí es una expresión.

Debido a esto, el código de React que escriben los desarrolladores tiende a constar de expresiones y usar patrones como en encadenamiento (_chaining_), por ejemplo, usando métodos funcionales de array para manejar listados en lugar de bucles. El encadenamiento consiste en operar sobre el resultado de una expresión encadenando otra acción mediante el operador punto `.`. Vamos a ver un ejemplo de esto que ya lo hemos estado usando:

```js
const numbers = [1, 4, 6, 8, 45, 89];

const incrementedAndEvenNumbers = numbers
  .map(n => n + 1)
  .filter(n => n % 2 === 0);
```

En este ejemplo, partimos de un conjunto de números, sobre los que queremos realizar 2 operaciones:

- incrementarlos en 1
- filtrar los pares

Hemos realizado ambas operaciones encadenando un `map` que añade 1 a cada número con un `filter` para quedarnos solo con los números pares resultado de la operación anterior.

#### EJERCICIO 1

**Numeritos**

Vamos a crear una aplicación de React que, dado un listado de números como el del ejemplo anterior, los pinta en pantalla (usaremos un `ul` y sus `li`s ¡por supuesto!). Para pintarlos vamos a usar la función `.map` para pasar de un listado de números a un listado de elementos de JSX.

a) Vamos a añadir un formulario a la página, que contiene un input donde podemos introducir un número. Si ponemos, por ejemplo un 6, se mostrarán en pantalla solo los números mayores de 6. Usaremos `filter` y el patrón _chaining_ para conseguirlo.

b) Vamos a añadir un nuevo campo al formulario de tipo checkbox, que al marcarlo filtre además los números pares, desapareciendo de pantalla los impares. Este filtro debe actuar además del anterior, es decir, podremos filtrar los números mayores de 6 y que además sean pares.

\_\_\_\_\_\_\_\_\_\_

## Pintado condicional

Otro de los patrones de uso de React es el _conditional rendering_ o pintado condicional. Usando expresiones (como hemos hablado antes) vamos a poder pintar en pantalla unos elementos u otros.

### Ternarios

Podemos usar los ternarios en lugar de los `if`/`else` para pintar algo en pantalla dependiendo, por ejemplo, del estado ya que los ternarios sí son expresiones.

```js
const { isEditMode } = this.state;

return isEditMode ? (
  <p>Editing mode is ON ...</p>
) : (
  <p>Editing mode is OFF ...</p>
);
```

Esto suele usarse mucho para mostrar elementos de _loading_ (_loaders_) mientras, por ejemplo, se carga información del servidor.

### Comprobaciones y valores por defecto

Muchas veces vamos a querer hacer comprobaciones antes de pintar cosas en pantalla, por ejemplo, que una variable o sus claves no sean nulas. Lo haremos usando el operador `&&` ya que las condiciones se ejecutan en orden desde la primera y, si alguna es falsa, dejan de ejecutarse. Por ejemplo, aquí comprobamos primero que `data` no sea null, luego que tenga una clave `name` que no sea nula y, si ambas se cumplen, pinta el contenido en pantalla. Si no se cumplen, no se pintará nada.

```js
return data && data.name && <p>Bienvenido, {data.name}</p>;
```

También se usa bastante el operador `||` que ya hemos visto y que sirve, por ejemplo, para dar valores por defecto. Esto es porque la segunda parte del las operaciones sólo se ejecuta si la primera es falsa (o null, que es un falsy).

```js
return data && <p>Bienvenido, {data.name || 'invitado'}</p>;
```

En este ejemplo dejamos la primera comprobación de que `data` no sea null; y luego, si el nombre no está definido, usamos el valor de `'invitado'`.

### `null` no pinta nada

Para terminar estos ejemplos sencillos de pintado condicional, debemos saber que si una expresión dentro de JSX devuelve `null` no se pintará nada en pantalla.

```js
const { quixoteFan } = this.state;

return quixoteFan ? <p>En un lugar de La Mancha ...</p> : null;
```

#### EJERCICIO 2

**Colapsables**

Vamos a partir de nuestro ya [querido JSON con un listado de paletas](https://beta.adalab.es/ejercicios-extra/js-ejercicio-de-paletas/data/palettes.json), para pintar un listado de colapsables. Vamos a pintar el nombre de la paleta y la flechita del colapsable por cada una. Al desplegar un colapsable, se muestra su contenido, que es simplemente el campo `from` del JSON.

> NOTA: Recordad que debemos guardar en el estado del colapsable de React si el colapsable está o no desplegados.

\_\_\_\_\_\_\_\_\_\_

## Listados y keys

Cuando manejamos listados de datos en React, normalmente convertimos estos arrays en arrays de elementos JSX para poder pintarlos. Para ayudar a que la librería de React tenga mejor rendimiento, es importante indicar un atributo `key` que sea único en los listado de componentes JSX. De hecho, seguramente ya te habrás topado con errores en la consola que React advierte por este motivo.

Para solucionarlo, debemos indicar un atributo `key` que sea único en ese array (no en la página).

```js
const fruits = ['orange', 'pear', 'apple'];

return (
  <ul>
    {fruits.map(fruit => (
      <li key={fruit}>{fruit}</li>
    ))}
  </ul>
);
```

Cuando no tenemos un identificador único, como último recurso podemos hacer uso del índice del elemento dentro del array.

```js
const fruits = ['orange', 'pear', 'apple', 'orange'];

return (
  <ul>
    {fruits.map((fruit, index) => (
      <li key={index}>{fruit}</li>
    ))}
  </ul>
);
```

#### EJERCICIO 3

**Keys or not keys**

a) Para terminar, vamos a repasar los ejercicios anteriores y comprobar que no tenemos errores en la consola debidos a la ausencia de keys.

b) En el ejercicio anterior vamos a extraer un nuevo componente llamado `ColapsiblePalette`. ¿Dónde hay que poner el `key` ahora?

\_\_\_\_\_\_\_\_\_\_

## Destructuring

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

#### EJERCICIO 4

**La carrera de escobas**

Partiendo de este array con los resultados de una carrera de escobas ya ordenados, vamos a sacar del array e imprimir en la consola el podium, es decir, los nombres y tiempos del primero, segundo y tercer clasificado usando destructuring del array.

```js
const users = [
  { name: 'Nymphadora Tonks', time: 9 },
  { name: 'Cedric Diggory', time: 28 },
  { name: 'Cho Chang', time: 35 },
  { name: 'Luna Lovegood', time: 45 },
  { name: 'Gregory Goyle', time: 56 }
];
```

\_\_\_\_\_\_\_\_\_\_

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

const { name } = person;
console.log(`Hello ${name}`); // Hello Marie
```

> Este caso es típico: si guardamos el nombre como `name` en este contexto (`window`), estaríamos sobrescribiendo `window.name`, que es una propiedad existente del objeto `window` en los navegadores.

Como no queremos sobreescrituras ¿Y si quisiéramos cambiarle el nombre a la variable porque el nombre de la propiedad no es apropiado?

```js
const { name: personName } = person;
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

const { languages } = person;
const [, secondLanguage] = languages;
console.log(`${secondLanguage} is my second language`); // French is my second language
```

Pero también podemos hacerlo todo en uno sin pasar por el paso intermedio de definir `languages` primero, aunque pueda parecer un lío:

```js
const {
  languages: [, secondLanguage]
} = person;
console.log(`${secondLanguage} is my second language`); // French is my second language
```

#### EJERCICIO 5

**De nuevo la carrera de escobas**

Revisa el ejercicio 4 para acceder al nombre y tiempo de los ganadores usando destructuring de array y de objeto para imprimirlos en la consola.

```js
const users = [
  { name: 'Nymphadora Tonks', time: 9 },
  { name: 'Cedric Diggory', time: 28 },
  { name: 'Cho Chang', time: 35 },
  { name: 'Luna Lovegood', time: 45 },
  { name: 'Gregory Goyle', time: 56 }
];
```

\_\_\_\_\_\_\_\_\_\_

### _Destructuring_ en React

Llegado este punto, es posible que te estés preguntando, "Por mis props, ¿dónde encaja esto en React?".
Piensa en los componentes que has desarrollado hasta ahora, ¿cuantas veces has escrito `this.props.something` (clase) o `props.something` (funcional)?, ¡seguro que bastantes!

Veamos un ejemplo de la definición de un componente llamado `Field` que pinta un `label` y un `input` cada vez que es instanciado.

```js
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class Field extends Component {
  render() {
    return (
      <div className={`Field ${this.props.name || ''}`}>
        <label htmlFor={this.props.id}>{this.props.label}</label>
        <input
          id={this.props.id}
          name={this.props.name || this.props.id}
          type={this.props.type}
          onChange={this.props.onChange}
          value={this.props.value}
        />
      </div>
    );
  }
}

Field.defaultTypes = {
  type: 'text'
};

Field.propTypes = {
  className: Proptypes.string,
  id: Proptypes.string.isRequired,
  label: Proptypes.string.isRequired,
  name: Proptypes.string,
  type: Proptypes.string,
  onChange: Proptypes.string.isRequired,
  value: Proptypes.string.isRequired,
  placeholder: Proptypes.string.isRequired
};

export default Field;
```

Si queremos que el `html` devuelto (`return`) en el `render` quede más limpito podemos hacer algo así:

```js
...

class Field extends Component {
  render() {
    const className = this.props.className;
    const id = this.props.id;
    const label = this.props.label;
    const name = this.props.name;
    const type = this.props.type;
    const onChange = this.props.onChange;
    const value = this.props.value;
    const placeholder = this.props.placeholder;

    return (
      <div className={`Field ${className || ''}`}>
        <label htmlFor={id}>{label}</label>
        <input
          id={id}
          name={name || id}
          type={type}
          placeholder={placeholder}
          onChange={onChange}
          value={value}
        />
      </div>
    );
  }
}

...
```

Este código es un poco más legible, pero a costa de escribir más lineas.

Si te fijas bien, hemos creado una constante por cada propiedad del objeto `this.props`. A esta constante la hemos llamado igual que a la propiedad que contiene el valor que queremos guardar en ella.

Con _destructuring_ podemos hacer esto mismo escribiendo menos código:

```js
...

class Field extends Component {
  render() {
    const {
      className,
      id,
      label,
      name,
      type,
      onChange,
      value,
      placeholder
    } = this.props;

    return (
      <div className={`Field ${className || ''}`}>
        <label htmlFor={id}>{label}</label>
        <input
          id={id}
          name={name || id}
          type={type}
          placeholder={placeholder}
          onChange={onChange}
          value={value}
        />
      </div>
    );
  }
}
...
```

Voilà!

#### EJERCICIO 6

**Destructurando props y estado**

Vamos a partir del ejercicio **Formulario para pelis** de la sesión **Estado en React 2** y a hacer destructuring de los objetos `this.props` y `this.state`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 7

**Destructuring everywhere**

En el ejercicio anterior ¿localizas algún otro objeto dónde hacer destructuring?

**PISTA**: observa tu handler, quizás estés creando una constante y asignandole el valor contenido en la propiedad `value` del objeto `event.currentTarget`.

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

- [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)
- [Lists and keys](https://reactjs.org/docs/lists-and-keys.html)
- [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
