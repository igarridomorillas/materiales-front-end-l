# Métodos del ciclo de vida de componentes en React

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

En esta sesión veremos el ciclo de vida de los componentes de React. Veremos ejemplos prácticos de cómo hacer operaciones comunes en componentes de clase y componentes funcionales.

## ¿Para qué sirven los que vamos a ver en esta sesión?

Como ya sabemos, React nos ayuda a modificar el DOM de nuestra aplicación de una forma fácil y óptima. Pero React no es todopoderoso, hay cosas que no puede o sabe hacer o que no debe controlar porque no es su responsabilidad (es la nuestra).

Al menos, los creadores de React han previsto esta situación y nos proporcionan **herramientas para que tomemos el control** de los componentes y programemos nosotras mismas aquellas cosas que React no sabe hacer.

Imaginemos que estamos programando un componente que muestra la evolución del IBEX 35 de hoy:

![IBEX 35](assets/images/3_12_trade.png)

Al **renderizarse por primera vez** nuestro componente debería pedir los datos del IBEX 35 a un servidor cada 5 segundos y repintar la gráfica con estos nuevos datos. Esta acción periódica la haríamos con un `setInterval`.

Cuando la usuaria cambie a otra página, **nuestro componente desaparecería**. En ese momento debemos programar un `clearInterval` para evitar que se siga llamando al servidor cada 5 segundos, y evitar así un consumo innecesario de la tarifa de datos de la usuaria.

En el ejemplo anterior hemos hablado de "renderizarse por primera vez" y "nuestro componente desaparecería". Estos dos conceptos los podemos traducir como que un componente **nace, vive y muere**. A estas acciones las llamamos **ciclo de vida de un componente**.

> **NOTA:** Al igual que en lecciones anteriores vamos a aprender por un lado **unos únicos conceptos** relativos al ciclo de vida de un componente. Pero vamos a ver **dos sintaxis diferentes**, una para componentes de clase (la antigua) y otra para componentes funcionales (la moderna).

## Ciclo de vida de un componente

Se llama **ciclo de vida a las acciones** que pasan desde que un componente se crea y la usuaria lo ve en pantalla hasta que se elimina. En un nivel un poco más técnico, podríamos decir que son las acciones desde que se carga en memoria del ordenador hasta que se elimina de la memoria.

Durante la _vida_ de un componente de React, **se ejecutan varios métodos** (en un componente de clase) **o hooks** (en un componente funcional), en función del momento. Gracias a estos métodos o hooks **nosotras podemos tomar el control y hacer ciertas acciones** como un `setInterval` y un `clearInterval`.

Los ciclos de vida de un componente son: **montaje, actualización y desmontaje**.

