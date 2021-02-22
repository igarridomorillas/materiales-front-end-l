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

En esta sesión vamos a seguir aprendiendo cómo funciona la librería [React.js][react]. En concreto, vamos a ver que está basada en componentes y cómo crear un componente personalizable.

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
import React from "react";
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

Crearemos nuestros componentes siempre con **mayúscula inicial**, independientemente de si usamos componentes de clase o funcionales. Así los diferenciaremos de los componentes en JSX que representan etiquetas de HTML.

Los componentes de clase tienen un método (o función) llamado `render()` que devuelve una etiqueta de HTML para que React lo pinte. Así que sobrescribiremos ese método (es decir, que declararemos un método con ese nombre):

```js
import React from "react";

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

_¡Ya está!_ Ahora para ver el resultado tendremos que decirle a React que lo pinte. Vamos a ver que para trabajar en React es buena idea utilizar `App.js` como componente principal que monte toda nuestra aplicación y llamar al resto de componentes desde ahí, así que para usar nuestro componente `RandomCat.js` en `App.js`, tendremos que importar nuestro componente del módulo, naturalmente. Escribiremos arriba:

**App.js**:

```js
import React from "react";
import RandomCat from "./RandomCat";
```

> Para importar de un archivo local, utilizaremos el prefijo `./` antes de la ruta. Sin embargo, no pondremos el prefijo cuando sea una dependencia en `npm`, como nos preconfigura `create-react-app` para `react` y `react-dom`.

Solo falta el paso final: es tan fácil como llamar a nuestro componente dentro del `return` de `App.js`:

```js
import React from "react";

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <RandomCat />
      </div>
    );
  }
}

export default App;
```

**Y voilá!** Nos debería quedar así:

**RandomCat.js**:

```js
import React from "react";

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
import React from "react";
import RandomCat from "./RandomCat";

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <RandomCat />
      </div>
    );
  }
}

export default App;
```

#### EJERCICIO 1

Vamos a partir del ejercicio 1 (o del 2) de la sesión anterior. Vamos a crear un nuevo componente `MediaCard` encargado de pintar una tarjeta social para un usuario. Vamos a cargar ese nuevo componente en nuestro componente principal `App.js`.

\_\_\_\_\_\_\_\_\_\_

### Componentes funcionales, otro tipo de componentes

Ya hemos visto cómo escribir un componente de clase en React, y curiosamente su estructura es igual a la estructura de las clases JS, vamos a ver ahora qué es un componente funcional.

Los componentes funcionales son otro tipo de componentes que utilizan la estructura de una función para definirse y en próximas lecciones, cuando veamos el uso de los hooks, aprenderemos que son los que vamos a utilizar en estos casos.

Actualmente, y dado que React es una tecnología muy nueva que aún está evolucionando, conviven estos dos tipos de componentes en los proyectos actuales (por eso, cuando habéis instalado React la primera vez habéis visto App.js escrtio en forma de función en lugar de como clase).

Vamos a ver cómo sería nuestro componente Greeting escrito como clase:

```js
import React from "react";

class Greetings extends React.Component {
  render() {
    return <h1>Hello, Maricarmen!</h1>;
  }
}

export default Greetings;
```

Ahora echa un vistazo a cómo sería Greeting escrito como componente funcional:

```js
import React from "react";

const Greetings = () => {
  return <h1>Hello, Maricarmen!</h1>;
};

export default Greetings;
```

Si lo combinamos con el _return_ implícito de las _arrow functions_ podríamos incluso hacer una estructura más corta, quedando así:

```js
import React from "react";

// "arrow function" sin llaves, con "return" implícito
const Greetings = () => <h1>Hello, Maricarmen!</h1>;

