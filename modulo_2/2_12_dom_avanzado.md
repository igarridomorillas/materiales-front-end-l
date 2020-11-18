# DOM avanzado

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

Siempre que queramos interactuar desde JavaScript con nuestras páginas vamos a necesitar saber cómo consultar/modificar los elementos que las componen. Hasta ahora hemos visto muy en la superficie cómo hacerlo pero ya vamos necesitando tener más opciones. Intentaremos también entender mejor un concepto que ya hemos estado manejando: el DOM.

### ¿Para qué sirve lo que vamos a ver en esta sesión?

Lo que vamos a ver en esta sesión cobra especial importancia en tres campos: rendimiento de una página web, prevención de posibles errores y mantenimiento y simplicidad del código.

### Mejorar el rendimiento

En cuanto a rendimiento, hasta ahora cuando utilizábamos `innerHTML` lo que hacía JavaScript, a grandes rasgos, era lo siguiente:

1. Leer el texto y parsearlo (convertirlo a HTML, como hemos visto con `JSON.parse`)
2. Crear cada uno de los elementos HTML en el momento
3. Añadir esos elementos como contenido a un elemento del DOM (un `p`, un `div` lo que fuese)

Con lo que vamos a ver en esta sesión el primer paso de parsear el texto no será necesario porque no utilizaremos texto para crear componentes sino JavaScript, lo cual reducirá drásticamente el tiempo que tarda en ejecutarse el código y, por tanto, mejorará el rendimiento de nuestra aplicación. Esto en pequeñas apps no va a ser fundamental pero en aplicaciones más grandes y complejas que requieren de pintar muchos elementos es clave para que no se note un retardo a medida que utilizamos las webs.

Además en esta sesión veremos cómo crear elementos por un lado y posteriormente añadirlos al DOM, es decir, con `innerHTML` se creaban (se convertía el texto en componentes HTML) y se añadían en el momento. Con lo que vamos a ver en esta sesión seremos capaces de crearlos antes y simplemente añadirlos, con lo cual en el momento de añadirlos solo se realizará un paso, porque tendremos creados previamente los componentes. Para ejemplificar esto, imaginemos que tenemos un código JavaScript que al pulsar en un botón añade tres párrafos a la página, si lo hago con `innerHTML`, en el momento que pulso el botón se convierte el texto de `innerHTML` en tres párrafos y se añaden. Si por el contrario lo hacemos con la alternativa que planteamos en esta sesión, podremos crear los párrafos en el momento en el que se empieza a ejecutar JavaScript y cuando el usuario pulse el botón lo único que se hará será añadir esos elementos ya creados previamente.

### Prevención de posibles errores

Cuando cambiamos el contenido de un elemento con `innerHTML`, ya sea añadiendo (`+=`) o reasignando (`=`) lo que estamos haciendo es obligar al navegador a crear de nuevo todos los *items* contenidos dentro del elemento modificado, es decir, el navegador creará todos los hijos de ese elemento de nuevo.

Esto puede derivar en un mal funcionamiento de nuestra página, porque sucederán cosas como las siguientes:

* Los eventos asignados a alguno de los elementos que había en el contenido se perderán y si, por ejemplo, tenemos un botón al que le hemos añadido un evento *click*, ese evento dejará de funcionar
* Si teníamos guardada en una variable de JavaScript la referencia a uno de los elementos (usando algo como `const btn = document.querySelector('.btn')`, por ejemplo) esa variable ya no será válida porque el elemento al que hace referencia ya no será el que se está mostrando en la pantalla.

Imagina la repercusión de este problema en aplicaciones complejas que tienen que estar repintando varias partes de su código varias veces, se puede montar un cristo bastante bueno e `innerHTML` nos puede perjudicar bastante en este caso frente a las alternativas que propondremos a continuación.

### Mantenimiento y simplicidad del código

