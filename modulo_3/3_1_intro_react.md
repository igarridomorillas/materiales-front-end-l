# Introducción a React

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)

<!-- /TOC -->

## Introducción

[wp-poo]: https://es.wikipedia.org/wiki/Programaci%C3%B3n_orientada_a_objetos
[wp-paradigma]: https://es.wikipedia.org/wiki/Paradigma_de_programaci%C3%B3n

En esta sesión veremos el concepto de clases, que está muy relacionado con la [programación orientada a objetos][wp-poo] (OOP, según sus siglas en inglés). La POO es una manera consensuada de pensar la programación (un [paradigma][wp-paradigma]) que se usa en una gran variedad de lenguajes de programación.

En la última sección, veremos cómo reutilizar nuestro código entre distintos proyectos, o importar código ajeno.

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
    console.log("Woof, woof!");
  }
}

const laika = new Dog();
const hachiko = new Dog();

laika.bark(); // Woof, woof!
hachiko.bark(); // Woof, woof!
```

> **Nota**: Debes notar que para declarar un método en una clase, no usamos la palabra `function` sino directamente el nombre del método

## El constructor y `this`

El `constructor()` es un método especial de las clases. El constructor es el método encargado de inicializar la instancia, es decir, de preparar todo lo necesario para su creación. El constructor recibe los parámetros que se pasan al instanciar la clase con `new`:

```js
class Dog {
  constructor(name) {
    console.log(`(I have a conscience now. My name is ${name})`);
  }
}

const laika = new Dog("Laika"); // (I have a conscience now. My name is Laika)
```

En el constructor, además, es donde se declaran los atributos de la clase. Vamos a declarar el parámetro `name` como un atributo:

```js
class Dog {
  constructor(name) {
    this.name = name;
  }
}

const laika = new Dog("Laika");
const hachiko = new Dog("Hachiko");

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
    console.log("Woof, woof!");
  }

  reactToCall(shout) {
    if (shout.includes(this.name)) {
      console.log(`${this.name} wags its tail, happily.`);
    } else {
      this.bark();
    }
  }
}

const laika = new Dog("Laika");

laika.reactToCall("Hey, Laika!"); // 'Laika wags its tail, happily.'
laika.reactToCall("Hey, Hachiko!"); // 'Woof, woof!'
```

## Módulos de JS

Los módulos nos facilitan dividir nuestro código en pequeñas partes reutilizables. Podemos dividir nuestro código en partes tanto para **organizar** un proyecto, **compartir** código entre distintos proyectos nuestros o para **usar librerías** de terceros.

**dog.js**:

```js
class Dog {
  bark() {
    console.log("Wan, wan!");
  }
}

const FAMOUS_DOGS = ["Hachiko", "Laika", "101 Dalmatians"];

export { Dog, FAMOUS_DOGS };
```

**main.js**:

```js
import { Dog, FAMOUS_DOGS } from "./dog.js";

const hachiko = new Dog();

console.log(`Some famous dogs in history: ${FAMOUS_DOGS.join(", ")}...`); // 'Some famous dogs in history: Hachiko, Laika, 101 Dalmatians...'
hachiko.bark(); // 'Wan, wan!'
```

### `export`

Todo lo que hay dentro de un módulo de JavaScript pertenece exclusivamente al módulo por defecto. Nada se puede acceder desde fuera excepto si se **exporta**. La palabra clave `export` nos permite exportar una variable (`var`, `let` o `const`), función o clase que podrá ser **importada** por otro código más tarde.

Podemos exportar de varias maneras. Podemos exportar individualmente valores que ya hayamos declarado:

**module.js**:

```js
export const aConstant = "constant";

export function aFunction() {
  /* function body */
}
```

También podemos exportar todo de una sola vez (como un objeto envoltorio), que mejora la legibilidad del código cuando es extenso:

**module.js**:

```js
const aConstant = "constant";

function aFunction() {
  /* function body */
}