export default Greetings;
```

### Algunos detalles para tener en cuenta

Los conceptos que manejamos en los dos tipos de componentes, props, eventos, datos... son los mismos. **Lo que cambia es la forma de escribirlos, es decir, la sintaxis.**

Los componentes de clase son antiguos. React ha decidido utilizar componentes funcionales porque son más sencillos y cómodos.
Por desgracia, hay muchas empresas que usan los componentes de clase y por ello tenemos que enseñar la versión antigua y la nueva. Puedes trabajar en un proyecto que maneje componentes de clase y es esencial que entiendas cómo se comportan hasta que el uso de hooks y componentes funcionales esté completamente extendido.

### Método render: un solo hijo

Es de suma importancia tener en cuenta que el método render solo puede tener un hijo o etiqueta HTML, y a partir de él sí que puede tener tantos nietos como sea necesario, esto es porque dicho método render contiene un return y solo puede retornar un elemento o etiqueta contenedora.

Por lo tanto algo como lo siguiente NO puede ocurrir, donde podemos observar que hay un return con dos hijos directos:

```js
render () {
  return (
    <p>Lorem</p>
    <h2>Lorem</h2>
  );
}
```

Si escribimos un componente con dos hijos directos en el `return` React lanzará un error.

## Las `props` para personalizar un componente

Hasta aquí todo bien, pero ¿y si queremos que `RandomCat` no sea siempre igual?

Recuerdas que JS usamos las funciones para reutilizar código y que gracias a los parámetros y argumentos podemos pasar datos a las funciones para personalizar su comportamiento. Pues las props es exactamente lo mismo. El componente (ya sea de clase o funcional) sería la función de JS (el código reutilizable) y las props serían los parámetros (datos que les pasamos para personalizar su comportamiento).

Otro ejemplo de lo que son las props también serían los partials de HTML que aprendimos en el módulo 1. A los partials les pasábamos datos (lo que aquí son las `props`) a través de los atributos. Dentro del partial usábamos esos datos con el `@@`.

### Props en los componentes de clase

```js
// componente madre
import React from 'react';
import Greeting from './Greeting'; // importamos el componente hija para usarlo en el render()

class App extends React.Component {
  render() {
    return (
      <Greeting name="María Moliner" />
    );
  }
}

export default App;
```

```js
// componente hija
import React from 'react';

class Greeting extends React.Component {
  // en this.props recibo las props que me pasa mi madre
  render() {
    return (
      <span>Hello, {this.props.name}!</span> // <span>Hello, María Moliner!</span>
    );
  }
}

export default Greeting;
```

Los datos que pasamos de un componente madre a su componente hija los llamamos `props` (properties). En el ejemplo superior `App.js` le pasa a `Greeting.js` las props `{ name: 'María Moliner' }`.

En los componentes de clase React las guarda en `this.props` y podemos usarlas escribiendo `this.props.name` o `this.props.nombreDeLaPropQueQuieroUsar`. `this.props` siempre es un **objeto** que contiene las claves y los valores de estos "atributos". Mira este ejemplo de props usadas en un componente de clase.

Una de las pocas reglas estrictas de React: **no debemos modificar nunca las `props`**. Las props las podmeos leer, añadir al HTML para que se pinten en pantalla, pero no modificarlas. Si necesitamos modificar una `prop` las guardaremos en variables o constantes para evitar modificar la `prop`, como vemos en el siguiente ejemplo.

```js
// componente hija
import React from 'react';

class Greeting extends React.Component {
  render() {
    console.log(this.props);
    const upperCaseName = this.props.name.toUpperCase();

    return (
      <span>Hello, { upperCaseName }!</span> // <span>Hello, MARÍA MOLINER!</span>
    );
  }
}

export default Greeting;
```

> **Nota:** hasta que domines las `props` es una buena práctica escribir `console.log(this.props);` al principio del método `render()` en los componentes de clase.

#### EJERCICIO 2

Vamos a partir del ejercicio 1. Vamos a usar las `props` para personalizar el contenido de una tarjeta social `MediaCard`. En concreto, vamos a personalizar:

- el nombre del usuario
- la fecha
- la imagen
- el texto descriptivo
- el número de likes
- si el corazón está o no relleno

Desde `App.js` vamos a pasar props al componente `MediaCard.js`. Este segundo componente debe usarlas.

\_\_\_\_\_\_\_\_\_\_

### Props en los componentes funcionales

Como hemos dicho anteriormente los conceptos que aprendemos sobre componentes de clases son exactamente igual que los que aprendemos en componentes funcionales. La diferencia entre uno y otro es simplemente un **cambio de sintaxis**. Por ello lo que hemos aprendido de `props` en los componentes de clase nos vale igual para los componentes funcionales.

En los componentes funcionales:

- Pasar `props` de un componente madre a un componente hija es exactamente igual.
- Recibir `props` en un componente hija cambia un poco.

Si pasamos el componente `Greeting` de clase a funcional el código sería el siguiente:

```js
// componente hija
import React from 'react';

