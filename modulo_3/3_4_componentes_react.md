# Componentes en React

[codepen-default-values]: https://codepen.io/adalab/pen/JMrJdK?editors=0010
[codepen-component-children]: https://codepen.io/adalab/pen/WdZEQv?editors=0010
[codepen-props-typechecking]: https://codepen.io/adalab/pen/ZvXqvm?editors=0010
[codepen-props-example]: https://codepen.io/adalab/pen/XVoVOa?editors=0110
[sección-recursos-externos]: #recursos-externos

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)

<!-- /TOC -->

## Introducción

Hasta ahora hemos visto cómo crear componentes sencillos y decirle a React que se encargue de pintarlos.

En esta sesión veremos cómo definir componentes más completos y robustos, y exploraremos las diferentes maneras de relacionar nuestros componentes entre sí.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Según vayamos creando aplicaciones web más grandes con React, necesitaremos definir mayor número de componentes que se relacionarán entre sí. Veremos cómo se relacionan los componentes padre/madre con los componentes hijo/hija, y un tipo especial de componente que tendrá más componentes arbitrarios en su interior.

También necesitaremos crear componentes con mayores garantías de funcionar. Para eso veremos `propTypes`, para obligar a las `props` a ser de un tipo de dato concreto, y cómo asignarles valores por defecto para hacer `props` opcionales.

## Componentes padre e hijo (madre e hija)

Vimos en la sesión anterior cómo usar un componente dentro de otro: el componente `CatList` renderizaba tres componentes `RandomCat`. Para referirnos a componentes que renderizan otros usaremos el término **componente padre o madre**, y para referirnos a componentes que son renderizados por otros, **componente hijo o hija**.

> No debemos confundir esta terminología con la terminología de la herencia de clases. Aunque las dos tengan jerarquía, esta terminología representa relaciones de **composición**, no de herencia. En React solo existe herencia en el hecho de que todos los componentes son subclases de `React.Component`.

Los componentes padre/madre pueden tener múltiples componentes hijo/hija, pero los componentes hijo/hija solo tienen un componente padre/madre. Cabe destacar que un componente puede ser hijo/hija de un componente padre/madre y a la vez ser padre/madre de otros componentes hijo/hija.

![CatList](assets/images/3_4_catlist.png)

Estas relaciones forman una jerarquía importante para entender React. Desde los componentes padre/madre podremos pasar datos _hacia abajo_ a los componentes hijo/hija, mediante las `props`, pero **no al revés**. Un hijo/a no podrá pasar datos _hacia arriba_ libremente. Veremos en una sesión posterior cómo "solucionar" los problemas que _a priori_ parece generar este **flujo unidireccional**.

## Ejemplos de app con varios componentes y cómo se pasan datos con las `props`

Vamos a ver un ejemplo para entender mejor el paso de información de un componente a sus hijas. Partimos de un componente `Item` que es un artículo que tenemos en una lista de la compra:

![Item example](./assets/images/4_4_item.png)

Como vemos en la imagen, un item tiene estas propiedades:

- nombre
- descripción
- cantidad
- categoría
- precio

Vamos a crear un componente `Item` con estas características, pero que los valores de esas propiedades le lleguen por `props`:

```js
class Item extends React.Component {
  render() {
    return (
      <div className="item">
        <h5 className="quantity">{this.props.quantity}</h5>
        <div>
          <h5>{this.props.name}</h5>
          <h6 className="text-muted">{this.props.description}</h6>
        </div>
        <div className="badge badge-info">{this.props.category}</div>
        <h5 className="price">{this.props.price}€</h5>
      </div>
    );
  }
}
```

Ahora, desde un componente padre para crear un item y pasarle la información por `props`, lo hacemos así (recordad que esto es JSX pero es la sintaxis de HTML que ya conocemos):

```js
<Item
  name="Cereales con chocolate"
  description="Cereales rellenos de chocolate"
  quantity={2}
  category="Cereales"
  price={5}
/>
```

Fíjate que cuando queremos pasar datos distintos a una string, tendremos que usar los {} para incrustar JS, en este caso, para meter un número.

> NOTA: el valor de los atributos de un componente en JSX debe ser **SIEMPRE** una cadena (entre comillas) o una expresión JS (entre llaves)

Para ver mejor cómo funciona, hemos creado otro componente `ItemList` que nos sirve para manejar listas de items. En este caso, va a crear varios items:

```js
class ItemList extends React.Component {
  render() {
    return (
      <ul className="item-list">
        <li>
          <Item
            name="Cereales con chocolate"
            description="Cereales rellenos de chocolate"
            quantity={2}
            category="Cereales"
            price={5}
          />
        </li>
        <li>
          <Item
            name="Hamburguesa con queso"
            description="Hamburguesa rica y saludable"
            quantity={1}
            category="Fast-food"
            price={15}
          />
        </li>
        //...
      </ul>
    );
  }
}
```

