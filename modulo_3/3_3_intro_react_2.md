# Introducción a React - II

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)

<!-- /TOC -->

## Introducción

[react]: https://reactjs.org/

En esta sesión vamos a seguir aprendiendo cómo funciona la librería [React.js][react]. En concreto, vamos a ver que está basada en componente y cómo crear un componentes personalizable.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Un **componente web** es una parte de la interfaz de una página o aplicación web que podemos reutilizar. Por ejemplo, una línea de producto de un carrito de la compra, o un elemento colapsable.

Los frameworks o las librerías como React se basan en este concepto de componentes. De esta forma, todo lo que vamos a desarrollar son componentes que iremos usando para crear la interfaz deseada.

Los componentes de React, además, pueden personalizarse a través de un mecanismo llamado `props`, que no es otra cosa que pasarle valores a través de los atributos del componente HTML.

Aprenderemos que en React actualmente conviven dos tipos de componentes, los componentes de clase y los componentes funcionales, así que aprenderemos las diferencias entre ellos y en qué casos podemos usar unos u otros.

## Creando nuestro primer componente de clase

_¡Manos a la obra!_ Vamos a crear nuestro primer componente de clase en React. Va a ser un componente que nos muestre una imagen aleatoria de un gato usando la web de lorempixel, y que además será un enlace a una página. Primero, creamos un proyecto nuevo con `create-react-app`.

Para comenzar, vamos a crear un nuevo módulo JavaScript para definir el componente.

Para empezar a trabajar con componentes, y como ya hemos visto cómo se ordenan los proyectos en React, vamos a crear una carpeta `components` donde guardaremos nuestro componente principal `App.js`y los nuevos componentes que creemos a partir de ahora.

Crearemos un archivo dentro de esta carpeta llamado `RandomCat.js`. Tendremos que importar React de su módulo, y también exportar nuestro componente para que pueda ser usado desde fuera, por lo que nuestro código debería tener este aspecto:

**RandomCat.js**:

```js
import React from 'react';
// ...
// ...AQUÍ ESCRIBIREMOS NUESTRO COMPONENTE
// ...
export default RandomCat;
```

Crearemos el componente después del `import`. Un componente de clase será una subclase de la clase `Component` de React, así que escribiremos lo siguiente:

```js
class RandomCat extends React.Component {
  // class body
}
```

> ¿Nos suena esta estructura? ¡Claro que sí! Es la misma que hemos aprendido en las clases de JS.

Crearemos nuestros componentes siempre con **mayúscula inicial**, independientemente de si usamos componentes de clase o funcionales. Así los diferenciaremos de los componentes en JSX que representan etiquetas de HTML.

Los componentes de clase tienen un método `render()` que devuelve un elemento de JSX para que React lo pinte. Así que sobrescribiremos ese método (es decir, que declararemos un método con ese nombre):

```js
class RandomCat extends React.Component {
  render() {
    return (
      <a href="http://lorempixel.com">
        <img src="http://lorempixel.com/400/200/cats/" alt="Random cat" />
      </a>
    );
  }
}
```

_¡Ya está!_ Ahora para ver el resultado tendremos que decirle a React que lo pinte. Vamos a ver que para trabajar en React es buena idea utilizar `App.js` como componente principal que monte toda nuestra aplicación y llamar al resto de componentes desde ahí, así que para usar nuestro componente `RandomCat.js` en `App.js`, tendremos que importar nuestro componente del módulo, naturalmente. Escribiremos arriba:

**App.js**:

```js
import React from 'react';
import RandomCat from './RandomCat';
```

> Para importar de un archivo local, utilizaremos el prefijo `./` antes de la ruta. Sin embargo, no pondremos el prefijo cuando sea una dependencia en `npm`, como nos preconfigura `create-react-app` para `react` y `react-dom`.

Solo falta el paso final: es tan fácil como llamar a nuestro componente dentro del `return` de `App.js`:

```js
class App extends React.Component {
  render() {
    return (
      <div className="App">
        <RandomCat/>
      </div>
    );
  }
}
```

**Y voilá!** Nos debería quedar así:

**RandomCat.js**:

```js
import React from 'react';

class RandomCat extends React.Component {
  render() {
    return (
      <a href="http://lorempixel.com">
        <img src="http://lorempixel.com/400/200/cats/" alt="Random cat" />
      </a>
    );
  }
}

export default RandomCat;
```

**App.js**:

```js
import React from 'react';
import RandomCat from './RandomCat';

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <RandomCat/>
      </div>
    );
  }
}

export default App;
```

#### EJERCICIO 1

Vamos a partir del ejercicio 1 (o del 2) de la sesión anterior. Vamos a crear un nuevo componente `MediaCard` encargado de pintar una tarjeta social para un usuario. Vamos a cargar ese nuevo componente en nuestro componente principal`App.js`.

