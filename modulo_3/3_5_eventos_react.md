# Eventos en React

[codepen-simple-jsx-event]: https://codepen.io/adalab/pen/zppdVP?editors=0010
[codepen-remembering-randomcat]: https://codepen.io/adalab/pen/YYYVvz?editors=0010
[codepen-handleevent-methods]: https://codepen.io/adalab/pen/NXXOGx?editors=0010
[codepen-lifting-events]: https://codepen.io/adalab/pen/wpmyjB?editors=0010

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

<!-- /TOC -->

## Introducción

Hasta ahora sólo hemos visto cómo pintar interfaces estáticas o independientes en React. Esta es la sesión divertida: en esta sesión veremos cómo añadir dinamicidad a los componentes con eventos.

Vamos a ver que los eventos nos permiten declarar qué reacciones tendrán nuestros componentes. Sin embargo, en ocasiones necesitamos que una reacción en un componente hijo/a, como puede ser la que causa un evento, provoque una reacción en el elemento padre/madre, o incluso más arriba en la cadena.

React solo nos permite pasar datos unidireccionalmente, de padres/madres a hijos/hijas. Aunque esto puede parecer una limitación, debemos recordar que las funciones en JavaScript se tratan como datos, podemos guardarlas en variables, y conservan las variables del ámbito donde se declararon. Así que, ¿y si declarásemos una función en el padre/madre que provoque una reacción en el propio componente y se la pasamos como `prop` a un hijo/a? Eso es una **práctica habitual en React** que se llama _lifting_, que significa "alzamiento".

## ¿Para qué sirve lo que vamos a ver en esta sesión?

React tiene un sistema de eventos sintéticos que ejecutan una acción cuando ocurre un acontecimiento. Con los eventos declararemos cómo _react-cionarán_ nuestros componentes a la interacción con el usuario. Por ejemplo, cuando haga clic en un botón dentro de un componente que hemos definido.

> **NOTA:** Tanto en React como en JavaScript nativo queremos escuchar eventos para hacer alguna acción. Normalmente lo que haremos será cambiar datos de la página y a continuación pintarlos, es decir, renderizarlos. En la próxima lección veremos cómo cambiar estos datos. Por ello la lección de hoy está un poco coja, y tendrá mucho más sentido cuando veamos la de mañana.

## Eventos sintéticos de React

