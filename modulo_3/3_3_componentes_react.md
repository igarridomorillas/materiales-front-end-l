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

Según vayamos creando aplicaciones web más grandes con React, necesitaremos definir mayor número de componentes que se relacionarán entre sí. Veremos cómo se relacionan los componentes madre con los componentes hija, y un tipo especial de componente que tendrá más componentes arbitrarios en su interior.

También necesitaremos crear componentes con mayores garantías de funcionar. Para eso veremos `propTypes`, para obligar a las `props` a ser de un tipo de dato concreto, y cómo asignarles valores por defecto para hacer `props` opcionales.

## Componentes madre e hija

Vimos en la sesión anterior cómo usar un componente dentro de otro: el componente `CatList` renderizaba tres componentes `RandomCat`. Para referirnos a componentes que renderizan otros usaremos el término **componente padre o madre**, y para referirnos a componentes que son renderizados por otros, **componente hijo o hija**.

Los componentes madre pueden tener múltiples componentes hija, pero los componentes hija solo tienen un componente madre. Cabe destacar que un componente puede ser hija de un componente madre y a la vez ser madre de otros componentes hija.

![CatList](assets/images/3_4_catlist.png)

Estas relaciones forman una jerarquía importante para entender React. Desde los componentes madre podremos pasar datos **hacia abajo** a los componentes hija, mediante las `props`, pero **no al revés**. Un componente no podrá pasar datos _hacia arriba_ libremente. Veremos en una sesión posterior cómo "solucionar" los problemas que _a priori_ parece generar este **flujo unidireccional**.

## Pintar listado en React

Cuando tenemos que pintar un listado (un `ul` con varios `li`) los podemos pintar a mano. Pero si son 1000 `li` tenemos un problema, nos vamos a cansar un poquito. Cuando tenemos que pintar un listado de datos que nos vienen de un API no sabemos cuántos `li` tenemos que pintar cuando estamos programando la web. En definitiva cuando tenemos que pintar un listado cuyos datos están en un array podemos hacer lo siguiente:

```js
import React from 'react';

class App extends React.Component {
  render() {
    const items = [
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
    return (
      <div>
        <h1>Pintar listados con React:</h1>
        {/* con este map iteramos iteramos el array de items */}
        {items.map(item => {
          // cada return retorna un li
          return (
            <li>
              <h2>Nombre: {item.name}</h2>
              <p>Descripción: {item.description}</p>
              <p>Cantidad: {item.quantity}</p>
              <p>Categoría: {item.category}</p>
              <p>Precio: {item.price}</p>
            </li>
          );
          // el map retorna un array de li, es decir, un listado de HTML
        })}
      </div>
    );
  }
}

export default App;
```

Por supuesto el `li` lo podemos cambiar por cualquier otra cosa, como por ejemplo un componente de React.

### Pintar listado en React: el problema de las keys

Si ejecutas este código, verás un **warning** en consola. ¿Sabrías solucionar este **warning** siguiendo el enlace que te sugiere React?

#### EJERCICIO 1

Partiendo de este array:

```js
const students = [
  {
    promo: 'A',
    name: 'Sofía',
    age: 20
  },
  {
    promo: 'B',
    name: 'María',
    age: 21
  },
  {
    promo: 'A',
    name: 'Lucía',
    age: 22
  }
];
```

1. ¿Sabrías pintar el listado con React?
1. A continuación antes de pintar ¿sabrías filtrar las estudiantes por las que pertenezcan a la promo A?

\_\_\_\_\_\_\_\_\_\_

## Uso de `children` para acceder a los componentes hijo cuando no los conoces

Algunas veces, al declarar un componente no sabremos o no nos importará qué otros componentes podrá contener dentro.

Un ejemplo es un componente Colapsable. Este componente se tiene que encargar de mostrar una cabecera, que si la pulsamos debe des/colapsar el contenido del colapsable. Pero a la hora de programar no vamos a saber cuál será dicho contenido. O en un sitio de nuestra página puede tener un contenido y en otro sitio otro. Dicho de otra forma el colapsable es el contenedor de un contenido que no conocemos.


Otro ejemplo es un componente `Popup` que gestiona una ventana (maquetada en HTML) que se pone por encima del resto de cosas de la página (con posición fija y esas cosas que ya sabemos).

En esos casos podremos usar una `prop` especial, `children`, para pasar directamente elementos:


```js
import React from 'react';
import Popup from './Popup';

class App extends React.Component {
  render() {
    return (
      <div>
        <Popup title="Esto es un popup">
          <h3>Soy el título del contenido</h3>
          <p>Y yo el texto del contenido</p>
        </Popup>
      </div>
    );
  }
}

export default App;
```

```js
import React from 'react';

class Popup extends React.Component {
  render() {
    return (
      <div>
        <h2>{this.props.title}</h2>
        <div className="popup__content">
          {this.props.children}
        </div>
      </div>
    );
  }
}

export default Popup;
```

Como se puede observar en `App.js` estamos pasando a `<Popup>` dos props:

- `title="Esto es un popup"`:
   - Que es una prop "normal"
   - En este cado es de tipo texto
- `<h3>Soy el título del contenido</h3><p>Y yo el texto del contenido</p>`
   - Que es una prop "especial".
   - Hasta ahora habíamos pasado props a nuestras hijas de tipo texto, número... en general cualquier tipo de variable o constante de JS.
   - También podemos pasar código JSX, es decir, etiquetas de HTML, textos y otros componentes de React.
   - Lo que pasemos a nuestra hija **entre las etiquetas de apertura y cierre de un componente** es recibido por el componente hija en `this.props.children`.
   - La componente hija debe encargarse de rendedirzarlo donde quiera. En el ejemplo anterior dentro del `div` con la clase `popup__content`.