\_\_\_\_\_\_\_\_\_\_

### Componentes funcionales, otro tipo de componentes

Ya hemos visto cómo escribir un componente de clase en React, y curiosamente su estructura es igual a la estructura de las clases JS, vamos a ver ahora qué es un componente funcional.

Los componentes funcionales son otro tipo de componentes que utilizan la estructura de una función para definirse y más adelante, cuando veamos el uso de los hooks, aprenderemos que son los que vamos a utilizar en estos casos.

Actualmente, y dado que React es una tecnología muy nueva que aún está evolucionando, conviven estos dos tipos de componentes en los proyectos actuales (por eso, cuando habéis instalado React la primera vez habéis visto App.js escrtio en forma de función en lugar de como clase).

Vamos a ver cómo sería nuestro componente Greeting escrito como clase:

```js
import React from 'react';

class Greetings extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

export default Greetings;
```

Ahora echa un vistazo a cómo sería Greeting escrito como componente funcional:

```js
import React from 'react';

const Greetings = props => {
  return <h1>Hello, {props.name}!</h1>;
};

export default Greetings;
```

> **IMPORTANTE:** Como se puede ver en los dos ejemplos de código anteriores:
> - Las props en un componente de clase se usan con `this.props.name`. Las props están en `this` porque **son un atributo** de una clase de JavaScript.
> - Las props en un componente funcional se usan con `props.name`. Aquí las props son **el primer argumento de la función** y son un argumento de tipo objeto.
>
> La única diferencia entre ambas es sintáctica. Por lo demás funcionan exactamente igual.

Si lo combinamos con el _return_ implícito de las _arrow functions_ podríamos incluso hacer una estructura más corta, quedando así:

```js
import React from 'react';
// "arrow function" sin llaves, con "return" implícito
const Greetings = props => <h1>Hello, {props.name}!</h1>;

export default Greetings;
```

Puesto que, como ya hemos visto actualmente nos encontraremos los dos tipos de componentes en proyectos React vamos a potenciar que manejéis el uso de componentes de clase para aquellos que tienen un estado (concepto que ya aprenderemos) y el uso de componentes funcionales si desarrollais con _hooks_ (también os los presentaremos en próximas lecciones).

### Algunos detalles para tener en cuenta

Los conceptos que manejamos en los dos tipos de componentes, props, eventos, datos... son los mismos. Lo que cambia es la forma de escribirlos.
Los componentes de clase son antiguos. React ha decidido utilizar componentes funcionales porque son más sencillos y cómodos.
Por desgracia, hay muchas empresas que usan los componentes de clase y por ello tenemos que enseñar la versión antigua y la nueva. Puedes trabajar en un proyecto que maneje componentes de clase y es esencial que entiendas cómo se comportan hasta que el uso de hooks y componentes funcionales esté completamente extendido.

## Las `props` para personalizar un componente

Hasta aquí todo bien, pero ¿y si queremos que `RandomCat` no sea siempre igual? De la misma manera que pasamos atributos a los elementos del DOM, podemos pasar datos a los componentes de React.

```js
class Greeting extends React.Component {
  render() {
    return (
      <span>Hello, {this.props.name}!</span> // <span>Hello, María Moliner!</span>
    );
  }
}

const componentToRender = <Greeting name="María Moliner" />;

ReactDOM.render(componentToRender, document.getElementById('root'));
```

Estos datos se llaman `props` y se guardan en un atributo de las instancias del mismo nombre. Podemos acceder a él a través de `this.props`, en el caso de los componentes de clase o directamente usando `props` en el caso de un componente funcional. Es un objeto que contiene las claves y los valores de estos "atributos". Mira este ejemplo de props usadas en un componente de clase.

```js
render() {
  console.log(this.props); // { name: 'María Moliner' }
  // ...
}
```

Una de las pocas reglas estrictas de React: **no debemos modificar nunca las `props`**, puesto que son como los parámetros que se le pasan a una función, o al constructor de una clase. Si queremos calcular con esos datos, podremos hacerlo dentro del `render()` del componente, antes de devolver el JSX:

```js
render() {
  const upperCaseName = this.props.name.toUpperCase();

  return (
    <span>Hello, { upperCaseName }!</span> // <span>Hello, MARÍA MOLINER!</span>
  );
}
```

#### EJERCICIO 2

Vamos a partir del ejercicio 1 (el anterior). Vamos a usar las `props` para personalizar el contenido de una tarjeta social `MediaCard`. En concreto, vamos a personalizar

- el nombre del usuario
- la fecha
- la imagen
- el texto descriptivo
- el número de likes
- si el corazón está o no relleno

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

Convierte el componente `MediaCard` del ejercicio anterior en un componente funcional.

\_\_\_\_\_\_\_\_\_\_

## Creando varios componentes

