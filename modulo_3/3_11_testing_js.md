# Introducción al testing con JavaScript

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)
- [EJERCICIO BONUS 8](#ejercicio-bonus-8)

## Contenidos


## Introducción

En esta sesión vamos a tener un primer contacto con el testing automático de nuestros proyectos de front-end, en concreto, de la parte de JavaScript.

Testing es ni más ni menos que probar que una aplicación funciona como se espera, es decir, que cumple con los requisitos con los que se definió. _¿Hasta ahora hemos estado haciendo testing?_ Pues claro, cada vez que creamos una funcionalidad en una web la vamos probando manualmente: abrimos el navegador y probamos, por ejemplo, que la tarea se tacha al marcarla como completada en nuestra lista de tareas, o que las nuevas tareas se guardan en LocalStorage y al recargar el navegador siguen ahí.

Todas estas pruebas las hacemos de forma manual, es decir, miramos directamente en el navegador si sucede el comportamiento que esperamos. Si no, pues hay un error y toca _debuggearlo_. ¿Existen otras formas de hacer testing? Sí, por ejemplo, los test de usuario se hacen para que un potencial usuario de nuestra web pruebe nuestro producto y nos dé feedback. También tenemos los **tests automáticos**, que son en los que nos vamos a centrar en esta sesión. Estos test, en lugar de realizarlos nosotras a mano los va a realizar una máquina por nosotras para hacerlo de forma más rápida y evitarnos ese trabajo tedioso de ir probando manualmente que todo funciona correctamente. ¿Y cómo es posible? Pues porque los vamos a programar. _¿¡A programar!?_ Pues sí, desarrollaremos por tanto un programa (se le llama _código de tests_) que prueba que nuestra aplicación (se le llama _código de producción_) funciona correctamente.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Desarrollar tests automáticos para un proyecto de software sirve principalmente para garantizar su calidad. A simple vista puede parecer poco, pero es demostrar que nuestro producto funciona como se espera y que no va a tener fallos (o al menos una serie determinada de fallos). Todo software serio tiene asociado un proceso de testing que, muchas veces, incluirá tests automáticos. En esta sesión aprenderemos a escribir tests automáticos que nos servirán para asegurar la calidad del código JavaScript que tenemos en el front-end de nuestra web.

Pero el testing, ¿lo hace también la programadora? ¿No hay equipos de QA (Quality Assurance) que se encargan de esto? Pues depende de cómo lo gestione la empresa. Pero, en general, los tests unitarios (que veremos qué son más adelante) van a ser responsabilidad de la propia programadora. Es decir, que debes ser responsable de que el código que entregas (que subes en un PR) funciona como se ha establecido en los requisitos.

Siendo la calidad el principal objetivo de desarrollar tests automáticos, existen otras consecuencias positivas. Una de ellas es mejorar la documentación del proyecto. Es decir, si tengo escrito un test que dice cómo funciona mi web entonces cuando alguien venga en el futuro a ver cómo funciona (que puedo ser yo misma dentro de unos meses o semanas) podrá leer el test y entenderlo.

Otra ventaja de tener tests automáticos relacionada con la calidad es combatir los _errores de regresión_. ¿Nunca os ha pasado que, al escribir código para una nueva funcionalidad de nuestra app... estropeamos algo que ya funcionaba? Pero quizá no nos damos cuenta en el momento porque solo hemos probado manualmente la nueva funcionalidad. Al tener tests automáticos (llamados _tests de regresión_), podremos detectar inmediatamente si estamos _rompiendo_ funcionalidades ya implementadas y actuar en consecuencia.

## ¿En qué casos se utiliza?

Como hemos mencionado antes, quién es responsable del testing depende de la empresa. De hecho, hay empresas (o clientes) que no quieren hacer testing automático. Pero cada vez más empresas se van dando cuenta de que es muy importante garantizar un mínimo de calidad en su software sobre todo para proyectos grandes, y la forma fundamental de garantizar esa calidad es tener una batería de tests automáticos. Como programadoras además, nos va a dar una sensación de tranquilidad saber que los tests están velando por nosotras. Que, por muy mal que vaya la cosa, garantizamos que ciertas cosas van a funcionar tal y como queremos.

## Testing

Dado que en esta sesión vamos a hablar de tests automáticos, vamos a dar una definición de diccionario:

> En las pruebas de software, la **automatización de pruebas** consiste en el uso de software especial (casi siempre separado del software que se prueba) para controlar la ejecución de pruebas y la comparación entre los resultados obtenidos y los resultados esperados.
>
> _Fuente_: [wikipedia](https://es.wikipedia.org/wiki/Automatizaci%C3%B3n_de_pruebas)

### Tipos de testing

Existen muchas clasificaciones de testing, pero aquí hemos elegido una de las más aceptadas que clasifica los tests por su nivel de granularidad en:

- **tests unitarios**: prueban un trozo de código (pieza) que solo hace una cosa (unidad), por ejemplo, una función.
- **tests de integración**: prueban que varias piezas de código funcionan bien juntas, por ejemplo, una función que llama a otras funciones; podemos juntar tantas piezas como queramos, hasta llegar a la aplicación completa.
- **test de regresión**: son un tipo de test que comprueba que las nuevas funcionalidades desarrolladas, no rompen las funcionalidades anteriores.
- **tests de aceptación o _end-to-end_**: son un tipo especial de tests de integración que están relacionados con los criterios de aceptación definidos por el cliente, es decir, que prueban algo que tiene valor a nivel de negocio; por ejemplo, que un usuario puede crear una tarea nueva en nuestra aplicación de gestión de tareas.

En el front-end normalmente vamos a tener muchos tests de integración puesto que estamos continuamente interactuando con componentes externos a nuestro código. Por ejemplo, serán tests de integración los que comprueban que algo se pinta bien en el DOM, guardan algo en LocalStorage o hacen una petición a un API.

Aún así, en esta sesión nos centramos en aprender a los tests más básicos, los unitarios, que son la base sobre la que se cimenta el testing automático.

### Anatomía de un test unitario

Como ya sabemos, los tests unitarios son una porción de software que se encarga de probar una funcionalidad pequeña de nuestra aplicación. Estos tests tienen una estructura que es siempre igual y que contiene estas 3 partes en este orden:

1. **Preparación**: en esta parte del tests preparamos el código para poder realizar la prueba. Por ejemplo, si probamos un método de una clase, primero tendremos que crear un objeto de esa clase para probarlo.
1. **Actuación**: realizamos la acción que queremos probar. Por ejemplo, invocar un método con unos parámetros.
1. **Aserción**: comprobamos si el resultado de la acción es el esperado. Por ejemplo, el resultado de la invocación del método anterior tiene que devolver un valor determinado.

En inglés estas partes tienen un acrónimo que es muy fácil de recordar _AAA_ (la triple _A_): _Arrange Act Assert_.

Vamos a ver un ejemplo de código aunque todavía no entendamos muy bien qué hace:

```js
test('fizzbuzz returns 1 when the input is 1', () => {
  //Arrange
  const number = 1;

  //Act
  const result = fizzbuzz(number);

  //Assert
  expect(result).toBe(1);
});
```

Este código comienza por una descripción de la regla que debe cumplir el test: debe devolver 1 cuando el parámetro de entrada a la función es 1. Luego, en el test en sí, primero preparamos un parámetro en una variable (_arrange_); luego ejecutamos una función `fizzbuzz` y recojo el resultado en otra variable (_act_). Finalmente compruebo si el resultado tiene el valor que espero (_assert_) usando la función `expect` que veremos más adelante para qué sirve.

A la hora de hacer tests es fundamental que los requisitos de cómo tiene que funcionar lo que hemos programado sean claros y tangibles. Por ejemplo, si hemos programado un campo de formulario para una contraseña deberemos tener claro si ese campo debe tener un mínimo de caracteres, si está permitido usar espacios o caracteres especiales, qué sucede cuando el usuario pulsa el botón de enviar y la fecha es incorrecta, etc.

En algunos casos se nos pasará algún detalle de estos requisitos, no pasa nada es normal y nos ha pasado a todos. Lo importante es que queden claras las reglas fundamentales que debemos testear y haya tests para probar esas reglas. Imagina la repercusión si eres un banco y tu campo de contraseña no funciona porque no se pueden meter números.

### Características de los tests unitarios

Los test unitarios se definen una serie de características

- **Rápidos**: comparados con los tests de integración, los unitarios deben ejecutarse muy rápido. Por ejemplo, cientos de tests en menos de un segundo. Son rápidos en comparación con los de integración, ya que muchos de ellos acceden a sistemas externos (APIs, base de datos, etc).
- **Aislados**: los tests unitarios deben probar una funcionalidad aislada de nuestra aplicación, es decir, una porción de código. Por ejemplo, un componente, sin hacer uso de otros componentes internos (otro componente hecho por mí) ni externos (DOM, API, etc).
- **Repetibles**: cuando repito un test con las mismas condiciones, el resultado debe ser el mismo. Por ejemplo, es complicado hacer tests de cosas no predecibles como números aleatorios o cuando alguna condición depende del tiempo.
- **Automatizados**: se deben poder comprobar sin intervención humana. Por ejemplo, no debe haber una persona revisando logs manualmente sino que debe ser un proceso totalmente automático.
- **Hechos a tiempo**: deberíamos hacer estos tests antes de que sucedan los errores, no a consecuencia de ellos. Y según _TDD_ (metodología que veremos más adelante) deben ser hechos antes incluso del código.

De nuevo, existe un acrónimo en inglés para recordar estas característica: _FIRST - Fast, Isolated, Repeatable, Self verifying, Timely_.

## Testing en JavaScript y React

Ahora que ya tenemos unos conocimientos básicos de testing, vamos a ver qué herramientas tenemos para poder hacer testing de nuestra aplicación en JavaScript. Hay montones de herramientas disponibles, pero vamos a centrarnos en una que está muy ampliamente adoptada en la comunidad de React: Jest. Esta herramienta nos proporciona mucha funcionalidad, pero vamos a centrarnos en lo más básico.

### Instalación

Crea un proyecto nuevo con `npm create-react-app` (no utilices tu `react-starter-kit`). Una vez creado el proyecto abre VS Code con ese proyecto y arráncalo.

> **Nota:** si quieres puedes borrar los ficheros que no vayas a utilizar y puedes recolocar cada fichero dentro de su carpeta, ya sabes `App.js` dentro de la carpeta `components`, los estilos dentro de la carpeta `stylesheets/`...
>
> Pero no borres los ficheros `setupTests.js` ni `App.test.js` ya que los vamos a utilizar para el testing.

A continuación vamos a arrancar los tests en una terminal y cada vez que cambiemos cualquier fichero de nuestro proyecto, se van a ejecutar los tests para comprobar en todo momento si nuestro código pasa los tests.

¿Cómo sabe Jest qué fichero es un test y qué fichero es un fichero normal de nuestra aplicación? pues porque los ficheros de test tienen la extensión `.test.js`. Por ejemplo el fichero `App.test.js` es el test del fichero `App.js`.

#### EJERCICIO 1

**Testeando componentes de React**

`create-react-app` nos crea muchos ficheros y entre ellos un test llamado `App.test.js` para testear el componente `App.js`. Sigue los siguientes pasos para saber cómo funciona.

1. Ya sabemos que con `npm start` arrancamos la aplicación, con `npm run build` (o `npm run docs`) generamos los ficheros para subirlos a GitHub Pages. Pues bien, ejecuta `npm run test` en una terminal de VS Code para arrancar los tests.
1. Abre el fichero `App.js` y mira lo que tiene.
1. Abre el fichero `App.test.js`.
   1. En la línea `import { render, screen } from '@testing-library/react';` importamos `render` y `screen` que nos ayuda a testear cosas de React.
   1. En la línea `import App from './App';` importamos el componente que queremos testear.
   1. Ojo: si hemos movido `App.js` a la carpeta `components/` deberemos poner algo como `import App from '../components/App';`
   1. Dentro `test(...)` tenemos:
      1. La línea `render(<App />);` que nos renderiza el componente `App`. Aquí estamos preparando el test, es la fase **Arrange**.
      1. La línea `const linkElement = screen.getByText(/learn react/i);` busca dentro de `App` y obtiene la etiqueta HTML que contenga el texto `learn react`. Aquí estamos actuando, es la fase **Act**.
      1. La línea `expect(linkElement).toBeInTheDocument();` comprueba el valor de `linkElement` y mira si está en el documento, es decir, dentro de la página. Es la fase **Assert**.
      1. Básicamente lo que hemos hecho es buscar una etiqueta HTML en el componente `App` y comprobar si existe. Si existe el test pasará. Si no existe el test no pasa y nos muestra un error en la terminal.

Supongamos que ahora nos viene la diseñadora y nos pide que en nuestra página no ponga **Learn React**, sino que ponga **Aprendiendo React**.

1. Edita `App.js` para que en la página ponga **Aprendiendo React**.
1. Arranca el proyecto con `npm start`.
1. Arranca los tests en otra terminal con `npm run test`.
1. Verás que el test está fallando. Hemos roto los tests, porque nuestra aplicación ha cambiado. Cada vez que hacemos un cambio en la aplicación debemos volver a ejecutar los tests para ver si fallan y si fallan hay que arreglarlos. ¿Qué debes cambiar en `App.test.js` para que el test vuelva a funcionar.

> **Nota:** normalmente hacemos testing con dos terminales abiertas, una para tener el proyecto arrancado y otra para tener los tests corriendo. Y siempre miramos la terminal para estar atentas a ver si los tests se rompen.

> **Nota:** los errores que aparecen en la terminal nos dan mucha información. Lo lógico es leer detenidamente dicha información pasar qué está fallando, en qué línea, en qué fichero...

\_\_\_\_\_\_\_\_\_\_

### Matchers

En el ejercicio anterior hemos visto la línea:

```js
expect(linkElement).toBeInTheDocument();
```

Con esta línea lo que estamos diciendo es que yo como programadora de test estoy esperando o suponiendo que `linkElement` va a estar en el documento (toBeInTheDocument).

`.toBeInTheDocument()` es un matcher. Es decir es lo que comprueba que lo que estoy esperando se ha cumplido.

- Si `linkElement` no está en el documento, no se cumple lo que yo suponía y el test falla.
- Si `linkElement` sí está en el documento se cumple lo que yo estaba esperando y el test ha funcionado.

Jest nos ofrece un montón de matchers para comparar el resultado de nuestra actuación con el resultado esperado.

El más típico es `toBe()`, que lo que hace es comparar con `===` si el valor que espero es exactamente igual al valor que obtengo. Por ejemplo se pondría así:

```js
import area from './services/area';

test('check square area', () => {
  // arrange
  const squareBase = 3;
  // act
  const squareArea = area.getSquareArea(squareBase);
  // assert
  expect(squareArea).toBe(9);
});
```

Aquí el valor que espero es 9 y el valor que obtengo de la función `area.getSquareArea` está en `squareArea`.

En Jest hay muchísimos matchers:

- `toEqual()` para comparar el contenido de 2 objetos o arrays
- `toBeGreaterThan()` para comparar que un número es mayor que otro
- `toContain()` para comprobar que un array contiene un valor

Puedes encontrar en resto de matchers y algunos tutoriales en la [documentación de Jest sobre matchers](https://facebook.github.io/jest/docs/en/using-matchers.html).

Si en algún momento queremos hacer una comparación muy compleja, por ejemplo que el número que espero sea mayor de 10 y menor de 20 y que sea impar y que no sea un número primo... podemos hacer dos cosas:

- Poner varios expects y matchers:
   ```js
   expect(expectedNumber).toBeGreaterThan(10); // compruebo si es mayor de 10
   expect(expectedNumber).toBeLessThan(20); // compruebo si es menor de 20
   ...
   ```
- Y / o progamar nosotras las comprobaciones que queramos y luego comprobarlas con un `.toBe()`;
   ```js
   const isOdd = expectedNumber % 2 === 1;
   expect(isOdd).toBe(true); // compruebo si es impar
   ```

#### EJERCICIO 2

**Testear el tipo de la etiqueta**

En el ejercicio 1 hemos visto que el test comprueba si hay una etiqueta HTML que tiene el texto **Aprendiendo React**. Pues bien ahora vamos a testear de qué tipo es esa etiqueta HTML, si es un link, un párrafo, una cabecera...

1. Añade a `App.test.js` un nuevo test con el siguiente código:
   ```js
   test('check if "Aprendiendo React" is a link', () => {
     // arrange
     render(<App />);
     // act
     const linkElement = screen.getByText(/aprendiendo react/i);
     console.log(linkElement.nodeName); // esto consolea A porque los links se crean con <a href="...">texto</a>
     const linkTagName = linkElement.nodeName;
     // assert
     // expect(linkTagName)...
   });
   ```
1. Descomenta la línea `expect(linkElement)...` y complétala para que el test pase correctamente.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

**Testear el href del link**

Partiendo del ejericio anterior vamos a comprobar si el href del link es `https://reactjs.org`.

1. Crea un nuevo test en `App.test.js`.
1. Pon una buena descripción dentro de `test('Descripción del test', ...)`.
1. Añade la línea `render(...)` para preparar el test.
1. Añade la línea `screen(...)` para ejecutar o actuar el test.
1. Añade un `expect(...)` con un matcher para que comprobemos que el href del link es `https://reactjs.org`.

Como ves podemos testear todo nuestro código JSX. React también nos da herramientas para testear el resto de funcionalidad de React como las props, eventos, estado...

La pregunta del millón es: ¿Cuántas cosas queremos testear de cada componente?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

**Testar JS**

Hasta ahora hemos testeado cosas de React y JSX. Ahora vamos a testear código JS puro y duro. Sobre el ejercicio anterior:

1. Crea el fichero en `src/services/area.js`:
   1. Este fichero debe tener una función llamada `getSquareArea()` que retorna el área de un cuadrado.
   1. Este fichero debe tener otra función llamada `getSquareTriangle()` que retorna el área de un triángulo.
   1. Este fichero debe exportar un objeto con las dos funciones dentro.
   1. Si quieres puedes usar estas funciones desde tu `App.js`, tampoco es que sea necesario para lo que queremos hacer en este ejercicio.
1. Crea el fichero en `src/area.test.js`:
   1. En este fichero debes importar el fichero a testear con `import area from '../services/area';`.
   1. Crea un test que compruebe que si le pasamos a la función `getSquareArea()` un 3 esta nos devuelve un 9.
   1. Crea otro test que compruebe que si le pasamos a la función `getSquareTriangle()` un 3 esta nos devuelve un 4.5.

Ahora mismo se me pasa por la cabeza una pregunta: ¿Qué debe hacer la función `getSquareArea()` si no le pasamos ningún argumento? ¿Debería dar un katakroker? ¿Devería devolver `undefined`, `null`, `false`...? ¿Debería devolver `0`?

Si da un katakroker mal asunto. Cuando terminemos de programar una aplicación, nunca debería haber katakrokers en la terminal.

Estas preguntas nos surgen cuando testeamos nuestro código, antes no habíamos pensado en ello. Es decir, el testing nos ayuda a replantearnos nuestro código desde otro punto de vista. Nos ayuda a pensar en todos los posibles errores que se pueden producir.

Pues ahora que te has hecho estas preguntas haz lo siguiente:

1. Edita la función `getSquareArea()` para que si el parámetro que recibe es `undefined` devuelva algo.
   1. Si recuerdas, cuando una función espera un parámetro y al ejecutarla no se le pasa ese parámetro, dentro de la función recibimos el parámetro como `undefined`.
   1. ¿Qué debería devolver la función en este caso? un `undefined`, `null`, `false` o `0`, lo que tú quieras, lo que consideres que es el comportamiento adecuado de esta función.
1. Añade un test más a `src/area.test.js` para que también comprobemos qué ejecutamos la función `getSquareArea()` sin argumentos, esta devuelva lo que tú hayas decidido que devuelva.

Y así hasta el infinito, nos debemos preguntar ¿Qué pasa si la función recibe parámetros pero no son números, son arrays, objetos, textos, booleanos...? Siempre que programemos una función debemos hacernos estas preguntas:

- ¿Quiero hacer un código tan robusto que la función `getSquareArea()` pueda recibir cualquier cosa?
- ¿Voy a ejecutar yo esa función simpre?
- ¿Desde donde se ejecuta la función hay posibilidad de pasar como argumentos algo que no sea un número?
- ¿La función va a ser ejecutada tras un evento de la usuaria y esta no tiene ni idea si en el campo de texto tiene que poner un número u otra cosa?
- ¿Tendría que hacer estas comprobaciones dentro de mi función o en el manejador del evento que es desde donde ejecutando mi función?
- ...

Según que respondas a esto deberemos hacer más o menos robusto nuestro código. Y según añadas más funcionalidad a tu código más código deberías testear.

\_\_\_\_\_\_\_\_\_\_

### Definiendo tests y test suites

Ya tenemos Jest funcionando. Ahora vamos a ver cómo lo usamos para escribir nuestros tests. En primer lugar, vamos a poner el ejemplo de un test sencillo:

```js
test('fizzbuzz returns 1 when the input is 1', () => {
  const number = 1; //Arrange

  const result = fizzbuzz(number); //Act

  expect(result).toBe(1); //Assert
});
```

En el ejemplo, usamos la función `test` (también puede usarse `it` que funciona igual) para definir un nuevo test, y les pasamos 2 parámetros

- Un string con la descripción del test.
- Una función con el contenido del test.

En esta función ejecutamos el código para realizar la prueba. Recordamos las partes: preparación, actuación y aserción. No siempre vamos a tener las 3 partes, por ejemplo, la de preparación no es obligatoria y a veces pueden mezclarse actuación y aserción en la misma línea. Preparación y actuación usan código JavaScript normal, pero en la aserción usamos otra función auxiliar de Jest `expect` que sirve para hacer la comprobación de nuestro test. A `expect` le pasamos el valor que queremos comprobar, en este caso el valor de la variable `result`. Después encadenamos un _matcher_, es decir, el tipo comprobación que queremos hacer sobre el resultado. En este caso usamos el matcher `toBe` y le pasamos un 1, es decir, que estamos comprobando que el valor de la variable `result` sea 1.

> NOTA: ¿Pero para esto no podemos usar un `if`? Pues en realidad estamos haciendo una comprobación como en un if, pero no queremos ejecutar código dependiendo de una condición (que es lo que nos permite `if`) sino indicar una condición para que el test sea correcto.

Cuando tenemos muchos tests normalmente vamos a querer agruparlos en los llamados _test suites_. Para definirlo, en Jest usamos la función `describe` a la que pasamos una descripción del suite y una función cuyo contenido son los tests.

```js
describe('Fizzbuzz', () => {
  test('returns 1 when the input is 1', () => {
    const number = 1; //Arrange

    const result = fizzbuzz(number); //Act

    expect(result).toBe(1); //Assert
  });

  test('returns 2 when the input is 2', () => {
    const number = 2; //Arrange

    const result = fizzbuzz(number); //Act

    expect(result).toBe(2); //Assert
  });
});
```

#### EJERCICIO 5

**Kata Padding**

A los ejercicios de programación que se usan para practicar testing muchas veces se les llama katas. Esta kata consiste en crear una función `paddingLeft` que se encarga de meter caracteres de relleno en un cadena por el lado izquierdo hasta llegar a un tamaño deseado. Toma 3 parámetros

- La cadena inicial
- Un tamaño final
- Un valor del padding, por defecto es un espacio

Si el tamaño final es menor o igual que la cadena inicial, se devuelve sin tocar la inicial.

Ejemplos:

- `paddingLeft('hola', 6, 'x')` devuelve `'xxhola'`
- `paddingLeft('hola', 6, 'a')` devuelve `'aahola'`
- `paddingLeft('ee', 4, 'aa')` devuelve `'aaee'`
- `paddingLeft('xxxx', 6, 'x')` devuelve `'xxxxxx'`
- `paddingLeft('', 6, 'x')` devuelve `'xxxxxx'`
- `paddingLeft('hola mi amigo', 6, 'x')` devuelve `'hola mi amigo'`
- `paddingLeft('xxxx', 0, 'x')` devuelve `'xxxx'`

En primer lugar, desarrollad el código de la función `paddingLeft` en un fichero. Cuando lo tengáis, cread un fichero de tests y cread un test para cada uno de los ejemplos anteriores. Así estamos comprobando que la función hace lo que se ha pedido que haga.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

**ES6 katas**

La web http://es6katas.org/ nos da una series de katas para repasar nuestros conocimientos de JavaScript, en concreto, de las novedades que trajo la versión ES6.

Para trabajar en una característica, hacemos clic en su nombre, por ejemplo, `string.includes()`. Esto nos lleva a una página donde tenemos un código de tests (editable) a la izquierda y el resultado de la ejecución de los tests a la derecha. Al comenzar todos los tests están en rojo, es decir, están fallando. El ejercicio consiste en modificar el código de la izquierda para ir arreglando los tests uno a uno, y que pasen a verde. Es muy importante ir leyendo la descripción de los tests porque nos dará pistas sobre qué característica de JS debemos usar para pasar el test. Para arreglar los tests podemos modificar el código excepto las líneas que tienen una sentecia `assert`. Esta función es equivalente al `expect` que hemos visto antes:

```js
expect(result).toBe(1);

//ES EQUIVALENTE

assert.equal(result, 1);
```

Vamos a ver por ejemplo el primer test de la sección de `string.includes()`:

```js
describe('`string.includes()` determines if a string can be found inside another one', function() {
  describe('finding a single character', function() {
    it('can be done (a character is also a string, in JS)', function() {
      const searchString = 'a';
      assert.equal('xyz'.includes(searchString), true);
    });
```

Leyendo la descripción del test nos explica qué hace includes. Para pasar el test sin modificar la línea del `assert` debemos modificar el valor de la variable `searchString` para que sea parte de la cadena `'xyz'`. Por ejemplo:

```js
const searchString = 'x';
```

Modificamos esa línea en la parte izquierda y le damos al botón 'Run tests' o las teclas Control + S. Se ejecurarán de nuevo los tests y el primero aparece pasado (en verde).

Debéis conseguir pasar el resto de tests de este fichero. Algunas katas que os recomendamos para repasar ES6 en el futuro: string, template strings, destructuring, rest operator, spread operator, arrow functions, array.find, block scope

\_\_\_\_\_\_\_\_\_\_

## BONUS: Introducción a TDD

TDD es una metodología de programación dentro de una metodología de trabajo denominada _eXtreme Programming_ o _XP_. XP define una serie de técnicas para mejorar los procesos de desarrollo de productos digitales, dentro de un marco de trabajo ágil. Algunas técnicas de XP son

- _pair programming_ o programación en parejas, que tiene toda una metodología de trabajo
- _code reviews_ o revisiones de código, antes de integrar un código es mejor que lo revisen programadoras que no lo han hecho
- integración continua, que consiste en integrar continuamente (diariamente) el código de todas las programadoras del proyecto
- despliegue continuo, que consiste en desplegar a producción continuamente nuevas versiones de nuestra aplicación
- _refactoring_, que pone de relieve la importancia de la calidad interna del código
- TDD o _Test Driven Development_, que es desarrollo dirigido por tests, es decir, que los tests son los que dirigen cómo programamos

Estas técnicas tienen dependencias entre ellas. Por ejemplo, no podré hacer despliegue continuo si no tengo integración continua de código antes. Y no podré tener integración continua (sin errores) si no tengo tests. También es mucho más difícil realizar refactorizaciones sin tener tests.

En esta sesión vamos a aprender TDD que consiste en **escribir los tests antes que el código**. Simplemente eso :) 🔥 (Acabo de oír cómo te explota la cabeza).

Al principio suena a locura el pensar que vamos a escribir algo que prueba un código sin tener ese código que queremos probar, pero si nos paramos a pensar un momento, siempre que empezamos a programar un código lo primero que necesitamos saber son los requisitos que debe tener ese código para que funcione correctamente. Pensemos en una función `isOdd` que comprueba si un número es impar o no. A menudo la reacción básica es ponernos a escribir el código, probar mil variaciones distintas y escribir, en muchas ocasiones, más código del que necesitamos. Pero lo lógico es empezar pensando qué queremos que haga esa función y, por tanto, cuáles son los requisitos o las reglas que debe pasar para que consideremos que funciona correctamente. En este caso sería:

- Si es un número par devuelve `true`
- Si es número impar devuelve `false`
- Si lo que me pasan no es un número devuelve un error

Estos son los requisitos, simples y claros. De haber empezado por el código estaríamos pensando en `if`s y `else`s en vez de definir qué es lo que queremos. Una vez hecho esto, el siguiente paso sería pasar esos requisitos a reglas, uno a uno, usando tests. Por tanto, la clave de TDD es que pensamos en qué queremos y cuáles son los criterios claros y tangibles para que eso funcione correctamente y, a partir de ahí, implementamos el código que cumplirá esas reglas.

### El ciclo de TDD

La metodología de TDD se basa en un proceso cíclico de 3 pasos:

1. Escribo un test definiendo qué tiene que hacer mi aplicación y lo veo fallar (se dice que el test _está en rojo_)
1. Escribo el código de producción para que ese test pase y lo veo pasar (se dice que el test _está en verde_)
1. Opcionalmente refactorizo el código de producción para mejorarlo, siempre que siga pasando todos los tests ¡claro!

En inglés el ciclo de TDD se suele describir brevemente como _Red - Green - Refactor_.

La mejor forma de aprender a usar esta metodología es, como casi todo en programación, practicándola. Hemos preparado algunos ejercicios para practicarlo juntos.

Algunas indicaciones a la hora de practicar TDD:

- Es importante destacar que un test falla cuando el test está bien escrito pero lo que está probando (una función, por ejemplo) no se está comportando tal y como se ha establecido en el test. Si el test falla porque hay un error de sintaxis en él o porque dice que una variable no está definida es que tenemos un error en el test y deberemos corregirlo antes de pasar a la siguiente fase
- empezamos siempre con el test más simple, y por el _happy path_, es decir, sin pensar en casos límite sino el comportamiento normal de nuestra aplicación
- tenemos que pensar siempre en pequeños pasos (en inglés se suele decir _baby steps_) centrándonos solo en lo siguiente que queremos que nuestra aplicación pueda hacer.
- suele ser complicado definir los primeros tests, así que tenemos que pensar qué queremos que haga nuestra aplicación de esta forma, que está relacionada con las 3 partes de un test unitario:

```
    Dado ESTO
    Cuando hago ESTO OTRO
    Espero que el resultado sea ESTE
```

#### EJERCICIO 7

**Kata Fizzbuzz**

Usando TDD, desarrollamos una función Fizzbuzz que toma como parámetro un número y devuelve

- "fizz" si es múltiplo de 3
- "buzz" si es múltiplo de 5
- "fizzbuzz" si es múltiplo de 3 y 5
- el mismo número si no se da ninguno de los casos anteriores

Este ejercicio es equivalente a la kata del ejercicio 3, pero vamos a hacerla usando la metodoogía de TDD, es decir, escribiendo los tests primero.

\_\_\_\_\_\_\_\_\_\_

## BONUS: ¿Y ahora qué? A refactorizar...

Como ya sabemos, _Refactorizar_ código consiste en modificar un código para mejorar su estructura pero sin añadir nuevas funcionalidades. En esta sección vamos a usarla íntegramente para practicar refactorización de código usando una _kata_.

Se pueden aprender muchas estrategias de cómo refactorizar y son temas avanzados, por ejemplo, usar _patrones de diseño de software_ para mejorar nuestro código. Además, se necesita experiencia para aprender a distinguir código bueno de código mejorable. Normalmente, cuando un código nos parece que puede mejorarse es que detectamos un _olor de código_ (en inglés _code smell_) que nos indica que algo no está hecho de la manera más simple y semántica. Algunos ejemplos de _code smells_ son

- duplicidad: si veo trozos de código que son casi iguales
- usar _números mágicos_ (_magic numbers_): que es usar números en nuestro código sin explicar lo que son (mejor definirlos en una variable para darles un nombre)
- funciones muy largas con muchos parámetros
- mal nombrado de variables y funciones

Esta parte de refactorización requeriría todo un curso en sí misma. Pero lo que sí queremos que entiendas es la importancia de tener tests para refactorizar, porque nos permiten cambiar cosas comprobando que nuestra aplicación sigue funcionando (no se rompe). Haremos un ejercicio específico para demostrar esta afirmación.

#### EJERCICIO BONUS 8

Para comprobar que se refactoriza mucho mejor con tests, os pasamos un ejercicio que ya tiene tests pero un código malísimo. Nuestro objetivo es mejorar el código que nos dan sin modificar el comportamiento (refactorizar) y que los tests sigan pasando. Se trata de la famosa [kata _Gilded Rose_ con JavaScript](https://github.com/gootyfer/gilded-rose-js-with-tests).

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

- [Jest](https://facebook.github.io/jest/)
- [Diseño ágil con TDD](http://www.carlosble.com/libro-tdd/?lang=es)
- [Extreme Programming en Wikipedia](https://en.wikipedia.org/wiki/Extreme_programming)
