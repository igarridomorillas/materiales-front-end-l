# Introducción a React

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)

<!-- /TOC -->

## Introducción

Esta es una sesión de introducción a React. Para aprender lo que es React antes tenemos que saber un poquito sobre las **Clases** y los **Módulos** de JavaScript.

Os recomendamos que leais los apartados de **Clases y objetos** y **Módulos de JS** con el objetivo de tener una idea general de cómo funcionan. La parte importante de esta sesión es la de **React JS**.

> **Nota:** las clases de JS no tienen nada que ver con las clases de CSS. Es un concepto nuevo.

## Clases y objetos

Ya sabemos lo que es un objeto en programación: es una entidad que contiene unas propiedades dadas, que pueden ser valores o funciones.

Cuando tenemos un puñado de objetos parecidos porque tienen las mismas propiedades, podemos decir que esos objetos son del mismo tipo. Es decir, son de la misma "clase". Una clase es justo eso, una abstracción de los objetos que nos indica qué tienen en común.

**Las Adalabers explícais las Clases como una plantilla o molde** del que sacar muchos objetos parecidos. Los objetos sacados de este molde tienen los mismos nombres de propiedades pero diferentes valores.

```js
class Dog {
  // class body
}

const laika = new Dog();
const hachiko = new Dog();
```

**Una instancia** es un objeto de una clase que hayamos especificado. En el ejemplo anterior, `hachiko` y `laika` son instancias de la clase `Dog`. Dándole la vuelta, cuando creamos un objeto de una clase con el operador `new`, entonces estamos **instanciando** una clase. Las instancias comparten los métodos y atributos de la clase.

Dicho de otra forma si la clase es un molde, las instancias son los objetos que sacamos de dicho molde.

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

> **Nota**: Debes notar que para declarar un método en una clase, no usamos la palabra `function` sino directamente el nombre del método.

## El constructor y `this`

El `constructor()` es un método especial de las clases. El constructor es el método encargado de inicializar (o arrancar) la instancia, es decir, de preparar todo lo necesario para su creación. El constructor recibe los parámetros que se pasan al instanciar la clase con `new`:

```js
class Dog {
  constructor(name) {
    console.log(`I have a conscience now. My name is ${name}`);
  }
}

const laika = new Dog("Laika"); // I have a conscience now. My name is Laika
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

La palabra clave `this` dentro de la declaración de una clase hace referencia a la instancia de la clase que crearemos. Cuando declaramos atributos en el constructor con `this.miAtributo` como en el ejemplo anterior, estamos efectivamente declarando que "la instancia resultante (`this`) tendrá la propiedad `miAtributo`".

Una vez creada la instancia, para acceder a los atributos lo hacemos directamente como en el ejemplo, `laika.name`.

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

Los módulos nos facilitan dividir nuestro código en pequeñas partes reutilizables. Podemos dividir nuestro código en partes para **organizar** un proyecto, **compartir** código entre distintos proyectos...

> **Nota:** en el módulo 1 aprendimos a trabajar con partials de CSS y HTML. En el módulo 2 aprendimos a trabajar con partials de JS, pero esos partials son la forma antigua de separar el código. La forma moderna de usar partials en JS es con los módulos de JS.

Los módulos JS nos permiten tener código privado, es decir, variables y funciones que no son globales, es decir, que no son accesibles desde otros ficheros.

Esto nos vale para que desde otros ficheros no se pueda cambiar dichas variables o ejecutar dichas funciones.

También nos permite publicar algunas de esas variables y funciones. De esta forma elejimos qué código de un módulo es público y qué parte es privado. Para publicar variables y funciones usamos `export` y para usarlas desde otro fichero usamos `import`.

Supongamos que tenemos estos dos ficheros en nuestro proyecto:

El módulo `area.js` nos ayuda a calcular el área de un cuadrado y un tríangulo:

```js
// fichero area.js

// función privada
const rectangle = (base, height) => {
  return base * height;
}

// función pública
const getSquareArea = (base) => {
  return rectangle(base, base);
}

// función pública
const getTriangleArea = (base, height) => {
  return rectangle(base, height) / 2;
}