#### EJERCICIO 1

Echa un ojo al [ejemplo anterior en codepen][codepen-props-example], e intenta añadir un nuevo `Item` a la lista.

Ahora tenemos los datos de cada item en un array de objetos (como variable global):

```js
const arrayOfItems = [
  {
    name: 'Cereales con chocolate',
    description: 'Cereales rellenos de chocolate',
    quantity: 2,
    category: 'Cereales',
    price: 5
  },
  {
    name: 'Hamburguesa con queso',
    description: 'Hamburguesa rica y saludable',
    quantity: 1,
    category: 'Fast-food',
    price: 15
  },
  {
    name: 'Agua mineral',
    description: 'Agua de un charco del Himalaya',
    quantity: 2,
    category: 'Bebida',
    price: 5
  }
];
```

a) ¿Serías capaz de crear el JSX que devuelve el método `render` de `ItemList` usando un bucle o un `map`? Para hacerlo debes saber que para pintar varios componentes en JSX basta con crear un array con cada JSX y devolverlo en una expresión entre {}.

b) Ahora vamos a filtrar el array antes convertirlo a JSX con `map`, tirando de nuestra amiga `filter`. Mostraremos en la página solo los productos cuyo precio es inferior a 10.

\_\_\_\_\_\_\_\_\_\_

## Uso de `children` para acceder a los componentes hijo cuando no los conoces

Algunas veces, al declarar un componente no sabremos o no nos importará qué otros componentes podrá contener dentro. Por ejemplo, un componente `Popup` o un componente genérico `Header`. En esos casos podremos usar una `prop` especial, `children`, para pasar directamente elementos:

```js
import React from 'react';

class Popup extends React.Component {
  render() {
    return (
      <div className={`alert alert-${this.props.styling}`} role="alert">
        {this.props.children}
      </div>
    );
  }
}

ReactDOM.render(
  <Popup styling="info">
    <h1 className="horizontal-center">Welcome</h1>
    <p>Thank you for visiting our webpage!</p>
    <p>We hope you enjoy our new shiny site!</p>
  </Popup>,
  document.getElementById('root')
);
```

[&rtrif; Componentes y `children` en Codepen][codepen-component-children]

Como se puede observar en el ejemplo, inyectaremos `props.children` en el JSX del componente genérico como una variable cualquiera. Cuando usemos el componente, escribiremos el contenido en JSX dentro de sus etiquetas de apertura (`<Popup>`) y de cierre (`</Popup>`).

#### EJERCICIO 2

Desarrolla un componente `HalfPage` que todo su contenido lo ponga en la mitad izquierda de la pantalla (mitad de ancho y todo el alto). Usa `children` para introducir todo el contenido entre la apertura y cierre de `HalfPage` en su interior. Crea 2 componentes `HalfPage` con algo de contenido HTML (en JSX) para ver cómo se posiciona en una mitad y la otra.

\_\_\_\_\_\_\_\_\_\_

## Valores por defecto de las `props`

En ocasiones querremos definir que algunas `props` no sean obligatorias, y cuando no se pasen querremos usar un valor por defecto. Esto se puede conseguir en React con `defaultProps`. Será un objeto con el nombre de las `props` que queremos que tengan valor por defecto y su correspondiente valor, y cuando se instancie el componente, se cogerán las `props` que falten de ese objeto. Lo definimos como una propiedad del componente, `NombreDelComponente.defaultProps = {}`, después de declarar la clase:

```js
import React from 'react';

class Button extends React.Component {
  render() {
    return (
      <button
        className={`btn btn-${this.props.styling}`}
        type="button"
        name="button"
      >
        {this.props.label}
      </button>
    );
  }
}

// Así definimos las defaultProps
Button.defaultProps = {
  styling: 'primary', // from Bootstrap classes: primary, secondary, success, info, warning, danger, link
  label: 'Aceptar'
};
```

[&rtrif; Valores por defecto en Codepen][codepen-default-values]

> No hace falta importar el paquete `prop-types` para usar valores por defecto

#### EJERCICIO 3

Partiendo del código del ejercicio 1, usa las `defaultProps` para que la descripción del item sea opcional y si no nos lo pasan por `props` aparezca 'No hay descripción'.

\_\_\_\_\_\_\_\_\_\_

## `props` tipadas con `propTypes`

JavaScript no tiene un sistema de tipado fuerte, lo que significa que nuestras variables pueden almacenar cualquier tipo de valor. Podemos declarar una variable `const nameOfAPerson` que debería almacenar una `string` y, sin embargo, podemos asignarle un valor numérico como `4`, tanto en su inicialización, como en un futuro si fuera `let` o `var`. Cuando controlamos una pequeña base de código, esto no supone ningún problema, pero existen dos casos en los que es más probable que empiecen a surgir incoherencias o errores:

