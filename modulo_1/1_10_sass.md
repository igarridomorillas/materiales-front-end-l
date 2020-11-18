# Sass

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO BONUS 5](#ejercicio-bonus-5)
- [EJERCICIO BONUS 6](#ejercicio-bonus-6)
- [EJERCICIO BONUS 7](#ejercicio-bonus-7)

<!-- /TOC -->


## Introducción

Con CSS podemos personalizar al píxel el aspecto de nuestra página y como hemos visto tiene una serie de reglas y de formas de hacer todo esto. Sin embargo el sector ha ido madurando y nos encontramos con que necesitaríamos poder trabajar con las hojas de estilos de una manera más ágil: permitiendo el uso de variables, pudiendo dividir los archivos en bloques más pequeños, pudiendo crear bloques de estilos que se repitan o incluso pequeñas funciones simples. Esto es posible con los preprocesadores CSS.

## ¿Qué es un preprocesador CSS?

Un preprocesador CSS es un lenguaje parecido al CSS pero que nos permite tener acceso a funcionalidades que no tiene el CSS y, tras el procesado, generar un CSS válido.

De esta manera ya no trabajaremos directamente el CSS sino con este preprocesador que, automáticamente, generará nuestros CSS finales.

Actualmente hay varios preprocesadores, realmente lo que los diferencia es la sintaxis de cada uno pero vienen a hacer un poco lo mismo. Los preprocesadores CSS más famosos son:

- [Sass (el que vamos a ver en Adalab)](http://sass-lang.com)
- [LESS](http://lesscss.org)
- [Stylus](http://learnboost.github.io/stylus/)

Nosotros vamos a usar Sass, concretamente SCSS, que es la sintaxis nueva :)

## Vale, ¿y esto cómo funciona?

Pues esto se instala y se ejecuta por terminal, pero para no sufrir lo tenemos integrado en el [Starter Kit de Adalab](https://github.com/Adalab/Adalab-web-starter-kit). Yay!

Al arrancarlo todo el SCSS de la carpeta **_src/assets/scss** se procesará en la carpeta **public/assets/css**, automáticamente y se recargará el navegador.

### Me estás liando, ¿Sass o SCSS?

El preprocesador CSS que vamos a usar se llama Sass (Syntactically Awesome StyleSheets) pero tiene dos sintaxis, Sass y SCSS. Usaremos SCSS porque es más parecida a CSS y no depende tantísimo de estar todo bien tabulado ya que usa las mismas llaves a las que estamos acostumbrados ya. Así que diremos `sass` pero usaremos `scss` ;)

## ¿Y qué puedo hacer con Sass/SCSS?

Maravillas, con Sass se pueden hacer maravillas.

Bueno, se pueden hacer muchas cosas, hoy vamos a ver las variables, como se anida, el símbolo `&` y las media queries, imports y mixins/funciones.

**¡Vamos a ello!**

### Variables

Se usan muy parecido a JavaScript, pero precedidas por el símbolo `$` y se asignan con los `:`

```scss
$colorLink: blue;
```

Ahora podríamos hacer algo como:

```scss
$color_link: blue;

a {
	color: $color_link;
}
```

El uso de variables nos da una serie de ventajas. Podemos definir al principio del documento todas nuestras variables y si una vez avanzados, o terminados, nuestros estilos queremos cambiar algún valor pues se cambia el valor de la variable que toque y se vuelve a generar el CSS.

¿Qué podemos usar como variables? Lo que queramos de los **valores** de las propiedades CSS.

```scss
$headerHeight: 100px;
$fontText: 'Roboto', arial, sans-serif;
$pathImages: '../images/';

body {
	font: 16px $fontText;
}
.header {
	background: url($pathImages + 'imagen.png') left top no-repeat;
	height: $headerHeight;
}
```

**¡Vamos a ponerlo en práctica!**

#### EJERCICIO 1

**Variables, variables everywhere**

En el siguiente [codepen](https://codepen.io/adalab/pen/aVrxYY) tenemos un ejemplo en css que vamos a reescribir a SCSS y modificar un poco.

1. Lo primero es configurarlo para usar SCSS: en la rueda de CSS, desplegar las opciones y elegir SCSS como preprocesador
1. Convertir a variables los valores de las líneas indicadas
1. Hacer los siguientes cambios sólo tocando la variables:
	1. Color del texto de `#414141` a `#010101`;
	1. Tamaño de fuente de la página a `18px`
	1. El margen de `.wrapper` a `0 60px`
	1. Fondo de header y footer a `yellow`
	1. Alto de header y footer a `50px`
	1. Fondo de `.main` a `cyan`

\_\_\_\_\_\_\_\_\_\_

**¿Cuándo hacemos variables y cuándo no?**

Quizás el primer impulso es empezar a crear variables como si no hubiera mañana pero el truco está en ver qué valores reutilizamos (misma altura para diferentes elementos, algunos márgenes, colores) y empezar creando sólo esas.

**Sobre los colores**

Lo ideal es usar variables que indiquen el tipo de elemento al que se va a aplicar un color y no tanto el color en sí. Es mejor `$colorLink` en lugar de variables tipo `$colorBlue` que tarde o temprano acaban valiendo un color diferente y va a desconcertar a quien coja el proyecto después. Aunque hay un término medio: definimos nuestros colores como el color que son y asignamos nuestra variable a otra variable que indique el elemento donde se va a usar.

```scss
$colorBlue: blue;
$colorDarkRed: #800;

$colorLink: $colorDarkRed;

a {
	color: $colorLink;
}
```

De esta manera tenemos un poco lo mejor de dos mundos.

### Nesting o anidado, y el símbolo `&`

Una maravilla que nos permite hacer Sass es anidar nuestros estilos.

Si queremos indicar que todos los `<p>` dentro de un elemento `.content` van a ser de color azul y si llevan enlace, éste, se mostrará en rojo, podemos escribir:
```scss
.content {
	p {
		color: blue;
		a {
			color: red;
		}
	}
}
```

Esto nos generará el siguiente CSS:

```css
.content p {
	color:blue;
}
.content p a {
	color:red;
}
```

El anidado nos permite anidar bloques asimilándose un poco a la jerarquía visual de HTML. Esto nos permite ver algunos bloques más claros o agrupar clases que nos interese ver juntas. Pero atención: anidar genera estilos más específicos y hay que usarlo con mucho cuidado.
Una buena regla es, cuando vayamos a añadir un cuarto nivel de anidación, pararnos a repensar si realmente es necesario. Pero con el uso iremos viendo cuándo usarlo y cuándo no ;)

### Referenciando al selector padre o madre: `&`

¡Pero no todo es tener cuidado! Una de las ventajas que nos ofrece el anidado es poder referenciar al selector padre o madre. Por ejemplo: queremos que los enlaces de nuestra página sean rojos, y el hover en azul, pero los enlaces del footer deben ser naranjas con el hover en verde.

```scss
a {
	color: red;
	&:hover {
		color: blue;
	}
	.footer & {
		color: orange;
		&:hover {
			color: green;
		}
	}
}
```

Esto generaría el siguiente CSS:

```css
a {color: red;}
a:hover {color: blue;}
.footer a {color: orange;}
.footer a:hover {color: green;}
```

En este [codepen](https://codepen.io/adalab/pen/JOqQGG) podéis verlo funcionando.

###  SASS & BEM. Una bonita pareja

Seguro que a estas alturas del temario ya habéis visto todas las ventajas que ofrece SASS para trabajar con CSS, y por eso, podéis imaginaros como era el mundo antes de SASS si no escribías tus hojas de estilo de manera ordenada… CAÓTICO.

Al afrontar proyectos de gran envergadura tu hoja de estilos crecía sin parar, pudiendo repetir nombres de clases, llenar tu css de `!important` por todas partes… en fin, convertir los estilos de tu proyecto en algo bastante difícil de mantener.

Por todo esto, aparecieron algunas convenciones de trabajo con CSS que intentaron minimizar el problema: OOCSS (Object Oriented CSS), SMACSS (Scalable and Modular Architecture CSS) y BEM (Block Element Modifier), esta última es la que os explicaremos, ya que encaja perfectamente con la manera de trabajar en SASS y es una de las más extendidas.

### ¿Pero qué es BEM?

Pues un marco de trabajo con CSS que hace que nuestro código quede limpio, ordenado y sobre todo, fácil de entender y mantener. La idea de la que parte es tan sencilla como nombrar cada clase que creamos en base a tres elementos:

**B-(Block)** Bloque contenedor principal del elemento al que queremos dar estilo
**E-(Element)** Elemento al que queremos dar estilo
**M-(Modifier)** Modificador de nuestro elemento

Pero vamos a por un ejemplo para verlo claro.

Supongamos que tenemos que crear tres botones en nuestro `header`. Uno llevaría los estilos por defecto de todos los botones de nuestra web, otro sería un botón de “success” con sus estilos propios y el último sería una variante del botón más pequeña.

¿Cómo resolveríamos esta nomenclatura de CSS en nuestro HTML? Pues así:

```html
<header class='header'>
   <button class="header__button"></button>
   <button class="header__button--success"></button>
   <button class="header__button--small"></button>
</header>
```

Siendo `.header` nuestro contenedor principal o “block”, `button` nuestro elemento principal “element”
y `success / small` nuestros *modifiers*.

Como puedes ver, para unir estos tres elementos utilizamos doble guión bajo y doble guión medio en todos los casos.

```css
.header__button--small {}
```

¿Y cómo traducimos esto a SCSS con SASS?

Pues gracias a la anidación o *nesting* de los elementos y a los selectores madre (&).

```scss
/***SCSS***/
.header {
   &__button{
      &--success {}
   }
}

/****PRECOMPILED CSS****/
.header {}
.header__button {}
.header__button--success {}
```

Como ya sabéis el selector `&` aplica estilos específicos a una etiqueta anidada dentro de un selector madre. Esto hace que el marco de trabajo que nos ofrece BEM sea el ideal para trabajar con SASS, pudiendo crear hojas de estilo limpias y ordenadas, así que a partir de ahora, las adalabers utilizaremos BEM para nombrar nuestras etiquetas y dar estilo a nuestros proyectos. Veréis qué fácil se hace mantener nuestra css y encontrar selectores concretos a medida que crece nuestro código ;)

> **Nota:** Os recomendamos leer la [documentación oficial de BEM](http://getbem.com/introduction/).

#### EJERCICIO 2

**Sass y BEM, cuanto más primo más me arrimo**

Utilizando el editor online https://sass.js.org/ y el operador `&` hay que reescribir el siguiente código con Sass. El reto está en escribir la palabra `card` una sola vez.

```css
.card {
	width: 100px;
	height: 100px;
	margin: 10px;
}
.card:hover {
	box-shadow: 10px 10px 5px 0px rgba(0,0,0,0.75);
}
.card--dark {
	background-color: #000;
	color: #fff;
}
.card--light {
	background-color: #fff;
	color: #000;
}
```

\_\_\_\_\_\_\_\_\_\_

### Mediaqueries

La posibilidad de anidar selectores nos permite una flexibilidad extra. Hasta ahora sólo podíamos meter selectores completos dentro de nuestras Mediaqueries, pero con Sass podemos incluir mediaqueries en nuestros selectores y hacer cosas como esta.

```scss
.wrapper {
	margin: 0 25px;
	@media all and (min-width:768px) {
		margin: 0 40px;
	}
	@media all and (min-width:1280px) {
		margin: 0 auto;
		max-width: 1200px;
	}
}
```

Y que generaría el siguiente CSS:

```css
.wrapper {
	margin: 0 25px;
}
@media all and (min-width:768px) {
	.wrapper {
		margin: 0 40px;
	}
}
@media all and (min-width:1280px) {
	.wrapper {
		margin: 0 auto;
		max-width: 1200px;
	}
}
```

#### EJERCICIO 3

**¡Medias a mi!**

Seguimos con el editor online https://sass.js.org/, hay que reescribir el siguiente código con Sass. Al turrón!

```css
.title {
  font-size: 16px;
}

@media (min-width: 768px) {
  .title {
    font-size: 18px;
  }
}

@media (min-width: 1024px) {
  .title {
    font-size: 20px;
  }
}
```

\_\_\_\_\_\_\_\_\_\_

### Imports y cómo organizar nuestro proyecto

Bueno, ¿qué más podemos hacer con Sass? Importar archivos. Esto es otra ventaja importante ya que nos permite modularizar nuestros estilos y trabajar en pequeños parciales que luego se unirán en el archivo final. Esto es gracias al `@import`.

Espera, CSS ya tiene un sistema de ´@import´ que todas sabemos que se colocan al principio del archivo CSS, ¿no? Pues sí, pero el ´@import´ de Sass lo puedes poner donde quieras del documento lo que nos permite plantear una estructura de componentes para llevar un orden en nuestros desarrollos. Hay muchas maneras de plantearlo así que os vamos a proponer una.

```
scss
	├─ main.scss o index.scss (archivo principal)
  ├─ core
  │  ├─ _functions.scss
  │  ├─ _mixins.scss
  │  └─ _variables.scss
  ├─ components
  │  ├─ _buttons.scss
  │  ├─ _forms.scss
  │  ├─ _hero.scss
  │  ├─ _newsletter.scss
  │  └─ _typography.scss
  ├─ layout
  │  ├─ _header.scss
  │  ├─ _footer.scss
  │  └─ _grid.scss
  └─ pages
     ├─ _about-us.scss
     ├─ _contact.scss
     └─ _home.scss
```

Tendríamos cuatro bloques de archivos: los de **core** como son las variables, nuestros mixins y funciones; el bloque principal de **layout** con la estructura del site y los componentes principales como header y footer; los diferentes **componentes** como puede ser un bloque de noticias, el formulario de contacto o los botones; y por último el bloque de **páginas** donde tendríamos los ajustes particulares de cada página.

En nuestro `main.scss` llamaríamos a todos estos archivos en orden:

```scss
// Core
@import 'core/functions';
@import 'core/mixins';
@import 'core/variables';

// Layout
@import 'layout/header';
@import 'layout/footer';
@import 'layout/grid';

// Components
@import 'components/buttons';
@import 'components/forms';
@import 'components/hero';
@import 'components/newsletter';
@import 'components/typography';

// Pages
@import 'pages/about-us';
@import 'pages/contact';
@import 'pages/home';
```

> **Nota 1:** si ponemos un archivo con un guión bajo delante Sass no lo procesará para convertirlo a CSS. La idea es que todos los nombres de archivos que vayamos a importar los escribamos con un guión bajo delante. Estos archivos a menudo se suelen llamar `parciales`, porque son partes del código final.

> **Nota 2:** es importante saber que el orden de los imports es importante y que tal como se carguen será como se importen y como se ejecuten para convertirse a CSS. ¡Recordad la cascada de CSS!

Una ventaja directa de trabajar con parciales es la cantidad de conflictos de git que nos vamos a ahorrar por no estar modificando el mismo fichero ;)

#### EJERCICIO 4

**Cada mochuelo a su olivo**

Vamos a crearnos un proyecto con nuestra estructura de imports de Sass. Usaremos el kit de Adalab. Recordad que **iremos haciendo parciales conforme los vayamos necesitando** y que **en cada carpeta estarán solo los que necesitemos**.
Para el ejercicio querremos:
- Un header de 75 de alto en móvil, 100 en tablet (768px) y 110 en desktop (1280px)
- Una home con 2 bloques:
	- Una sección principal que ocupe la mitad del alto de la pantalla con un texto en el centro
	- Una sección con un título y un botón rojo, con bordes de 5px de radio y 45px de altura

> Por ejemplo: En la carpeta `core` siempre tendremos nuestras variables pero si no tenemos mixins o funciones pues no existirán esos parciales.

\_\_\_\_\_\_\_\_\_\_

Y hasta aquí el contenido de la sesión, pero si quieres saber más tenemos contenido extra...

## BONUS

### Mixins y funciones

Vale, ¿qué es esto de mixins y funciones? ¡Lo mejor!

### Mixins

Los **mixins** son bloques de código que vamos a querer reutilizar y/o personalizar. Veamos un ejemplo.

```scss
@mixin absoluteCentered() {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%, -50%);
}

.container {
	position: relative;
}

.content {
	@include absoluteCentered();
}
```

Y esto generará:

```css
.container {
	position: relative;
}
.content {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%, -50%);
}
```

También podemos crear mixins "personalizables" con parámetros. Otro ejemplo.

```scss
@mixin t($fontSize, $lineHeight) {
	font-size: $fontSize;
	line-height: $lineHeight;
}
.main__title {
	@include t(32px, 40px);
}
.main__content p{
	@include t(18px, 24px);
}
```

Que generará el siguiente CSS:

```css
.main__title {
	font-size: 32px;
	line-height: 40px;
}
.main__content p{
	font-size: 18px;
	line-height: 24px;
}
```

#### EJERCICIO BONUS 5

**A mezclar**

Crea 3 mixins con tu compañera. Pensad en casos de uso comunes, como: propiedades de background, estilos de texto o media queries.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO BONUS 6

**MediaMixins**

Queremos rehacer el ejercicio 3 para poder escribir nuestro código así:

```scss
.title {
  font-size: 16px;

  @include tablet {
    font-size: 18px;
  }

  @include desktop {
    font-size: 20px;
  }
}
```

¿Te animas a hacer los mixins 'tablet' y 'desktop' para que funcione?

**Pista**: investiga la directiva `@content`

\_\_\_\_\_\_\_\_\_\_

### Funciones

Sass viene con un un [juego de funciones](http://sass-lang.com/documentation/Sass/Script/Functions.html) y además podemos crear las nuestras propias.
Por ejemplo, vamos a crear una función para poder escribir nuestras unidades en rem, pero elegantemente. ¿O qué?

Recordemos que `rem` es una medida relativa al tamaño de fuente especificado en nuestra etiqueta `<html>`, por defecto este tamaño es de 16px.

Vamos a crear una función a la que le pasemos los pixels que queremos y que ella se busque la vida para transformarlo a los `rem` correctos.

```scss
// Esta es la variable que usaremos como tamaño por defecto
$defaultFontSize: 16;

// la función acepta un número de pixels (los que vayamos a usar). Y nos devuelve el cálculo en unidades `rem` :)
@function rem($pixels) {
	@return ( $pixels / $defaultFontSize * 1rem );
}
// esta función iría en su archivo dentro de la carpeta core/ que luego podríamos usar así:

p {
	font-size: rem(18);
	margin: 0 rem(10);
}
```
Y generará:
```css
p {
	font-size: 1.125rem;
	margin: 0 0.625rem;
}
```

Mola, ¿o qué?

#### EJERCICIO BONUS 7

**Hágase la luz**

Investigad la función `lighten` en la docu de Sass, comentadla y probadla para ver su utilidad.

\_\_\_\_\_\_\_\_\_\_

## Recursos externos

- [Editor online para hacer pequeñas pruebas](https://sass.js.org/)
- [Guía de estilo subjetiva para escribir Sass sano, sostenible y escalable](https://sass-guidelin.es/es/)