// con esta línea exportamos las funciones getSquareArea y getTriangleArea dentro de un objeto, por eso son públicas
// no exportamos rectangle porque no queremos, por eso es privada
export {
  getSquareArea: getSquareArea,
  getTriangleArea: getTriangleArea
};
```

El fichero **main.js** es el fichero principal de nuestra web:

```js
// fichero main.js

// con esta línea importamos todo lo que exporta el fichero ./area.js
import area from "./area.js";

// area es un objeto
const triangleArea = area.getTriangleArea(3, 6);

console.log(`Un triangulo de base 3 y altura 6 tiene un área de ${triangleArea}`); // 9
```

El fichero `area.js` es un módulo porque exporta cosas. El fichero `main.js` no es módulo porque no exporta nada.

### Librería Math

En el módulo 2 hemos usado **Math** para calcular un número aleatorio con `Math.random()`. Este es un buen ejemplo de cómo funcionan los módulos.

La librería Math tiene muchísimo código dentro pero solo exporta lo que quiere que usemos desde fuera. Ningún fichero externo a Math puede saber qué funciones y variables privadas tiene Math. Nadie sabe cómo calcula los números aleatorios. Solo sabemos que es capaz de calcularlos.

### `export`

Con `export` exportamos lo que queramos, una función, un array, un objeto, una variable, una constante, una clase...

Si queremos exportar varias cosas lo que hacemos es exportar un objeto que contenga dichas cosas.

El fichero `area.js` exporta un objeto con dos funciones dentro.

> **Nota:** Siempre hay que escribir `export` después de la variable, constante, función... que estamos exportando. Por ello es una buena practica escribir los `export` al final de nuestro fichero.

### `import`

Para usar código de un módulo, primero tendremos que importarlo desde el fichero principal. Si el módulo exporta un objeto, en el fichero principal obtenemos un objeto. Si el módulo exporta una función en el fichero principal obtenemos una función.

En el ejemplo de las áreas estamos importando todo el objeto:

```js
// fichero main.js
import area from "./area.js";
// area es un objeto
```

Pero si queremos importar solo la función `getTriangleArea` podemos hacer lo siguiente:

```js
// fichero main.js
import { getTriangleArea } from "./area.js";
// getTriangleArea es una función
```

De esta forma podemos elegir si importar todo el objeto o una propidad del objeto que nos interesa.

> **Nota:** Siempre hay que escribir `import` antes de usar la variable, constante, función... que estamos importando. Por ello es una buena practica escribir los `import` al principio de nuestro fichero.

> **Nota:** cuando ponemos `import area from "./area.js";` entre comillas debemos poner la ruta relativa entre el fichero `main.js` que es el que importa y el módulo `area.js` que es el que exporta. Esto es así para JS sepa relacionar los dos ficheros.

## React

[react]: https://reactjs.org/

En este módulo trabajaremos en la librería [React.js][react]. React es una librería para crear interfaces de usuario que se creó en 2013 en el seno de Facebook y goza de buena salud en el ecosistema de JavaScript.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Es muy común en todos los ecosistemas de programación usar librerías o _frameworks_ que permiten terminar productos mucho más rápido y ahorran escribir código. JavaScript no es una excepción, y en su historia podemos contar varias librerías y _frameworks_ populares como jQuery &mdash;que suplió las carencias iniciales del lenguaje mientras maduraba&mdash;, Backbone.js, Angular o Vue.js.

En particular, el manejo del DOM en proyectos grandes de JavaScript es una fuente de problemas. Desde las _single page applications_ (SPAs) se empezaron a desarrollar _frameworks_ que ayudaban a controlar esto, entre otras cosas. Hoy en día, React es una de las librerías más extendidas y maduras, con gran soporte de la comunidad y muchos recursos disponibles. React es una librería especializada en crear interfaces de usuario componentizadas. Es decir que vamos a dividir nuestro HTML en componentes.

Una vez que sepáis trabajar con React os va a ser muy fácil aprender otras librerías.

## ¿En qué casos y por qué se utilizan los _frameworks_?

Un framework o librería JavaScript nos soluciona uno de los principales problemas de la programación front-end: pintar los datos (o lo que es lo mismo, el estado) en el HTML de forma sencilla.

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

Este código de sincronización puede complicarse mucho (como habéis podido comprobar en el proyecto grupal del módulo anterior). Y es también muy acoplado a la interfaz (cambiar el HTML implica cambios en JS) y es muy propenso a errores. Por esto, las librerías como React nos ayudan mucho porque hacen esta sincronización por nosotros y nos evitan muchos problemas. A cambio, vamos a tener que trabajar de una forma determinada para aprovechar las ventajas que el frameworks nos da.

A parte de esta ventaja fundamental, otras ventajas de usar frameworks son:

- facilitan el trabajo con componentes web
- tienen extensiones del navegador que facilitan el debugging
- facilitan el desarrollo de SPAs (del inglés _Single Page Applications_)

## Qué es React

Hasta ahora hemos visto cómo crear webs escribiendo la vista en archivos HTML y el comportamiento, la lógica, en archivos JavaScript. La tendencia actual es escribir vista y comportamiento juntos, en lo que llamamos componentes, que serán reutilizables.

React es una librería que nos permite hacer componentes gráficos (botones, listados, cabeceras, inputs...) con los que estructurar nuestra web. Los componentes gráficos se pintarán "solos" en el DOM, sin que tengamos que manejarlo "a mano". Además, React lo hace de una manera pensada para que los componentes cambien, así que crearemos webs muy reactivas y rápidas.

Es intuitivo hacer webs con React porque todo son componentes que llaman a otros componentes. El flujo es unidireccional (de arriba a abajo), así que es fácil entender y solucionar los errores que pueda haber.

## "Hola, mundo" con `create-react-app`

Vamos a crear nuestro primer "¡Hola, mundo!" con React. Usaremos `create-react-app`, un generador que nos automatiza instalar React y Babel, que transformará código ES6 en ES5, y nos preconfigura un proyecto. ¡Manos a la obra!

Create react app es el starter kit de React.

Necesitaremos Node.js instalado, pero esto ya lo tenemos. Primero instalamos de forma global la utilidad de `create-react-app`, y luego creamos nuestro proyecto de React 'my-react-project' ejecutando esto en un terminal:

```bash
npm install -g create-react-app
```

```bash
create-react-app my-react-project
```

> **NOTA:** Recuerda que si al instalar algo en la consola nos da un error **EACCES** es porque necesitamos hacerlo con permisos de super administrador y para ello usamos `sudo`.

Esto nos creará una carpeta `my-react-project` y dentro tendremos todo listo. Además de crear el proyecto `create-react-app` nos hace un `npm install` para que no tengamos que hacerlo nosotras.

Para verlo, entramos dentro de la carpeta y ejecutaremos el proyecto con `npm`:

```sh
cd my-react-project
```

```bash
npm start
```

Cuando `npm start` esté listo podremos abrir la página http://localhost:3000 para ver nuestra web.

`create-react-app` nos ha instalado un _live-server_, así que sin cerrar el navegador ni el terminal, vamos a abrir el archivo `my-react-project/src/App.js` y probar a cambiar la frase **Edit src/App.js and save to reload** por **¡Hola, mundo!**. Guardamos y cambiamos al navegador.

!["Hola, mundo" en React](assets/images/3_4_react-hello-world.png)

## Estructura de un proyecto React creado con `create-react-app`

Un proyecto en React, en principio, tendrá un solo archivo HTML, y al menos un archivo JavaScript desde el que importaremos la librería de React. Sin embargo, trabajaremos con una estructura bien organizada para crear proyectos de mediano tamaño con `node` y `npm` más parecida a esta:

```
my-react-project
├─ .gitignore
├─ package.json
├─ node_modules
├─ public
│  └─ index.html
└── src
    ├─ images
    │  └─ logo.png
    ├─ stylesheets
    │  ├── index.scss
    │  └─ index.scss
    ├─ components
    │  ├─ footer.js
    │  ├─ header.js
    │  └─ main.js
    └─ index.js
