# Anexo al Proyecto 2

## Índice

1. Seleccionar elementos HTML desde JavaScript
2. Cambiar el contenido de elementos HTML

## Introducción
Aunque este contenido se verá en detalle más adelante en el módulo, ya que hemos utilizado el `prompt` para recoger datos y almacenarlos en una variable nos queda cómo conectar nuestro JS con nuestro HTML de cada a completar el segundo hito del proyecto:

	Desarrollar una primera versión básica de la web, con la maquetación de la estructura básica (para web y móvil) y la funcionalidad de meter contenido en el currículum mediante el uso de los `prompt` de JavaScript.


## Seleccionar elementos HTML desde JavaScript
Para poder cambiar el contenido de una etiqueta HTML necesitamos una forma de localizarla, lo haremos con `document.querySelector(selector)`.

Usando Javascript, `document.querySelector(selector)` nos permite, usando un selector como haríamos en CSS (clase, id...), localizar el primer elemento en nuestra página que coincida con este selector.

Supongamos que tenemos un HTML como:

```html
<!DOCTYPE html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<title>Mi página</title>
</head>
<body>
	<div id="card1" class="card">
		<h2 class="card__title">Título</h2>
		<p class="card__content">Contenido de mi bloque</p>
	</div>
</body>
</html>
```

Y queremos seleccionar el elemento `h2` que tiene clase `card__title` y asignarlo a la variable `title`:

```javascript
var title = document.querySelector('.card__title');
```

O si queremos seleccionar el elemento con `id="card1"`:

```javascript
var card = document.querySelector('#card1');
```

Recordemos que esto nos devuelve el primer elemento que coincida con el selector: sólo 1 elemento.

### ¿Y si necesitamos seleccionar varios?
Pues tenemos una forma de selecionar todas las que cumplan con el selector elegido: `document.querySelectorAll(selector)`.

```html
<!DOCTYPE html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<title>Mi página</title>
</head>
<body>
	<div class="boxes">
		<div class="box box--1">box 01</div>
		<div class="box box--2">box 02</div>
		<div class="box box--3">box 03</div>
	</div>
</body>
</html>
```

Y si queremos seleccionar todos los elementos con clase `.box` podemos usar:

```javascript
var box = document.querySelectorAll('.box');
```

Nos devuelve una lista de elementos que cumplen con el selector usado, en este caso `.box`, y podemos acceder a uno de ellos, o saber cuántos hay:

```javascript
var box = document.querySelectorAll('.box');

alert('Hay ' + box.length + ' elementos');
// Devuelve: "Hay 3 elementos"

alert('El contenido del elemento 2 es: ' + box[1].innerHTML);
/*
Devuelve "El contenido del elemento 2 es: box 02"
Los elementos del listado que devuelve querySelectorAll
se numeran empezando por 0.
 */
```

## Cambiar el contenido de elementos HTML
Y esto nos lleva a `element.innerHTML` que es la forma que tenemos de consultar o cambiar el contenido de una etiqueta HTML.

Si por ejemplo tenemos un HTML como:
```html
<!DOCTYPE html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<title>Mi página</title>
</head>
<body>
	<h1 class="mood">:(</h1>
</body>
</html>
```

Y queremos tener un título más feliz podemos usar `querySelector` e `innerHTML`:

```javascript
var moodElement = document.querySelector('.mood');
/*
Asignamos a la variable moodElement el elemento HTML
que devuelve querySelector
 */

var currentMood = moodElement.innerHTML;
alert(currentMood);
/*
currentMood valdrá el contenido nuestro elemeto selecionado,
que es :(
 */

moodElement.innerHTML = ':)';
/*
Esto hace que se pinte en el HTML el nuevo contenido que
queremos para nuesto elemento, :)
 */
```
Con `innerHTML` podemos consultar el contenido HTML que hay dentro de una etiqueta, es decir, todo lo que hay entre su etiqueta de apertura y la de cierre. Por tanto, puede haber tanto texto como otras etiquetas HTML y siempre accedemos a ellas en formato cadena (string). Con `innerHTML` podemos tanto consultar este contenido como modificarlo.

Veamos otro ejemplo:
```html
<!DOCTYPE html>
<html lang="es">
<head>
	<meta charset="UTF-8">
	<title>Mi página</title>
</head>
<body>
</body>
</html>
```
Partimos de un HTML vacío y queremos queremos añadir el estado de ánimo desde JavaScript.

```javascript
var body = document.querySelector('body');
/*
Asignamos a la variable body el elemento HTML
que devuelve querySelector
 */

body.innerHTML = '<h1>:)<h1>';
/*
Esto hace que se pinte en el HTML un nuevo título que contiene :) Si había algo antes en el body se machacaría.
 */
```


## Resumen

Con estas herramientas y lo que hemos aprendido hasta ahora estamos en condiciones de preparar una primera versión de nuestra web usando el `prompt`. Yay!