const Greeting = (props) => { // en los componentes funcionales recibimos las props como único parámetro de la función
  console.log(props);
  const upperCaseName = props.name.toUpperCase();
  return (
    <span>Hello, { upperCaseName }!</span>
  );
}

export default Greeting;
```

Es decir, los componentes funcionales no son clases y por ello no tienen `this.props`. A cambio un componente funcional (que es una función) recibe las `props` por los parámetros de la función. Por ello, si un componente de clase usábamos `this.props.name` en uno funcional usamos `props.name`.

Los componentes funcionales solo reciben un argumento que es `props`. Los componentes no los ejecutamos nosotras directamente, es React quien los ejecuta y quién decide qué recibimos como parámetros de la función.

> **Nota:** hasta que domines las `props` es una buena práctica escribir `console.log(props);` al principio de la función en los componentes funcionales.

### Props que no existen

Si tenemos estos dos componentes:

```js
// componente madre
import React from 'react';
import Greeting from './Greeting';

class App extends React.Component {
  render() {
    return (
      <Greeting name="María Moliner" />
    );
  }
}

export default App;
```

```js
// componente hija
import React from 'react';

class Greeting extends React.Component {
  // en this.props recibo las props que me pasa mi madre
  render() {
    console.log(this.props)
    return (
      <span>Hello, {this.props.title}!</span>
    );
  }
}

export default Greeting;
```

Podemos ver que el componente hija `Greeting.js` está intentando usar `this.props.title`. Sin embargo el componente madre `App.js` está pasando a su hija el componente `name="María Moliner"`.

Esté código está mal porque desde la madre pasamos la prop `name` y en la hija la intentamos usar como `title`. Es decir, en la hija `this.props.title` es `undefined`.

Por ello cuando pasamos `props` de madres a hijas, nos tenemos que preocupar de dos cosas:

- Que el nombre de la `prop` sea igual en la madre y en la hija.
- Que el tipo de dato tenga sentido. Si desde la madre pasamos un texto en la hija trabajaremos con una hija. Si desde la madre pasamos un array en la hija deberemos hacer cosas que se puedan hacer con un array como por ejemplo recorrerlas en un bucle.

### Componentes de clase y funcionales trabajando juntos

En un proyecto podemos tener componentes de clase y funcionales trabajando juntos. Cada componente de un proyecto puede ser de un tipo u otro.

**Un componente no sabe de qué tipo es su componente madre, ni sabe de qué tipo son sus componentes hijos.**
#### EJERCICIO 3

Convierte el componente `MediaCard` del ejercicio anterior en un componente funcional.

### Muchos niveles de componetes

Si tenemos un componente abuela, otro madre y otro nieta podemos pasar `props` de la abuela a la nieta pasando a través de la madre. Aquí tenemos un ejemplo:

```js
// componente abuela
import React from 'react';
import Greeting from './Greeting';

class App extends React.Component {
  render() {
    return (
      <Greeting name="María Moliner" />
    );
  }
}

export default App;
```

```js
// componente madre
import React from 'react';
import Title from './Title';

class Greeting extends React.Component {
  // en this.props recibo las props de la abuela
  render() {
    console.log(this.props)
    return (
      <span>Hello,
        {/* aqui le paso la prop name de la abuela a la nieta, y se la paso llamándola title */}
        <Title title={this.props.name} />
      !</span>
    );
  }
}

export default Greeting;
```

```js
// componente nieta
import React from 'react';

class Title extends React.Component {
  // en this.props recibo las props de la madre
  render() {
    console.log(this.props)
    return (
      {/* aqui recibo la prop title de la madre y la nieta, como la madre me pasa la prop title aquí puedo usarla con this.props.title */}
      <span>{this.props.title}</span>
    );
  }
}

export default Title;
```

Si nos fijamos el componente madre `Greeting.js` funciona como un componente intermediaria entre la abuela y la nieta.

\_\_\_\_\_\_\_\_\_\_

## Creando varios componentes

Vamos a hacer un componente de clase más que sea la sección donde se mostrarán distintos gatos. Tendrá un título y una lista con los gatos. Así veremos cómo usar componentes anidados.

En nuestra carpeta components vamos a crear un nuevo archivo `CatList.js`:

**components/CatList.js**:

```js
import React from "react";

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
          <li>Moar cat</li>
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
import React from "react";
import RandomCat from "./RandomCat";
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
import React from "react";
import CatList from "./CatList";

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <CatList />
      </div>
    );
  }
}