Ya hemos visto cómo escribimos código parecido a HTML con JSX que se transforma en código HTML de verdad tras pasar por React. De una manera parecida, en React tenemos un sistema de **eventos sintéticos** que usaremos como si fueran normales. Aunque están diseñados para que pasen por [eventos regulares](https://www.w3.org/TR/DOM-Level-3-Events/), igual que JSX pasa por etiquetas HTML normales, cabe destacar que son una capa que nos proporciona React y que **no son eventos reales del DOM**, y por eso se llaman **sintéticos**.

En el módulo 2 vimos los eventos del DOM y cómo escuchar eventos desde JavaScript con `addEventListener()`. También vimos una manera de hacerlo desde atributos de HTML que **recomendamos no utilizar**, pero la enseñamos por si os la encontrábais en el futuro. Las funciones escuchadoras (_listeners_) de React se declaran de forma parecida a aquellos que no recomendábamos. Esto no es una contradicción: recordemos que en React escribimos interfaces declarativas, y esto es solo una sintaxis comprensible para asignar comportamiento. No debéis declarar funciones escuchadoras así fuera de React.

> Cuando escuchamos un evento en JavaScript normal, declaramos una función escuchadora (_listener_) con un `addEventListener`. En React funciona igual pero lo escribimos de otra manera. React hace un `addEventListener` por detrás, invisible para nosotras y nos facilita una sintaxis más sencilla.

Vamos a ver un ejemplo. Queremos escuchar un evento de `click` desde un botón que declaramos con JSX. Escribiremos el botón (`<button>texto</button>`) y en un atributo `onClick` (ojo con la mayúscula) añadiremos la función "escuchadora", que será la reacción. Quedará así:

```jsx
const alertButton = (
  <button onClick={ /* aquí va la función */ }>
    Pedir más información
  </button>
);
```

Podríamos escribir directamente la función escuchadora como una _arrow function_ ahí, pero no quedaría legible. Preferiremos declararla fuera y la pasaremos (sin llamarla) al atributo de JSX:

```jsx
const onClickListener = ev => {
  alert('Para más información, acuda a recepción.');
};
const alertButton = (
  <button onClick={onClickListener}>Pedir más información</button>
);
```

Ya está. Cuando hagamos clic en el botón, React se encargará de escuchar el evento y de ejecutar la función.

[&blacktriangleright; Evento simple en Codepen][codepen-simple-jsx-event]

Naturalmente, hay más atributos para escuchar eventos a parte de `onClick`. Los nombres de los atributos tendrán la forma `onEventoEscuchado`, con cada palabra del nombre del evento que se escucha escrita con mayúsculas iniciales. Es decir, escucharemos el evento `focus` rellenando el atributo `onFocus`, el evento `mouseover` rellenando el atributo `onMouseOver`, y así sucesivamente. Podéis consultar [el listado completo de atributos soportados](https://reactjs.org/docs/events.html#supported-events), pero a continuación vamos a listar los más usados, como ya hicimos en la sesión de eventos:

- Escuchadores de eventos de ratón:
  - `onClick`: botón izquierdo del ratón
  - `onMouseOver`: pasar el ratón sobre un elemento
  - `onMouseOut`: sacar el ratón del elemento
- Escuchadores de eventos de teclado:
  - `onKeyPress`: pulsar una tecla
  - `onKeyUp`: levantar el dedo de una tecla
- Escuchadores de eventos sobre elementos:
  - `onFocus`: poner el foco (seleccionar) en un elemento, por ejemplo un `<input>`
  - `onBlur`: quitar el foco de un elemento
  - `onChange`: al cambiar el contenido de un `<input>` , `<textarea>` o `<select>` (no es necesario quitar el foco del `input` para que se considere un cambio, al contrario que en el DOM)
- Escuchadores de eventos de formularios:
  - `onSubmit`: pulsar el botón submit del formulario
  - `onReset`: pulsar el botón reset del formulario

React no puede controlar los eventos de la ventana, así que los siguiente eventos sintéticos no existen (sí existen sus correspondientes eventos de DOM):

- ~~Escuchadores de eventos de la ventana~~
  - ~~`onResize`: se ha cambiado el tamaño de la ventana~~
  - ~~`onScroll`: se ha hecho scroll en la ventana o un elemento~~

#### EJERCICIO 1

**Odio la cebolla**

Vamos a crear un componente `OnionHater` que consta de un `textarea`. Escucharemos los evento de cambio del valor del `textarea` de forma que, si el texto escrito contiene la palabra 'cebolla' hagamos un `alert` diciendo 'ODIO LA CEBOLLA'.

> PISTA: para acceder al valor del `textarea` lo podemos hacer desde el objeto evento, el parámetro de la función escuchadora, con `ev.target.value`

> PISTA: para comprobar si una cadena contiene un texto podemos usar el método `includes` de las cadenas

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

**Elige tu destino**

Vamos a crear un componente `Destiny` que contiene un `select` con un listado de ciudades: Buenos Aires, Sydney, Praga, Boston y Tokio. Al cambiar el valor del `select`, haremos aparecer un `alert` que diga 'Tu destino es viajar a XXX', siendo XXX la ciudad seleccionada.

\_\_\_\_\_\_\_\_\_\_

## Uso de métodos `handleEvent` para manejar eventos

No solo podemos usar funciones escuchadoras en componentes funcionales de React, como hemos hecho en la sección anterior, sino que también podemos declararlas en nuestros componentes de clase. Pero antes de hacerlo, vamos a aclarar un término. Las funciones escuchadoras también se llaman _"event handlers"_, que significa "encargadas del evento", porque son **las funciones encargadas** de reaccionar al evento. En esta sección las llamaremos así para entender mejor y recordar los nombres que usaremos para estas funciones.

Es una práctica común declarar **dentro** del componente las _event handlers_ que se usan en el componente. Como los componentes son clases, los _event handlers_ serán **métodos** de la clase, y su nombre suele empezar por `handle` ("encargarse de", en inglés), seguido del nombre del evento. Por ejemplo, un _event handler_ que se ocupe del evento `click` se llamará `handleClick()`.

Vamos a ver un ejemplo. Recordaréis [el componente `RandomCat`][codepen-remembering-randomcat] que creamos en una sesión anterior. Este componente pintaba una foto aleatoria con un gato. Pero algunos días como hoy nos gusta más Bill Murray que los gatos, así que haremos un componente `RandomMurray` que pinte una foto aleatoria de Bill:

```js
const getRandomInteger = (max, min) =>
  Math.floor(Math.random() * (max - min + 1)) + min;
const MIN_SIZE = 200;
const MAX_SIZE = 400;

class RandomMurray extends React.Component {
  render() {
    const randomMurray = getRandomInteger(MAX_SIZE, MIN_SIZE);

    return (
      <img
        src={`http://www.fillmurray.com/200/${randomMurray}`}
        alt="Random murray"
      />
    );
  }
}
```

Lo modificaremos para que, cuando hagamos clic en la imagen, se genere otra imagen. Para ello, declararemos un método `handleClick` en el componente:

```js
// ...
class RandomMurray extends React.Component {
  handleClick() {
    // method body
  }
  // class body
}
```

La función que pinta nuestro componente, `render()`, es también la función que genera una imagen aleatoria al llamar a `getRandomInteger()`. Si pudiéramos hacer desde nuestra función `handleClick()` que React pintase con `render()` nuestro componente de nuevo, la imagen se generaría de nuevo. Afortunadamente, los componentes de React tienen un método `forceUpdate()` que sirve justo para eso:

```js
// ...
class RandomMurray extends React.Component {
  handleClick(event) {
    this.forceUpdate();
  }