Vamos a hacer un componente de clase más que sea la sección donde se mostrarán distintos gatos. Tendrá un título y una lista con los gatos. Así veremos cómo usar componentes anidados.

En nuestra carpeta components vamos a crear un nuevo archivo `CatList.js`:

**components/CatList.js**:

```js
import React from 'react';

class CatList extends React.Component {
  // class body
}

export default CatList;
```

El método `render()` devolverá un elemento `section` con un `h1` y una lista `ul` con tres elementos `li`:

**components/CatList.js**:

```js
// ...
class CatList extends React.Component {
  render() {
    return (
      <section className="section-cats">
        <h1>All Cats Are Beautiful</h1>
        <ul className="section-cats_list">
          <li>A cat</li>
          <li>Another cat</li>
          <li>
            <i>Moar</i> cats
          </li>
        </ul>
      </section>
    );
  }
}
// ...
```

Como queremos usar `RandomCat` dentro de `CatList`, tendremos que importarlo en la parte superior del archivo:

**components/CatList.js**:

```js
import React from 'react';
import RandomCat from './RandomCat';
// ...
```

Lo siguiente tenemos que agradecérselo a JSX: para usar nuestro componente solo tendremos que usarlo como si fuera una etiqueta de HTML normal. Así que cambiaremos cada uno de los textos de dentro de los elementos `li` por `<RandomCat />`:

**components/CatList.js**:

```js
// ...
<ul className="section-cats_list">
  <li>
    <RandomCat />
  </li>
  <li>
    <RandomCat />
  </li>
  <li>
    <RandomCat />
  </li>
</ul>
// ...
```

Finalmente, en el componente principal `App.js` importaremos el componente `CatList`:

**App.js**:

```js
import React from 'react';
import CatList from './CatList';

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <CatList/>
      </div>
    );
  }
}

export default App;
```

Ahora se verán tres gatos iguales por la caché de los navegadores web (la dirección de la imagen es la misma y reutilizan la llamada al servidor). Podemos modificar el componente `RandomCat` para que siempre sea diferente generando un número aleatorio. Declaramos una pequeña función y el número de gatos disponibles:

**RandomCat.js**:

```js
import React from 'react';

const getRandomInteger = maxNumber => Math.floor(Math.random() * maxNumber);
const NUMBER_OF_CATS = 10;
// ...
```

Y ahora solo tendremos que modificar el método `render()` para incluir la llamada a la función, que se ejecutará cada vez que React pinte un componente `RandomCat`:

**RandomCat.js**:

```js
// ...
render() {
  const randomCat = getRandomInteger(NUMBER_OF_CATS);

  return (
    <a href="http://lorempixel.com">
      <img src={ `http://lorempixel.com/400/200/cats/${randomCat}` } alt="Random cat" />
    </a>
  );
}
```

**¡Genial!** Nos quedará así:

**components/App.js**:

```js
import React from 'react';
import CatList from './CatList';

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <CatList/>
      </div>
    );
  }
}

export default App;
```

**components/CatList.js**:

```js
import React from 'react';
import RandomCat from './RandomCat';

class CatList extends React.Component {
  render() {
    return (
      <section className="section-cats">
        <h1>All Cats Are Beautiful</h1>
        <ul className="section-cats_list">
          <li>
            <RandomCat />
          </li>
          <li>
            <RandomCat />
          </li>
          <li>
            <RandomCat />
          </li>
        </ul>
      </section>
    );
  }
}

export default CatList;
```

**components/RandomCat.js**:

```js
import React from 'react';

const getRandomInteger = maxNumber => Math.floor(Math.random() * maxNumber);
const NUMBER_OF_CATS = 10;

class RandomCat extends React.Component {
  render() {
    const randomCat = getRandomInteger(NUMBER_OF_CATS);

    return (
      <a href="http://lorempixel.com">
        <img
          src={`http://lorempixel.com/400/200/cats/${randomCat}`}
          alt="Random cat"
        />
      </a>
    );
  }
}

