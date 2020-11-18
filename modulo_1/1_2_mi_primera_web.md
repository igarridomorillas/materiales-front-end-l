# Mi primera página web

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

Hasta ahora hemos visto una pequeña introducción a unos elementos básicos de HTML y CSS, pero hay más.

## Más etiquetas HTML

La etiquetas HTML nos permiten estructurar nuestro contenido según su función o carga semántica. Vamos a ver más etiquetas:

- para **definir nuestra página**
- para agrupar en **secciones**
- para identificar semánticamente el **contenido**
- para crear **tablas de datos**

> **Nota:** Todavía no lo hemos dicho expresamente pero lo normal es anidarlas, meter etiquetas dentro de etiquetas.

```html
<html>
  <body>
    <header>
      <h1>Título</h1>
    </header>
    <main>
      <section>
        <h2>Subtítulo</h2>
        <p>Contenido y más contenido</p>
        <p>Contenido con <a href="">enlaces</a></p>
        <ul>
          <li>lista</li>
          <li>de</li>
          <li>cosas</li>
        </ul>
      </section>
    </main>
  </body>
</html>
```

## Secciones

Normalmente no vamos a querer meter nuestro contenido en la página y ya está, querremos darle una estructura y agruparlo en bloques. Para ello tenemos la etiqueta `<section>`. Usaremos una sección para agrupar contenidos por temática:

Por ejemplo, en la página de un producto agruparemos la descripción del producto por un lado y los comentarios de los compradores/usuarios por otro.

Hay una serie de secciones especiales que tienen asignado un significado semántico predeterminado:

- `<header>`: una cabecera o sección de presentación de un bloque
- `<main>`: indica la principal sección de contenido
- `<footer>`: un pie o sección final de un bloque
- `<nav>`: un bloque de navegación, para un menú.
- `<aside>`: un bloque de contenido de menor importancia o con contenido relacionado
- `<article>`: un artículo, el cual aunque elimináramos el resto de contenido seguiría teniendo sentido por si mismo.

Estos bloques especiales se pueden usar unos dentro de otros según tenga sentido: por ejemplo, un `<article>` puede tener cabecera y pie, mientras que una cabecera no debería tener pie.

> **Nota:** Si usamos mal estos elementos el navegador no va a dar error, pero estaremos haciendo un favor muy pobre a aquellos usuarios que necesiten este extra semántico para navegar (por ejemplo, una usuaria ciega).

## Contenido

Dentro de estas secciones querremos incluir nuestros contenidos. Además de los encabezados, párrafos y listas tenemos un juego importante de etiquetas.

### Enlaces

Uno de los conceptos básicos de HTML es el enlace que nos permite vincular páginas o partes de ellas de manera que la información no quede como algo aislado sino conectado.

Un ejemplo es la wikipedia, donde en cada artículo se añaden enlaces relacionados que hacen que puedas completar la información a medida que la vas consultando.

El enlace se escribe con la etiqueta `<a>` y con un atributo `href=""` que indica a dónde enlaza.

Podemos enlazar a:

- una página o archivo
- una posición dentro de la misma u otra página

El primer enlace es muy fácil, simplemente ponemos la dirección de nuestra página o archivo como valor del atributo href:

```html
<a href="https://www.wikipedia.org">Wikipedia.com</a>
```

El segundo tipo de enlace necesita de un atributo especial que es el `id=""`. Cualquier elemento de nuestra página puede llevar este atributo pero al tratarse de un identificador no debe haber dos elementos con la misma id en la misma página.

En mi página voy a identificar la cabecera y el contenido principal:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="utf-8" />
    <title>Mi página</title>
  </head>
  <body>
    <header id="top">
      <h1>Título de mi página</h1>
    </header>
    <main id="main">
      <h2>Texto en latín</h2>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt
        ut labore et dolore magna aliqua.
      </p>
    </main>
  </body>
</html>
```

Ahora podría añadir un enlace abajo del todo para ahorrarle el scroll a las usuarias poniendo en el href el símbolo `#` seguido del id que quiero enlazar:

**index.html**

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="utf-8" />
    <title>Mi página</title>
  </head>
  <body>
    <header id="top">
      <h1>Título de mi página</h1>
    </header>
    <main id="main">
      <h2>Texto en latín</h2>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt
        ut labore et dolore magna aliqua.
      </p>
    </main>
    <footer>
      <a href="#top">Volver arriba</a>
    </footer>
  </body>
</html>
```

Si quisiese enlazar al contenido principal de mi página desde otra página usaría:

**product.html**

```html
<a href="index.html#top">Volver arriba de la página principal</a>
```

En estos dos casos se dice que las rutas son **relativas** porque apuntan dentro de nuestro proyecto. Si incluimos el dominio donde está alojada la página o archivo, aunque sea en nuestro dominio, diremos que la ruta es **absoluta**.

Si conocemos una página que use id, podemos enlazar directamente a esa parte del contenido . Vamos a enlazar a la wikipedia, justo a la parte donde se habla de la piratería en la edad media:

```html
<a href="https://es.wikipedia.org/wiki/Piratería#La_Edad_Media">La piratería en la edad media</a>
```

Aquí el atributo `href` lleva la dirección de la página de la Wikipedia sobre la piratería y el `id` de la sección que se refiere a la edad media.

> **Nota:** Si quieres ver los enlaces relativos que estamos utilizando en esta página ve arriba del todo y pulsa en los enlaces de cada uno de los ejercicios.

La etiqueta `<a>` tiene otros atributos que debemos conocer:

- `title=""`: Donde podemos añadir un texto complementario que el navegador mostrará en un pequeño tooltip cuando pongamos el cursor sobre el enlace. Me interesa usarlo cuando tengo un enlace tipo "descargar" y quiero asociarle el texto "Descargar archivo PDF".
  **Ejemplo:**
  ![Ejemplo de title=""](assets/images/1-2/title.png)
- `target=""`: Aquí podemos especificar donde se abre el enlace. Por ejemplo con el valor `_blank`, indicamos que sea en una nueva pestaña, lo cual nos interesa cuando en nuestra página enlazamos a páginas de otros y no queremos que el usuario "pierda" nuestra página al hacer clic en ellos.

### Negritas, cursivas

Tradicionalmente se usaban las etiquetas `<b>` y `<i>` para poner un texto en negrita (_bold_) o en cursivas o itálicas (_italic_). Estas etiquetas se mantienen aunque no tienen carga semántica, no significan nada más allá de que muestran el texto visualmente en negrita o cursiva.

Las nuevas etiquetas, `<strong>` y `<em>`, aunque visualmente hacen lo mismo (strong muestra el texto en negrita y em, en cursiva) sí que tienen una carga semántica, para indicar el nivel de énfasis o de importancia.
Con `<em>` resaltas un texto importante, y con `<strong>` resaltas un texto más importante.

```html
<p>
  Dentro de este párrafo tenemos <em>un texto importante</em> y
  <strong>uno que es muy importante</strong>
</p>
```

> **Nota:** El aspecto visual de estas etiquetas es una convención entre los diferentes navegadores y, como veremos, se puede cambiar.

### Imágenes

Muchas veces querremos acompañar nuestro contenido con imágenes, ya sea para acompañarlo (imágenes de una noticia, … ), o como motivo principal (una galería de ilustraciones,…).

Para ello tenemos la etiqueta `<img>`, que tiene varios atributos:

- `src=""`: Aquí indicamos la ruta de nuestro archivo de imagen
- `alt=""`: El atributo alt es el texto que va a mostrar el navegador en caso de la imagen no se pueda cargar, pero también es muy importante para la accesibilidad, cuando la imagen es parte del contenido debemos usarlo añadiendo un texto descriptivo. Cuando la imagen sea meramente decorativa, se recomienda dejar el valor vacío, pero no omitirlo.
  **Ejemplo:**
  ![Ejemplo de alt=""](assets/images/1-2/alt.png)

### Saltos de línea

Aunque es recomendable usarlo con tiento tenemos unas etiquetas que fuerzan un salto de línea: `<br>`.
Desde que empezamos a separar el contenido y el diseño esta etiqueta ha quedado relegada a un lugar muy secundario pero todavía hay veces en los que vas a querer forzar una línea nueva en mitad de un texto y está bien conocerla.

```html
<h1>Mi título genial <br />en dos líneas</h1>
```

### Contenedores generales

Aparte de las secciones tenemos un par de contenedores sin propósito específico que nos sirven para hacer agrupaciones sin carga semántica. Son el `<div>` y el `<span>`. Mientras que el **div** es para bloques de contenido el **span** está indicado para partes del texto o elementos en linea. Los iremos viendo más adelante.

### Tablas

Hubo un tiempo en el que las tablas eran la base sobre la que se maquetaba cualquier página web. Hoy se utilizan para lo que son: presentar datos tabulados.

La tabla básica tiene una estructura bastante simple y tiene tres etiquetas principales:

- una etiqueta que marque que se va a escribir una tabla
- una etiqueta para las filas
- una etiqueta para las celdas

En una imagen, una tabla de 3 filas y 3 columnas sería algo asi:
![Tabla de 3x3](assets/images/1-2/table.png)

y en código quedaría así:

```html
<table>
  <tr>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