  render() {
    const randomMurray = getRandomInteger(MIN_SIZE, MAX_SIZE);

    return (
      <img
        src={`http://www.fillmurray.com/200/${randomMurray}`}
        alt="Random murray"
        onClick={this.handleClick}
      />
    );
  }
}
```

> No debemos usar el método `forceUpdate()` indiscriminadamente, sino delegar el `render`izado de componentes en React. De momento, solo sabemos que nuestros componentes se re-`render`izan cuando cambian sus `props`, pero en la próxima lección aprenderemos cómo hacerlo sin usar `forceUpdate()`.

Como nuestro método `handleClick()` contiene un `this` y el método lo ejecutará React desde otro contexto, tendremos que asegurarnos de que el `this` que usará es el `this` que queremos. Para eso, en el `constructor()` enlazaremos (_bind_, en inglés) el método a nuestro componente para que siempre que lo llamemos, se ejecute bien:

```js
// ...
class RandomMurray extends React.Component {
  constructor(props) {
    super(props);

    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.forceUpdate();
  }

  // ...
}
```

> **Nota:** Si utilizamos `this` dentro de un método escuchador **sin haber hecho el `bind` en el constructor** nos dará un error en consola. Este es un error que nos pasa mucho al principio de trabajar con React.

Ahora que tenemos nuestro método `handleClick()` declarado y enlazado, podemos registrarlo en el elemento JSX donde queremos escuchar el evento.

```js
const getRandomInteger = (max, min) =>
  Math.floor(Math.random() * (max - min + 1)) + min;
const MIN_SIZE = 200;
const MAX_SIZE = 400;

