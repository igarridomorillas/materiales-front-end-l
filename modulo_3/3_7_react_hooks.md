# 3.7 React Hooks

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)

<!-- /TOC -->

## Introducción

En esta sesión vamos a aprender una nueva manera de trabajar con el estado en componentes funcionales, los React Hooks.

Hemos visto que en React podemos crear tanto componentes de clase como componentes funcionales. Los componentes de clase al ser más complejos nos permiten hacer más cosas, como por ejemplo tener un estado para manejar los datos de nuestra aplicación y modificarlo para que se repinte por medio del método render.

El problema es que los componentes de clase son más complejos y nos obligan a escribir más. Por ello, los creadores de React, han desarrollado los Hooks. **Los Hooks son una nueva característica de React 16.8 que nos permite usar el estado y otras características sin escribir una clase.** Es una nueva forma de escribir el código, una nueva sintáxis. **Los conceptos que manejábamos hasta ahora como estado, eventos, lifting... se mantienen**, pero con los Hooks cambia la forma de escribirlos.

Ahora nuestros componentes funcionales también manejarán el estado.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Ya sabemos lo que es el estado de nuestra aplicación y cómo lo hemos manejado hasta ahora a través de componentes de clase. A medida que las aplicaciones crecían y se volvían más grandes, los componentes de clase se volvían más complejo. Por eso, a partir de la versión 16.8 de React, surgió una nueva manera de manipular el estado a través de componentes funcionales, evitando así todo el "engorro" de tener que escribir un componente de clase cada vez que necesitábamos manejar el estado de una aplicación. En el mundo React actualmente conviven las dos maneras de trabajar, ya que los React Hooks son un concepto muy nuevo y aún no están completamente extendidos.
Antes de continuar, debes saber que los Hooks son:

 - Completamente opcionales. Es necesario que sepas que existen pero su uso no es obligatorio.
 - 100% compatibles con versiones anteriores de React.
 - Por el momento no hay planes para eliminar los componentes de clases de React.

Los Hooks no reemplazan tu conocimiento de los conceptos de React. Todo lo contrario, complementan y amplian estos conceptos que ya conoces: props, estado, lifting... y otros que veremos más adelante. Además, seguiremos manejando la estructura que ya conocemos con un componente principal que "dirija" nuestra aplicación, la única diferencia es que ya podríamos usarlo como componente funcional y seguir controlando el estado.

## Qué son los hooks

La palabra Hook se traduce como Gancho en español, y la razón de este nombre, es que un Hook en React te permite "colgarte" del estado y los métodos del ciclo de vida de un componente (que veremos en próximas lecciones), desde un componente funcional.

Vamos a recordar cómo escribíamos hasta ahora un componente de clase con estado, por ejemplo App.js. Imagina que desde App.js se llama a otro componene RandomInteger que tiene un botón para generar un número aleatorio y pintarlo. La estructura de App.js sería la siguiente:

**App.js como componente de clase**

```jsx
import React from 'react';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.handleRandomInteger = this.handleRandomInteger.bind(this);
    this.getRandomInteger = this.getRandomInteger.bind(this);
    this.state = {
      number: 0
    };
  }

  getRandomInteger() {
    return Math.floor(Math.random() * 100);
  }

  handleRandomInteger() {
    this.setState({
      number: this.getRandomInteger()
    });
  }

  render() {
    return (
      <div className="App">
        <RandomInteger getRandom={this.handleRandomInteger} randomNumber={this.state.number}/>
      </div>
    );
  }
}
```

Bien, hasta aquí es terreno conocido, y ahora ¿cómo podríamos pasar App.js a componente funcional utilizando hooks? La respuesta es sencilla por medio de nuestro nuevo mejor amigo `useState`. Echa un vistazo a cómo quedaría App.js con hooks:

**App.js como componente funcional con el hook useState**

```jsx
import React, { useState } from 'react';

const App = () => {
  const [number, setNumber] = useState(0);
  const generateRandomInteger = () => Math.floor(Math.random() * 100);

  const handleRandomInteger = () => {
    setNumber(generateRandomInteger());
  }

  return (
    <div className="App">
      <RandomInteger getRandom={handleRandomInteger} randomNumber={number}/>
    </div>
  );
}
```

Como puedes ver, y aunque explicaremos más adelante este primer hook, con `useState`, el tamaño y la complejidad del componente se ha reducido. Además, se ha eliminado la posible confusión que generan el uso de componentes de clase.