export { aConstant, aFunction };
```

Por último, podemos declarar un valor exportado por defecto, si queremos. Solo puede haber un valor exportado por defecto en cada módulo, y puede o no tener nombre:

**module_default-unnamed.js**:

```js
export default function () {
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
import { aConstant } from "./module.js";

console.log(aConstant); // 'constant'
```

E importaremos varios valores así:

**main.js**:

```js
import { aConstant, aFunction } from "./module.js";

aFunction(); // do things as declared in module.js
console.log(aConstant); // 'constant'
```

Si queremos cambiarle el nombre a algún valor, lo podemos hacer con `as`:

**main.js**:

```js
import { aFunction as functionFromModule } from "./module.js";

functionFromModule(); // do things as declared in module.js
```

```js
import { aConstant, aFunction as functionFromModule } from "./module.js";

functionFromModule(); // do things as declared in module.js
console.log(aConstant); // 'constant'
```

```js
import {
  aConstant as constantFromModule,
  aFunction as functionFromModule,
} from "./module.js";

functionFromModule(); // do things as declared in module.js
console.log(constantFromModule); // 'constant'
```

También podemos importar todo el contenido de un módulo con `*`. Esto nos importa todos los valores dentro de un objeto envoltorio al que debemos darle nombre con `as`:

**main.js**:

```js
import * as module from "./module.js";

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

## React

[react]: https://reactjs.org/

En este módulo trabajaremos en la librería [React.js][react]. React es una librería para crear interfaces de usuario que se creó en 2013 en el seno de Facebook y goza de buena salud en el ecosistema de JavaScript.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Es muy común en todos los ecosistemas de programación usar librerías o _frameworks_ que permiten terminar productos mucho más rápido y ahorran escribir código. JavaScript no es una excepción, y en su historia podemos contar varias librerías y _frameworks_ populares como jQuery &mdash;que suplió las carencias iniciales del lenguaje mientras maduraba&mdash;, Backbone.js, Angular o Vue.js.

En particular, el manejo del DOM en proyectos grandes de JavaScript es una fuente de problemas. Desde las _single page applications_ (SPAs) se empezaron a desarrollar _frameworks_ que ayudaban a controlar esto, entre otras cosas. Hoy en día, React es una de las librerías más extendidas y maduras, con gran soporte de la comunidad y muchos recursos disponibles. React es una librería especializada en crear interfaces de usuario componentizadas, no un _framework_, pero se suele meter en el "saco de los frameworks de front-end".

En nuestra actividad profesional nos encontraremos con diferentes _frameworks_ y librerías. Aprender a usar una librería externa nos ayudará a enfrentarnos a estas situaciones en la vida real.

## ¿En qué casos y por qué se utilizan los _frameworks_?

Un framework o librería JavaScript nos soluciona uno de los principales problemas de la programación front-end: mantener la **interfaz de usuario** (UI, del inglés _User Interface_) en sincronización con el **estado** nuestra aplicación.

Pero, _¿qué es el estado de una aplicación web?_ Una aplicación web, a diferencia de una simple página web, se encarga de **gestionar datos**. Por ejemplo, en una aplicación como GMail gestionamos datos de correos (nuevos, leídos, archivados, etc.) desde una interfaz. En una simple aplicación de una lista de tareas, manejamos datos de tareas, si están completados o las fechas de realización.

Volviendo a los frameworks, estos nos facilitan sincronizar el estado (los datos) con la interfaz (lo que se ve en la pantalla). Vamos a verlo con un ejemplo que ya conocemos: el juego de adivinar el número del módulo anterior. Necesitamos bastante código para tener sincronizado el estado del juego (el feedback sobre un intento y el número de intentos) con la interfaz.

```js
function showFeedback(text) {
  const feedbackContainer = document.querySelector(".feedback");
  feedbackContainer.innerHTML = text;
}

function incrementTrials() {
  trials++;
  const trialsOnPage = document.querySelector(".trials");
  trialsOnPage.innerHTML = trials;
}
```

Este código de sincronización puede complicarse mucho (como habéis podido comprobar en el proyecto grupal del módulo anterior). Y es también muy acoplado a la interfaz (cambiar el HTML implica cambios en el código) y es muy propenso a errores. Por esto, las librerías como React nos ayudan mucho porque hacen esta sincronización por nosotros y nos evitan muchos problemas. A cambio, vamos a tener que trabajar de una forma determinada para aprovechar las ventajas que el frameworks nos da.

A parte de esta ventaja fundamental, otras ventajas de usar frameworks son

- facilitan el trabajo con componentes web
- tienen extensiones del navegador que facilitan el debugging
- facilitan el desarrollo de SPAs (del inglés _Single Page Applications_)

## Qué es React

Hasta ahora hemos visto cómo crear webs escribiendo la vista en archivos HTML y el comportamiento, la lógica, en archivos JavaScript. La tendencia actual es escribir vista y comportamiento juntos, en lo que llamamos componentes, que serán reutilizables.

React es una librería que nos permite hacer componentes gráficos con los que estructurar nuestra web. Los componentes gráficos se pintarán "solos" en el DOM, sin que tengamos que manejarlo "a mano". Además, React lo hace de una manera pensada para que los componentes cambien, así que crearemos webs muy reactivas y rápidas.

Es intuitivo hacer webs con React porque todo son componentes que llaman a otros componentes. El flujo es unidireccional (de arriba abajo), así que es fácil entender y solucionar los errores que pueda haber: si el error no está en mi componente, está en quien ha llamado a mi componente y cómo.

## "Hola, mundo" con `create-react-app`

Vamos a crear nuestro primer "¡Hola, mundo!" con React. Usaremos `create-react-app`, una herramienta generador que nos automatiza instalar React y Babel, que transformará código ES6 en ES5, y nos preconfigura un proyecto. ¡Manos a la obra!

Necesitaremos Node.js instalado, pero esto ya lo tenemos. Primero instalamos de forma global la utilidad de `create-react-app`, y luego creamos nuestro proyecto de React 'my-react-project' ejecutando esto en un terminal:

```sh
npm install -g create-react-app
create-react-app my-react-project
```

> **NOTA:** Recuerda que si al instalar algo en la consola nos da un error **EACCES** es porque necesitamos hacerlo con permisos de super administrador y para ello usamos `sudo`.

Esto nos creará una carpeta `my-react-project` y dentro tendremos todo listo. Para verlo, entramos dentro de la carpeta y ejecutaremos el proyecto con `npm`:

```sh
cd my-react-project
npm start
```

`create-react-app` nos ha instalado un _live-server_, así que sin cerrar el navegador ni el terminal, vamos a abrir el archivo `my-react-project/src/App.js` y probar a cambiar la frase **Edit src/App.js and save to reload** por **¡Hola, mundo!**. Guardamos y cambiamos al navegador.

!["Hola, mundo" en React](assets/images/3_4_react-hello-world.png)

## Estructura de un proyecto React creado con `create-react-app`

Un proyecto en React, en principio, tendrá un solo archivo HTML, y al menos un archivo JavaScript desde el que importaremos la librería de React.Sin embargo, trabajaremos con una estructura bien organizada para crear proyectos de mediano tamaño con `node` y `npm` más parecida a esta:

```
my-react-project
├── .gitignore
├── package.json
├── node_modules
│   ├── react
│   └── react-dom
├── public
│   └── index.html
└── src
    ├── images
    │   └── logo.png
    ├── stylesheets
    │   ├── index.scss
    │   └── index.css
    ├── components
    │   └── a-component.js
    └── index.js
```

`npm` instalará las dependencias en la carpeta `node_modules`, de donde podremos importar módulos de JS como `react` y `react-dom` a nuestro código.
Nuestro código se agrupará dentro de la carpeta `src`, excepto el único archivo HTML que usaremos, que estará en `public/index.html`.

Nuestros componentes de React irán en la carpeta `src/components`, cada uno en su fichero.

Basta de cháchara: ¡empecemos!

Cuando creamos un proyecto nuevo de React se nos crea una estructura la estructura de ficheros y carpetas que hemos visto antes. Vamos a ver cuáles son los ficheros principales que necesitamos conocer.

### `public/index.html`

Es el único fichero HTML que usaremos en nuestra aplicación. Podemos modificar algunas cosas pequeñas para personalizar la aplicación: añadir etiquetas `meta`, cargar fuentes, definir el título, etc. En el `body` se carga un `div` con identificador `root` que será donde se carga la aplicación de React.

### `src/index.js`

Este será el fichero JS de entrada a nuestra aplicación React. Será el único en el que carguemos `ReactDOM` y se encarga de acceder a un nodo del DOM (el `div` que antes identificamos como `root`) e importar y pintar el componente principal de la aplicación, en este caso, llamado `App`.

```js
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```

Para pintar el componente `App` usamos una sintaxis un poco rara: _¡es como si `App` fuese una etiqueta del HTML!_ Vamos a verlo en más profundidad en el siguiente fichero.

### `src/App.js`

Este fichero corresponde a nuestro primer _componente_ de React, pero ya veremos qué es un componente más adelante. De momento, vamos a pensar que quizá al modificar el archivo `App.js` os haya sorprendido algo. _"¿Eso no es HTML? ¡Pero si esto es un archivo JavaScript!"_:

#### IMPORTANTE

En las nuevas versiones de **Create React App** el componente `App` ya no es una clase sino una función y algunos de los ejemplos de código pueden variar. En clase veremos cómo gestionar esto y para ello debéis instalar esta extensión de Code: [react-pure-to-class-vscode](https://marketplace.visualstudio.com/items?itemName=angryobject.react-pure-to-class-vscode).

```js
import React, { Component } from "react";
import logo from "./logo.svg";
import "./App.css";

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">¡Hola, mundo!</h1>
        </header>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;
```

Esas etiquetas `div`, `header`, `img`, `h1` y `p` son una extensión de la sintaxis de JavaScript que se llama **JSX**. JSX nos facilita escribir código que React transformará luego en elementos reales del DOM. De esta forma podemos definir fácilmente el contenido de un elemento porque usa la sitaxis de HTML que ya conocemos.

Como JSX no deja de ser **código JavaScript**, lo podemos tratar como tal. Por ejemplo, podemos guardar elementos en una variable. También podemos usar expresiones JavaScript dentro de esa sintaxis con `{` y `}`, como si fuera la interpolación de cadenas de ES6 (pero sin `$`):

```js
const titleElement = <h1>¡Hola, mundo!</h1>;

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">{titleElement}</header>
      </div>
    );
  }
}
```

Como es HTML, podemos añadir atributos a los elementos que definamos con JSX:

```js
const titleElement = <h1 className="App-title">¡Hola, mundo!</h1>;
```

> **NOTA**: `class` es una palabra reservada en JavaScript, así que tendremos que usar `className` como nombre de atributo cuando queramos asignar una clase CSS

Por último, hay que destacar otra cosa de este fichero: estamos importando imágenes y CSS. _¿Y esooo?_ Pues porque en React tenemos la posibilidad y es una buena práctica trabajar de esta forma: desde un componente (fichero JS) importamos las imágenes y CSS que necesitemos para montar la interfaz del componente. Y confiamos en que la configuración del automatizador que tenemos por debajo (en este caso webpack), se encarga de importar los CSS desde el HTML (para que el navegador los entienda) y modificar las imágenes por su ruta para que puedan ser visualizadas. De momento nos quedamos con que _en React se hace así_.

### JSX y el método `render`

Para terminar, recordemos que el JSX que escribimos al final se convierte en código JavaScript. Pero entonces, ¿por qué usamos JSX y no directamente escribimos JavaScript? Porque la sintaxis de JSX es muy cercana a HTML, mucho más legible y simplifica el desarrollo de nuestros componentes. _¿Y si no usáramos JSX?_ Vamos a ver un ejemplo:

```js
const titleClassNames = "App-title";
const titleElement = <h1 className={titleClassNames}>¡Hola, mundo!</h1>;
```

Este ejemplo de JSX se transformará en este JavaScript:

```js
const titleClassNames = "App-title";
const titleElement = React.createElement(
  "h1",
  { className: titleClassNames },
  "¡Hola, mundo!"
);
```

React pintará en el DOM el HTML correspondiente al JSX que se devuelve desde el método `render()`. En este caso, el HTML quedará así:

```html
<h1 class="App-title">¡Hola, mundo!</h1>
```

Muy parecido al JSX que hemos escrito, ¿verdad?

#### EJERCICIO 1

Vamos a crear un nuevo proyecto de React llamado **mediacard**. Vamos a maquetar esta tarjeta dentro del método `render` de nuestro componente `App` para que tenga un diseño lo más parecido posible al de la imagen. Podéis usar una imagen a vuestra elección en lugar de la que aparece en el diseño, y Font-Awesome para el icono del corazón. De esta forma, aprenderemos a cómo trabajar con cosas que ya conocemos (HTML y CSS) en una aplicación de React.

![Media Card](assets/images/3_4_media-card.png)

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

Partiendo del ejercicio anterior, en este ejercicio aprenderemos mejor cómo funciona JSX. Para ello vamos a asignar nombres a las variables, un tema que será importante cuando creemos nuestros componentes más adelante. Partiendo del ejercicio anterior vamos a hacer que el `return` de `render()` devuelva una sola variable, para ello, vamos a extraer a variables cada una de las "etiquetas" del contenido del `return` del ejercicio original. Por ejemplo, una variable para la cabecera, y otra para el párrafo. Haremos que los nombres de nuestras variables sean descriptivos y, cuando sea posible, cortos.

```js
render() {
  /* aquí irán el resto de variables que extraeremos */
  const appRoot = (
    <div className="card">
    ...
    </div>
  );

  return appRoot;
}
```

\_\_\_\_\_\_\_\_\_\_

## Usando Sass en nuestro proyecto de React

Durante el curso hemos usado `gulp` para compilar Sass en nuestro proyectos. En el caso de los proyectos de React, que creamos con `create-react-app`, ya tienen su propio sistema de automatización de tareas que convierte los ficheros en ES6 a ES5 con Babel, y lanza un servidor local. Es mejor que, por tanto, en vez de incluir más herramientas como `gulp` usemos el sistema de automatización que ya tenemos (basado en [webpack](https://webpack.js.org/), por cierto) para observar los ficheros SCSS y compilarlos a CSS.

Para utilizar SASS en nuestro proyecto REACT simplemente podemos enlazar ficheros `.scss` desde nuestros componentes y webpack se encargará de hacer la conversión a CSS. El único paso adicional es instalar `node-sass`, cuando lo hagamos nos aparecerá este warning al intentar usar Sass por primera vez.

```
To import Sass files, you first need to install node-sass.
Run `npm install node-sass@4.14.1` or `yarn add node-sass` inside your workspace.
```

Así que si ejecutamos `npm install node-sass` en nuestra terminal la primera vez, tendremos listo nuestro proyecto para utilizar SASS.

### ¿Y cómo quedará esto en nuestros proyectos?

Vamos a partir del proyecto base que nos crea `create-react-app` y vamos a cambiar nuestro `App.css` a `App.scss`, ahora enlazamos directamente nuestro scss:

**App.js**

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.scss';

class App extends Component {
  ···
}

export default App;
```

Vale, ¿y si quiero tener archivos importados para usar variables y parciales?

Pues igual que siempre, en el mismo ejemplo: Desde `App.scss` vamos a importar un archivo de variables `_vars.scss`, y a usarlo!

**\_vars.scss**

```scss
$bg: #282c34;
```

**App.scss**

```scss
@import 'vars';
.App {
  text-align: center;
}

.App-logo {
  animation: App-logo-spin infinite 20s linear;
  height: 40vmin;
}

.App-header {
  background-color: $bg;
  ···
}
```

y `App.js` se mantiene igual que antes:

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.scss';

class App extends Component {
  ···
}

export default App;
```

#### EJERCICIO 3

Vamos a modificar el ejercicio anterior de la tarjeta para hacerlo con Sass dentro de nuestro proyecto de React.

\_\_\_\_\_\_\_\_\_\_

## BONUS: Interfaz declarativa VS imperativa

Con React haremos interfaces declarativas, en vez de imperativas. La programación declarativa nos permite focalizarnos en **el resultado final** de lo que programamos, en vez de en los detalles específicos de cómo se lleva a cabo el resultado.

No tendremos que seleccionar qué elemento del DOM tiene que cambiar cuando se cumpla una condición y qué otro cambiará cuando se cumpla otra. En vez de eso, **declararemos** lo que debe resultar, el QUÉ, y ya se encargará React del CÓMO pintar en el DOM.

```js
const person = {
  fullName: {
    name: "Ada",
    lastName: "Lovelace",
  },
  title: "Countess of Lovelace",
  areas: ["Mathematics", "Computing"],
};
const personCardElement = document.getElementById("person-card");

// CÓMO, imperativa
const cardTitle = document.createElement("h2");
cardTitle.textContent = `${person.fullName.name}, ${person.title}`;
cardTitle.classList.add("card-title");
personCardElement.appendChild(cardTitle);

const cardList = document.createElement("ul");
cardList.classList.add("card-area-list");
for (const area of person.areas) {
  const cardListItem = document.createElement("li");
  cardListItem.classList.add("card-area");
  cardListItem.textContent = area;
  cardList.appendChild(cardListItem);
}
personCardElement.appendChild(cardList);

// QUÉ, declarativa (React)
const personCardComponent = (
  <article>
    <h2 className="card-title">
      {person.fullName.name}, {person.title}
    </h2>
    <ul className="card-area-list">
      {person.areas.map((area) => (
        <li className="card-area">{area}</li>
      ))}
    </ul>
  </article>
);

ReactDOM.render(personCardComponent, personCardElement);
```

Este flujo es más útil cuando creamos una aplicación web compleja que cambie mucho con la interacción del usuario o si recibimos **datos dinámicos** de un servidor. No importa lo que recibamos, una vez hayamos declarado lo que pintar en función a un formato dado, se pintará _solo_.

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

### React Docs

La documentación de React está **muy bien organizada y explicada**. Os recomendamos que recurráis a ella como consulta y ampliación de nuestros materiales:

- [Getting started](https://reactjs.org/docs/)
- [Versión española](https://es.reactjs.org/)

### Create React App

Guía oficial de instalación y uso de `create-react-app`.

- [Getting started with `create-react-app`](https://github.com/facebookincubator/create-react-app#getting-started)