export default RandomCat;
```

> **NOTA**: cuando manejamos un listado de componentes hermanos (como en los `li`s del ejemplo anterior), React nos da un _warning_ en la consola indicando que debemos dar un atributo `key` a cada elemento del listado. Este atributo debe ser único para cada elemento de la lista, normalmente se usa el `id` del elemento si viene del servidor aunque si no lo tenemos puede usarse el índice de un `for` o un `map`. Sirve para que React internamente pueda optimizar el pintado de los elementos.

#### EJERCICIO 4

Vamos a partir del ejemplo con un listado de gatos con fotos aleatorias. Usaremos las `props` para pasar el tamaño de la imagen a `RandomCat`. Pasaremos una anchura (`width`) y una altura (`height`), que serán enteros (píxeles). En el caso de que no se pasen `props`, `width` será de `400` y `height` será `200`.

Desde `CatList` declararemos que se pinten tres componentes `RandomCat`:

- Uno de 200x200 px
- Otro de 200x400 px
- Otro, al que no pasaremos `props`, que será de 400x200 px

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 5

En nuestra web de tarjetas sociales, vamos a crear un nuevo componente `MediaList` para manejar una lista de componentes `MediaCard`. Para ello, mostrará una nueva sección con un título y un listado de 3 componentes `MediaCard`. Cada tarjeta tendrá datos personalizados que definiremos mediantes `props` desde el componente madre, es decir, el que maneja la lista.

\_\_\_\_\_\_\_\_\_\_

## Publicar nuestra app React en GitHub Pages

`create-react-app` nos crea un entorno de desarrollo donde empezar a trabajar con React en nuestra máquina. Si queremos enseñar el resultado con GitHub Pages hay que hacer algunas cosillas antes de generar una versión para producción:

- rutas a los archivos principales serán relativas al dominio
- necesitaremos una carpeta determinada
- y, quizás, haya que cambiar algo de `http` a `https`.

> GitHub Pages se sirve como https y "pide" que el resto de recursos externos que pidamos usen el mismo protocolo. Esto se aplica, por ejemplo, a las peticiones a una API o las rutas de las imágenes.

Entraremos por terminal a nuestra carpeta de proyecto y esto es lo que hay que hacer:

1. Modificar `package.json` para que las rutas sean relativas a nuestros archivos: hay que añadir `"homepage": "./",`.
1. Ya que lo vamos a servir desde GitHub, y usa https, tendremos que cambiar cualquier recurso `http` a `https`: por ejemplo, en un fetch.
1. Ejecutar `npm run build` para que nos cree la versión para producción en la carpeta **build/**.
1. GitHub Pages funciona en la carpeta raíz o en la **docs/** de la rama master, así que querremos cambiar la carpeta **build/** por la carpeta **docs/**. Para ello, desde la terminal y colocados en la carpeta raíz del proyecto ejecutaremos `mv build docs`. Es importante saber que este paso lo tendremos que hacer cada vez que hagamos cambios y queramos reflejarnos en nuestra página de GitHub Pages.
1. Add, commit y push.
1. Casi listo, solo falta activar GitHub Pages para que se sirva desde la carpeta docs de nuestra rama master. Para eso como ya sabéis, desde la página principal del repositorio, podéis ir a la pestaña de Settings y una vez dentro, en la sección GitHub Pages, donde pone _"Source"_ seleccionar _"master branch /docs folder"_

**Y ya estaría.**

#### EJERCICIO 6

Publiquemos la aplicación del último ejercicio en GitHub Pages. ¡A por ello!

\_\_\_\_\_\_\_\_\_\_

## _Debugging_ de aplicaciones en React

[react-devtools-firefox]: https://addons.mozilla.org/firefox/addon/react-devtools/
[react-devtools-chrome]: https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi
[react-devtools-standalone]: https://www.npmjs.com/package/react-devtools

React, en cierto modo, reemplaza la jerarquía de elementos del DOM por una jerarquía de componentes. Además, prácticamente todo el comportamiento se deriva de los valores que tienen las `props` y el estado de los componentes. Por todo esto, a veces resulta un poco difícil de depurar con las herramientas de desarrollo incluídas en los navegadores web.

Para solucionar esto, el equipo de React proporciona una _webextension_ (extensión de navegador) específica para depurar aplicaciones en React. La extensión está disponible para [Chrome][react-devtools-chrome], para [Firefox][react-devtools-firefox] y también como [aplicación separada][react-devtools-standalone].

La extensión de los navegadores se integra con las herramientas de desarrollo (<kbd>F12</kbd>) en ambos navegadores:

![React DevTools integrado con las herramientas de desarrollo de Chrome](assets/images/3_13_react-devtools.png)

Cuando estemos en una página hecha con React, la pestaña React de las herramientas de desarrollo nos mostrará la **jerarquía de componentes**:

![React DevTools mostrando jerarquía de componentes de la página](assets/images/3_13_devtools-tree-view.png)

Tras seleccionar un componente, en el panel lateral de esa misma pestaña podremos ver más detalles y cambiar las `props` y el estado del componente en tiempo real:

![React DevTools editando el estado de un componente en tiempo real](assets/images/3_13_devtools-side-pane.gif)

## Recursos externos

### Egghead

Serie de clases en vídeo que introduce y explora los fundamentos básicos de React.

- [Start using React to build web applications](https://egghead.io/courses/start-learning-react)

### Web components

- [What are web components?](https://www.webcomponents.org/introduction)

### React documentation

- [Components and props](https://reactjs.org/docs/components-and-props.html)

### Documentación oficial de React devtools

- [React Developer Tools](https://github.com/facebook/react-devtools)
