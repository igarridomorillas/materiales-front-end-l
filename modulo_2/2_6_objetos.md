# Objetos

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)

<!-- /TOC -->

## Introducción

Los objetos son un tipo de dato en JavaScript, como lo son `number`, `string`, `boolean`, `undefined`... Los objetos son en cierta forma diferentes a estos porque permiten agrupar varios datos de forma estructurada. En esta sesión, veremos tanto los aspectos que los diferencian como aquellos que los asemejan.

En JavaScript los objetos conforman un grupo de datos compuestos por una _clave_ a la que va asociado un _valor_. En esta sesión vamos a ver los _objetos literales_ o _diccionarios_, por cómo se asocia la clave a su valor, pero normalmente los llamaremos simplemente _objetos_.

La idea de los objetos viene del mundo real. En nuestro mundo un objeto tiene una serie de características (_propiedades_) y puede realizar una serie de acciones (_métodos_). Si pensamos en algo tan sencillo como un lápiz podremos ver que algunas de sus propiedades podrían ser el color de la mina, nivel de afilado, cantidad de mina restante, etc. Por otro lado sus acciones serían muy reducidas y básicamente se resumiría en una, pintar.

Si trasladamos estos objetos a la web, el ejemplo más sencillo es el de un contador. Este contador tiene una serie de propiedades como pueden ser el valor inicial, el valor máximo permitido, el valor mínimo permitido y el valor actual. Por otro lado tiene también acciones, como aumentar la cuenta o reducirla. Los valores inicial, máximo, mínimo y actual serán _propiedades_ del objeto, y aumentar y reducir la cuenta serán acciones o _métodos_ (funciones).

Hasta aquí hay algo que no termina de cuadrar: ¿para que quiero que sean objetos? Es decir, a mí, como programadora ¿de qué me sirven? En programación interactuaremos con estos objetos, que no dejan de ser abstracciones de conjuntos de datos y acciones. Lo que haremos será, mediante código, decirle que cuando pulsemos un botón, por ejemplo, se ejecute el método para aumentar la cuenta y cambie así el valor actual del contador. Esto no es que cree un objeto y él trabaje por su cuenta sin que le digamos nada, todo el código (excepto el que nos brinda de serie JavaScript) lo creamos nosotros. La idea de utilizar esto es crear entidades o representaciones con las que es más fácil trabajar. Si vemos lo siguiente:

```
si se pulsa el botón, el contador aumenta
```

Es más claro que:

```
Si se pulsa el botón
Se comprueba si la cantidad actual más uno es menor que el valor máximo y si se puede aumentar
Si puede ser aumentado, se aumenta en 1 la variable cuenta actual
```

Además, otro de los beneficios de los objetos es que agrupa los datos por estructuras dejando claro que pertenecen a un mismo grupo. Igual, es más fácil trabajar con algo como:

```
- Contador
  - valor inicial
  - valor máximo
  - valor actual
  - valor mínimo
  - aumentar valor
  - disminuir valor
```

Que trabajar con:

```
Valor inicial del contador
Valor máximo del contador
Valor actual del contador
Valor mínimo del contador
Aumentar valor del contador
Disminuir valor del contador
```

De la primera forma agrupamos todo dentro del contador, así es más fácil ver la relación que tienen entre ellos los elementos y saber que van a tener sentido sólo dentro de éste.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Lo que vamos a ver en esta sesión es fundamental. Los objetos están presentes en todo momento en la web y toda ella se compone de objetos con los que interactuaremos en un futuro. Por ejemplo, la ventana (_window_) de la web es un objeto, la página (_document_) es un objeto, cada elemento HTML es un objeto. Estos tienen las mismas características que cualquier otro, tienen propiedades y métodos, y nos servirán para obtener información y ejecutar acciones sobre ellos.

Otro de los beneficios de entender los objetos es que aprenderemos a crear un código de mayor calidad ya que creamos abstracciones para que en vez de leer cien líneas de código leamos una y entendamos qué hace. Uno de los beneficios de los _métodos_ de los objetos es que nos permiten crear un código muy complejo con el que actuar sea algo sencillo. Por poner un símil, sería como un coche, el motor tiene miles de piezas y una complejidad que poca gente podría entender pero para interactuar con él es bastante sencillo. Giras la llave y arranca el motor, pisas el acelerador y el coche acelera, pisas el freno y frena y no hace falta entender toda la complejidad del motor. En los objetos es igual, la única diferencia es que en vez de interactuar con ellos de forma física, ejecutamos sus métodos y leemos y modificamos sus propiedades. A un contador le diremos que se aumente igual que con el coche le decimos que acelere, la interacción es diferente pero la base del concepto es la misma.