class RandomMurray extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick(event) {
    this.forceUpdate();
  }

  render() {
    const randomMurray = getRandomInteger(MIN_SIZE, MAX_SIZE);
    return (
      <img
        src={`http://www.fillmurray.com/200/${randomMurray}`}
        alt="Random murray"
        onClick={this.handleClick}
      />
    );
  }
}
```

[&blacktriangleright; Métodos `handleEvent()` en Codepen][codepen-handleevent-methods]

#### EJERCICIO 3

**Expreso mi odio en rojo**

Partiendo del código del ejercicio 1, vamos a hacer que nuestro componente ocupe toda la pantalla disponible, y tenga el `textarea` en el centro. Vamos a hacer que al detectar la palabra cebolla en el texto del `textarea`, en vez de mostrar un alert mostrando nuestro odio, pongamos el fondo del componente de color rojo. Al volver a un texto sin cebolla, el fondo vuelve a ser blanco.

1. Guardaremos la información de si estamos odiando o no en un atributo de la clase. Para ello en el constructor pondremos `this.isHating = false`.
2. En la función que maneja el evento `change` del textarea modificaremos el atributo `isHating` y usaremos el método `this.forceUpdate()` para forzar el repintado.

> PISTA: recuerda que para que el `this` funcione correctamente en nuestra función de _handle_ debemos hacer el `bind` adecuado en el constructor

_BONUS_: ¿Podrías hacer que nuestro odio aparezca tanto si 'cebolla' tiene mayúsculas o minúsculas?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

**Visualiza tu destino**

Vamos a partir del ejercicio 2 sobre elegir tu destino. Vamos a crear un nuevo componente `CityImage` que muestra una imagen de una ciudad que recibe por props. Por ejemplo

```html
<CityImage city="Praga" />
```

Debe mostrar una imagen de Praga. Para facilitar este comportamiento, este componente debe tener como uno de sus atributos un objeto literal con el formato:

```js
{
  'Praga': 'http://path-to-praga-image.jpg',
  'Boston': 'http://path-to-boston-image.jpg',
  ...
}
```

Una vez que tenemos este componente funcionando, vamos a crear uno como hija de nuestro componente `Destiny`, es decir, vamos a hacer que `Destiny` contenga un `CityImage`. Para eso vamos a pintarlo en el JSX de su `render`.

Para terminar, vamos hacer que la magia suceda: en vez de hacer un alert, cuando la usuaria elija una ciudad en el select aparece la imagen de esa ciudad y se muestra el texto 'Tu destino es viajar a XXX'.
Para conseguirlo os recomendamos usar un atributo de la clase `this.city` que cambie su valor al cambiar el select. También tendremos que usar `forceUpdate` para se ejecute el método `render` y a) se pasen unas props diferentes al componente `CityImage` y b) se pinte una ciudad diferente en el título.

\_\_\_\_\_\_\_\_\_\_

## _Lifting_ (alzamiento) para pasar datos de hijos a padres

_Lifting_ es una técnica que consiste en pasar funciones a los hijos/as y que sean estos quienes se encarguen de ejecutarlas cuando sea necesario, provocando un cambio _hacia arriba_, en los padres. Generalmente se usa para cambiar el _estado_ de los padres, que luego provocará un re-`render`izado de los hijos/as con nuevas `props`. Aún no sabemos qué es el estado de un componente ni cómo usarlo, así que de momento utilizaremos `forceUpdate()` para provocar el re-renderizado manualmente.

Hasta ahora hemos pasado `props` desde un componente madre a sus componentes hijas para pintar cada hija con una información u otra. Estas `props` son strings, números, booleanos...

Con el lifting lo que vamos a hacer es pasar desde un componente madre a sus hijas una **función o método**. Las hijas ejecutarán ese método cuando suceda un evento. Dicho de otra forma es como si una madre le dice a su hija: "Hija, toma este método y cuando quieras avisarme de algo lo ejecutas, y así yo me enteraré.".

Vamos a ver un ejemplo, con Murrays de nuevo. Tenemos tres componentes, `MurrayList`, `RandomMurray` y `ReloadButton`, cada uno en su módulo. `MurrayList` renderiza una lista con varios componentes `RandomMurray`, y además un botón `ReloadButton`.

**components/MurrayList.js**

```js
import React from 'react';
import RandomMurray from `./RandomMurray`;
import ReloadButton from './ReloadButton';

class MurrayList extends React.Component {
  constructor(props) {
    super(props);

    // nos aseguramos de que este callback se ejecute siempre sobre el componente enlazándolo a la instancia con "bind"
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.forceUpdate(); // se ejecutará el método `render()` de MurrayList, que hará a su vez que se ejecute de nuevo el método `render()` de los hijos
  }

  render() {
    const handleClick = this.handleClick;

    return (
      <section className="section-murrays">
        <h1>All <del>Cats</del> Murrays Are Beautiful</h1>
        <ul className="section-murrays_list">
          <li><RandomMurray /></li>
          <li><RandomMurray /></li>
          <li><RandomMurray /></li>
        </ul>
        {/* pasamos handleClick al hijo como prop */}
        <ReloadButton actionToPerform={ handleClick } label="More murrays"/>
      </section>
    );
  }
}

export default MurrayList;
```

Como vemos en el componente `MurrayList` llamamos a un componente `ReloadButton` al que pasamos por `props` una función que llamamos `actionToPerform`. Esta prop apunta al método `handleClick` que simplemente hace un `forceUpdate` que provoca una llamada al render y por tanto el re-renderizado de todas las hijas, las 3 `RandomMurray`, provocando el pintado de 3 nuevas imágenes aleatorias.

**components/ReloadButton.js**

```js
import React from 'react';

class ReloadButton extends React.Component {
  render() {
    const actionToPerform = this.props.actionToPerform;
    const label = this.props.label || 'More';

    return (
      // Registramos el escuchador que recibimos por props. ¡Lifting hecho!
      <button onClick={actionToPerform}>{label}</button>
    );
  }
}

export default ReloadButton;
```

En `ReloadButton` es donde sucede el _lifting_: recogemos la función que llega de la madre por props (`actionToPerform`) y se la asignamos al `onClick` del botón. De esta forma, al hacer click en el botón ejecutamos una función de la madre.

**components/RandomMurray.js**

```js
import React from 'react';

