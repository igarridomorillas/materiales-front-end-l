# Programación orientada a objetos

<!-- TOC START min:4 max:4 link:true update:true -->
- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)

<!-- TOC END -->


## Introducción

En esta sesión vamos a profundizar en algunos conceptos avanzados de JavaScript. En primer lugar exploraremos el contexto de las funciones y qué representa `this` que ya hemos visto en alguna ocasión. También veremos cómo se trabaja con objetos en JavaScript, cómo crearlos y definir prototipos para tener datos y comportamientos compartidos entre varios objetos.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

En una aplicación web sencilla como las que hemos hecho hasta ahora, tenemos variables y funciones en el ámbito global y se trabaja sin ningún problema. Pero cuando el código empieza a crecer, hacer algún cambio puede convertirse en algo inmanejable (por ejemplo, ¿dónde estaba la función de callback de este botón?). Para estructurar mejor nuestro código JS tenemos la posibilidad de trabajar con objetos. Los objetos al final son abstracciones de objetos del mundo real, que tienen
- **atributos**, que son datos del cualquier tipo: cadenas, números, arrays, booleanos, objetos, etc.
- **métodos**, que establecen comportamientos y son funciones

Por ejemplo, si en nuestra web tenemos un carrito de la compra con varios artículos, podemos crear
- un objeto artículo `Article` que tenga como atributos el nombre, descripción, precio y y métodos para mostrarlo en pantalla de varias formas
- un objeto carrito `ShoppingCart` que tenga como atributo un listado de artículos, y métodos para añadir/eliminar artículos, calcular el precio total, etc.

## ¿En qué casos se utiliza?

Como ya hemos adelantado, cuando trabajamos con una base de código grande y compleja, los objetos nos ayudan a estructurar nuestro código. Por tanto, en grandes empresas y grandes proyectos se utilizan objetos. También en la mayoría de librerías JavaScript que usamos el código está estructurado en un objeto, el cual creamos al comienzo y vamos ejecutando sus métodos para ayudarnos en nuestras tareas.

## Tipos de objetos

En JavaScript podemos trabajar con 2 tipos de objetos: los objetos literales y los objetos "normales".

### Objetos literales

Los **objetos literales**, que definimos con `{}`, donde podemos definir datos como `name` y comportamiento como `jump`

```js
var person = {
  name: 'María',
  jump: function(){
    console.log('Jump');
  }
};

console.log(person.name); //María
```

Los objetos literales son muy útiles para transmitir información, de hecho, el formato JSON está basado en este tipo de objetos. Tienen la ventaja de ser muy simples, pero si queremos tener varios objetos similares tenemos que crear uno a uno a mano.

### Objetos "normales"

El otro tipo de **objetos**, los "normales", son objetos que creamos a partir de una función *constructora* usando `new`, por ejemplo, cuando hacemos `new XMLHttpRequest()`. Estas funciones se escriben por convención con la primera letra en mayúscula. A la función constructora le pasamos unos parámetros que estarán relacionados con los atributos del objeto. Esta función constructora tendremos que ejecutarla con `new` delante y pasarle los parámetros que queremos del objeto. Sólo declarar la función sin ejecutarla, como ya sabemos, no hace nada. Vamos a ver un ejemplo y lo explicamos después:

```js
function Person(name) {
  this.name = name;
};

var maria = new Person('María');
console.log(maria.name); //María

var carmen = new Person('Carmen');
console.log(carmen.name); //Carmen
```

En este ejemplo definimos un nuevo tipo de objeto `Person` que es nuestra función constructora. Toma como parámetro `name` que es el nombre de la persona, es decir, los datos que nos interesa almacenar sobre la persona. Luego con `this.name` declaramos un atributo de este tipo de objeto con el nombre name. Es similar a declarar una variable `var` pero que sólo tiene sentido dentro de `Person`. A este atributo le asignamos el valor que nos llega por parámetros (el `name` a la derecha del `=`).

Una vez definida la función constructora, vamos a crear un nuevo objeto de tipo `Person` poniendo el `new` delante y ejecutando la función constructura pasándoles como argumento el nombre de la persona, "María". Podemos fácilmente crear una nueva persona que tenga un nombre diferente.

Estos objetos con más complejos que los literales, pero nos permiten reutilizar más el código si vamos a crear varios objetos del mismo tipo.

### Prototipos