En JavaScript casi todo son objetos, si entendemos cómo funcionan y cómo trabajar con ellos tendremos una muy buena base para progresar rápidamente con este lenguaje.

## ¿En qué casos se utiliza?

Los objetos, de la forma en la que los vamos a ver en esta sesión se utilizan para estructurar cualquier tipo de dato y poder obtener información de él de forma sencilla y modificarlo también con la misma simplicidad:

- El contador que hemos comentado sería un ejemplo
- Un usuario podría ser perfectamente un buen ejemplo de un objeto. Este tendrá nombre, apellidos, edad, etc...
- Los datos para un mensaje también tendría sentido que fuesen un objeto: título, mensaje, imagen, mostrar mensaje, ocultar mensaje, etc.
- Un post de Facebook es un objeto en el que contiene título, imagen, likes, etc...

## Objetos literales

Los objetos son abstracciones inspiradas en el mundo real que permiten estructurar objetos ficticios en JavaScript de forma simple usando grupos de pares de clave/valor. Podemos crear _propiedades_, que representan las características, y _métodos_, que representan las acciones que podrán llevar a cabo esos objetos.

Usamos objetos en JavaScript para crear estructuras que agrupen datos y a las que se pueda acceder de forma sencilla sin necesidad de comprender la complejidad que albergan.

La sintaxis para crear un objeto es la siguiente:

- indicamos el nombre de la variable donde guardamos el objeto, por ejemplo, `adalaber`
- el contenido del objeto irá entre llaves `{ }`
- dentro de las llaves ponemos parejas `clave: valor`, donde la clave será el nombre de la propiedad y el valor puede ser de cualquier tipo de datos (cadena, número, booleano...), por ejemplo, `name: 'María'`
- separamos cada pareja `clave: valor` con una coma `,`

```js
const adalaber = {
  name: 'María',
  age: 31,
  isMarried: false
};
```

Como los objetos también son tipos de datos, una propiedad de un objeto podría ser también un objeto. Por ejemplo:

```js
const adalaber = {
  name: 'María',
  age: 31,
  isMarried: false,
  address: {
    street: 'Colegiata',
    number: 9
  }
};
```

Para acceder (leer) al valor de una propiedad de un objeto, podemos hacerlo de 2 formas:

- al nombre de la variable (el nombre del objeto) le ponemos detrás un punto `.` y luego el nombre de la propiedad
- al nombre de la variable (el nombre del objeto) le ponemos detrás unos corchetes `[ ]` y dentro el nombre de la propiedad como una cadena (entre comillas)

```js
// Muestra en la consola 'María'
console.log(adalaber.name);

// Muestra en la consola 'María'
console.log(adalaber['name']);
```

Ambas formas son equivalentes. La primera es más corta de escribir y es la que usaremos normalmente. Pero a veces necesitaremos usar la segunda, por ejemplo, si el nombre de la propiedad lo tenemos guardado en una constante.

```js
const nameKey = 'name';

// Muestra en la consola 'María'
console.log(adalaber[nameKey]);
```

Para actualizar el valor de una propiedad de un objeto, accedemos de una de las 2 formas anteriores y asignamos el valor como a una variable con `= nuevoValor`.

```js
adalaber.name = 'Lucía';

// Muestra en la consola 'Lucía'
console.log(adalaber.name);
```

### Creando objetos a partir de objetos vacíos

Otra forma de crear objetos equivalente a la anterior es crear primero un objeto vacío y luego ir añadiendo las propiedades en las siguientes instrucciones. Vamos a ver un ejemplo:

```js
const adalaber = {};
adalaber.name = 'María';
adalaber.age = 31;
adalaber.isMarried = false;

// Muestra en la consola 31
console.log(adalaber.age);
```

#### EJERCICIO 1

**Bio de Adalabers**

Crea un nuevo objeto en JavaScript `adalaber1` que nos sirva para representar (modelar) a una Adalaber. Tenemos estos datos:

- Susana, 34 años, periodista

Luego muestra en la web una frase como esta, accediendo a los datos del objeto:

'Mi nombre es Susana, tengo 34 años y soy periodista'

Ahora hacemos lo mismo (crear el objeto `adalaber2` y mostrar una frase descriptiva) con una nueva Adalaber con estos datos:

- Rocío, 25 años, actriz

\_\_\_\_\_\_\_\_\_\_

### Métodos

Los métodos son funciones asociadas a la propiedad de un objeto. Estas funciones suelen definirse como `arrow functions` o funciones anónimas. Para ejecutar un método, accedemos a él como a una propiedad y le pasamos los argumentos entre paréntesis `( )`. Ejemplo:

