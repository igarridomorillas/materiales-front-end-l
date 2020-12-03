# Eventos

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)
- [EJERCICIO 8](#ejercicio-8)
- [EJERCICIO 9](#ejercicio-9)
- [EJERCICIO 10](#ejercicio-10)
- [EJERCICIO 11](#ejercicio-11)
- [EJERCICIO 12 BONUS](#ejercicio-12-bonus)

<!-- /TOC -->

## Introducción

Ya hemos aprendido a modificar cosas en nuestra página web mediante JavaScript: cambiar contenidos, estilos, etc. Pero hasta ahora nuestro script (código JavaScript) se ejecutaba al cargar la página. En esta sesión vamos a aprender a hacer nuestra web interactiva, es decir, que haya modificaciones también de contenidos o estilos pero en respuesta a la interacción de la usuaria. La forma de modelar esa interacción de la usuaria en la web es mediante _eventos_. Un evento representa una interacción, que normalmente es de la usuaria, tras la cual podemos realizar una acción. Vamos a ver algunos ejemplos de acciones que implican eventos:

- mostrar una alerta cuando la usuaria hace click en un botón
- cambiar el tamaño de una cabecera fija cuando la usuaria llega a un punto de scroll
- abrir una sección oculta de un formulario cuando hago click sobre un botón
- cerrar una ventana modal cuando termina un temporizador de 15 segundos (aquí no hay acción de la usuaria)
- deshabilitar algunos campos de un formulario, cuando la usuaria selecciona una opción de un select
- enviar una petición al servidor para pedir los datos de los artículos que coinciden con la búsqueda, cuando la usuaria pincha en el botón de buscar en Amazon. Y cuando los datos del servidor llegan al navegador, pintarlos en la página

Es importante entender que nosotros no creamos eventos desde JavaScript sino que un evento se genera pero desde JavaScript podemos saber que ha sucedido. Ejemplos de eventos:

- click en un botón
- scroll en la página
- un cambio en el contenido de un input
- expira un temporizador
- llegan los datos del servidor

Lo que podemos hacer desde JavaScript es escuchar y responder a estos eventos. ¿Cómo? Creando una función que se va a ejecutar cuando el evento sucede.

Vamos a entender cómo actuamos en JavaScript con los ejemplos anteriores:

- cuando la usuaria hace click en el botón _más info_, ejecutamos una función que muestra una información que estaba escondida
- cuando el usuario hace scroll en la página, ejecutamos una función que comprueba si la posición de la pantalla es mayor que _x_ y en caso afirmativo aplica una clase CSS a la cabecera

## Escuchando eventos desde JavaScript

Vamos a ver cómo traducimos lo anterior a JavaScript. Escuchar un evento es decirle al navegador: vigila un determinado elemento de HTML, y cuando alguien haga `click` sobre él, ejecuta esta función que he preparado.
Técnicamente, registramos en el navegador una `función escuchadora` o `listener` sobre un elemento para que ejecute una `función manejadora de eventos` o `handler` cuando el evento suceda.

Vamos a ver el ejemplo de mostrar una alerta pulsando un botón.

Dado este HTML:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="utf-8" />
    <title>Ejemplo de alerta</title>
  </head>
  <body>
    <button type="button" name="button" class="alert">Alerta</button>
    <script type="text/javascript" src="js/index.js"></script>
  </body>
</html>
```

Para empezar, tendremos que recoger de HTML el elemento sobre el que queremos escuchar los eventos. Para ello, usaremos nuestro ya habitual `querySelector`.

```js
const button = document.querySelector('.alert');
```

A continuación, vamos a usar el método `addEventListener` de los elementos de HTML para escuchar eventos. Le pasaremos 2 argumentos: el tipo de evento a escuchar y la función que tiene que ejecutar cuando suceda el evento. Primero vamos a definir la función manejadora (`handler`), y luego registramos la función escuchadora (`listener`).

```js
// elemento de HTML
const button = document.querySelector('.alert');

// handler
function showAlert() {
  console.log('Alerta');
}

// listener sobre el elemento, con tipo de evento y handler
button.addEventListener('click', showAlert);
```

[Aquí podéis jugar con el ejemplo en codepen](https://codepen.io/adalab/pen/RjvLXe?editors=1010).

De esta forma, cuando hagamos click sobre el botón se ejecutará la función `showAlert`. Es importante que os fijéis en algunos detalles importantes:

- la función `addEventListener` la registramos sobre `button` que es un elemento de HTML (en este caso un botón)
- el primer argumento que le pasamos a `addEventListener` es una cadena con el nombre del evento, en este caso `click`
- el segundo argumento que le pasamos a `addEventListener` es una función, es decir, ponemos el nombre de la función pero no la ejecutamos (no ponemos paréntesis al final)

Vamos a detenernos un momento aquí: **el segundo argumento es una función**. Y es que en JavaScript podemos pasar el nombre de una función como argumento de otra. Es esta función que recibe el argumento la que se encarga de ejecutarla. Podéis ver un ejemplo en este [pen](https://codepen.io/adalab/pen/xyZexZ?editors=1011).

Observa la diferencia entre la ejecución de una función

- `logError()`

y el nombre de una función

- `logError`

Esto os puede parecer un poco raro y complejo al principio, pero iremos descubriendo en el curso que es muy útil. A este tipo de funciones que se pasan como argumentos a otras, se les llama **callbacks**.

Por lo tanto la función que le pasamos a `addEventListener` como segundo argumento es un `callback`, no la ejecutamos nosotras, es ejecutada por el navegador cuando sucede el evento.

Para pasar un _callback_ como argumento, podemos utilizar el nombre de una función ya declarada (como vimos en el ejemplo anterior), o podemos declararla directamente. Son dos maneras diferentes de hacer lo mismo. Vamos a ver el ejemplo anterior, pero declarando la función cuando la pasamos como argumento.

```js
const button = document.querySelector('.alert');
button.addEventListener('click', function showAlert() {
  console.log('alerta');
});
```

Esta versión tiene sólo 2 líneas y es un poco más enrevesada, pero funciona igual que la anterior. Vamos a verla con una arrow function:

```js
const button = document.querySelector('.alert');
button.addEventListener('click', () => console.log('alerta'));
```

> NOTA:
> Es muy importante entender que la función sólo se ejecutará cuando suceda el evento. Si el evento nunca sucede, la función nunca se ejecutará. Nosotros nunca ejecutamos la función: es el navegador quien la ejecuta cuando sucede el evento.

#### EJERCICIO 1

**Hola click**

Crear una página HTML con un párrafo en el que ponga Hola y un botón. Cuando se pulse el botón hay que cambiar ese texto por "Mi primer click, ¡ole yo y la mujer que me parió!

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

**¿Cómo te llamas?**

Crear una página HTML con un input de tipo texto para introducir tu nombre y un botón. Al pinchar sobre el botón, imprimir en la consola el mensaje 'Hola {nombre}', con el nombre que aparece en el input de texto.

> **Nota**: La etiqueta `input` no tiene apertura y cierre, por lo tanto técnicamente no tiene contenido. Si para leer y modificar el contenido de una etiqueta con apertura y cierre utilizábamos `innerHTML`, en el caso de los inputs utilizaremos `value`.

\_\_\_\_\_\_\_\_\_\_

Aparte del evento click, podéis ver [el listado completo de eventos que podemos escuchar en MDN](https://developer.mozilla.org/en-US/docs/Web/Events). Aquí vamos a listar algunos de los más usados:

- Eventos de ratón
  - `click`: botón izquierdo del ratón
  - `mouseover`: pasar el ratón sobre un elemento
  - `mouseout`: sacar el ratón de un elemento
- Eventos de teclado
  - `keydown`: pulsar una tecla
  - `keyup`: soltar una tecla
- Sobre elementos
  - `focus`: poner el foco (seleccionar) sobre un elemento, por ejemplo un input
  - `blur`: quitar el foco de un elemento
  - `change`: al cambiar el contenido de un input (hay que quitar el foco para que se considere un cambio) o de un select
- Formularios
  - `submit`: pulsar el botón submit del formulario
  - `reset`: pulsar el botón reset del formulario
- De la ventana
  - `resize`: se ha cambiado el tamaño de la ventana
  - `scroll`: se ha hecho scroll en la ventana o un elemento

#### EJERCICIO 3

**Dame ipsum**

Crear una página HTML con un párrafo con `lorem ipsum`. Al poner el ratón sobre el párrafo, vamos a añadir un nuevo párrafo a la página con `lorem ipsum`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

**Scroll es de colores**

Cambiar el color de fondo de la página cuando se haga scroll. Para ello tenemos que:

- Añadir un `div` con suficiente texto dentro para que haya scroll. Podéis usar el siguiente comando de emmet para hacerlo `p*50>lorem`.
- Preparar classes para cambiar el color de fondo del `div`.
- Escuchar el evento scroll sobre la ventana `window`.
- Cuando la posición del scroll vertical supere 250 píxeles poner un color de fondo, cuando sea inferior a 250 píxeles poner otro.

> **Nota**: `window.scrollY` nos devuelve la posición del scroll vertical.

\_\_\_\_\_\_\_\_\_\_

## Información sobre el evento

Como hemos visto, cuando registramos un listener para escuchar un evento, es el navegador quien ejecuta la función `handler`.

Al ejecutarla, le pasa unos argumentos que podremos recoger si definimos parámetros en nuestra función `handler`. El primero de ellos es un objeto que se suele denominar `event` y que contiene información acerca del evento.
Aún no hemos visto los objetos, pero ahora mismo basta decir que son como una variable con muchas variables dentro.

```js
const buttonElement = document.querySelector('.button');

function handleButtonClick(event) {
  console.log(event);
}

buttonElement.addEventListener('click', handleButtonClick);
```

Vamos a ver alguna de la información útil que contiene:

### event.key

En los eventos de teclado podemos [consultar la propiedad `key`](https://keycode.info/) para saber qué tecla se ha pulsado.

#### EJERCICIO 5

**Jugando con el teclado**

Tenemos que crear una página vacía. Al pulsar la tecla 'r' su color de fondo cambia a rojo y al pulsar la 'm' a morado. Vamos a escuchar un evento de teclado directamente sobre el elemento `document`.

\_\_\_\_\_\_\_\_\_\_

### event.currentTarget

`event.currentTarget` contiene el **elemento sobre el que pusimos el listener**.

```js
const buttonElement = document.querySelector('.button');

function handleButtonClick(event) {
  console.log(event.currentTarget);
}

buttonElement.addEventListener('click', handleButtonClick);
```

Prueba el ejemplo de código anterior y observa en la consola el valor de `event.currentTarget`. Contiene exactamente el mismo elemento que la constante `buttonElement`, a la que le pusimos el listener.

#### EJERCICIO 6

**Información instantánea**

Crear una página con un input de texto y un párrafo vacío. Cada vez que la usuaria escriba una letra tenemos que recoger el valor del input al que le pusimos el listener y escribirlo en el párrafo.

> **Nota**: el objetivo es hacerlo utilizando `event.currentTarget`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 7

**Otro botón**

Vamos a preparar un botón y una clase de CSS. La clase tiene que cambiar alguno de los estilos del botón (por ejemplo el color de fondo), pero no se la vamos a poner inicialmente. Cada vez que la usuaria pulse el botón hay que:

- añadir la clase si no la tiene
- quitarla la clase si la tiene

> **Nota**: para facilitar añadir y quitar clases de CSS, os recomendamos usar `classList.toggle`

\_\_\_\_\_\_\_\_\_\_

`event.currentTarget` es muy útil cuando queremos que varios elementos tengan el mismo handler.

Por ejemplo, pensemos en un listado en el cual al pinchar sobre un elemento este cambia de estilo indicando que ha sido seleccionado.

Vamos a verlo con un ejemplo:

```html
<ul class="fruits">
  <li class="fruit fruit-strawberry">Fresa</li>
  <li class="fruit fruit-banana">Plátano</li>
  <li class="fruit fruit-kiwi">Kiwi</li>
</ul>
```

```css
.fruit {
  padding: 6px;
  cursor: pointer;
  border-bottom: 3px solid #b9b8ba; /* grey */
}
.fruit--selected {
  border-bottom: 3px solid #64dac4; /* green */
}
```

```js
const strawberry = document.querySelector('.fruit-strawberry');
const banana = document.querySelector('.fruit-banana');
const kiwi = document.querySelector('.fruit-kiwi');

function handleFruitClick(event) {
  // Asignamos a una constante el elemento
  // sobre el que pusimos el `listener`
  // para trabajar cómodamente con él
  const selectedFruit = event.currentTarget;

  selectedFruit.classList.toggle('fruit--selected');
}

strawberry.addEventListener('click', handleFruitClick);
banana.addEventListener('click', handleFruitClick);
kiwi.addEventListener('click', handleFruitClick);
```

Así podemos tener una sola `función manejadora` para dominarlos a todos :)

#### EJERCICIO 8

**Más botones**

Partiendo del ejercicio anterior vamos a añadir un nuevo botón a nuestra página. Tenemos que ponerle un listener y a reutilizar el handler que ya teníamos. Es decir, los dos botones deben tener el mismo handler.

Cuando la usuaria pulse un botón el cambio de clase sucederá solamente sobre el botón pulsado.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 9

**Favoritos**

Hemos preparado un [HTML](https://codepen.io/adalab/pen/xyEwVj) con tres tarjetas.
Al pinchar en un elemento del listado tenemos que:

- Añadir la clase `.teacher--selected` si no la tiene, o quitarla si la tiene.
- Modificar el texto del span `.favorite` sustituyéndolo por 'Quitar' si en ese momento contiene 'Añadir', o por 'Añadir' si contiene 'Quitar'.

> **Nota**: con `querySelector` buscamos un elemento dentro de otro. Hasta ahora lo habíamos usado para buscar dentro de `document` (todo nuestro documento HTML), con `document.querySelector()`.

> Si tuviéramos una constante llamada, por ejemplo, `sectionAboutElement` en la que hemos guardado un elemento de HTML, podríamos buscar dentro él otro elemento, tal que así `sectionAboutElement.querySelector()`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 10

**¿Qué vemos esta noche?**

Vamos a partir de un HTML con un botón 'Empezar'. Al hacer click, vamos a pintar en el HTML un listado de películas que tenemos en JavaScript:

```js
const inception = 'Inception';
const theButterFlyEffect = 'The butterfly effect';
const eternalSunshineOfTheSM = 'Eternal sunshine of the spotless mind';
const blueVelvet = 'Blue velvet';
const split = 'Split';
```

Después vamos a escuchar eventos sobre cada elemento de la lista, de forma que al hacer click sobre el nombre de una película aparezca en la consola el nombre de esa película.

\_\_\_\_\_\_\_\_\_\_

### event.preventDefault()

Algunos elementos de HTML tienen comportamientos por defecto ante eventos, por ejemplo:

- al hacer click en un input de tipo checkbox este se marca/desmarca
- al hacer click en un botón o un input de tipo submit que se encuentra en un formulario el navegador intenta enviar los datos al servidor
- al hacer click en un enlace navegamos al mismo

El método **`event.preventDefault()` nos permite prevenir** estos **comportamientos por defecto** desde JavaScript.

Uno de los casos más comunes es prevenir el envío de un formulario.

Aunque aún no hemos visto cómo enviar un formulario desde JavaScript, prevenir que lo envíe el navegador sería el primer paso para poder controlarlo, validando sus datos, enviándolos al servidor desde JavaScript y mostrando _feedback_ a la usuaria sobre el proceso.

- [Ejemplo de botón submit en un formulario](https://codepen.io/adalab/pen/bjwJGv)

#### EJERCICIO 11

[comment]: <> (Hay una referencia a este ejercicio 5 de DOM avanzado)

**Para ese link**

¿Recuerdas el proyecto del módulo uno? Los enlaces de la cabecera de nuestra página tenían un problema, como nuestra cabecera era flotante, al navegar a una sección parte del contenido de quedaba oculto tras la cabecera.

Vamos a animarnos y a preparar un HTML muy sencillo con:

- una cabecera flotante que contenga un menu con tres enlaces
- tres secciones con bastante 'lorem ipsum' para que haya un scroll generoso

El primer paso para arreglar este comportamiento es escuchar el click en los enlaces y prevenir el comportamiento por defecto.

Hhhmm, pero entonces no pasa nada al hacer click... Correcto, ¡ejercicio terminado!

> **Nota**: no te preocupes, veremos cómo hacer que esos enlaces acaben de funcionar en futuras lecciones.

\_\_\_\_\_\_\_\_\_\_

## Dejando de escuchar eventos

Puede llegar un punto en que queramos dejar de escuchar eventos sobre un elemento. Para eso usaremos la función `removeEventListener` pasándole los mismos argumentos que al registrarlo.

```js
const buttonElement = document.querySelector('.alert');
buttonElement.removeEventListener('click', showAlert);
```

## BONUS

### event.target

En **`event.target`** encontraremos el **elemento sobre el que ha sucedido el evento**. Este elemento no tiene porqué ser el mismo sobre el que pusimos el listener.

```css
.btn {
  font-size: 24px;
}
```

```html
<button class="btn">
  <span class="btn__star">
    &#9733;
  </span>
  <span class="btn__text">
    Rate
  </span>
</button>
```

```js
const btnEl = document.querySelector('.btn');

const handleBtnClick = event => {
  console.log(event.currentTarget);
  console.log(event.target);
};

btnEl.addEventListener('click', handleBtnClick);
```

Si pruebas el ejemplo anterior al hacer click sobre el texto y después sobre la estrella podrás ver la diferencia entre `target` y `currentTarget`.

- `currentTarget` nunca cambia, es el elemento al que le pusimos el listener. Por lo tanto siempre es el elemento que escribimos antes del punto de `addEventListener`.

- `target` es el elemento sobre el que sucede el evento, puede coincidir con `currentTarget` o estar dentro de él.

En este [vídeo os mostramos la diferencia entre `ev.target` y `ev.currentTarget`](https://www.youtube.com/watch?v=qflQrH0CL4g). Os recomendamos ver solo los 3 primeros minutos del vídeo.

En la mayoría de los casos querremos trabajar con `currentTarget`. Pero no está mal que nos suene cómo funciona `target`.

#### EJERCICIO 12 BONUS

**Un listener para todos**

Vamos a _refactorizar_ el [EJERCICIO 9](#ejercicio-9) para mejorarlo. Tenemos que quitar ese mogollón de listeners en los `li`s, reemplazarlos por uno solo en la etiqueta madre (`ul`) y trabajar con `event.target`.

¡A por ello!

> **Nota**: esta técnica de poner un listener en la madre y acceder a la hija sobre la que se ha hecho click se llama **event delegation**.

\_\_\_\_\_\_\_\_\_\_

## Burbujeo de eventos o `event bubbling`

Cada vez que sucede un evento sobre un elemento de HTML, este 'burbujea' hacia arriba. Esto quiere decir que el evento sucede en ese elemento, y después en el elemento padre, y después en el abuelo, y así hasta llegar al último ancestro, `html`.

Aunque no lo vemos, esto está sucediendo continuamente en el navegador, por ejemplo cada vez que movemos el ratón, o hacemos click en cualquier sitio.
Los eventos suceden, independientemente de que los estemos escuchando o no.

Este comportamiento hace que:

- podamos 'escuchar' un evento en un elemento, sin que esto implique que se haya iniciado en él
- podamos poner `listeners` con `handlers` en varios padres y que todos se ejecuten si sucede un evento en un hijo común

Pincha en los `divs` de este [codepen](https://codepen.io/adalab/pen/MPjyyW?editors=1010) y observa cómo se comportan.

En este [pen](https://codepen.io/adalab/pen/zLKwwP) puedes ver cómo manejar eventos anidados sin que entren en conflicto.

## Otras formas de escuchar eventos

Existen otras formas de escuchar eventos que veréis por Internet, y que aunque siguen funcionando **no recomendamos** usar. La principal razón es porque queremos separar contenido (HTML), diseño (CSS) y funcionalidad (JavaScript). Estas otras formas de escuchar eventos se basan es el uso del atributo `onclick` (en realidad, on + evento), que pueden usarse desde HTML:

```html
<button type="button" name="button" class="alert" onclick="showAlert()">
  Alerta
</button>
```

O desde JavaScript:

```javascript
const button = document.querySelector('.alert');
button.onclick = function() {
  alert('Alerta');
};
```

A partir de ahora usaremos **siempre, siempre, siempre** la forma recomendada, es decir, `addEventListener`.

## Resumen

En esta sesión hemos visto: cómo hacer nuestras webs interactivas de verdad, escuchando eventos y reaccionando a ellos gracias a `addEventListener(type, handler)`. Cómo utilizar información que nos devuelve el navegador sobre los eventos:

- `event.currentTarget`: elemento con el listener
- `event.target`: elemento sobre el que sucede el evento
- `event.preventDefault()`: método para prevenir el comportamiento por defecto de un evento sobre un elemento

También, nos hemos acercado a los conceptos:

- `event bubbling`: los eventos pasan de unos elementos a otros de manera ascendente
- `event delegation`: gracias al burbujeo de los eventos podemos poner `listeners` a elementos padres para controlar eventos en hijos

Y hemos visto nueva información que no es exclusiva de los eventos como:

- `classList.toggle`: quita o añade una clase de CSS
- `inputNameElement.value`: nos devuelve el valor de un input
- `callback`: una función ejecutada por otra función

## Recursos externos

- [key codes info](https://keycode.info/)
- [Introduction to event listeners](https://www.youtube.com/watch?v=EaRrmOtPYTM&list=PLyuRouwmQCjnEupVi5lpP6VrLg-eO-Zcp&index=1)
- [currentTarget vs target](http://joequery.me/code/event-target-vs-event-currenttarget-30-seconds/)
- [classList.toggle](https://alligator.io/js/classlist/#toggle)