## Manejando el estado con hooks.useState()

Existen dos tipos de Hooks en React, los hooks de la propia librería, que vienen predefinidos y los hooks personalizados (que no veremos de momento).

Uno de los hooks predefinidos más populares y útiles es `useState`. Por cierto, la convención para nombrar un Hook es usar la palabra 'use', seguida de otra palabra que lo describa, como en este caso 'state' porque a través de este hook podemos manejar el estado del componente.

Para usar un Hook primero necesitamos un componente funcional, ojo, los hooks sólo funcionan con componentes funcionales y no con componentes de clase. También necesitamos importar el hook que vamos a utilizar, en este caso, useState:

**App.js**

```jsx
import React, { useState } from 'react';

const App = () => {
  return (
    <div>{name}</div>
  )
}
```

`{name}` será una propiedad de nuestro componente funcional que aún no hemos definido, pero que tiene la particularidad de poder ser modificado, por lo que es parte del estado del componente, hasta antes de los hooks eso significaba que teníamos que migrar nuestro componente funcional a uno de clase, pero ya no más.

Para definir una propiedad del estado del componente con hooks usamos algo así:

```jsx
const [name, setName] = useState('Elena');
```

`name` es una variable que contiene el valor del estado y `setName` es una función para modificar ese estado respectivamente. El valor que enviamos como argumento de `useState` es el valor por defecto o valor inicial para `name`, el equivalente a `this.state = { name: 'Elena' }`. Una vez declarado nuestro hook si queremos setear de nuevo el estado utilizaremos la función que hemos creado para ello:

```jsx
setName('Daenerys');
```

Que es el equivalente a lo que en componentes de clase usamos como:

```jsx
this.setState({
  name: 'Daenerys'
});
```

Después de cada modificación React sabrá que tiene que actualizar el estado del componente como siempre lo ha hecho.

> **NOTA:** La forma de declarar `name` y `setName` con esta sintaxis `const [name, setName] = useState('Elena');` todavía no la conocéis, se llama [destructuring](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Operadores/Destructuring_assignment) y la explicaremos en próximas lecciones.

Todo esto es muy bonito, pero ¿podemos ver un ejemplo más real?

Mira el componente App.js que hemos utilizado al inicio:

**App.js**

```jsx
import React, { useState } from 'react';

const App = () => {
  const [number, setNumber] = useState(0);
  const generateRandomInteger = () => Math.floor(Math.random() * 100);

  const handleRandomInteger = () => {
    setNumber(generateRandomInteger());
  }

  return (
    <div className="App">
      <RandomInteger getRandom={handleRandomInteger} randomNumber={number}/>
    </div>
  );
}
```

Como puedes ver es nuestro ya conocido componente principal que renderiza a su vez un componente llamado RandomInteger.

**RandomInteger.js**

```jsx
import React from 'react';

const RandomInteger = props => {

  const getRandomNumber = function() {
    props.getRandom();
  }

  return (
    <div>
      <span>Mi número aletorio es {props.randomNumber}</span>
        <button type='button' onClick={getRandomNumber}>Dame random</button>
    </div>
  );
}
```

RandomInteger recibe el valor del estado actual de `number` a través de las props, también recibe una función para ejecutar por lifting y actualizar el valor de `number`.

En App.js primero definimos nuestro hook useState, dando un nombre a la variable que contendrá el valor de nuestro estado `{number}` y a la función que se encargará de actualizar dicho estado `setNumber()`, a las que accederemos mediante destructuring. Lo que recibirá `setState` como argumento será el valor inicial de number, 0.

```jsx
const [number, setNumber] = useState(0);
```

Así nuestro componente App.js quedaría así:

```jsx
import React, { useState } from 'react';

const App = () => {
  const [number, setNumber] = useState(0);

  return (
    <div className="App">
      <RandomInteger getRandom={handleRandomInteger} randomNumber={number}/>
    </div>
  );
}
```

Pero claro, como hemos visto nuestro componente RandomInteger consta de un botón para generar un número aleatorio, es decir, actualizar o setear de nuevo el estado de `{number}` ¿cómo lo hacemos?. Pues de esta manera:

```jsx
const generateRandomInteger = () => Math.floor(Math.random() * 100);

const handleRandomInteger = () => {
  setNumber(generateRandomInteger());
}
```

