# Clases y objetos

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO BONUS A](#ejercicio-bonus-a)
- [EJERCICIO 3](#ejercicio-3)

<!-- /TOC -->

## Introducción

[wp-poo]: https://es.wikipedia.org/wiki/Programaci%C3%B3n_orientada_a_objetos
[wp-paradigma]: https://es.wikipedia.org/wiki/Paradigma_de_programaci%C3%B3n

En esta sesión veremos el concepto de clases, que está muy relacionado con la [programación orientada a objetos][wp-poo] (OOP, según sus siglas en inglés). La POO es una manera consensuada de pensar la programación (un [paradigma][wp-paradigma]) que se usa en una gran variedad de lenguajes de programación.

En la última sección, veremos cómo reutilizar nuestro código entre distintos proyectos, o importar código ajeno.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

JavaScript es un lenguaje muy flexible. Por eso, en la práctica, muchos programadores recurren a otros conceptos asentados de programación al escribir JavaScript. Con ES6 se guiñó un ojo a los programadores que usaban las posibilidades de JavaScript para la POO y se introdujeron las **clases**.

Las clases nos ayudan a delimitar la responsabilidad de ciertas partes de nuestro código y organizarlo de manera más clara. También nos ayudan a reutilizar partes del código y ahorrar líneas y posibilidades de error.

## Clases y objetos

Ya sabemos lo que es un objeto en programación: es una entidad que contiene unas propiedades dadas, que pueden ser valores o funciones. Cuando tenemos un puñado de objetos parecidos porque tienen las mismas propiedades, podemos decir que esos objetos son del mismo tipo. Es decir, son de la misma "clase". Una clase es justo eso, una abstracción de los objetos que nos indica qué tienen en común.

```js
class Dog {
  // class body
}

const laika = new Dog();
const hachiko = new Dog();
```

Una instancia es un objeto de una clase que hayamos especificado. En el ejemplo anterior, `hachiko` y `laika` son instancias de la clase `Dog`. Dándole la vuelta, cuando creamos un objeto de una clase con el operador `new`, entonces estamos **instanciando** una clase. Las instancias comparten los métodos y atributos de la clase.

## Métodos y atributos

Los objetos se caracterizan por sus propiedades, que pueden ser funciones o valores. En las clases, llamaremos _métodos_ a las funciones de una clase, y _atributos_ a los valores. Veremos cómo declarar atributos en la sección sobre el constructor. De momento, vamos a declarar un método para la clase `Dog`:

```js
class Dog {
  bark() {
    console.log('Woof, woof!');
  }
}

const laika = new Dog();
const hachiko = new Dog();

laika.bark(); // Woof, woof!
hachiko.bark(); // Woof, woof!
```

> **Nota**: Debes notar que para declarar un método en una clase, no usamos la palabra `function` sino directamente el nombre del método

#### EJERCICIO 1

Vamos a crear un programita que haga cálculos geométricos sencillos. En el programa definiremos la clase `Square`, que tendrá al menos:

- Un método para calcular el perímetro (`perimeter()`) del cuadrado (multiplica la longitud del lado por el número de lados)
- Un método para calcular el área (`area()`) del cuadrado (elevar al cuadrado el lado)

Los métodos recibirán la longitud del lado (`side`) como parámetro.

Calcularemos y mostraremos el perímetro y el área de un cuadrado de `9` de lado.

\_\_\_\_\_\_\_\_\_\_

## Métodos de clase VS métodos de instancia

Como hemos visto, las instancias comparten los métodos de la clase de la que vienen. Pero las instancias también pueden declarar los suyos propios e individuales. En este ejemplo, la instancia `hachiko` declara un método `waitForOwner` que solo puede usar ella.

```js
class Dog {
  bark() {
    console.log('Woof, woof!');
  }
}

const laika = new Dog();
const hachiko = new Dog();

hachiko.waitForOwner = () => {
  console.log('Hachiko is waiting.');
};

hachiko.waitForOwner(); // Hachiko is waiting.
laika.waitForOwner(); // TypeError: laika.waitForOwner no es una función
```

Si una instancia declara un método con el mismo nombre que la recibida de su clase, entonces el método se **sobrescribe** para esa instancia solo:

```js
class Dog {
  bark() {
    console.log('Woof, woof!');
  }
}

const laika = new Dog();
const hachiko = new Dog();

hachiko.bark = () => {
  console.log('Wan, wan!'); // Hachiko barks in Japanese
};

laika.bark(); // 'Woof, woof!'
hachiko.bark(); // 'Wan, wan!'
```

## El constructor y `this`

El `constructor()` es un método especial de las clases. El constructor es el método encargado de inicializar la instancia, es decir, de preparar todo lo necesario para su creación. El constructor recibe los parámetros que se pasan al instanciar la clase con `new`:

```js
class Dog {
  constructor(name) {
    console.log(`(I have a conscience now. My name is ${name})`);
  }
}

const laika = new Dog('Laika'); // (I have a conscience now. My name is Laika)
```

En el constructor, además, es donde se declaran los atributos de la clase. Vamos a declarar el parámetro `name` como un atributo:

```js
class Dog {
  constructor(name) {
    this.name = name;
  }
}

const laika = new Dog('Laika');
const hachiko = new Dog('Hachiko');

console.log(laika.name); // 'Laika'
console.log(hachiko.name); // 'Hachiko'
```

La palabra clave `this` dentro de la declaración de una clase hace referencia a la instancia de la clase que crearemos. Cuando declaramos atributos en el constructor con `this.miAtributo` como en el ejemplo anterior, estamos efectivamente declarando que "la instancia resultante (`this`) tendrá la propiedad `miAtributo`". Una vez creada la instancia, para acceder a los atributos lo hacemos directamente como en el ejemplo, `laika.name`.

De igual manera que los declaramos, con `this` podemos acceder a esos atributos desde los métodos:

```js
class Dog {
  constructor(name) {
    this.name = name;
  }

  bark() {
    console.log('Woof, woof!');
  }

  reactToCall(shout) {
    if (shout.includes(this.name)) {
      console.log(`${this.name} wags its tail, happily.`);
    } else {
      this.bark();
    }
  }
}

const laika = new Dog('Laika');

laika.reactToCall('Hey, Laika!'); // 'Laika wags its tail, happily.'
laika.reactToCall('Hey, Hachiko!'); // 'Woof, woof!'
```

#### EJERCICIO 2

Vamos a mejorar nuestra calculadora geométrica sencilla. En el programa definiremos la clase `Square`, que tendrá al menos:

- Un atributo para la longitud del lado (`side`) del cuadrado
- Un método para calcular el perímetro (`perimeter()`) del cuadrado (multiplica la longitud del lado por el número de lados - 4)
- Un método para calcular el área (`area()`) del cuadrado (elevar al cuadrado el lado)

Los métodos no recibirán parámetros, sino que cogerán los datos necesarios de los atributos de la instancia.

Crearemos tres instancias: una con `1` de lado, otra con `3` y otra con `7`. Llamaremos a los dos métodos en todas las instancias.

\_\_\_\_\_\_\_\_\_\_

## Herencia (`extends`)

Una de las características más potentes de las clases es que podemos crear subclases. Una subclase es una clase que **hereda** los métodos y atributos de otra clase. De esta manera, podemos hacer clases más concretas cuando nos haga falta sin tener que reescribir partes del código.

> **Nota**: Existe diferente terminología para hablar de herencia. A las subclases también se las llama clases "hija" de una clase "padre" (o "madre"). Las clases de las que se hereda también se llaman clases "base" o superclases.

Para que una clase herede de otra, usamos la palabra clave `extends`:

```js
class QuadrupedAnimal {
  constructor() {
    this.legs = 4;
  }
}

class Dog extends QuadrupedAnimal {
  // class body
}

const hachiko = new Dog();

console.log(`Hachiko has ${hachiko.legs} legs because it's a quadruped animal.`);
// 'Hachiko has 4 legs because it's a quadruped animal.'
```

Las subclases tienen un método especial `super()` que debe llamarse al principio del constructor (si se escribe). El método `super()` llama al constructor de la superclase; así podemos pasar parámetros de la subclase al constructor de la superclase:

```js
class Animal {
  constructor(name, legs) {
    this.name = name;
    this.legs = legs;
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name, 4);
  }

  bark() {
    console.log('Woof, woof!');
  }
}

const hachiko = new Dog('Hachiko');

hachiko.bark(); // 'Woof, woof!'
console.log(`${hachiko.name} has ${hachiko.legs} legs.`); // 'Hachiko has 4 legs.'
```

Las subclases pueden declarar nuevos métodos y atributos:

```js
class Animal {
  constructor(name, legs) {
    this.name = name;
    this.legs = legs;
  }
}

class Dog extends Animal {
  constructor(name, owner) {
    super(name, 4);
    this.owner = owner;
  }

  bark() {
    console.log('Woof, woof!');
  }
}

const hachiko = new Dog('Hachiko', 'Eisaburō Ueno');

console.log(hachiko.owner); // 'Eisaburō Ueno'
hachiko.bark(); // 'Woof, woof!'
```

Las subclases también pueden **sobrescribir** métodos de las superclases:

```js
class Dog {
  constructor(name) {
    this.name = name;
  }

  bark() {
    console.log('Woof, woof!');
  }
}

class JapaneseDog extends Dog {
  bark() {
    console.log('Wan, wan!');
  }
}

class RussianDog extends Dog {
  bark() {
    console.log('Gav, gav!');
  }
}

const laika = new RussianDog('Laika');
const hachiko = new JapaneseDog('Hachiko');

// Every dog barks in its own language
hachiko.bark(); // Wan, wan!
laika.bark(); // 'Gav, gav!'

// Regular dogs bark as usual in English
const leo = new Dog('Leo');
leo.bark(); // 'Woof, woof!'
```

#### EJERCICIO BONUS A

Vamos a mejorar ¡aún más! nuestra calculadora geométrica sencilla. En el programa definiremos la clase `Polygon`, `Square` y `Triangle` para polígonos regulares (todos sus lados miden lo mismo). Ya os imagináis por dónde van los tiros: las clases `Square` y `Triangle` serán subclases de `Polygon`. La clase `Polygon` tendrá, al menos:

- Un atributo para el número de lados (`numberOfSides`)
- Dos atributos más: para la longitud de la base (`base`) y de la altura (`height`)
- Un método para calcular el perímetro (`perimeter`) (multiplicar la longitud del lado base por el número de lados)
- Un método para calcular el área (`area`) (multiplicar base por altura)

La subclase `Square` tendrá:

- Un atributo lado (`side`) igual a la base
- Un constructor que recibirá exclusivamente la longitud del lado

La subclase `Triangle` tendrá:

- Un constructor que recibirá base y altura
- Un método `area()` que sobrescibirá al de la clase base. Devolverá la mitad de lo que devuelva llamar al área de la clase base (`super.area() / 2`)

Crearemos dos instancias: un cuadrado de `4` de lado y un triángulo de `4` de base y `3` de altura. Llamaremos a los dos métodos en todas las instancias.

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

export function aFunction() {
  /* function body */
}
```

También podemos exportar todo de una sola vez (como un objeto envoltorio), que mejora la legibilidad del código cuando es extenso:

**module.js**:

```js
const aConstant = 'constant';

function aFunction() {
  /* function body */
}

export { aConstant, aFunction };
```

Por último, podemos declarar un valor exportado por defecto, si queremos. Solo puede haber un valor exportado por defecto en cada módulo, y puede o no tener nombre:

**module_default-unnamed.js**:

```js
export default function() {
  /* function body */
}
```

**module_default-named.js**:

```js
export default aFunction;
```

> **Nota:** Siempre hay que escribir `export` después de la variable, constante, función... que estamos exportando. Por ello es una buena practica escribir los `export` al final de nuestro fichero.

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
import { aConstant, aFunction as functionFromModule } from './module.js';

functionFromModule(); // do things as declared in module.js
console.log(aConstant); // 'constant'
```

```js
import {
  aConstant as constantFromModule,
  aFunction as functionFromModule,
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

> **Nota:** Siempre hay que escribir `import` antes de usar la variable, constante, función... que estamos importando. Por ello es una buena practica escribir los `import` al principio de nuestro fichero.

### Declarar módulos

Podemos declarar archivos de JavaScript como módulos en el HTML de la siguiente manera:

**index.html**:

```html
<script type="module" src="route/to/module.js"></script>
```

En el ejemplo, declararíamos **main.js** de esta manera.

Sin embargo, esta forma de trabajo [no está completamente soportada aún](https://caniuse.com/#feat=es6-module) por los navegadores: un 90% de las últimas versiones de los navegadores lo soporta (en marzo de 2020). Sin embargo, no tendremos ningún problema cuando usemos _module bundlers_ o [Babel](http://babeljs.io/) para compilar nuestro código, y en estos casos no será necesario declarar los módulos en el HTML.

#### EJERCICIO 3

Prueba los ejemplos anteriores exportando datos desde un fichero e importándolos desde otros. Asegúrate de entender bien cómo funcionan las rutas para importar/exportar adecuadamente.

\_\_\_\_\_\_\_\_\_\_

<!--

## BONUS: _getters_ y _setters_

Los _getters_ y _setters_ nos permiten declarar en las clases unos atributos especiales que ejecutan una función.

Por un lado, los _getters_ se ejecutan cuando usemos un atributo. Esto puede ser útil para atributos "calculados" que dependen de los valores de otros atributos:

```js
class Dog {
  constructor(name) {
    this.name = name;
    this.barkingSound = 'Woof';
  }

  get barking() {
    return `${this.barkingSound}, ${this.barkingSound.toLowerCase()}!`;
  }

  bark() {
    console.log(this.barking); // accedemos como si fuera un atributo
  }
}

const leo = new Dog('Leo');
leo.bark(); // 'Woof, woof!'
```

Por el otro lado, los _setters_ se ejecutan cuando asignemos un nuevo valor a un atributo. Esto puede ser útil para especificar un efecto secundario que tendrá el cambio de valor:

```js
class Dog {
  constructor(name) {
    this._name = name; // Atributo interno
    this.happiness = 100;
  }

  get name() {
    return this._name;
  }

  set name(newName) {
    this._name = newName;
    this.lowerHappinessBy(75);
  }

  lowerHappinessBy(quantity) {
    if (this.happiness > quantity) {
      this.happiness -= quantity;
    } else {
      this.happiness = 0;
    }
  }

  printHappiness() {
    console.log(`${this.name} is ${this.happiness}% happy.`);
  }
}

const hachiko = new Dog('Hachiko');
hachiko.printHappiness(); // 'Hachiko is 100% happy.'

hachiko.name = 'Little Paws';
hachiko.printHappiness(); // 'Little Paws is 25% happy.'
```

> Es una convención usar nombres de atributos precedidos con barra baja (`_atributo`) para diferenciar los atributos de uso interno, que no deben ser usados desde fuera de la declaración.

#### EJERCICIO BONUS B

Vamos a mejorar crear una clase `Person` que recibe un nombre `firstName` y apellido `lastName` como parámetros de su constructor.

También definiremos un _getter_ `fullName` para obtener el nombre completo, que es una concatenación de nombre y apellido.

Crearemos 2 instancias con distintos nombres para probar que funciona.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO BONUS C

Vamos a mejorar ¡aún más, siempre más! nuestra calculadora geométrica sencilla. En el programa definiremos la clase `Polygon`, `Square` para polígonos regulares (todos sus lados miden lo mismo). La clase `Square` será subclase de `Polygon` y serán iguales a las del **ejercicio bonus A**.

Aquí viene lo distinto: la clase `Square` tendrá un _getter_ y un _setter_ para consultar o modificar el lado.

> Desde una subclase podemos acceder a las propiedades de la clase original con `super.propiedad`.

Crearemos una instancia: un cuadrado de `7` de lado. Haremos lo siguiente:

1. Pediremos el área y la guardaremos en una variable
2. Cambiaremos el lado del cuadrado por `47`
3. Pediremos de nuevo el área y la guardaremos en otra variable
4. Compararemos que los valores son distintos. Si son iguales, ¡meeec!

\_\_\_\_\_\_\_\_\_\_

-->

## Recursos externos

### Mozilla Developer Network

Páginas donde se explica en más profundidad los conceptos de esta sesión

- [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
- [Constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor)
- [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

### Mozilla Hacks: ES6 in Depth

Lista de artículos de colaboradores de Mozilla explicando las novedades de ECMAScript 6

- [ES6 in Depth - Classes](https://hacks.mozilla.org/2015/07/es6-in-depth-classes/)
- [ES6 in Depth - Subclassing](https://hacks.mozilla.org/2015/08/es6-in-depth-subclassing/) (herencia)
- [ES6 in Depth - Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)

### This y classes pre ES6

- [Understanding the "this" keyword, call, apply, and bind in JavaScript](https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/)
- [A Beginner's Guide to JavaScript's Prototype](https://tylermcginnis.com/beginners-guide-to-javascript-prototype/)