const getRandomInteger = (max, min) =>
  Math.floor(Math.random() * (max - min + 1)) + min;
const MIN_SIZE = 200;
const MAX_SIZE = 400;

class RandomMurray extends React.Component {
  render() {
    const randomMurray = getRandomInteger(MIN_SIZE, MAX_SIZE);

    return (
      <img
        src={`http://loremmurray.com/400/200/${randomMurray}`}
        alt="Random murray"
      />
    );
  }
}

export default RandomMurray;
```

**index.js**

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './stylesheets/index.css';
import MurrayList from './components/MurrayList';

ReactDOM.render(<MurrayList />, document.getElementById('root'));
```

&blacktriangleright; [_Lifting_ de eventos en Codepen][codepen-lifting-events]

#### EJERCICIO 5

**Ciudades**

Para terminar de entender bien cómo funciona el lifting vamos a hacer un ejercicio muy sencillo. Partimos de un select con nombre de ciudades que encapsulamos en un componente `CitySelector`. Vamos a hacer que, al seleccionar una ciudad del select, aparezca una foto de la misma al lado. La diferencia con ejercicios anteriores es que ahora el select está en su propio componente. Para llevarlo a cabo debemos:

- guardar en un atributo de la clase la ciudad seleccionada como inicial, por ejemplo, `this.selectedCity = 'Madrid'` y usarlo para pintar la imagen en el `render`
- crear un método `handleClick` que actualice el valor de `selectedCity` y llame a `forceUpdate` para forzar el repintado de la imagen
- y usar lifting para pasarlo al componente hijo que se ejecute al cambiar el select

> NOTA: en la próxima sesión veremos el estado de React que nos facilitará este flujo, pero de momento hacemos el repintado "a mano" con `forceUpdate`

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

**Traductor MIMIMI**

¿No os ha pasado nunca que habéis dicho algo y se han burlado de vosotras con un MIMIMI?

- "Al final de esa línea te falta un punto y coma."

- "Il finil di isi linii ti filti in pinti y cimi."

Pues es hora de contraatacar y crear nuestro propio traductor MIMIMI con React.

Vamos a partir de un formulario simple con un textarea donde escribimos una frase. Según vamos escribiendo, obtendremos en un párrafo el resultado de la traducción a MIMIMI. Es importante que tanto el formulario como el párrafo resultado estén cada uno en su propio componente independiente. El componente del formulario, por ejemplo `TextInput`, simplemente se encarga de recoger los cambios de la usuaria y enviarlo al componente madre `App`, que los guarda en un atributo y fuerza el repintado. El componente `MIMIMITranslator` recoge el texto que le pasan por props, lo traduce y muestra en un párrafo.

> PISTA: para realizar la traducción basta con buscar [una expresión regular (RegExp)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) y el método `replace` de las cadenas. Si buscas "javascript regex replace vowels" en Google va a ser fácil de encontrar.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 7

**Filtrando artículos**

Vamos a partir del ejercicio 1 de la sesión 3.4 (los items de la lista de la compra). Si recuerdas bien, teníamos un componente `ItemList` que mostraba un listado de `Item`s. Vamos a crear un nuevo componente `CategoryButton` que es un botón con el nombre de una categoría de productos y que recibe por `props` el nombre de la categoría.

```html
<CategoryButton category="Bebida" />
```

En nuestro `ItemList` vamos a pintar, además del `ul` con el listado de items, un botón con una categoría, por ejemplo, 'Bebida'.

> Recuerda que un componente de React sólo debe tener un elemento raíz en su método `render` y si queremos meter más cosas debemos agruparlas, por ejemplo, en un `div`.

Ahora viene lo bueno: vamos a escuchar eventos `click` sobre el botón de la categoría, de forma que se invoca un método del componente madre (`ItemList`) que hemos recibido por `props` (_lifting_). A este método de la madre le pasamos como parámetro el nombre de la categoría, para que sepa qué botón se ha clicado.

En `ItemList` definimos ese método para que si se pulsa el botón de la categoría bebidas sólo aparezcan los items de esa categoría en pantalla. Esto lo hacemos filtrando los items del array para dejar solo los de la categoría seleccionada.

Al final tendremos que realizar un cambio en un atributo y forzar la ejecución del método `render` de `ItemList` que a su vez fuerza el de sus hijas.

_BONUS_: cuando tenemos todo funcionando para una categoría, podemos añadir botones para cada de las que tengamos productos. Incluso un botón especial 'Todos' para mostrar de nuevo los productos de todas las categorías.