```

`npm` instalará las dependencias en la carpeta `node_modules`, de donde podremos importar módulos de JS como `react` y `react-dom` a nuestro código.
Nuestro código se agrupará dentro de la carpeta `src`, excepto el único archivo HTML que usaremos, que estará en `public/index.html`.

Nuestros componentes de React irán en la carpeta `src/components`, cada uno en un fichero.

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
const titleElement = <h1 className="title">¡Hola, mundo!</h1>;
```

> **NOTA**: `class` es una palabra reservada en JavaScript, así que tendremos que usar `className` como nombre de atributo cuando queramos asignar una clase CSS.

Por último, hay que destacar otra cosa de este fichero: estamos importando imágenes y CSS. _¿Y esooo?_ Pues porque en React tenemos la posibilidad y es una buena práctica trabajar de esta forma: desde un componente (fichero JS) importamos las imágenes y CSS que necesitemos para montar la interfaz del componente. Y confiamos en que la configuración del automatizador que tenemos por debajo, se encarga de importar los CSS desde el HTML (para que el navegador los entienda) y modificar las imágenes por su ruta para que puedan ser visualizadas. De momento nos quedamos con que _en React se hace así_.

### JSX y el método `render`

Para terminar, recordemos que el JSX que escribimos al final se convierte en código JavaScript. Pero entonces, ¿por qué usamos JSX y no directamente escribimos JavaScript? Porque la sintaxis de JSX es muy cercana a HTML, mucho más legible y simplifica el desarrollo de nuestros componentes. _¿Y si no usáramos JSX?_ Vamos a ver un ejemplo:

