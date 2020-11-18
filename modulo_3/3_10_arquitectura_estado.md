# Arquitecturas de aplicaciones React

[codepen-lifting-state-up]: https://codepen.io/adalab/pen/xpzBYz?editors=0010

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)

<!-- /TOC -->

## Introducción

Hay montones de definiciones de qué es la _arquitectura de software_. Una de ellas es que la arquitectura es tanto la estructura de nuestro proyecto (carpetas/ficheros, componentes y cómo se relacionan, etc.) como los _patrones_ que usamos para recoger, procesar y almacenar información en esa estructura.

Mencionamos también los _patrones de software_, que no son más que recetas de cómo estructurar el código y los datos, que nos han funcionado en un contexto y seguro pueden servirle a alguien más. Podéis leer más sobre patrones típicos de React en los recursos externos.

Como sabemos, React es relativamente reciente así que van apareciendo arquitecturas y patrones de uso constantemente. Porque al final para cada caso de uso (aplicación) va a funcionar mejor una forma de estructurarlo que otra. En la visión de Dan Abramov, uno de los ingenieros que trabaja en el proyecto de React, [no existe la arquitectura perfecta que valga para todo](http://react-file-structure.surge.sh/).

![Dan Abramov tweet](assets/images/3_10_dan-abramov.png)

En esta sesión vamos a ver buenas prácticas para organizar nuestras aplicaciones de React: estructura de componentes, uso del estado, servicios que no son componentes, etc.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Ya sabemos que existen un montón de formas de hacer las cosas en programación, y con React no es una excepción. Pero hay algunas formas que funcionan mejor que otras para construir frontales basados en componentes.

En esta sesión vamos a proponeros una arquitectura concreta para trabajar con componentes web con estado. También cómo estructurar una aplicación React que trabaja tanto con componentes como con _servicios_, es decir, partes de código JS que no son componentes visuales.

## Arquitectura de componentes con estado

Cuando trabajamos en aplicaciones React con varios componentes, la gestión de estado se vuelve compleja. Cuando desde un componente necesito unos datos que están en otro, primero tendré que identificar en cuál están y luego acceder a ellos, ya sea por _props_ o _lifting_. Para manejar esta situación, existen distintas arquitecturas de componentes. En esta sesión os proponemos una concreta con la que trabajar que, aunque no es la única ni vale para todas las situaciones, sí que os va a ayudar a estructurar mejor vuestra aplicación React.

A pesar de que todos los componentes pueden tener estado, a la hora de hacer aplicaciones web con React, preferiremos **agrupar todos los estados en el componente raíz**. El resto de componentes serán _dummies_ (títeres), que significa que no tendrán estado. Podemos referirnos al estado del componente raíz como **estado de la aplicación** o **estado global**.

_¿Por qué hacemos esto?_ En los estados guardaremos diferentes datos, algunos de los cuales habremos recibido de servidores: una lista de artículos en venta, sus precios y un booleano de si mostramos el IVA o no, por ejemplo. El mejor sitio para guardar esos datos es siempre el componente raíz, porque es el sitio desde el que cualquier componente hijo podrá acceder a ellos.

_¿Y cómo lo haremos?_ Como vimos en la sesión anterior podemos pasar datos de hijos a padres/madres **mediante _lifting_**. Recordemos que la técnica de _lifting_ consistía en pasar una función definida en el padre/madre a un componente hijo mediante las `props`. Esa función puede modificar a la madre. Ahora que hemos visto los estados, podemos ver un nuevo uso del _lifting_: **actualizar estados de los padres/madres desde los hijos**.

```js
const ENDPOINT = 'https://...';

class AppRoot extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      reasonsStore: []
    };

    this.fetchNewReasons = this.fetchNewReasons.bind(this);
  }

  fetchNewReasons() {
    fetch(ENDPOINT)
      .then(response => response.json())
      .then(data => {
        this.setState({
          reasonsStore: data.reasons
        });
      });
  }

  render() {
    const { reasonsStore } = this.state;

    return (
      <section>
        <ReasonsList reasons={reasonsStore} />
        <UpdateButton updateList={this.fetchNewReasons} />
      </section>
    );
  }
}

class UpdateButton extends React.Component {
  render() {
    const { updateList } = this.props;

    return <button onClick={updateList}>Update reasons</button>;
  }
}
```

[&blacktriangleright; _Lifting_ de estados en Codepen][codepen-lifting-state-up]

> **NOTA**: En algunos casos una parte del estado tiene sentido que esté en un componente que no sea el raíz. Por ejemplo, para un componente colapsable tiene sentido que la información de si está desplegado o no sea del propio componente y no del raíz. Este tipo de casos específicos vamos a ir identificándolos con la práctica.

## Servicios en módulos externos

Una buena práctica en desarrollo de software en general es desacoplar las distintas partes de una aplicación y que puedan funcionar de forma independiente. Si, por ejemplo, tenemos desacoplado el acceso a un API que nos da información sobre el tiempo, vamos a poder cambiar de proveedor de weather.com a accuweather.com sólo modificando ese módulo. Otro ejemplo: si tenemos un módulo de nuestra aplicación que guarda la información de nuestros usuarios en una base de datos, vamos a poder cambiar el servicio de AWS a Firebase sólo modificando ese módulo.

Siguiendo con el ejemplo anterior, os proponemos usar una carpeta `services` con un servicio `ReasonsService.js` que NO es un componente visual sino simplemente se encarga de hacer las peticiones al API:

**ReasonsService.js**

```js
const ENDPOINT = 'https://...';

const fetchReasons = () => fetch(ENDPOINT).then(response => response.json());

export { fetchReasons };
```

**App.js**

```js
import {fetchReasons}  from './services/ReasonsService';

class AppRoot extends React.Component {

  ...

  fetchNewReasons() {
    fetchReasons()
      .then(data => {
        this.setState({
          reasonsStore: data.reasons
        });
      });
  }
...

```

A primera vista no parece ninguna mejora, simplemente que nos complica más al tener que tener un nuevo fichero. Pero cuando la aplicación va creciendo, vamos a ver que es muy útil tener esta parte desacoplada de los componentes de React.

## Loader

Un patrón común en React, y en general en las aplicaciones web, es usar loaders, es decir, indicadores de que algo está cargando para mantener informado al usuario. En React normalmente tendremos un componente `Loader` que será un texto o una imagen de un spinner, y que mostraremos hasta que tengamos los datos y podamos mostrarlos. Normalmente usaremos un patrón habitual de React, _conditional rendering_, que consiste en pintar un componente u otro dependiendo de una condición. Habitualmente usaremos ternarios para hacer esta comprobación directamente en el método render del componente principal.

Vamos a ver un ejemplo con Murrays. Definimos una clase `Loader` con nuestro mensaje de cargando. En nuestro componente principal tenemos en nuestro estado un booleano para saber si se han terminado de cargar los datos, que por defecto es falso. Cuando terminen de cargarse, lo pondremos a verdadero. Finalmente pintamos en el método render el `Loader` o los datos, dependiendo del valor del estado.

```js
class Loader extends React.Component {
  render() {
    return <p>Loading...</p>;
  }
}

class MurrayList extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      loading: true
    };
    //Simulamos que los datos se han cargado tras 2 segundos
    setTimeout(() => this.setState({ loading: false }), 2000);
  }

  render() {
    const { handleClick } = this;

    return (
      <section className='section-murrays'>
        <h1>
          All <del>Cats</del> Murrays Are Beautiful
        </h1>

        {this.state.loading ? (
          <Loader />
        ) : (
          <ul className='section-murrays_list'>
            <li>
              <RandomMurray />
            </li>
            <li>
              <RandomMurray />
            </li>
            <li>
              <RandomMurray />
            </li>
          </ul>
        )}

        {/* pasamos handleClickAndReload al hijo como prop */}
        <ReloadButton actionToPerform={handleClick} label='More murrays' />
      </section>
    );
  }
}
```

&rtrif; [Puedes jugar con el ejemplo en Codepen](https://codepen.io/adalab/pen/qLrZJz?editors=0010).

## Fragments

Otro patrón propio de React muy útil son los `Fragments`. Como sabéis tenemos la limitación de tener cada componente debe devolver en su método render un único elemento que contiene al resto. Pero esto muchas veces nos obliga a tener que meter contenedores (div) que muchas veces no queremos. Para solucionar este problema tenemos los Fragments, que nos permiten agrupar elementos sin tener que introducir ningún contenedor en el HTML.

En este ejemplo, nuestro render puede devolver 3 componentes agrupados en un Fragment que no introduce ningún contenedor adicional en HTML.

```js
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
}
```

#### EJERCICIO 1

**Directorio**

En este ejercicio vamos a realizar un directorio de personas, al estilo de LinkedIn, con unos filtros que permiten seleccionar las personas que aparecen. Para ello vamos a partir de un array de datos de gente aleatoria generado por https://randomuser.me/. Por ejemplo, un listado de 50 personas con datos aleatorios: https://randomuser.me/api/?results=50

Vamos a mostrar de cada persona

- su nombre
- foto
- ciudad
- edad

Vamos a poder filtrar por

- ciudad
- género

El resultado debe ser parecido a este diseño de LinkedIn:

![Faceted search](assets/images/3_9_faceted-search.png)

> **Nota:** os recomendamos hacer este ejercicio con componentes de clase ya que para hacerlo con un componente funcional necesitamos el Hook `useEffect` que lo aprenderemos en los ciclos de vida de los componentes.

**¡Al lío!**

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

### Egghead

Serie de clases en vídeo que introduce y explora los fundamentos básicos de React (en inglés).

- [Componentes de orden superior (con lógica) o contenedores](https://egghead.io/lessons/react-react-fundamentals-higher-order-components-replaces-mixins)

### React patterns

- [React patterns](https://reactpatterns.com/)

- [Fragments](https://reactjs.org/docs/fragments.html)
