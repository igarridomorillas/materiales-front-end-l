# Formularios en React

[codepen-form-example]: https://codepen.io/adalab/pen/WyBqdK?editors=0010

## Contenidos

<!-- TOC -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
<!-- /TOC -->

## Introducción

Los formularios funcionan un poco diferente en React que un formulario simple HTML. Los elementos de formulario almacenan de por sí un estado, que es el valor del input. En React, cuando creamos un formulario vamos a manejar el estado de los input usando el estado de los componentes de React. Manejarlo de esta forma nos va a facilitar procesar los datos introducidos por el usuario, ya sea para hacer validaciones o a la hora de enviar los datos a un servidor.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Para crear apps de React que tienen un formulario, y hacerlo de la forma correcta en React. Por ejemplo, ¿no estáis haciendo un proyecto que tiene formularios?

## Formularios

Los elementos `input` de formulario, como bien sabemos, tienen un estado interno: su propiedad `value` se actualiza cuando el usuario modifica su contenido. En React, además, otros elementos de formulario como `textarea` y `select` tienen un comportamiento similar que facilita acceder a estos datos.

Cuando queremos realizar procesamiento de estos datos que introduce el usuario, ya sea para enviar los datos a un API o realizar validaciones, ¿qué hacíamos hasta ahora? Pues teníamos que buscar cada elemento en el DOM y recoger su `value`. Pero en React sabemos que la información de la interfaz la tenemos en el estado del componente: ¿y si guardamos los datos que introduce el usuario en el estado del componente cada vez que cambia un elemento? Pues es así exactamente como se hace en React.

Partimos de un formulario simple que recoge el nombre del usuario:

```js
class AwesomeForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: ''
    };

    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(event) {
    this.setState({ name: event.target.value });
  }

  render() {
    return (
      <form>
        <label htmlFor="name">Name:</label>
        <input id="name" type="text" onChange={this.handleChange} />
        <input type="submit" value="Enviar" />
      </form>
    );
  }
}
```

Hemos creado un componente simple, `AwesomeForm`, que tiene un formulario con un nombre. Al `input` de tipo texto para el nombre, le hemos añadido un escuchador de eventos `onChange` para que cada vez que se modifique el `input`, se guarde la información en el estado.

> NOTA: Fíjate también que en la etiqueta `label` hemos usado el atributo `htmlFor` en lugar de `for`, ya que es una palabra reservada de JavaScript, lo mismo que con pasaba con `class` y `className`.

### Componentes controlados

Muy bien, pero hay una cosa más que tenemos que hacer para asegurarnos de que la información que guardamos en el estado sea "de verdad verdadera" la que introduce el usuario. Y es obligar a que su `value` tome los datos directamente del estado, es decir, que se muestren de nuevo en el `input`.

El ciclo que siguen los datos es:

1. el usuario escribe en el `input`
2. a través del evento de cambio se guardan en el estado
3. al cambiar el estado se ejecuta en método `render` y se asignan como `value` al `input`

¿Y para qué tanto lío? Pues para garantizar que en el estado tenemos todos los datos necesarios para pintar la interfaz. Vamos a ver cómo queda en el ejemplo anterior.

```js
class AwesomeForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: ''
    };

    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(event) {
    this.setState({ name: event.target.value });
  }

  render() {
    return (
      <form>
        <label htmlFor="name">Name:</label>
        <input
          id="name"
          type="text"
          value={this.state.name}
          onChange={this.handleChange}
        />
        <input type="submit" value="Enviar" />
      </form>
    );
  }
}
```

A estos elementos de formulario, que tienen su `value` enlazado al estado del componente, se les llama **componentes controlados** (_controlled components_) y son la forma habitual de manejar campos de formulario en React.

Usar un _componente controlado_ tiene más ventajas, por ejemplo, nos permite validar los datos que introduce el usuario. Como nosotras guardamos los datos en el estado, podemos ejecutar el código que queramos antes de guardarlo, y lo que hagamos se verá reflejado en el `input`, puesto que está enlazado al estado a través de su `value`. Veamos el ejemplo anterior, pero forzando a que el nombre esté en mayúsculas.

```js
    handleChange(event) {
        this.setState({name: event.target.value.toUpperCase()});
    }
```

[&blacktriangleright; Usando un componente controlado en Codepen][codepen-form-example]

#### EJERCICIO 1

**Formulario para pelis**

Vamos a crear un formulario en un componente de React que recoja información de una película:

- **nombre**, en un campo de texto
- **descripción**, en un textarea
- **idioma**, en un select donde podemos seleccionar entre Español, Inglés o Portugués

El resultado de rellenar el formulario, debe aparecer en una tarjeta de previsualización que va mostrando la información según se rellena.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

**Refactor del formulario**

Vamos a hacer un pequeño refactor del código del ejercicio anterior: usaremos una única función escuchadora para el evento `change` de cada campo. Para eso, recordad que podemos acceder a la clave de un objeto cuyo nombre tenemos en una variable usando el operador `[key]` siendo `key` la variable que tiene el nombre de un campo del objeto. Por ejemplo:

```js
this.state = {
  name: 'Groundhog Day',
  description:
    'A weatherman finds himself inexplicably living the same day over and over again.'
};
...
...
onChange = event => {
  const name = event.target.name;
  this.setState({
    [name]: 'Leaving Las Vegas'
  });
}

```

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

**Más datos de las pelis**

Vamos a añadir más información a nuestro formulario de películas

- **clasificación por edades**, donde usaremos radio buttons con las opciones: A (todos los públicos, aparece marcada por defecto), 7, 12, 16 y 18
- **género**, donde usaremos checkboxes y podrán marcarse un máximo de 3 de las opciones: comedia, drama, fantasía, acción, familia, terror

\_\_\_\_\_\_\_\_\_\_

## Refs

Hasta ahora sabemos que para pintar la información de nuestros componentes en el DOM hemos delegado totalmente en React: nos hemos olvidado de los `querySelector` y los `innerHTML`. Para modificar en pantalla los datos de un componente, le pasamos nuevas `props` o modifica su estado y se vuelve a pintar actualizado.

Pero para algunos casos concretos vamos a necesitar acceder al DOM directamente y, para estos casos, React nos ofrece una alternativa: los Refs o referencias al DOM. Debemos usarlos solo en ocasiones muy específicas como:

- manejar el foco de un elemento de un formulario, la selección de texto o la reproducción multimedia
- iniciar animaciones
- integrar en nuestra aplicación librerías externas que usan el DOM

### Usando refs

Para poder usar refs en nuestro código de React tenemos que seguir estos sencillos pasos:

1. declarar un atributo en el `constructor` llamando a la función `React.createRef()`
2. crear un atributo `ref` en el elemento que necesitamos referenciar, y le damos como valor el atributo anterior
3. para poder usar una referencia al DOM desde un método cualquiera de la clase usamos la propiedad `current` del atributo declarado en el punto 1

Vamos a ver un ejemplo de la documentación de React que sigue estos 3 pasos para que, al pinchar en un campo, cambiamos el foco a otro campo usando refs.

```js
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = React.createRef();
    this.focusTextInput = this.focusTextInput.bind(this);
  }

  focusTextInput() {
    this.textInput.current.focus();
  }

  render() {
    return (
      <div>
        <input type="text" ref={this.textInput} />

        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```

### Componentes no controlados: el `input` de tipo `file`

Existe una excepción en el uso de elementos de formulario como componentes controlados, y es al usar un campo de tipo fichero (`file`). En este caso, no puede ser controlado ya que se trata de un campo de solo lectura porque el único que puede modificarlo, por temas de seguridad, es el usuario de la web.

Para trabajar con este `input` y, por ejemplo, acceder a su contenido tendremos que acceder a él como un nodo del DOM. Por tanto, vamos a usar las Refs que hemos visto antes para acceder a la información del fichero que ha elegido la usuaria.

Veamos un ejemplo de la documentación de React.

```js
class FileInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.fileInput = React.createRef();
  }
  handleSubmit(event) {
    event.preventDefault();
    alert(`Selected file - ${this.fileInput.current.files[0].name}`);
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Upload file:
          <input type="file" ref={this.fileInput} />
        </label>
        <br />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

#### EJERCICIO 4

**Pelis con carátula**

Partiendo del ejercicio anterior, vamos a añadir un campo más al formulario que sea la carátula de la película. Al elegir el usuario una carátula, se muestra una previsualización de la misma, y se guardan los datos en el estado. Recuerda que para leer la información de ficheros debemos usar un `FileReader` y para recoger la información de una imagen su método `readAsDataURL`.

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

### Documentación de React

Documentación oficial de React (en inglés).

- [Formularios en React](https://reactjs.org/docs/forms.html)

- [Manejo del input tipo `file` en React](https://reactjs.org/docs/uncontrolled-components.html#the-file-input-tag)

- [Refs y el DOM](https://reactjs.org/docs/refs-and-the-dom.html)