![Fases del ciclo de vida de componentes](assets/images/3_12_lifecycle.png)
> Ciclo de vida de un componente de clase. Fuente: [React lifecycle methods diagram](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

### Montaje de un componente

El montaje es la **primera fase del ciclo de vida** de un componente. Es la parte en la que se crea el componente. En el momento en que este componente se pinta en el DOM y aparece visualmente en la página web, decimos que ese componente está **montado**.

> **Ejemplo:** en esta fase podemos iniciar acciones periódicas con un `setInterval()`.

### Actualización de un componente

Como ya sabemos, mientras un componente está montado, **si cambian las `props`, el estado o ejecutamos un `this.forceUpdate()`**, el componente se **vuelve a renderizar**.

Con los métodos o los hooks del ciclo de vida podemos adaptar esto a nuestras necesidades y tomar el control. Podremos hacer operaciones en distintos puntos de la actualización o hasta impedir que el componente se re-renderice si se dan unas condiciones.

> **Ejemplo:** cuando se ejecute la función que hemos puesto dentro del `setInterval` podemos modificar el estado y provocar un re-renderizado.

### Desmontaje de un componente

Si el montaje es la primera fase del ciclo de vida de un componente, el **desmontaje es la última fase del ciclo de vida** del componente. Es la parte en la que se va a destruir el componente y va a dejar de mostrarse en pantalla y de existir en la memoria del ordenador.

Cuando React elimina un componente del DOM y, por lo tanto, ya no se visualiza en pantalla, decimos que ese componente se ha **desmontado**.

> **Ejemplo:** cuando cambiamos de una página a otra React Router desmonta los componentes que ya no se deben visualizar.

Una vez que ya tenemos claros los conceptos vamos a ver **la sintaxis en un componente de clase y uno funcional**.

## Componente de clase

Veamos el siguiente código que muestra un contador con un componente de clase:

```jsx
import React from 'react';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    };
    this.incrementCounter = this.incrementCounter.bind(this);
  }
  componentDidMount() {
    // guardamos el identificador del interval para limpiarlo en componentWillUnmount
    this.intervalId = setInterval(this.incrementCounter, 1000);
    // NOTA: guardamos el identificador en un atributo de la clase y
    // no en el estado ya que no queremos pintar el identificador en el DOM
  }
  componentWillUnmount() {
    // limpiamos el interval
    clearInterval(this.intervalId);
  }
  incrementCounter() {
    this.setState(prevState => {
      return { counter: prevState.counter + 1 };
    });
  }
  render() {
    return <div>Contador: {this.state.counter}</div>;
  }
}

export default App;
```

### Montaje de un componente de clase

Los siguientes métodos se ejecutan **en este orden** cuando React monta un componente:

1. **`constructor()`:** este ya lo conocemos. Se ejecuta **una sola vez** cuando se crea el componente y se le pasan las `props` iniciales. En este método:
   - inicializamos el estado y
   - enlazamos los _event handlers_ a la instancia con `.bind(this)`
1. **`render()`:** un viejo amigo. En este método:
   - devolvemos el código JSX que se pinta en el DOM
1. **`componentDidMount()`:** que significa literalmente "el componente se ha montado". Este método se ejecuta justo después de que el componente se haya montado en el DOM (pintado en pantalla). Por ejemplo en este método:
   - podemos pedir datos a un servidor, con `fetch`
   - podemos ejecutar un `setInterval` u otro código que nos dé datos de manera periódica

### Actualización de un componente de clase

Los siguientes métodos se ejecutan **en orden** cuando modificamos las `props` o el estado de un componente React lo actualiza:

1. **`shouldComponentUpdate(nextProps, nextState)`:** que significa literalmente "¿debe actualizarse el componente?". Con este método tomamos el control y decidimos si el componente debe re-renderizarse o no:
   - si este método devuelve un `true` el componente se re-renderizará
   - si este método devuelve un `false` el componente se NO re-renderizará
   - este método recibe como argumentos las nuevas `props` en `nextProps` y el nuevo estado en `nextState` para que nosotras comprobemos si queremos o no que el componente se re-renderice
   - al igual que en el resto de métodos de un componente, podemos acceder a `this.props` y `this.state` para compararlo con `nextProps` y `nextState`
1. **`render()`:** siempre puro y fiel, [_hay un amigo en él_](https://www.youtube.com/watch?v=-KmBrQEcNUI)
   - si el método `shouldComponentUpdate` retorna `true` o no hemos declarado `shouldComponentUpdate` sí se ejecuta `render`
   - si el método `shouldComponentUpdate` retorna `false` no se ejecuta `render`
1. **`componentDidUpdate(prevProps, prevState)`:** que significa literalmente "el componente se ha actualizado".
   - se ejecuta justo después de re-renderizar un componente
   - si el componente hace peticiones que dependen de una `prop`, este es buen lugar para volverlas a hacer
   - si queremos guardar datos del estado en `localStorage` este es un buen lugar para hacerlo, puesto que aquí el estado está correctamente actualizado

### Desmontaje en un componente de clase

El siguiente método se ejecuta cuando React desmonta un componente:

1. **`componentWillUnmount()`:** que significa literalmente "el componente se va a desmontar". En este método:
   - **limpiaremos** todo lo residual que pueda dejar nuestro componente una vez no exista
   - podemos decir que es el opuesto a `componentDidMount()`
   - aquí eliminaremos los `setInterval` con un `clearInterval`

> **NOTA:** Si no limpiásemos lo residual del componente, nos aparecerán errores de partes del código que intentan acceder a un componente que ya no existe.

#### EJERCICIO 1

**El contador con ciclo de vida**

1. Vamos a crear dos páginas con React Router.
1. La primera página va a mostrar el componente `Counter`. Podeís copiar el componente que hemos puesto de ejemplo más arriba.
1. La segunda página va a mostrar el componente `Relax` que pinte una frase relajante que nos haga olvidarnos del contador.
1. Recuerda preparar un sencillo menú que nos permita navegar entre ambas.
1. Observa qué se pinta en la página del contador.
1. Comenta el método `componentWillUnmount` y observa qué aparece en consola. ¿Sabrías decir por qué?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

Partiendo del ejercicio anterior pon un console la primera línea de todos los métodos del componente `Counter` del tipo `console.log('Se está ejecuntando el método NOMBRE_DEL_MÉTODO');` y observa el orden de ejecución de los métodos.

\_\_\_\_\_\_\_\_\_\_


## Componente funcional

Veamos el mismo ejemplo de un contador pero esta vez con un componente funcional:

```jsx
import React, { useState, useEffect } from 'react';

const App = () => {
  // usamos el hook useState para crear counter en el estado del componente
  const [counter, setCounter] = useState(0);
  // usamos el hook useEffect para gestionar los ciclos de vida del componente
  useEffect(() => {
    // las 3 siguientes líneas se ejecutan al montar y renderizar el componente
    let intervalId = setInterval(() => {
      setCounter(counter + 1);
    }, 1000);
    // la función retornada a continuación se ejecuta al desmontar y renderizar el componente
    return () => {
      clearInterval(intervalId);
    };
  });
  return <div>Contador: {counter}</div>;
};

export default App;
```

> **NOTA:** En un componente funcional no tenemos métodos, por ello toda la lógica del ciclo de vida está dentro de la función del componente, en el ejemplo anterior está dentro de `App`.

### Hook useEffect

Ya conocemos el Hook `useState` para gestionar el estado del componente. Ahora vamos a aprender el hook `useEffect` que se usa para **realizar acciones en las diferentes fases del ciclo de vida**. Se llama `useEffect` porque también **nos sirve para producir efectos secundarios** en la página, es decir, aquellas acciones que React no sabe hacer.

Si analizamos el código de `useEffect` vemos:

- `useEffect` **recibe como primer parámetro una función (sin ejecutar)**, que React ejecutará en el montaje del componente. Son las líneas:
   ```js
   let intervalId = setInterval(() => {
     setCounter(counter + 1);
   }, 1000);
   ```
- `useEffect` puede **retornar una función (sin ejecutar)**, que React ejecutará en el desmontaje del componente. Son las líneas:
   ```js
   () => {
     clearInterval(intervalId);
   };
   ```
- Puesto que `useEffect` está en el scope del componente podemos acceder desde `useEffect` a todas las variables y constantes del componente.
- Podemos tener tantos `useEffect` como queramos en un único componente.

### Montaje de un componente funcional

El orden de ejecución es el siguiente:

1. Se ejecuta la función principal del componente y se retorna el código JSX.
   - React coge el código JSX retornado por la función y lo pinta en el DOM.
   - El componente ha sido montado.
   - Esta ejecución corresponde al método `render` de un componente de clase.
1. Se ejecuta la función que **recibe `useEffect` como primer parámetro**.
   - En el ejemplo anterior son las 3 líneas:
      ```js
      let intervalId = setInterval(() => {
        setCounter(counter + 1);
      }, 1000);
      ```
   - Esta ejecución corresponde al método `componentDidMount()` de un componente de clase.

### Actualización de un componente funcional

Cada vez que se ejecuta un cambio de estado o de `props` el componente se re-renderiza. El orden de ejecución es el siguiente:

1. Se ejecuta la función principal del componente y se retorna el código JSX.
   - React coge el código JSX retornado por la función y lo pinta en el DOM.
   - Esta ejecución corresponde al método `render` de un componente de clase.
1. Se ejecuta la función que se **retorna dentro de `useEffect`**.
   - En el ejemplo anterior son las 3 líneas:
      ```js
      () => {
        clearInterval(intervalId);
      };
      ```
   - Esta ejecución corresponde al método `componentWillUnmount()` de un componente de clase.
1. Se ejecuta la función que **recibe `useEffect` como primer parámetro**.
   - En el ejemplo anterior son las 3 líneas:
      ```js
      let intervalId = setInterval(() => {
        setCounter(counter + 1);
      }, 1000);
      ```
   - Esta ejecución corresponde al método `componentDidMount()` de un componente de clase.

Si observamos este orden de acciones, podemos pensar que cada vez que se renderiza el componente React **primero lo desmonta y luego lo vuelve a montar**. Esto no es realmente así porque React no quita el componente del DOM y luego lo vuelve a añadir.

¿Entonces por qué React funciona así? ¿Acaso nos quiere torturar? Pues no, pero lo veremos en el apartado **Componente de clase VS componente funcional**.

### Desmontaje en un componente funcional

El orden de ejecución es el siguiente:

1. Se ejecuta la función que se **retorna dentro de `useEffect`**.
   - En el ejemplo anterior son las 3 líneas:
      ```js
      () => {
        clearInterval(intervalId);
      };
      ```
   - Esta ejecución corresponde al método `componentWillUnmount()` de un componente de clase.

#### EJERCICIO 3

**El contador con ciclo de vida** (one more time pero esta vez con el componente funcional):

1. Partiendo del ejercicio anterior vamos a sustituir el contenido del componente `Counter` por el código de ejemplo del componente funcional.
1. Observamos que si ejecutamos la página el comportamiento es exactamente el mismo, ya que son dos formas de hacer lo mismo.
1. Comenta el retorno de la función `useEffect` y observa qué aparece en consola. ¿Sabrías decir por qué?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

Partiendo del ejercicio anterior pon los siguientes consoles en:

- Primera línea del componente: `console.log('Me estoy renderizando');`
- Primera línea del `useEffect`: `console.log('Me estoy montando');`
- Primera línea de la función retornada en `useEffect`: `console.log('Me estoy desmontando');`

Lo que sucederá a continuación te sorprenderá!!!

\_\_\_\_\_\_\_\_\_\_

## Componente de clase VS componente funcional

Las diferencias y semejanzas entre los ciclos de vida de un componente de clase y un componente funcional son:

1. Con ambos tipos de componentes podemos controlar lo que React no sabe controlar.
1. Con ambos tipos de componentes es nuestra responsabilidad decidir en qué fase hacemos cada cosa.
1. En los **componentes de clase** tenemos métodos para tomar el control:
   - Cuando se monta el componente.
   - Antes de que se renderice.
   - Cuando se renderiza.
   - Después de que se renderice.
   - Cuando se desmonta el componente.
1. En los **componentes funcionales** tenemos código para tomar el control:
   - Cuando se monta el componente.
   - Cuando se renderiza.
   - Cuando se desmonta el componente.
1. Dicho de otra forma el Hook `useEffect` **equivale a** `componentDidMount`, `componentDidUpdate` y `componentWillUnmount` combinados.
1. En los **componentes funcionales** parece que tenemos menos fases. **Por ello parece que cada vez que se renderiza el componente se desmonta y se vuelve a montar.**
1. En los **componentes funcionales** se complica la sintaxis pero se simplican las fases.
1. ¿`useEffect` es un poco jaleo porque mezcla un montón de cosas? Sí, lo es.
1. En los **componentes de clase** el código relativo a hacer algo en el montaje y a deshacerlo en el desmontaje se reparte en varios métodos. Esto hace que el componente sea más complejo.
1. En los **componentes funcionales** el código relativo a hacer algo en el montaje y a deshacerlo en el desmontaje se agrupa en un solo `useEffect`. Esto hace que el componente sea más simple y legible.
1. Si en un **componente funcional** queremos hacer varias cosas diferentes en el montaje y deshacerlas en el desmontaje usaremos varios `useEffect`.

#### EJERCICIO 5

Vamos a crear un componente de clase que pinte un campo de texto. Cuando la usuaria escriba algo en el campo de texto tenemos que guardar dicho texto en el nuestro querido `localStorage`. Cuando la usuaria refresque la página debemos recuperar el texto del `localStorage` y pintarlo dentro del campo de texto.

> **Pista:** leeremos del `localStorage` en `componentDidMount` y guardaremos la info en el estado. Escribiremos en el `localStorage` en `componentDidUpdate`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

Vamos a repetir el mismo ejercicio de antes pero con un componente funcional.

> **Pista:** inicializaremos el estado con la info del `localStorage`. Guardaremos en el `localStorage` dentro de `useEffect`.

\_\_\_\_\_\_\_\_\_\_

## Peticiones a un servidor al arrancar la página

Si queremos traer datos del servidor **al arrancar la página** tenemos que hacerlo durante la **fase de montaje** del ciclo de vida del componente.

### En un componente de clase

Aquí es sencillo, llamamos al servidor en el `componentDidMount`, es decir, cuando el componente está montado en el DOM.

```jsx
import React from 'react';

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: {}
    };
    this.getDataFromApi = this.getDataFromApi.bind(this);
  }
  componentDidMount() {
    // una vez montado el componente iniciamos la llamada al servidor
    this.getDataFromApi();
  }
  getDataFromApi() {
    // hacemos la llamada al servidor
    fetch('https://api.rand.fun/number/integer')
      .then(response => response.json())
      .then(responseData => {
        // y cuando responde el servidor guardamos los datos en el estado
        this.setState({ data: responseData });
      });
  }
  render() {
    return <div>Número aleatorio: {this.state.data.result}</div>;
  }
}

export default App;
```

### En un componente funcional

Aquí es un poco menos sencillo, llamamos al servidor en el `useEffect`, es decir, cuando el componente está montado en el DOM.

```jsx
import React, { useState, useEffect } from 'react';

const App = () => {
  const [data, setData] = useState({});
  useEffect(() => {
    // hacemos la llamada al servidor
    fetch('https://api.rand.fun/number/integer')
      .then(response => response.json())
      .then(responseData => {
        // y cuando responde el servidor guardamos los datos en el estado
        setData(responseData);
      });
  }, []); // y con este array vacío le decimos a React que solo ejecute este useEffect una vez

  return <div>Número aleatorio: {data.result}</div>;
};

export default App;
```

Pero como ya sabemos, `useEffect` se ejecuta en cada render. Por ello sucedería lo siguiente:

1. Se ejecuta el componente sin pintar ningún número. El componente es montado en el DOM.
1. Se ejecuta **la función que recibe `useEffect`** y se piden los datos al servidor.
1. El servidor responde y se actualiza el estado con `setData`, lo que provoca un re-renderizado.
1. Al volverse a renderizar se vuelve a ejecutar `useEffect` y volveríamos al paso 2 y **BUCLE INFINITO!!!!**

> **IMPORTANTE:** Para **evitar que `useEffect` se ejecute más de una vez** debemos poner un array vacío `[]` como segundo parámetro de `useEffect`.

La [explicación es un poco compleja](https://es.reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects) pero se resume en que `useEffect` recibe como segundo parámetro un array de datos. Si estos datos son los mismos que la vez anterior que se ejecutó `useEffect`, no se vuelve a ejecutar. Si pasamos como segundo parámetro un array vacío, **siempre es igual que la vez anterior y por ello no se vuelve a ejecutar**.

## Recursos externos

### Documentación de React

Componentes de clase:

- [Añadir métodos del ciclo de vida](https://es.reactjs.org/docs/state-and-lifecycle.html#adding-lifecycle-methods-to-a-class)
- [El ciclo de vida del componente](https://es.reactjs.org/docs/react-component.html#the-component-lifecycle)

Componentes funcionales:

- [Usando el Hook de Efecto](https://es.reactjs.org/docs/hooks-effect.html)
- Os recomendamos leer más sobre [Hooks de React](https://es.reactjs.org/docs/hooks-intro.html) y [cuáles hay](https://es.reactjs.org/docs/hooks-reference.html).