\_\_\_\_\_\_\_\_\_\_

### Lifting en componentes funcionales

Como ya hemos visto en lecciones anteriores, todo lo que se puede hacer con componentes de clase también se puede hacer con componentes funcionales. Vamos a ver un ejemplo de **lifting con componentes funcionales**.

Tenemos un componente principal que es `Form.js`, en el que podemos ver que:

- En la línea 12 y 18 estamos usando dos veces el componente hijo `InputText`. Esto es lo que llamamos **reutilización de componentes**.
- Al componente `InputText` le estamos pasando por props un `id`, `label` y `name` que son strings. Estas props se usan en `handleInput` para crear el código HTML personalizado.
- Además, al componente `InputText` le estamos pasando por props un `handleInput` que es una función. **La función `handleFormInput` será ejecutada por el componente hijo `handleInput` cuando suceda un evento.** A esto es a lo que llamamos **lifting**.

```jsx
// Form.js
import React from 'react';
import InputText from './InputText';

const handleFormInput = data => {
  console.log(data);
};

const Form = () => {
  return (
    <form>
      <InputText
        id="name"
        label='Escribe tu nombre:'
        name='name'
        handleInput={handleFormInput}
      />
      <InputText
        id="email"
        label='Escribe tu email:'
        name='email'
        handleInput={handleFormInput}
      />
    </form>
  );
};

export default Form;
```

El componente hijo es `InputText.js`, en el que podemos ver que:

- Este componente `InputText`, recibe por props `id`, `label` y `name` para generar un HTML personalizado.
- En la línea 23 estamos escuchando el evento `keyup`.
- Cuando la usuaria produce un `keyup` en el input, React ejecuta la función `handleKeyUp` de la línea 6.
- Cuando React ejecuta la función `handleKeyUp` se ejecuta la función `props.handleInput` en la línea 11. Aquí se produce el lifting: **un componente hijo ejecuta una función que ha recibido por props del componente madre**.
- En la línea 11 estamos ejecutando `props.handleInput`. Ya que estamos ejecutando una función, si queremos podemos pasarle datos por parámetros. Estos datos los estamos generando en el objeto `data` en la línea 7.
- Os preguntaréis por qué hemos metido la función `handleKeyUp` dentro del componente `InputText` y no lo hemos puesto fuera como habíamos hecho hasta ahora. La respuesta es que si queremos usar las props dentro de la función `handleKeyUp` (como por ejemplo `props.name` y `props.handleInput`) **necesitamos hacerlo en un ámbito o scope donde tengamos acceso a las props**. Si hubieramos puesto la función `handleKeyUp` en la línea 3, `props` no existiría.

```jsx
// InputText.js
import React from 'react';

const InputText = props => {

  const handleKeyUp = ev => {
    const data = {
      name: props.name,
      value: ev.currentTarget.value
    };
    props.handleInput(data);
  };

  return (
    <div>
      <label htmlFor={props.id}>
        {props.label}
      </label>
      <input
        id={props.id}
        type='text'
        name={props.name}
        onKeyUp={handleKeyUp}
      />
    </div>
  );
};

export default InputText;
```

En resumen, para hacer lifting con componentes funcionales **tenemos que ejecutar la función que nos pasan por props** (en este caso `props.handleInput(data);`) **dentro del componente funcional** (en este caso `InputText`).

#### EJERCICIO 8

Copia estos dos ficheros del ejemplo anterior en un proyecto de React. Y a continuación:

- Añade un tercer campo al formulario para que la usuaria escriba su ciudad.
- Observa los datos que aparecen en consola cuando la usuaria escribe en los campos del formulario.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 9

Si observamos la función `handleFormInput` del ejercicio anterior verás que recibe un único argumento llamado data de tipo objeto que tiene las propiedades `name` y `value`.

Te pedimos que cambies las funciones `handleFormInput` y `handleKeyUp` para que `handleFormInput` en vez de recibir un argumento reciba:

- Primer argumento: un string con el nombre del input modificado.
- Segundo argumento: un string con el valor del input modificado.

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

### Egghead

Serie de clases en vídeo que introduce y explora los fundamentos básicos de React.

- [Eventos sintéticos de React](https://egghead.io/lessons/react-react-synthetic-event-system)

### Documentación oficial de facebook sobre lifting

- [Lifting State Up](https://reactjs.org/docs/lifting-state-up.html)

- [JavaScript Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