```

En principio, en las tablas siempre tiene que haber igual número de celdas en cada fila.

#### EJERCICIO 1

**Organizando la semana**

Hacer una tabla con la comida de cada día de la semana usando `<th>` para las celdas que contienen los días.

\_\_\_\_\_\_\_\_\_\_

### La MDN

Buscar información sobre todos estos elementos en la [MDN](https://developer.mozilla.org/es/docs/Web/HTML/Elemento) para ir conociéndolos y familiarizándote con ellos

- Definición de página
  - doctype
  - html
  - head
  - title
  - link
  - meta \* body
- Secciones de página
  - section
  - header, main, footer, nav, aside, article
- Contenido
  - div/span
  - h1-h6
  - p
  - blockquote
  - ol/ul, li
  - img
  - a
  - strong, em
  - small, abbr, sup, sub
  - br, hr
- Tablas
  - table
  - tr
  - td, th
  - caption
  - thead
  - tbody
  - tfoot
  - col, colgroup

#### EJERCICIO 2

**Una página clásica**

Realizar una página semántica explicando algunos de los lenguajes de programación que vamos a aprender durante el curso, con:

- Un título principal.
- Contenido:
  - Tres párrafos con el contenido.
  - Dos párrafos con anuncios secundarios.
  - Un listado de 4 lenguajes de programación.
- Un texto de copy (© 2020).

\_\_\_\_\_\_\_\_\_\_

## CSS

Todos los elementos HTML tienen una apariencia que comparte cada navegador, con pequeñas variaciones. Por defecto, el tamaño de texto es de 16px, con un interlineado de 1.15. Los encabezados y párrafos tienen un margen superior e inferior relacionado con el tamaño de texto: el `<h1>` se muestra con un tamaño de 32px y tiene 22px de margen. El fondo de la página es blanco y el color del texto es negro...

> **Nota:** La medida básica en web es el pixel o px, cada dispositivo tiene su pantalla que tiene unas dimensiones definidas en pixels, por ejemplo, la pantalla de móvil más pequeña tiene 320x480px (si no se indica lo contrario siempre es "alto por ancho").

### Hojas de CSS reset y normalización

Debido a las pequeñas variaciones de la apariencia por defecto de los diferentes elementos HTML en cada navegador existen unas hojas de estilos más o menos estándar y más o menos completas que se llaman hojas de CSS _reset_ o normalización.
Se trata de una hoja de estilos que intenta que todos los elementos se muestren igual en todos los navegadores y no hay un estándar para hacerlo.

Ahora mismo hay parte de la comunidad de desarrollo que no considera que estas hojas de reset sean necesarias porque:

- Las páginas deben verse bien en todos los navegadores, no exactamente igual
- Las últimas versiones de los navegadores son bastante decentes y la época dura de los navegadores antiguos, ya pasó
- No hay un método estándar de reseteo de CSS

> **Nota:** Aún así, en algunos casos puede interesar usar una o incluso hacerse una propia, así que conocerlas es importante.

- [Reset CSS](https://es.wikipedia.org/wiki/Reset_CSS)
- [Normalice CSS](https://github.com/necolas/normalize.css)

## Selectores de CSS

Los navegadores ofrecen este aspecto por defecto pero nosotros lo podemos cambiar con CSS, creando estilos para definir la apariencia de nuestras página.

Para cambiar el aspecto de un elemento usamos un selector, hay varios tipos de selectores:

- la propia etiqueta del elemento: h1, a, p,…
- una clase que hayamos incluido con el atributo `class=""`
- a través de un identificador en el atributo `id=""`
- a través de una pseudo clase, que son unas palabras claves que añadidas al selector especifican un estado especial del elemento.
- a través de una mezcla de los anteriores

Vamos a ver cada uno de los casos.

### El propio elemento como selector

Esto no es lo ideal y se aplica los estilos a cada elemento de este tipo que aparezca en la página, así que hay que usarlo con tiento.

Podemos, por ejemplo, hacer que todos los enlaces sean rojos.

```css
a {
  color: red;
}
```

### Clases como selectores

Las clases son palabras claves que atribuimos a elementos HTML para poder agruparlos por función o apariencia y diferenciarlos del resto de elementos de su mismo tipo.

Por ejemplo: La clase "text-link" nos permite aplicar estilos particulares a los enlaces que lleven dicha clase sin afectar al resto de etiquetas.

```html
<a href="#" class="text-link">Enlace de texto</a>
```

En CSS creamos clases para aplicar a grupos de elementos como pueden ser todos los enlaces de texto, los elementos del listado de ingredientes o a los párrafos del pié de página.
La manera de indicar en css que se trata de una clase es escribiendo un `.` primero:

```css
.text-link {
  color: red;
}
```

### _id_ como selector

Ya habíamos visto que los _id_ eran una palabra clave que usábamos como identificador para un único elemento. En CSS también los podemos usar como selector, pero al no poder haber más de uno por página no es recomendable usarlo salvo en casos muy excepcionales.

En una lista de acciones, por ejemplo, podemos tener unas clases para añadir estilos a los elementos del bloque y, ademas, añadir un identificador único para cada elemento.

```html
<ul class="actions">
  <li class="action">
    <a id="add-user" href="" class="button">Nuevo usuario</a>
  </li>
  <li class="action">
    <a id="rename-user" href="" class="button">Renombrar usuario</a>
  </li>
  <li class="action">
    <a id="delete-user" href="" class="button">Eliminar usuario</a>
  </li>