#### EJERCICIO 2

1. Desarrolla un componente `HalfPage` que mida el 50% de ancho del viewport. Este componente debe recibir de su componente madre código JSX.
1. Desde el componente madre `App` usa el componente `HalfPage` y pásale un `H1` y un párrafo que ponga "Estoy en la izquierda".
1. Desde el componente madre `App` añade un segundo `HalfPage` y pásale un `H2` y otro párrafo que ponga "Estoy en la derecha".

El resultado debería ser que en la mitad izquierda de la página debe aparecer el `H1` y el "Estoy en la izquierda" y el la mitad derecha el `H2` y el "Estoy en la derecha".

\_\_\_\_\_\_\_\_\_\_

## Fragments

Anteiormente en Adalab... os hemos comentado que todo componente debe tener una única etiqueta HTML como hija directa del `render()`.

Si tenemos que meter dos etiquetas hermanas estamos obligadas a meter una etiqueta contenedora, por ejemplo un `<div>`;

Pero a veces eso nos rompe la estructura HTML de la página. Por ejemplo, si en el componente madre tenemos:

```js
render() {
  return (
    <ul>
      <Item />
    </ul>
  );
}
```

Y en el componente hija `Item` queremos tener:

```js
render() {
  return (
    <li>Uno</li>
    <li>Dos</li>
  );
}
```

Esto provocará un error. Y React nos pedirá que metamos una etiqueta que agrupe los dos `li`, de esta forma:

```js
render() {
  return (
    <div>
      <li>Uno</li>
      <li>Dos</li>
    </div>
  );
}
```

Esto es pecado mortal de necesidad porque el hijo directo de un `ul` siempre debe ser `li`. Pero no te preocupes, tenemos la solución:

```js
render() {
  return (
    <> {/* a esto se le llama fragment */}
      <li>Uno</li>
      <li>Dos</li>
    </>
  );
}
```

Con la etiqueta de apertura especial de React `<>` y la de cierre `</>` podemos agrupar los dos `li` en un contenedor único y el `render()` solo tendrá un único hijo directo.

Solo si te atreves... prueba este código en una web e inspecciona con DevTools, para ver qué código HTML está generando. Mañana me dices si te mola o no.

## Valores por defecto de las `props`

> **Nota:** lo que vamos a explicar sobre `defaultProps` nos ayuda a la hora de programar. A nuestras usuarias finales no les aporta nada.

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

> **Nota:** una `defautlProps` solo se aplica si desde el componente madre no nos están pasando una `prop`. Si nos pasan la `prop` con un `string` vacío, un `null`, un `undefined` o cualquier otro valor, React no aplicará el valor por defecto.

Esto nos ayuda a:

- No tener que pasar una `prop` a una componente hija, si la mayoría de las veces va a tener el mismo valor.
- Si otra compañera llega nueva al proyecto, le es muy fácil identificar qué props son opcionales (que son las que estén en `defaultProps`) y cuáles obligatorias (que son el resto).

> Esta funcionalidad viene instalada ya dentro de React, no hace falta instalar nada nuevo.

#### EJERCICIO 3

Partiendo del código del ejercicio 1, usa las `defaultProps` para que la descripción del item sea opcional y si no nos lo pasan por `props` aparezca 'No hay descripción'.

\_\_\_\_\_\_\_\_\_\_

## `props` tipadas con `propTypes`

> **Nota:** lo que vamos a explicar sobre `propTypes` nos ayuda a la hora de programar. A nuestras usuarias finales no les aporta nada.

JavaScript no tiene un sistema de tipado fuerte, lo que significa que nuestras variables pueden almacenar cualquier tipo de valor.

Podemos declarar una variable `const nameOfAPerson` que debería almacenar una `string` y, sin embargo, podemos asignarle un valor numérico como `4`, tanto en su inicialización, como en un futuro si fuera `let`.

Cuando trabajamos en un código pequeño, esto no supone ningún problema, pero existen dos casos en los que es más probable que empiecen a surgir incoherencias o errores:

- Cuando nuestro código es o va a ser muy grande (escalabilidad)
- Cuando nuestro código será usado por otras personas (amabilidad, legibilidad, elegancia, saber estar... ;)

> **Nota:** existen algunas variantes de JavaScript como [TypeScript](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html). Se puede decir que CSS es a Sass lo que JS a TypeScript, un preprocesador que nos obliga a trabajar con variables que no pueden cambiar su tipo.

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
- Y más. La lista completa está en los [enlaces externos][sección-recursos-externos].

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

Podemos combinar `propTypes` con `children` también, y obligar a que nuestro componente tenga un solo a, por ejemplo:

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

Si pasamos a un componente hija una `prop` que no cumple esta validación o comprobación de `propTypes` React mostrará un **warning** en consola, pero la aplicación seguirá funcionando.

Esto es muy útil para:

- Documentar el componente: con `propTypes` estamos diciendo qué `props` recibe el componente y de qué tipo son.
- Si creamos un componente que va a ser usado por otras personas de la empresa o de la otra parte del mundo, les estaremos mostrando un warning si no usan bien nuestro componente. Por ello facilitamos la vida a otras personas y mejoramos la calidad del código.

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