- Cuando nuestra base de código es o va a ser muy grande (escalabilidad)
- Cuando nuestro código será usado por otras personas (amabilidad, ;)

Existen algunas variantes de JavaScript como [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html) o [Flow](https://flow.org/en/docs/getting-started/) que resuelven este problema añadiendo tipos a todo nuestro código. Estas opciones resuelven el primer punto de arriba, pero no el segundo.

Afortunadamente, React tiene un sistema de comprobación de tipos para las `props` de nuestros componentes que nos permitirá que sean más robustos, las `propTypes`. Se utiliza muy parecido a las `defaultProps`, salvo que tendremos que instalar e importar el paquete `prop-types` de `npm` primero. Lo instalaremos en nuestro proyecto desde un terminal:

```sh
npm install --save prop-types
```

Después, ya en nuestro archivo JavaScript, lo importaremos como un módulo después de importar `React`:

```js
import React from 'react';
import PropTypes from 'prop-types';
// ...
```

Del mismo modo que con `defaultProps` y después de declarar el componente, definimos una propiedad del componente, `NombreDelComponente.propTypes = {}`, que será un objeto con el nombre de las props y el tipo que queremos que sea:

```js
import React from 'react';
import PropTypes from 'prop-types';

class Button extends React.Component {
  render() {
    return (
      <button
        className={`btn btn-${this.props.styling}`}
        type="button"
        name="button"
      >
        {this.props.label}
      </button>
    );
  }
}

// Así definimos las propTypes
Button.propTypes = {
  styling: PropTypes.string,
  label: PropTypes.string
};
```

Podemos declarar los siguientes tipos básicos de JavaScript:

- `PropTypes.array` para arrays
- `PropTypes.bool` para booleanos
- `PropTypes.func` para funciones
- `PropTypes.number` para números
- `PropTypes.object` para objetos
- `PropTypes.string` para cadenas de texto

También podemos declarar tipos más complejos:

- `PropTypes.element` para elementos/componentes de React
- `PropTypes.instanceOf(Class)` para una instancia de una clase; en este ejemplo, `Class`
- `PropTypes.arrayOf(PropTypes.number)` para arrays que contengan solo un tipo básico; en este ejemplo, números
- `PropTypes.oneOf(['apple', 'pear', 'lemon', 'orange'])` para valores limitados a los del array especificado
- Y más. La lista completa está en los [enlaces externos][sección-recursos-externos]

Además de todo esto, podemos obligar a que se le pase valor a la `prop` añadiendo `.isRequired` a cualquiera de los tipos:

```js
import React from 'react';
import PropTypes from 'prop-types';

class Button extends React.Component {
  // class body
}

const stylingValues = [
  'primary',
  'secondary',
  'success',
  'info',
  'warning',
  'danger',
  'link',
];
Button.propTypes = {
  label: PropTypes.string,
  styling: PropTypes.oneOf(stylingValues).isRequired // obligamos a que tenga valor
};

// Y también definimos valores por defecto
Button.defaultProps = {
  // no incluímos "styling" porque con propTypes y "isRequired" obligamos a que se pase un valor
  label: 'Aceptar'
};
```

[&rtrif; Validar `props` de React en Codepen][codepen-props-typechecking]

Podemos combinar `propTypes` con `children` también, y obligar a que nuestro componente tenga un solo hijo/a, por ejemplo:

```js
import React from 'react';
import PropTypes from 'prop-types';

class VerticalCenter extends React.Component {
  render() {
    return <div className="vertical-center">{this.props.children}</div>;
  }
}

VerticalCenter.propTypes = {
  children: PropTypes.element.isRequired
};
```

#### EJERCICIO 4

Dado el resultado del ejercicio 3, vamos a hacer que el nombre de los items sea obligatorio y que el precio sea también obligatorio y de tipo numérico. Crea después un nuevo item con valores erróneos para ver qué pinta tiene el error que nos envía React.

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

### React Docs

Documentación oficial de React (en inglés).

- [Composición de componentes (`children`)](https://reactjs.org/docs/composition-vs-inheritance.html#containment)
- [Validar propiedades con `propTypes` y valores por defecto](https://reactjs.org/docs/typechecking-with-proptypes.html):
  - [Lista completa de tipos y validadores con `PropTypes`](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes)
  - [Valores por defecto](https://reactjs.org/docs/typechecking-with-proptypes.html#default-prop-values)

### Egghead

Serie de clases en vídeo que introduce y explora los fundamentos básicos de React.

- [Cómo usar componentes como `children` de otros componentes en React](https://egghead.io/lessons/react-use-react-components-as-children-for-other-components)
