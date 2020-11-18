# Sesión de repaso 3.1

Vamos a hacer cada uno de estos ejercicios en parejas, así que buscad una compañera para trabajar.

1. Idos turnando en cada apartado del ejercicio, de forma que no sea siempre la misma quien escribe en el ordenador.
1. Antes de empezar, tenéis que crear un nuevo repositorio en GitHub (en la cuenta de cualquiera de las dos), con el nombre `s3` y el nombre del ejercicio.
1. Partiremos del [Adalab Web Starter Kit](https://github.com/Adalab/Adalab-web-starter-kit) y trabajaremos con *gulp*.
1. Por cada apartado completado del ejercicio, y antes de cambiar quien teclea en la pareja, debéis hacer un commit describiendo los cambios nuevos que habéis introducido, en inglés.
1. Al finalizar un ejercicio completo, subiremos el resultado a GitHub y lo publicaremos con GitHub Pages.

## Header responsive e interactivo

En este ejercicio vamos a crear la cabecera de una página responsive. Para ello empezaremos con el diseño y el código adaptado a pantallas móviles y a partir de ahí empezaremos a crear los estilos para pantallas de mayor tamaño.

La estructura de la cabecera será la siguiente:

- Tendrá un logotipo a la izquierda que será un enlace (basta con poner `href=”#”`)
- En pantallas pequeñas tendrá un botón para mostrar el menú. El funcionamiento será bastante sencillo, por defecto cuando pulses aparecerá un menú con una transición. Tanto la forma en la que aparezca como los efectos serán libres pero tiene que tener una interacción animada a la hora de mostrarse. El botón permitirá tanto mostrar como ocultar dicho menú.
- En pantallas grandes no se mnuestra el botón y aparecerá un menú con varios enlaces (típicos About, Careers, Blog, Contact) que se mostrará en línea al lado derecho.

Este ejercicio contempla una serie de requisitos fundamentales que son los siguientes:

- Los estilos deberán de estar creados con Sass y Autoprefixer para generar automáticamente los vendor prefixes (-moz-, -webkit-, -o-, etc.)
- Trabajaremos paso a paso y seguiremos los pasos explicados en clase (cambios > commit > enviar al servidor y así continuamente). Utilizaremos buenas prácticas como editar el código CSS en el inspector de Chrome y no guarrear nuestro código hasta que no sepamos qué propiedades de CSS debemos usar.
- Usaremos animaciones de CSS y eventos de JavaScript para implementar la funcionalidad del botón.

Cómo recursos para inspiraros podéis echar un ojo a los siguientes enlaces. Pensad en la complejidad de cada uno y en los conocimientos y el tiempo que tenemos para desarrollar el ejercicio :).

- [Menu Off Canvas](https://tympanus.net/Development/OffCanvasMenuEffects/)
- [Best website design inspiration](https://85ideas.com/blog/best-website-header-design-inspiration/)
- [Collect UI - Header navigation](http://collectui.com/challenges/header-navigation)


## Layouts comunes usando CSS grid y Bootstrap grid

Vamos a crear el layout para páginas con las que habitualmente trabajaremos, usando CSS grid y/o el sistema de grid de Bootstrap. Para ello, os proponemos replicar [el experimento de Jo Franchetti de este artículo en Medium](https://medium.com/samsung-internet-dev/common-responsive-layouts-with-css-grid-and-some-without-245a862f48df), donde replica layouts típicos usando CSS grid. Realizad al menos el primer ejemplo *"Large Image followed by articles"* usando Sass y el sistema de grid que elijáis.