</ul>
```

Y ahora podríamos usar el _id_ para cambiar el tamaño del texto de uno de los elementos. Para ello, usamos la `#` seguida de la id como selector.

```css
#add-user {
  font-size: 24px;
}
```

### Pseudo clase como selector

Las pseudo clases son palabras claves que añadidas a alguno de los selectores anteriores especifican un estado concreto del elemento. El más usado es el estado de `hover`, que ocurre cuando colocamos el ratón encima del elemento.

Las pseudo clases se escriben usando el selector, seguido de `:` y la palabra clave para el estado.

Por ejemplo, como en uno de los ejemplos anteriores, tenemos un enlace al cual le vamos a poner el texto de color rojo, pero al pasar el cursor encima invertiremos los colores y lo mostraremos con fondo rojo y color blanco. Partimos del mismo `html` que anteriormente.

```html
<a href="#" class="text-link">Enlace de texto</a>
```

Y el css sería:

```css
.text-link {
  color: red;
}
.text-link:hover {
  background-color: red;
  color: white;
}
```

[&rtrif; Codepen con ejemplo de hover](https://codepen.io/adalab/pen/QZmVjK)

### Los selectores se pueden mezclar

De los ejemplos de las pseudo clases vemos que los selectores se pueden mezclar. Esto nos ayuda a contemplar casos particulares sin tener que usar las ID.

Un elemento HTML puede tener tantas clases como queramos y las indicamos en su atributo `class` separadas cada una por un espacio.

Por ejemplo, si tenemos una lista de botones como la anterior:

```html
<ul class="actions">
  <li class="action">
    <a href="" class="button button--new">Nuevo usuario</a>
  </li>
  <li class="action">
    <a href="" class="button button--rename">Renombrar usuario</a>
  </li>
  <li class="action">
    <a href="" class="button button--delete">Eliminar usuario</a>
  </li>
</ul>
```

Hemos eliminado el atributo `id` y hemos añadido una clase extra para cada tipo de botón. De esta manera tenemos por cada "botón" una clase general `.button` donde colocaremos los estilos comunes a todos los botones y luego una particular (`.button--new`, `.button--rename` y `.button--delete`) donde solo pondremos los ajustes particulares.

Digamos que queremos que los botones tengan una caja con bordes redondeados pero que el de añadir usuario tenga fondo verde, el de renombrar azul y el de borrar, claramente, rojo muerte.

```css
.button {
  background-color: grey;
  border-radius: 20px;
  color: white;
  display: inline-block;
  margin-bottom: 1em;
  padding: 10px 20px;
  text-decoration: none;
}

.button--new {
  background-color: green;
}

.button--rename {
  background-color: blue;
}

.button--delete {
  background-color: red;
}
```

[&rtrif; Codepen de ejemplo de composición de clases](https://codepen.io/adalab/pen/KGoxam)

### ¡A jugar!

Para practicar los selectores, desde los más sencillos a los más complejos, te recomendamos [practicar con este divertido juego](https://flukeout.github.io/).

### Herencia en CSS

Hay una serie de estilos que se heredan, es decir, que se transmiten a las hijas. Entonces, si aplicamos una de estas propiedades a una etiqueta, todos las etiquetas anidadas en ella la heredarán también.

#### EJERCICIO 3

**Coloreame esos links**

El color es una de la propiedades que se heredan así que si tenemos esta estructura:

```html
<article>
  <h2>Título</h2>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit</p>
  <p>Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua</p>
  <aside class="links">
    <h3>Enlaces relaccionados</h3>
    <ul>
      <li><a href="#">Enlace 1</a></li>
      <li><a href="#">Enlace 2</a></li>
      <li><a href="#">Enlace 3</a></li>
      <li><a href="#">Enlace 4</a></li>
    </ul>
  </aside>
</article>
```

y al `<aside>` con clase `.links` le aplicamos una regla que ponga el texto rojo, ¿qué quedará en rojo?

\_\_\_\_\_\_\_\_\_\_

- [Más info sobre herencia en la MDN](https://developer.mozilla.org/es/docs/Web/CSS/inheritance)

#### EJERCICIO 4

**Herencia para todas**

Partiendo del [ejercicio 2](#ejercicio-2) vamos a hacer uso de la herencia, y utilizando un solo selector de css vamos a hacer que:

- el tamaño de fuente de la página sea de `18px`
- el tipo de fuente sea `Tahoma`
- el color de fuente sea `rebeccapurple`
- el color de fondo sea `mediumpurple`
- el interlineado sea de 1.5

> **Pista**: Tenemos que trabajar con la primera etiqueta del contenido de `html` que es `<body>`, y utilizar el selector de etiqueta para que todas sus hijas anidadas hereden de ella.

\_\_\_\_\_\_\_\_\_\_

### Cascada y especificidad de selectores

CSS es, en español, "hojas de estilo en cascada". La "cascada" se refiere al proceso de combinación y aplicación de estilos en CSS y cómo se resuelven los conflictos entre ellos.

Acabamos de ver que a veces varios selectores se aplican al mismo elemento, es el algoritmo de la cascada lo que decide qué propiedades se aplicarán.

La cascada depende de 3 factores:

1. La **importancia**: hay una palabra clave (`!important`) que hace que nuestra propiedad se aplique siempre. Cuando en un proyecto se abusa del uso de `!important` siempre llega un momento en el que queremos cambiar un estilo que ya tiene la palabra clave `important` y como es importante no podemos. Por ello se recomienda usar `!important` lo menos posible y en su lugar usar la especificidad.
2. La **especificidad**: es un arma de doble filo porque cuanto más específico sea un selector más fuerza tendrán sus reglas sobre las demás. Pero es una buena práctica escribir los selectores lo menos específicos posible.
3. El **orden** en el archivo CSS: si varios selectores tienen la misma "fuerza" ganarán los que estén más abajo porque el CSS se aplica en orden de escritura.

[En este enlace de la MDN viene perfectamente explicado](https://developer.mozilla.org/es/docs/Learn/CSS/Introduction_to_CSS/Cascada_y_herencia).

Dos enlaces sobre la especificidad más... a menos

- [CSS Specifity Wars](https://stuffandnonsense.co.uk/archives/css_specificity_wars.html)
- [CSS SPECIFITY](http://cssspecificity.com/#)

#### EJERCICIO 5

**Conociendo la especifidad**

Partiendo de este [Codepen de ejemplo](https://codepen.io/oneeyedman/pen/vWEBex):

1. ¿Por qué los enlaces son verdes y no rojos?
2. Hacer que los enlaces sean rojos.
3. Rehacer el HTML usando `<div>` en lugar de `<ul>` y `<li>`. ¿Qué pasa?
4. Comentar el CSS que no se puede tocar y reescribirlo usando solo selectores de clase, es decir, sin utilizar selectores de etiqueta.
5. BONUS: Cambiar ahora entre `<div>` y `<ul>`/`<li>`.

\_\_\_\_\_\_\_\_\_\_

## Colores

Para empezar, vamos a ver los distintos formatos que podemos usar para indicar colores, por ejemplo como valor de nuestra querida propiedad CSS `color`.

### Colores con palabras clave

La primera forma de indicar un color es mediante la palabra clave que indica el nombre del color. Hay un montón de palabras clave para colores que podemos usar que podéis ver en [la tabla de este artículo](http://devdocs.io/css/color_value#Color_keywords).

```css
p {
  color: fuchsia;
}
```

### Colores en hexadecimal

De forma equivalente a las palabras clave, podemos expresar un color con formato hexadecimal. En este formato declaramos un color con una almohadilla `#` y sus 3 componentes RGB - R (rojo), G (verde), B (azul). Cada uno de los componentes se representa con 2 dígitos en hexadecimal, es decir, cada dígito puede tener 16 valores, entre 0 - 9 y A - F. Por ejemplo, el color fucsia se compone de una componente máxima de rojo (ff), nada de verde (00) y máxima de azul (ff).

```css
p {
  color: #ff00ff;
}
```

Suele ser habitual expresar algunos colores comunes de forma simplificada. Si los dígitos de cada componente son iguales (por ejemplo, `ff`) puede escribirse el color de una forma simplificada escribiendo sólo una vez el dígito repetido. Por ejemplo, el fucsia puede simplificarse porque todos los componentes tienen el dígito repetido.

```css
p {
  color: #f0f;
}
```

### rgb y rgba

Como hemos visto en el caso anterior, los colores podemos expresarlos con sus componentes RGB (Red, Green, Blue). En CSS existe la posibilidad de, en lugar de usar 2 dígitos hexadecimales, expresar el color usando el valor decimal (número normal) de cada componente RGB, que tendrá un valor entre 0 y 255 (los mismos valores que podíamos indicar con 2 dígitos hexadecimales).

```css
p {
  color: rgb(255, 0, 255);
}
```

Existe además la posibilidad de indicar un nivel de opacidad al color con el formato RGBA que añade el canal alpha o transparencia. Este último componente tiene valores decimales entre 0 (totalmente transparente) y 1 (totalmente opaco).

```css
p {
  color: rgba(255, 0, 255, 0.7);
}
```

### hsl y hsla

Igual que el RGB nos permite expresar colores a partir de sus componentes de color rojo/verde/azul, existe otro sistema, HSL, que nos permite expresarlos a través de H (hue - matiz), S (saturation - saturación), L (lightness - luminosidad). El matiz se expresa con un valor numérico y tanto saturación como luminosidad con un valor en %. En este caso, también existe la posibilidad de añadir un canal alpha para indicar transparencia.

```css
p {
  color: hsl(300, 100%, 50%);
}

p {
  color: hsla(300, 100%, 50%, 0.7);
}
```

Para más información, consultad [la guía de colores de MDN](http://devdocs.io/css/color_value).

### Background

Como veremos más adelante, cada elemento se puede ver como una caja, veamos cómo añadir un fondo a dicha "caja":

Gracias a la propiedad _background_ podemos rellenar el fondo de nuestro contenedor con una imagen, con un color, o ambos:

![Ejemplos de background](assets/images/1-2/ejemplos-de-background.png)

La propiedad background se construye con estos posibles valores:

- url de la imagen
- posición de la imagen dentro del contenedor (horizontal y vertical)
- modo de repetición de la imagen
- color de fondo

```css
.box {
  background: url('url-de-la-imagen') left top no-repeat #ffcc00;
}
```

> **Nota:**
> El orden no tiene que ser necesariamente ese, pero os proponemos usarlo.

Realmente, la propiedad _background_ es una versión acortada de estas propiedades:

- **background-image:** [Ver detalle](http://devdocs.io/css/background-image)
- **background-position:** [Ver detalle](http://devdocs.io/css/background-position)
- **background-repeat:** [Ver detalle](http://devdocs.io/css/background-repeat)
- **background-color:** [Ver detalle](http://devdocs.io/css/background-color)
- **background-size:** [Ver detalle](http://devdocs.io/css/background-size)
- **background-attachment:** [Ver detalle](http://devdocs.io/css/background-attachment)
- **background-clip:** [Ver detalle](http://devdocs.io/css/background-clip)
- **background-blend-mode:** [Ver detalle](http://devdocs.io/css/background-blend-mode)

#### EJERCICIO 6

¿Sabrías replicar los ejemplos de fondo usando [este Codepen](https://codepen.io/adalab/pen/JLwQpz)?

\_\_\_\_\_\_\_\_\_\_

### Cuándo usar las propiedades de background o la versión acortada

Usar estas dos propiedades produce el mismo resultado pero no son lo mismo:

```css
.box {
  background-color: green;
}
.box {
  background: green;
}
```

Mientras que en el primer caso estamos diciendo que el color de fondo sea `green`, en el segundo estamos diciendo eso y que el resto de valores pasen a su valor por defecto.

¿Sabrías adelantar el resultado de aplicar esta clase?:

```css
.box {
  background-image: url('https://www.fillmurray.com/150/1500');
  background: red;
}
```

- [ ] Se verá a Bill Murray de fondo
- [ ] Se verá a Bill Murray de fondo pero lo que no rellene la imagen será de color rojo
- [ ] Solo se verá un color rojo de fondo
- [ ] Otra

Cuando usamos un atajo estamos definiendo TODAS las opciones, aunque no las usemos, por eso siempre deberíamos usar las propiedades que necesitemos, y solo usar los atajos cuando realmente estemos usando la mayoria de las propiedades :)

Si solo queremos cambiar el color de fondo deberíamos usar
`background-color`.
Si por el contrario queremos poner una imagen, en una posición y con una repetición, deberíamos usar el acortador `background` ya que realmente se escribe menos:

```css
.box {
  background-image: url('https://www.fillmurray.com/150/150');
  background-position: left top;
  background-repeat: no-repeat;
}
```

```css
.box {
  background: url('https://www.fillmurray.com/150/150') left top no-repeat;
}
```

## Background-size

Desde hace tiempo hay una propiedad nueva que nos permite redimensionar la imagen de fondo y hasta definir cómo se debe ajustar a nuestro contenedor: `background-size`.

Nosotros vamos a ver cómo ajustar el fondo a nuestro contenedor pero puedes consultar la [documentación completa](http://devdocs.io/css/background-size).

Hay dos valores especialmente interesantes ya que permiten definir cómo se ajustará nuestra imagen de fondo al contenedor: **contain** y **cover**.

### Contain

Aumenta o reduce la imagen proporcionalmente todo lo que pueda sin deformarla para que quepa en nuestro contenedor.

### Cover

Aumenta o reduce la imagen proporcionalmente para asegurarse que siempre cubre todo el área de nuestro contenedor, aunque eso signifique que parte de la imagen pueda quedar oculta.

[Ejemplos de uso de Contain y Cover](https://codepen.io/adalab/pen/aGojMd)

## BONUS

### Accesibilidad

Os dejamos un par de enlaces muy interesantes sobre accesilibidad web:

- [Introduction to Web Accessibility and W3C Standards (video: 4:07)](https://www.w3.org/WAI/videos/standards-and-benefits/es)
- [Introducción a la accesibilidad web (charla)](https://es.slideshare.net/tayzee/11-introduccin-a-la-accesibilidad-web)

### Figma

[Figma](https://www.figma.com/) es una herramienta online para diseñar y prototipar que permite hasta tres proyectos gratuitos. Este tipo de herramientas son muy útiles para las frontend, ya que nos pueden servir para algo sencillo como medir o recortar una imagen de manera ágil, o para algo más complejo como diseñar nuestra web personal.