Los prototipos son una forma que tenemos de compartir atributos (datos) y métodos (comportamiento) entre distintos objetos de la misma clase. En el constructor definimos atributos, pero puede que queramos definir algunos más después. Y también puede que queramos definir métodos en nuestro tipo de objetos `Person`. [Vamos a ver cómo hacerlo](https://codepen.io/adalab/pen/govvEa) con la propiedad especial `prototype`.

```js
function Person(name) {
  this.name = name;
};

Person.prototype.jump = function() {
  console.log('Jump, ' + this.name);
}

var maria = new Person('María');
maria.jump(); //Jump, María

var carmen = new Person('Carmen');
carmen.jump(); //Jump, Carmen
```

Vemos que sobre nuestra función constructora `Person` llamamos a la propiedad `prototype` y definimos una nueva propiedad (en este caso un método porque es una función) `jump`. Esta función hace un `console.log` pero crea la cadena usando `this.name` que es el nombre que le hemos dado a la persona al hacer el `new`. Es decir, desde el método `jump` puedo acceder a los atributos como `name` escribiendo `this.name`. De igual forma, si desde un método quiero ejecutar otro método del mismo objeto también podré hacerlo mediante `this`. Para definir un nuevo método lo haremos de la misma forma, pero tendremos que hacerlo antes de crear los objetos con `new` si queremos que los objetos tengan este nuevo método.

```js
Person.prototype.sayHi = function(){
  console.log('Hi, ' + this.name);
}
```

## Contexto `this`

Un concepto muy importante de los objetos, y de las funciones también, es el contexto o `this`. En los objetos, `this` representa a la instancia concreta del objeto en cuestión. Es decir, cuando creamos a la persona de nombre María desde dentro del objeto si llamo a `this` es para acceder a algo de la persona María, que pueden ser sus atributos o métodos.

Pero el contexto `this` en las funciones es mucho más peliagudo y puede modificarse. Es decir, una misma función puede tener comportamientos diferentes si se ejecuta en contextos distintos. No es necesario que en este punto entendamos perfectamente cómo funciona, pero sí que es algo complejo y que si uso `this` dentro de una función luego cuando la ejecute tengo que tener mucho cuidado de darle el contexto adecuado. En el pasado hemos usado `this` en algunas funciones de callback para acceder al elemento sobre el que había sucedido un evento (usábamos si recuerdas, `event.currentTarget` o `this`).

Al ejecutar una función si queremos que se ejecute en un contexto determinado muy concreto (queremos indicar explícitamente el valor de `this`), podemos usando el método `bind` que crea una nueva función en el contexto indicado. Ahora no vamos a usarlo pero queremos que te suene este concepto en el futuro.


## Creando un objeto para un componente de la web

Vamos a ver ahora algunos ejemplos de cómo usar objetos que representen componentes de nuestra web.

Primero vamos a crear un [objeto de tipo botón](https://codepen.io/adalab/pen/JMprQz) que nos permita crear botones con distintos iconos y textos en objetos `<button>` del DOM.

```js

function Button (selector, text, icon){
  this.element = document.querySelector(selector);
  this.text = text;
  this.icon = icon;
}

Button.prototype.render = function(){
  this.element.innerHTML =
    '<i class="fa fa-' + this.icon + '"></i>' + this.text;
}


var favButton = new Button('.fav-button', 'Marcar como favorito', 'star');
favButton.render();

var shareButton = new Button('.people-button', 'Compártelo', 'users');
shareButton.render();
```

La función constructora de botones que tiene como parámetros
1. el elemento del DOM donde está el objeto `<button>`
2. el texto del botón
3. un icono del botón nombrado con el [nombre de clase de Font Awesome](http://fontawesome.io/icons/) (la librería CSS está importada en el pen para que funcione ;)

En la función constructora almacenamos los parámetros de texto e icono, pero en lugar de guardar el selector CSS guardamos directamente el elemento del DOM.

Luego definimos un método `render` que accede a ese elemento del DOM (el `<button>`) y modifica su contenido para meter el text y el icono.

Finalmente definimos 2 nuevos objetos botón, uno de favorito y otro de compartir, y ejecutamos sus metodos `render` respectivamente, para comprobar que funciona como esperamos.

***

#### EJERCICIO 1

**Hagamos botones**

Partiendo del codepen anterior, crear 3 nuevos botones para entender cómo funciona:
- botón de alerta
- botón de información
- botón de error

***

#### EJERCICIO 2

**Personaliza los botones**

Partiendo del ejercicio anterior, vamos a añadir un nuevo atributo a los botones que sea el color de letra. Para eso:
- añade un nuevo parámetro a la función constructora
- almacena el parámetro en el objeto usando `this`
- modifica el método `render` para que aparezca del color deseado (con el atributo `style` podría ser sencillo)
- modifica la creación de los objetos (`new`) para pasar el nuevo parámetro que es un color

***

Vamos a ver un segundo ejemplo de uso de objetos: [un carrusel de imágenes](https://codepen.io/adalab/pen/qpxoJO).

En la parte de JS empezamos creando una función constructora `Carousel` que toma dos parámetros: un selector CSS para acceder a la imagen y un array de `sources` que es un array con el listado de URL de las imágenes a mostrar en el carrusel. En el constructor definimos un atributo `current` que representa el estado actual del carrusel, es decir, qué imagen está siendo mostrada en este momento por medio de un índice. Empezaremos con el índice 0 para seleccionar con la primera foto del array. También definimos un parámetro `sources` para almacenar el array de imágenes. Y un tercer atributo `img` donde guardamos directamente la referencia a la imagen en el DOM. También definimos un método `render` que se encarga de modificar la imagen del DOM y asignarle como `src` la imagen del array `sources` en el índice `current`, es decir, la primera imagen del array.

```js
function Carousel(imgSelector, sources) {
  this.current = 0;
  this.sources = sources;
  this.img = document.querySelector(imgSelector);
}

Carousel.prototype.render = function() {
  this.img.src = this.sources[this.current];
}
```

También vamos a añadir al objeto carrusel métodos para mostrar la siguiente foto `next` o la anterior `prev`. El método `next` incrementa en 1 la posición actual y luego usa un truco matemático con el módulo para que si llegamos al final de array comience desde el principio. Luego llamamos a método `render` para que este cambio se vea reflejado en la página. Muy similar es `prev` que primero resta uno a la posición actual, y volvemos a hacer el mismo truco con el operador módulo (además suma la longitud del array para que el resultado nunca sea negativo) y también ejecuta `render`.

```js
Carousel.prototype.next = function() {
  this.current = (this.current + 1 ) % this.sources.length;
  this.render();
}

Carousel.prototype.prev = function() {
  this.current = (this.sources.length + this.current - 1 ) % this.sources.length;
  this.render();
}
```
Con nuestro objeto ya creado, vamos a crear un par de carruseles para probarlo. Primero un carrusel de gatetes. Para empezar, necesitamos definir nuestros elementos HTML, que son 2 botones de navegación por el carrusel y la imagen en el centro.

```html
<div>
  <button type="button" name="button" class="prev-cat">Prev</button>
  <img class="cat" src="" alt="">
  <button type="button" name="button" class="next-cat">Next</button>
</div>
```

En la parte de JavaScript definimos un array `cats` con el listado de imágenes de gatos que queramos. Luego creamos un nuevo objeto carrusel `catCarousel` que toma como parámetro el selector de la imagen '.cat' y el array de imágenes `cats`. Luego llamamos a `render` para mostrar la primera imagen.

Ya solo nos falta hacer que al clickar en los botones el carrusel pase a la siguiente imagen o a la previa. Para eso usamos nuestro viejo amigo `addEventListener` y en el evento 'click' le pedimos que ejecute la función correspondiente (`prev` o `next`) de nuestro objeto `catCarousel`. Pero tenemos uno de esos problemas raros de contexto que mencionábamos antes que se solucionan con `bind` ya que no somos nosotros quiénes llamamos a la función `catCarousel.next()` sino que es el navegador quien la llama cuando sucede el evento (es un callback). Así que pasamos a `bind` el objeto `catCarousel` para que sea el `this` dentro de esta función cuando el navegador la ejecute.

```js
var cats = [  ]; // Cat images
var catCarousel = new Carousel('.cat', cats);
catCarousel.render();

document.querySelector('.prev-cat').addEventListener('click', catCarousel.prev.bind(catCarousel));
document.querySelector('.next-cat').addEventListener('click', catCarousel.next.bind(catCarousel));
```

De esta forma ya tenemos funcionando nuestro carrusel. En el codepen también hemos creado un carrusel de fotos de perros para que veas que se puede reutilizar nuestra función constructora para crear todos los carruseles que queramos.

***

#### EJERCICIO 3

**Carrusel de loros**

Partiendo del codepen anterior, vamos a crear un nuevo carrusel, esta vez con fotos de loros 😱 Para hacerlo, sigue estos pasos:
- crea el HTML necesario para implementar el carrusel: los botones y la imagen
- ya en JS, crea un array con un listado de imágenes de loros
- crea una nueva instancia (`new`) de carrusel y llama a su método `render`
- añade como callback del click de los botones los métodos correspondiente
- disfruta de tu carrusel recién creado :)

***

#### EJERCICIO 4

**Carrusel con cosas**

Para terminar, vamos a añadir un par de cosas molonas a nuestro carrusel:

**Indicador de estado**

Para saber en qué estado está el carrusel, es decir, por qué foto vamos, podemos pintar un indicador de estado sencillo basado en texto. Por ejemplo, '1/5' si estamos en la primera foto de un total de 5. Al pasar a ls siguiente '2/5' y así. Para modificar el aspecto visual del carrusel tendrás que modificar su método `render` que es el que accede al DOM, y necesitarás el atributo `current` y la longitud de `sources` para saber qué pintar.

**Temporizador**

Para rizar el rizo, vamos a hacer un carrusel especial que esté temporizado. Para eso, vamos a modificar la función constructora para añadir un parámetro más que sea un booleano que indique si es un carrusel temporizado. Si lo es, en el propio constructor usaremos a nuestro viejo conocido `setInterval` para que pase a la siguiente foto cada 3 segundos. Para eso, la función de callback del `setInterval` tendrá que llamar primero al método `next` para pasar a la siguiente imagen y luego a `render` para reflejar los cambios en la página. *¡Verás como queda de molón!*

***

## Recursos externos

- [Object oriented JS - MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS)
- [Object prototypes - MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)
- [Método `bind` de las funciones en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