En nuestra función manejadora del click ejecutamos la función que setea el nuevo valor de number (lo que antes hacíamos con setState), y le pasamos el valor que devuelve nuestra función `generateRandomInteger`, de esto modo nuestro App.js completo quedaría así:

**App.js**

```jsx
import React, { useState } from 'react';

const App = () => {
  const [number, setNumber] = useState(0);
  const generateRandomInteger = () => Math.floor(Math.random() * 100);

  const handleRandomInteger = () => {
    setNumber(generateRandomInteger());
  }

  return (
    <div className="App">
      <RandomInteger getRandom={handleRandomInteger} randomNumber={number}/>
    </div>
  );
}
```

#### EJERCICIO 1

Hoy nos sentimos como si fuera nuestro cumpleaños así que vamos a crear un componente funcional con un texto y un botón que diga "Hazme más viejo". El texto contendrá la frase: "Hoy tengo 20 años de edad", siendo 20 una variable que se actualice un año cada vez que pulse el botón. La única regla es que lo hagas por medio de hooks.

\_\_\_\_\_\_\_\_\_\_

## Manejando el estado de varias propiedades

Hasta ahora hemos visto cómo se maneja el estado de una propiedad, pero ¿y si tengo varias propiedades en el estado? muy sencillo, en el cuerpo de nuestra función vamos a ir escribiendo cada uno de los hooks que vamos a necesitar para actualizar el estado de cada una de las propiedades. Mira este ejemplo:

**App.js**

```jsx
import React, { useState } from 'react';

const App = () => {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');

  const handleInputName = (evt) => {
    setName(evt.target.value);
  };
  const handleInputEmail = (evt) => {
    setEmail(evt.target.value);
  };

  return (
    <div className='App'>
      <form>
        <label htmlFor='name'>Nombre</label>
        <input type='text' name='name' onChange={handleInputName} placeholder='Escribe aquí tu nombre' />
        <label htmlFor='email'>Email</label>
        <input type='text' name='email' onChange={handleInputEmail} placeholder='Escribe aquí tu email' />
      </form>

      <section>
        <p>Tu nombre es: {name}</p>
        <p>Tu email es: {email}</p>
      </section>
    </div>
  );
};
```

Como puedes ver en nuestro componente principal tenemos dos hooks, uno que actualiza el estado de mi input "name" y otro que actualiza el estado de mi input "email" cuando hago click en el botón.

Cada uno de esos hooks actúa sobre la propiedad especificada por medio de la función que le hemos pasado en cada caso, recibiendo como argumento inicial de useState un string vacío.

#### EJERCICIO 2

Vamos a partir del componente del ejercicio 1, ahora vamos a tener otro texto que diga "Tengo 1 regalo" con un nuevo botón "Dame regalos". Cada vez que pulse en el botón debo incrementar en uno mi número de regalos, manteniendo la funcionalidad de hacerme un año más viejo.

\_\_\_\_\_\_\_\_\_\_

## Otros hooks predefinidos importantes

Aunque useState sea probablemente el más importante ya que nos permite controlar el estado de nuestra aplicación hay muchos otros hooks listos para usar que realizan distintas funciones, algunos los veremos más adelante.
 - useEffect (controla el ciclo de vida de nuestros componentes y lo veremos más adelante)
 - useRef
 - useContext
 - useReducer

Entre muchos otros que puedes encontrar aquí: https://reactjs.org/docs/hooks-reference.html

## Limitaciones de los hooks

Aunque los hooks son el futuro de React y son geniales, tienen alguna que otra limitación.
Debido a cómo interpreta React el orden en que ejecutas tus hooks siempre debes declararlos en el cuerpo de tu componente funcional y no pueden llamarse dentro de condicionales, ciclos, o cualquier otra estructura que agregue un nuevo nivel de ejecución al componente:

**CORRECTO VS INCORRECTO**

```javascript
import React, { useState } from 'react';

const App = () => {
  const [name, setName] = useState('Elena'); // Correcto ✅
  if (true) {
    const [counter, setCounter] = useState(0) // Incorrecto ❌
  }
  return (
    <div>{name}</div>
  );
}
```

## Recursos externos

### Documentación en React sobre hooks
https://es.reactjs.org/docs/hooks-intro.html

### Tutorial explicando el uso de hooks en profundidad
https://www.youtube.com/watch?v=ISGCTngdp8c&t=16s