```js
const adalaber = {};
adalaber.name = 'María';
adalaber.speak = phrase => `Yo digo: ${phrase}`;

// Muestra en la consola 'Yo digo: Hola'
console.log(adalaber.speak('Hola'));
```

> NOTA: Por convención, los métodos suelen tener como nombre un verbo (`show`, `hide`, `reset`, etc.) y las características (propiedades) suelen tener un sustantivo (`color`, `size`, `type`, `content`, `text`, etc).

#### EJERCICIO 2

**A la carrera**

Partiendo del objeto `adalaber1` del ejercicio anterior, añade un método (una función) `run` que muestre en la consola (lo llamamos _loguear_) la frase 'Estoy corriendo'.

Ahora, vamos a añadir un nuevo método `runAMarathon` que toma un parámetro `distance` que es un número. Al ejecutarlo, debe mostrarse en la consola el texto 'Estoy corriendo un maratón de 50 kilómetros' siendo 50 el valor del argumento `distance` que le hemos pasado.

\_\_\_\_\_\_\_\_\_\_

### Breve introducción a `this`

Desde un método de un objeto podemos acceder al resto de propiedades de ese objeto usando la palabra `this` antes del nombre de la propiedad. Vamos a ver un ejemplo:

```js
const adalaber = {};
adalaber.name = 'María';
adalaber.sayHello = function() {
  return 'Hola, me llamo ' + this.name;
};

// Muestra en la consola 'Hola, me llamo María'
console.log(adalaber.sayHello());
```

> NOTA: una cosa importante que debemos saber es que si queremos usar `this` en un método de un objeto tenemos que usar una función anónima y no una arrow function. Dicho de otro modo, tenemos que escribir la palabra `function` y no `=>`.

> NOTA: El concepto de `this` en JavaScript es mucho más complejo de lo que hemos aprendido aquí. Por el momento con lo que hemos visto nos sirve para empezar a trabajar con él, pero sabiendo que alberga muchas más posibilidades.

#### EJERCICIO 3

**Bio de Adalabers 2**

Partiendo del objeto `adalaber1` del ejercicio anterior, añade un método (una función) `showBio` que muestra en la consola la frase 'Mi nombre es María, tengo 34 años y soy periodista', usando el nombre, edad y estudios que están almacenados en el objeto.

Hacemos lo mismo para `adalaber2` definida en el ejercicio 1. ¿Hemos tenido que modificar mucho el método `showBio`? ¿Ves alguna ventaja respecto a cómo hacíamos lo mismo en el ejercicio 1?

> **Nota**: para que el ejercicio funcione bien debéis usar funciones normales, no _arrow funtions_. En siguientes sesiones veremos por qué cambia el `this` al usar _arrow funtions_.

\_\_\_\_\_\_\_\_\_\_

### Objetos del navegador

Hay varios objetos que crea el navegador y pone a nuestro servicio para facilitarnos la vida.
En realidad hemos estado trabajando con ellos desde el primer día.

Por ejemplo,