Utilizar HTML como strings en JavaScript puede ser bastante molesto, se nos puede olvidar un más en alguna concatenación, tenemos que poner todo en una línea o usar `+` o escapar saltos de línea (usando `\` antes del salto) para poder poner el código en varios renglones, no se puede indentar... Esto lo podemos solucionar hoy en día con las __template strings__ de ES6.

Todo esto hace que cuando empiezan a crecer nuestros strings con código HTML sea bastante engorroso y además complica el beneficiarnos de funciones para crear elementos. Si por el contrario utilizamos JavaScript para realizar esa misma tarea podremos beneficiarnos de indentación y separación en líneas, simplicidad a la hora de crear un elemento y reutilización de código mediante funciones, lo cual hará que nuestro código sea más fácil de mantener y más sencillo de entender.

Aparte de esto existen otras mejoras en temas de seguridad y otros aspectos avanzados que hacen que `innerHTML` no sea el candidato indicado en proyectos de gran envergadura o mayor exigencia en cuanto a rendimiento y seguridad.

Y ahora estarás pensando «¿y por qué entonces he aprendido `innerHTML`?» Gracias a haber trabajado con `innerHTML` ahora estás preparada para seguir avanzando y profundizar un poquito más en formas avanzadas de trabajar con el DOM, que son las que veremos hoy.

## ¿En qué casos se utiliza?

Lo que vamos a ver hoy te servirá para generar un código más adecuado para proyectos más exigentes, como podría ser una librería de JavaScript, el código de una aplicación compleja o proyectos en los que necesites tener más posibilidades aparte de modificar el contenido de un elemento por completo (añadir algo antes o después, eliminarlo, seleccionar un elemento madre o hija, etc.)

`innerHTML` nos seguirá sirviendo en el futuro para hacer código sencillo que podamos desarrollar de forma rápida y hacer pequeñas pruebas y prototipos. Además, hasta ahora nos ha permitido poder trabajar con el DOM en JavaScript de forma sencilla y hacer menos dura la manipulación del contenido de nuestra página.

## Pero, ¿qué es el DOM?

En el momento en el que el navegador carga la página lo primero que hace es leer el contenido del archivo HTML (con su correspondiente CSS y JavaScript), lo procesa y genera un esquema virtual representando los elementos de nuestra página como si fuese un árbol de objetos (con sus propiedades y métodos). Cada uno de estos objetos será un nodo de ese esquema, una pequeña parte de la red que conecta con el resto de elementos (madres e hijas).

![Paso de HTML al DOM](assets/images/2_7html_to_dom.png)

Por simplificarlo un poco, sería como si el navegador fuese una persona y leyese el HTML y en su cabeza esbozase una idea de cómo es la estructura que forma el código HTML con las determinadas relaciones: este elemento es hijo de este otro y contiene otros dos elementos y así con toda la página. Esa estructura que tiene en su mente sería el DOM, la representación abstracta de la estructura de nuestra página web. Las siglas de DOM vienen de *document object model*, que en español sería Modelo de Objetos del Documento, un modelo que representa como objetos los distintos elementos de un documento, una página web. Ese DOM lo genera el navegador pero no se muestra en ningún sitio, simplemente le servirá a este para estructurar nuestro contenido, ser capaz de pintar lo que vemos en la ventana y brindarnos la oportunidad de poder obtener información de este y poder modificarlo.

Entonces, ¿el DOM sería una representación de mi HTML? No realmente, en gran parte su contenido se generará a partir del HTML pero el DOM también poseerá las modificaciones que hagamos desde nuestro código de JavaScript y la información generada a partir de CSS. Por lo tanto podríamos decir que el DOM generará su contenido a partir de HTML, CSS y JavaScript pero además ofrecerá una serie de propiedades, métodos y eventos disponibles para modificar y crear páginas web organizadas en objetos.

Una representación visual del DOM (que no el DOM en sí) sería el código que aparece a la hora de abrir nuestro inspector. En este caso el DOM está representado con la sintaxis de HTML y es muy similar a nuestro código HTML pero no son lo mismo. Para demostrar esto no hace falta más que escribir en nuestro HTML algunas etiquetas sin cerrar o mal colocadas, si hacemos esto veremos que, aunque en nuestro HTML estén sin cerrar o mal, en la representación del DOM se verá todo correcto, porque este se ha sido procesado por el navegador.

![Inspector](assets/images/2_7_inspector.png)

Bien, te estarás preguntando ¿y para qué quiero saber yo todo esto?. Pues bien, entender esto nos permitirá entender, en primer lugar, cómo procesa nuestro código un navegador web y en segundo, entenderemos mejor qué es eso de los objetos y para qué sirve realmente y cómo trabajar de forma correcta con los elementos de nuestra página.

## Cómo hemos manipulado el DOM hasta ahora

Hasta ahora hemos hecho una pequeña aproximación y sabemos trabajar con clases con la propiedad `classList` y sus métodos:
* `.add()` para añadir clases a un elemento
* `.contains()` para comprobar si un elemento tiene cierta clase
* `.remove()` para eliminar clases de un elemento
* `.toggle()` para poner/quitar una clase en caso de que no la tenga (o sí)

Además sabemos cómo seleccionar elementos HTML:
* Por su `id`, con `document.getElementById()`
* Con los selectores de CSS:
	- El primer elemento que cumple el selector con `document.querySelector()`
	- Todos los elementos que cumplan el selector `document.querySelectorAll()`

Y cómo modificar el DOM con:
* `innerHTML` para consultar/modificar el contenido HTML de un elemento

Por último, también sabemos trabajar con atributos:
* Modificando la propiedad del elemento que lleva el mismo nombre (`href`, `src`, `value`...)

## Nuevas formas de seleccionar, crear, añadir y borrar elementos

Partimos de este punto y vamos a ver qué más opciones tenemos para ampliar nuestro repertorio de herramientas.

Vamos a partir de un pequeño HTML para los siguientes ejemplos:

```html
<div id="container" class="container">
  <ul class="items">
    <li class="item item--1">Item 1</li>
    <li class="item item--2">Item 2</li>
    <li class="item item--3">Item 3</li>
  </ul>
</div>
```


### `.parentElement`
A veces nos interesará seleccionar un elemento e ir directamente a por su contenedor madre:

```js
const item1 = document.querySelector('.item--1');
console.log(item1); // Devuelve una representación del elemento como HTML
console.dir(item1); // Devuelve una representación del elemento como objeto

const mother = item1.parentElement;

console.log(`La madre de nuestro elemento es un <${mother.nodeName.toLowerCase()}> y tiene la clase .${mother.className}`);
// Devuelve "La madre de nuestro elemento es un <ul> y tiene la clase .items"
```

[Ejemplo en Codepen](https://codepen.io/adalab/pen/QaQObq)

### Crear elementos

Hasta ahora insertábamos HTML creando una cadena de texto (a las bravas o a las bravas usando un `for`) e inyectándolo con innerHTML.
Otra opción que tenemos es crear un elemento con `.createElement()` y añadirle contenido con `.createTextNode()`, vamos a verlo:

```js
// Creamos un elemento nuevo, un <li>
const newItem = document.createElement('li');
console.log(newItem); // Devuelve "<li></li>"

// Ahora creamos algo de contenido
const newContent = document.createTextNode('Item nuevo');

// Y se lo añadimos a nuestro <li>
newItem.appendChild(newContent);
console.log(newItem); // Devuelve "<li>Item nuevo</li>"
```
[Ejemplo en Codepen](https://codepen.io/adalab/pen/MrQOrz)

Con estos métodos conseguimos un elemento HTML pero todavía tenemos que añadirlo a nuestro DOM para poder verlo.

### Añadir elementos al DOM

Mientras que con `.innerHTML` podríamos inyectar una cadena de texto como HTML a nuestro DOM ahora veremos cómo añadir elementos como el que hemos creado hace un momento.

`.appendChild()` nos permite añadir elementos a nuestra web, siguiendo el ejemplo de esta sesión vamos a añadir el `<li>` que acabamos de crear:
```js
const newItem = document.createElement('li');
const newContent = document.createTextNode('Item nuevo');
newItem.appendChild(newContent);

const items = document.querySelector('.items');
items.appendChild(newItem);
```
[Ejemplo en Codepen](https://codepen.io/adalab/pen/mpXqow)

#### EJERCICIO 1

**1, 2, 3, lo hacemos otra vez**

Crear una página HTML con una lista `ul` vacía. Vamos a partir de un array con 3 elementos `const numbers = [1, 2, 3]`. Vamos a añadir a la lista tres elementos `li`, que corresponden al contenido del array. Usaremos los métodos avanzados para manipular el DOM, no `innerHTML`.

\_\_\_\_\_\_\_\_\_\_

### Borrar elementos del DOM

Vamos a utilizar en este caso el método `remove()` (eliminar en español) que como su nombre indica eliminará el elemento y lo hará desaparecer del DOM y por tanto también de la página:

```js
const items = document.querySelector('.items');
items.remove();
```

De nuevo, tras ejecutar el método la vista se actualiza y en este caso, la imagen desaparece, por lo que comprobamos que con los métodos también se produce esa actualización.


Sabemos cómo borrar un elemento, pero ¿y si queremos borrar una de las hijas de nuestro contenedor? Tenemos `.removeChild()` para ello:
```js
const itemList = document.querySelector('.items');
const item2 = itemList.querySelector('.item--2');
itemList.removeChild(item2);
// Elimina el elemento con clase .item--2 que es descendiente de .items
```
[Ejemplo en Codepen](https://codepen.io/adalab/pen/MrQrwM)

### Obtener información sobre los atributos de un elemento y modificarlos

Vamos a ver cómo trabajar con los atributos de un elemento HTML. Esto nos permitirá hacer muchas cosas útiles como cambiar la ruta de una imagen para que se vea una imagen u otra, comprobar el valor de un input para añadirlo, por ejemplo, en nuestro currículum, etc.

Para los siguientes atributos, si queremos obtener un valor o modificarlo, utilizaremos el nombre de la propiedad:

- `src`
- `value`
- `type`
- `style`
- `href`

Por ejemplo para obtener el valor actual de un `input` usaremos:

```js
// Si tenemos <input type="text" name="firstname" id="firstname" value="Ada">
const nameInput = document.querySelector('#firstname');

console.log(nameInput.value); // Pintará el valor actual, 'Ada'
nameInput.value = 'Joan'; // Rellenará el input con el valor 'Joan'

/*
Para poner un estilo, lo asignaremos usando la siguiente notación
style.propiedadCSS = 'valor'

De esta forma no modificaremos los estilos previamente asignados

Si la propiedad CSS tiene un guión (background-color) lo convertiremos a camelcase
backgroundColor
*/
nameInput.style.backgroundColor = 'red';


/*
Si queremos poner varios estilos a la vez o sobreescribir los anteriores,
usaremos esta notación
*/
nameInput.style = 'color: red; color: blue;';
```

En el caso de que la propiedad no esté en la lista anterior, deberemos usar `getAttribute`.

```js
// Si tenemos <label class="firstname-label" for="firstname"></label>
const label = document.querySelector('.firstname-label');
label.getAttribute('for'); // devolverá firstname
```

Para añadir un elemento que no está en la lista que hemos mencionado anteriormente, usaremos `setAttribute`.

```js
// Si tenemos <label class="firstname-label"></label>
const label = document.querySelector('.firstname-label');
label.setAttribute('for', 'firstname'); // asignará for="firstname" al label
```

#### EJERCICIO 2

**De viaje**

Crea una página que contenga tres imágenes, usando un select de formulario pregúntale a la usuaria qué ciudad quiere visitar.

- Si la usuaria elige Madrid, haz que en cada imagen se muestre una foto de Madrid
- Haz lo mismo para París y Nueva York

> **Nota**: Usa imágenes que encuentres por Internet.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

**Autocompletado**

Vamos a crear nuestro propio autocompletado de formularios. Para ello vamos a crear un formulario con tres campos:

- Nombre
- Apellidos
- Teléfono

Por otro lado, en JavaScript tendremos un array de 3 objetos con esa estructura. Es decir, un listado 3 objetos, cada uno con nombre apellidos y teléfono. Pediremos a la usuaria que elija uno de esos 3 con un `select` con el nombre. Al seleccionarlo se rellenará el formulario automáticamente.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

**Párrafos de altura**

Vamos a crear un div en HTML que contenga tres párrafos con un texto aleatorio. Con la ayuda de JavaScript vamos a obtener su tamaño usando la propiedad [`offsetHeight`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight). Posteriormente y usando el atributo HTML [style](https://www.w3schools.com/Tags/att_global_style.asp) vamos a configurar que su altura será un tercio de la actual.

\_\_\_\_\_\_\_\_\_\_

## Atributos `data-*`

En algunas ocasiones nos puede ser útil almacenar algún tipo de información (datos) asociada a un elemento HTML. Por ejemplo, para referenciar al elemento HTML donde queremos hacer scroll. O cuando tenemos 2 elementos relacionados, y al interactuar sobre uno queremos un efecto sobre el otro. Por ejemplo, cuando un `select` cambia de valor queremos que un párrafo se modifique.


Para ello, simplemente definimos un nuevo atributo en el elemento que comienza con `data-` seguido del nombre que queremos darle a esos datos, por ejemplo, `data-id`. Para crearlos en HTML, los cremos como un atributo más del elemento, por ejemplo, `<a href="#" data-id="title1">`. Para acceder a ellos desde JavaScript usamos los métodos `getAttribute` y `setAttribute` que ya conocemos.

Como alternativa, podemos acceder también mediante `dataset`. Esta propiedad de los elementos contiene un objeto cuyas claves coinciden con el nombre que le hemos dado a los datos (sin `data-`).

Así que podriamos acceder al valor guardado en `data-id` con `myLink.dataset['id']` o con `myLink.dataset.id`.

#### EJERCICIO 5

**Anclas de verdad**

Vamos a partir del ejercicio 11 de la sesión 2.5, donde aprendimos a eliminar el comportamiento por defecto del enlace. En este ejercicio vamos a terminar lo que empezamos, y podremos hacer *scroll* hasta cada sección usando enlaces desde JS.

Para ello seguimos estos pasos:

1. Ponemos un atributo `data-id` a los enlaces para indicar a qué elemento debemos hacer *scroll*.
1. Al hacer *click*, eliminamos el comportamiento por defecto.
1. Con [getBoundingClientRect](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect) buscamos la posición del elemento en la página.
1. Usando [window.scrollTo](https://developer.mozilla.org/en-US/docs/Web/API/Window/scrollTo) hacemos scroll hasta el elemento pero restando alguno píxeles para que la cabecera fija no lo tape.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

**Castigo**

La hemos fastidiado. Otra vez. Y el profe nos ha castigado, ¡y encima sin tener la razón! Nos ha pedido que escribamos 100 veces en la pizarra una frase. ¿Podremos hacer un poco de trampa para que nos ayude JavaScript? Vamos a crear todos los elementos HTML como hemos aprendido en esta sesión, es decir, sin `innerHTML` ;)

1. Repítelo 100 veces

	¡Es hora de actuar! En la pizarra (nuestra página web) tenemos que escribir 100 veces la frase "He aprendido bien cómo funcionan los bucles". Cada frase en una línea diferente. ¿Podremos conseguirlo? Primero dale a la web aspecto de pizarra: el fondo de negro, las letras en blanco, tipografía que simula el pintado con tiza tipo [*chalkboard*](http://www.fontspace.com/category/chalkboard), etc. Y luego, ¡a escribir!

2. Un combo por frase

	¡Seguimos con nuestra pizarra! Ahora vamos a añadir un combo (elemento `select` de HTML) al final de cada línea de texto. En el combo podremos seleccionar un color de los siguientes: blanco, azul, rojo, verde, amarillo, rosa. Por defecto, el combo tendrá seleccionado el color blanco que es el color del texto de los párrafos.

3. Vamos a darle color

	Ahora viene lo bueno: vamos a añadir el comportamiento a la web para que al modificar un combo se cambie el color del texto de esa línea al color indicado en el combo. Por ejemplo, si modificamos el color del combo de la línea 3 a rosa, el texto de la línea 3 se convierte en rosa.

	Algunas pistas para esta tercera parte:

	- primero haced funcionar un combo para una única línea
	- investigad cómo funciona el evento `change` de los elementos tipo `select` ([documetación de MDN](https://developer.mozilla.org/en-US/docs/Web/Events/change))
	- desde el objeto `event` de la función de callback, podemos acceder al `select` que ha provocado el evento mediante `event.currentTarget`; incluso al índice (como en un array) de la opción seleccionada con `event.currentTarget.selectedIndex`

**¡A por ello!**

\_\_\_\_\_\_\_\_\_\_

## Resumen de la sesión

El objetivo de la sesión es tener un abanico más amplio de opciones a la hora de manipular el DOM y potenciar la consulta de recursos como la MDN.