export default App;
```

Ahora se verán tres gatos iguales por la caché de los navegadores web (la dirección de la imagen es la misma y reutilizan la llamada al servidor). Podemos modificar el componente `RandomCat` para que siempre sea diferente generando un número aleatorio. Declaramos una pequeña función y el número de gatos disponibles:

**RandomCat.js**:

```js
import React from "react";

const getRandomInteger = (maxNumber) => Math.floor(Math.random() * maxNumber);
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
import React from "react";
import CatList from "./CatList";

class App extends React.Component {
  render() {
    return (
      <div className="App">
        <CatList />
      </div>
    );
  }
}

export default App;
```

**components/CatList.js**:

```js
import React from "react";
import RandomCat from "./RandomCat";

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
import React from "react";

const getRandomInteger = (maxNumber) => Math.floor(Math.random() * maxNumber);
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

## Create-react-app y Git

Una cosa que debéis saber. Cuando creamos un proyecto con `create-react-app` puede pasar dos cosas:

- Que estemos creando el nuevo proyecto **fuera** de un repo de Git. En ese momento `create-react-app` creará el `package.json`, el `README.md`, la carpeta `src/`... y también una carpeta `.git`. Esta carpeta `.git` está pensada para ser un repo de Git, pero no está enlazada con ningún repo de GitHub. Por ello la podemos borrar. **Dicho de otra forma, si `create-react-app` nos crea una carpeta `.git` la podemos borrar.**
- Que estemos creando el proyecto dentro de un proyecto que sí es un repo de Git enlazado con GitHub. En este caso `create-react-app` no nos creará la carpeta `.git`. En este caso no tendremos que hacer nada.

## Publicar nuestra app React en GitHub Pages

`create-react-app` nos crea un entorno de desarrollo donde empezar a trabajar con React en nuestra máquina. Si queremos enseñar el resultado con GitHub Pages hay que hacer algunas cosillas antes de generar una versión para producción:

- rutas a los archivos principales serán relativas al dominio
- necesitaremos una carpeta determinada
- y, quizás, haya que cambiar algo de `http` a `https`.

Entraremos por terminal a nuestra carpeta de proyecto y esto es lo que hay que hacer:

1. Modificar `package.json` para que las rutas sean relativas a nuestros archivos: hay que añadir `"homepage": "./",` en la línea 2. **Esto es importante y siempre se nos olvida.**
1. Ya que lo vamos a servir desde GitHub, y usa https, tendremos que cambiar cualquier recurso `http` a `https`: por ejemplo, en un fetch. [Más info aquí](../modulo_6/errores_comunes_en_programacion.md#mixed-content-http-vs-https).
1. Crear la versión de producción:
   1. Ejecutar `npm run build` para que nos cree la versión para producción en la carpeta **build/**.
   1. GitHub Pages funciona en la carpeta raíz o en la **docs/** de la rama master, así que querremos cambiar la carpeta **build/** por la carpeta **docs/**. Para ello, desde la terminal y colocados en la carpeta raíz del proyecto ejecutaremos `mv build docs`. Es importante saber que este paso lo tendremos que hacer cada vez que hagamos cambios y queramos reflejarnos en nuestra página de GitHub Pages. Otra opción es cambiarlo a mano desde el explorador de carpetas de nuestro ordenador. Lo importante es que esa carpeta se llame `docs/`.
1. Add, commit y push.
1. Casi listo, solo falta activar GitHub Pages para que se sirva desde la carpeta docs de nuestra rama master. Para eso como ya sabéis, desde la página principal del repositorio, podéis ir a la pestaña de **Settings** y una vez dentro, en la sección GitHub Pages, donde pone **Source** seleccionar `master branch /docs folder`.

**Y ya estaría.**

#### EJERCICIO 6

Publiquemos la aplicación del último ejercicio en GitHub Pages. ¡A por ello!

\_\_\_\_\_\_\_\_\_\_

## Debugging de aplicaciones en React

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