- el objeto [`console`](https://developer.mozilla.org/en-US/docs/Web/API/Console) cuyos métodos nos permiten interactuar con la consola del navegador
- el objeto `document` que representa la página y nos permite interactuar con su contenido a través de sus métodos y propiedades.

## event

En la sesión anterior vimos el parámetro `event` del `handler` de un `listener`. Ahora ya sabemos que es un objeto que tiene propiedades como `currentTarget` y métodos como `preventDefault`.

#### EJERCICIO 4

**Investigando event**

Tenemos que preparar un botón con un `listener` para _loguear_ el objeto `event` en la consola.
Investigar si la clave `type` que encontramos en él es una propiedad o un método.

> **Nota**: cuando _logueamos_ un objeto en la consola, a su izquierda aparece un triangulo que nos permite _desplegarlo_ para ver sus métodos y propiedades.

\_\_\_\_\_\_\_\_\_\_

### Elementos de HTML

Un elemento de HTML es un objeto que representa una etiqueta de HTML y nos permite interaccionar con ella.

```js
const titleElement = document.querySelector('#mainTitle');
```

En anteriores lecciones hemos estado usando varios de sus métodos y propiedades como:

```js
titleElement.innerHTML;
titleElement.value;
titleElement.querySelector('.icon-star');
titleElement.classList;
titleElement.classList.contains('.icon-star');
```

#### EJERCICIO 5

**Investigando los elementos**

Vamos a preparar un input de tipo texto, a recogerlo desde JavaScript y a imprimirlo en la consola con `console.dir` para investigarlo y comentar con la compañera estas propiedades:

- value
- nodeName
- required

> **Nota** Cuando _imprimimos_ un elemento en la consola con `console.log` vemos la etiqueta de HTML y podemos _desplegarla_ para ver su contenido. Si queremos ver el objeto con sus propiedades y métodos tendremos que usar `console.dir`.

\_\_\_\_\_\_\_\_\_\_

## null

`null` es un tipo de dato en JavaScript que representa un objeto nulo. Normalmente se utiliza de forma intencionada, para indicar que esa variable debería contener un objeto (siendo posible que se rellene más tarde, por ejemplo con los datos que nos envíe el servidor, o con los datos de un formulario).

```js
let userData = null;
```

Con esto ya habríamos visto la mayoría de tipos de datos en JavaScript. Vamos a recordarlos:

Primitivos:

- Boolean
- Null
- Undefined
- Number
- String
- Symbol (el único que no veremos, llegó con ES6)

No primitivos:

- Object

### BONUS: Los objetos son un tipo de datos especial

Cuando asignamos un objeto a una variable, realmente no estamos guardando su valor en la caja de la variable, como sucede con los números o los strings. En este caso lo que sucede es que se crea un objeto y en la variable guardamos _una referencia o un enlace a ese objeto_. Por lo tanto, si guardamos esa variable en otra variable lo que estaremos haciendo es crear un nuevo enlace que apunta al mismo objeto. Vamos a entenderlo mucho mejor con un ejemplo:

```js
const adalaber = {
  name: 'Rosa'
};
adalaber.name; // Rosa

// Creamos una nueva variable que apunta al mismo objeto
const adalaber2 = adalaber;
adalaber2.name; // Rosa

// Cambiamos la propiedad `name`
adalaber.name = 'Rocío';

// Al acceder al objeto el nombre es el nuevo
adalaber.name; //Rocío
// Pero también a través de la otra variable 😱
adalaber2.name; //Rocío
```

### BONUS: Usando otros tipos de datos como objetos

Los `strings` y los números también tienen propiedades y métodos, como los objetos, pero tienen sus diferencias.

En el caso de las cadenas podemos acceder a algunas propiedades y métodos:

- `length` es una propiedad que representa la longitud de la cadena
- `toLowerCase` es un método que pasa la cadena a minúscula
- `trim` es un método que elimina espacios al principio y final de la cadena

Puedes consultar el [listado completo de propiedades y métodos de las cadenas en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/String).

En el caso de los números necesitamos crearlos de una forma especial `Number(4)` para poder acceder a sus métodos:

- `toFixed` es un método que devuelve el número como una cadena con un número fijo de decimales

Puedes consultar el [listado completo de propiedades y métodos de los números en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Number).

#### EJERCICIO 6

**Crear una cesta de peras**

Vamos a crear un objeto que sea una cesta de peras y que debe tener varias propiedades:

- Número máximo de peras
- Número mínimo de peras
- Número actual de peras
- Número inicial de peras

Y varios métodos que hagan:

- Añadir al cesto una pera
- Sacar del cesto una pera
- Restablecer el número de peras al valor inicial.

Con la ayuda de `console.log` probaremos a usar varios métodos distintos y comprobar el número actual de peras para ver si funciona correctamente.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 7

**Estructura de datos para un usuario**

Vamos a crear un objeto para almacenar la información de un usuario y una constante llamada `job` donde guardaremos el valor `'developer'`. A continuación seguiremos los siguiente pasos:

Usando la notación con punto o la notación con corchetes (`[]`) (ej: `obj.prop` o `obj["prop"]`):

1. Añadiremos una propiedad llamada `firstName` y le asignaremos un valor.
2. Añadiremos una propiedad llamada `lastName` y le asignaremos un valor.
3. Añadiremos una propiedad llamada `age` y le asignaremos un valor numérico.
4. Añadiremos una propiedad `job` a la que asignaremos el valor de la constante `job`
5. Comprobaremos que al obtener el valor de cada una de las propiedades que hemos definido hasta ahora, este es correcto
6. Cambiaremos el nombre del usuario por otro distinto
7. Aumentaremos en 1 la edad del usuario
8. Comprobaremos de nuevo que todo sigue funcionando correctamente

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

### Ada Lovelace en Youtube

En este curso veremos tanto una introducción breve a los objetos como la sintaxis básica para trabajar con ellos. La idea es aprender métodos, propiedades y entender qué es un objeto en sí y por qué son tan útiles.

- [Introducción a los objetos en Javascript](https://www.youtube.com/watch?v=ycfoaxNhYbk&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=27)
- [Definición de objetos](https://www.youtube.com/watch?v=xDqTEsiNgBw&index=28&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o)
- [Propiedades](https://www.youtube.com/watch?v=jj9em_PDBH8&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=30)
- [Métodos](https://www.youtube.com/watch?v=BZE85nUjLHA&index=31&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o)