```js
const titleClassNames = "title";
const titleElement = <h1 className={titleClassNames}>¡Hola, mundo!</h1>;
```

Este ejemplo de JSX se transformará en este JavaScript que usa las funciones del DOM avanzado:

```js
const titleClassNames = "title";
const titleElement = React.createElement(
  "h1",
  { className: titleClassNames },
  "¡Hola, mundo!"
);
```

React pintará en el DOM el HTML correspondiente al JSX que se devuelve desde el método `render()`. En este caso, el HTML quedará así:

```html
<h1 class="title">¡Hola, mundo!</h1>
```

Muy parecido al JSX que hemos escrito, ¿verdad?

#### EJERCICIO 1

Vamos a crear un nuevo proyecto de React llamado **mediacard**. Vamos a maquetar esta tarjeta dentro del componente `App.js` para que tenga un diseño lo más parecido posible al de la imagen. Podéis usar una imagen a vuestra elección en lugar de la que aparece en el diseño, y Font-Awesome para el icono del corazón. De esta forma, aprenderemos a cómo trabajar con cosas que ya conocemos (HTML y CSS) en una aplicación de React.

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

Si queremos usar CSS en nuestro proyecto solo tenemos que editar el fichero `index.css`.

Si queremos usar Sass tenemos que hacer varias cosas:

- Instalar Sass en el proyecto con `npm install node-sass`.
- Crear un fichero con la extensión Sass, por ejemplo `App.scss` que sea hermano de `App.js`.
- Importar `App.scss` desde `App.js` escribiendo la línea `import './App.scss'` al principio del fichero `App.js`.
- Escribir nuestro código Sass dentro de `App.scss`.

Podemos usar todas las funcionalidades propias de Sass como anidación, variables, partials, mixins...

### ¿Y cómo quedará esto en nuestros proyectos?

Vamos a partir del proyecto base que nos crea `create-react-app` y vamos a cambiar nuestro `App.css` a `App.scss`, ahora enlazamos directamente nuestro scss:

**App.js**

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.scss';

...

export default App;
```

#### EJERCICIO 3

Vamos a modificar el ejercicio anterior de la tarjeta para hacerlo con Sass dentro de nuestro proyecto de React.

\_\_\_\_\_\_\_\_\_\_

## BONUS: Interfaz declarativa VS imperativa

Con React haremos interfaces declarativas, en vez de imperativas. La programación declarativa nos permite focalizarnos en **el resultado final** de lo que programamos, en vez de en los detalles específicos de cómo se lleva a cabo el resultado.

No tendremos que seleccionar qué elemento del DOM tiene que cambiar cuando se cumpla una condición y qué otro cambiará cuando se cumpla otra. En vez de eso, **declararemos** lo que debe resultar, el QUÉ, y ya se encargará React del CÓMO pintar en el DOM.

```js
// programación imperativa
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
```

```js
// programación declarativa
const person = {
  fullName: {
    name: "Ada",
    lastName: "Lovelace",
  },
  title: "Countess of Lovelace",
  areas: ["Mathematics", "Computing"],
};

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
