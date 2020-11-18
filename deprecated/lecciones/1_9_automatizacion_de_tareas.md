# Automatización de tareas

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

En esta sesión usaremos herramientas para automatización de tareas en nuestro flujo de trabajo en front-end. Estas herramientas son muy útiles porque nos ayudarán a ser más eficientes en nuestro trabajo y nos ahorrarán tareas repetitivas.

> **NOTA:** En esta sesión vamos a dar un repaso por encima a un flujo de trabajo con Gulp y Node pero no tendremos que configurarnos todavía nuestro entorno de trabajo, os proporcionaremos una base ya configurada sobre la que trabajar lo que queda de módulo :)

> **NOTA:** Para esta sesión debemos tener Node instalado en nuestro ordenador. Si no lo tenemos instalado debemos hacerlo siguiendo los pasos de Guía de instalación de ordenadores.

## ¿En qué casos se utiliza?

En nuestro flujo de trabajo realizamos algunas tareas repetitivas. Por ejemplo, convertir el Sass en CSS. Sass es una tecnología que veremos en la próxima sesión y escribimos el código en un lenguaje que luego se convierte en CSS.

Otra tarea habitual que se suele hacer es optimizar los ficheros CSS y JavaScript antes de subir la web al servidor (a GitHub en nuestro caso). Esta optimización se realiza para que el navegador pueda cargar y ejecutar los archivos más rápido y mostrar la página con más rapidez.

Con una herramienta como Gulp, vamos a poder hacer que nuestro código Sass se convierta en CSS al guardar el fichero; y ejecutar una tarea para que nos guarde el CSS/JS con código optimizado que más tarde subiremos a nuestro servidor (de nuevo, GitHub en nuestro caso).

## Gulp

![Gulp](assets/images/1-9/logo-gulp.png)

Gulp es una herramienta de automatización de tareas que está programada con JavaScript. Gulp no tiene interfaz gráfica sino que se ejecuta desde la terminal de comandos, al igual que sucede con git. Primero vamos a ver cómo instalarla y después la configuraremos para ayudarnos con algunas tareas.

Decir que Gulp lo usaremos a través del terminal, que no tiene interfaz gráfica y que la configuración te la tienes que hacer tú mismo hace que sea difícil de vender como algo mejor. Pero la clave de Gulp reside en esa última característica, la de configurarlo a través de JavaScript. La potencia de usar una herramienta de automatización de tareas como Gulp es que podemos configurarla a nuestra manera y añadir procesos y tareas a medida que las necesitemos e ir mejorando poco a poco estos para adaptarlos a nuestras necesidades. Esto es el motivo principal por el que en la mayoría de las empresas tienen automatizadas las tareas con herramientas como Gulp. En esta sesión veremos alguna novedad como poder visualizar nuestra página directamente desde el móvil sin tener que subirla al servidor, pero esto es solo la punta del iceberg, existen cientos de utilidades que podremos utilizar con Gulp y que nos facilitarán mucho la tarea de desarrollar páginas web.

### Node

Hasta ahora sabíamos que JavaScript se ejecuta siempre en un navegador web. Pero qué pasa si queremos ejecutar JavaScript fuera de un navegador?

Node es una plataforma que nos permite ejecutar código JavaScript en nuestro ordenador o un servidor, ya sea para programar un back-end o para ejecutar pequeños programas de código que nos sirvan de herramientas, llamados scripts, y todo ello usando código JavaScript, fantástico ¿no?.

Para poder usar _Gulp_ en nuestro ordenador, necesitamos tener instalado _Node.js_.

No nos vamos a poner a instalar Node en el ordenador, ya está instalado y vamos a comprobarlo. Para ello como suele ser común, escribiremos en la terminal el nombre del comando, seguido de `-v` o similar, como hemos hecho anteriormente con git, en este caso escribiremos:

```shell
node --version
```

Una vez hecho esto nos aparecerá un mensaje en la terminal. Si nos aparece un mensaje del estilo `El comando no existe` o `command not found` es que no tenemos instalado Node en nuestro ordenador. Si por el contrario, se muestra la versión de Node que tenemos instalada, por ejemplo `v10.16.0`, sabremos que lo tenemos instalado y por tanto podemos saltarnos el paso de la instalación.

> Si nos aparece otro mensaje es que no se ha instalado correctamente, es el momento de instalarlo :)

### npm

Node viene con un gestor de paquetes llamado _npm_. Npm nos permite instalar paquetes, es decir, pequeñas librerías de código que usamos para construir aplicaciones o para usar como herramientas. Una de estas herramientas será el propio Gulp. Para comprobar que está bien instalado, ejecutamos en la terminal este comando que debería devolver la versión de npm que tenemos instalada:

```shell
npm --version
```

Si tras ejecutarlo nos devuelve un número de versión, es que todo está correcto y podemos continuar con la instalación de Gulp. Para ello ejecutamos esto en la terminal (si da error de permisos, tendremos que poner `sudo` delante del comando):

```shell
npm -g install gulp-cli
```

El `-g` indica que se instala de forma global y se puede usar la utilidad de Gulp (como nuevo comando de la terminal) en todos los proyectos de nuestro ordenador.

> **NOTA:** Instalar `gulp` en casa para que en clase que nos pongamos a trabajar en los ejercicios.

### Usando Gulp en nuestro proyecto

Ahora que ya tenemos todo instalado, vamos a utilizar Gulp en nuestro proyecto. Vamos a crear un nuevo proyecto, para ello creamos una nueva carpeta (podemos hacerlo desde la terminal con `mkdir <nombre_carpeta>`). **Y nos movemos dentro de la carpeta con `cd <nombre_carpeta>`**.

Para indicar que en este proyecto vamos a usar npm, necesitamos crear un fichero llamado `package.json` que indica la configuración de npm del proyecto. Es un fichero en formato JSON, tiene el aspecto de un objeto de JavaScript que ya veremos en el próximo módulo. La forma más sencilla de crear este fichero es ejecutando desde la terminal:

`npm init`

Al hacerlo, nos irá pidiendo información sobre el proyecto: nombre, descripción, etc. Podemos escribir esta información o pulsar la tecla `Enter` para aceptar la información que viene por defecto y que aparece entre paréntesis al lado de donde escribimos. Una vez haya terminado de hacer preguntas, creará el archivo `package.json` en nuestra carpeta, si lo abrimos veremos que la pinta algo así:

```json
{
  "name": "testing-gulp",
  "version": "1.0.0",
  "description": "A project to play around with Gulp",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Adalab",
  "license": "ISC"
}
```

> **Nota**: Es importante recordar que NUNCA debemos llamar a nuestro proyecto "gulp" o "node"

Ahora tenemos que instalar Gulp de forma local en nuestro proyecto. Para eso ejecutamos:

`npm install --save-dev gulp`

Con esto, instalamos Gulp para nuestro proyecto e indicamos que se use sólo en el entorno de desarrollo `--save-dev` porque en producción ya tendremos el código final y no necesitaremos volver a procesarlo (si desarrollo y producción te suenan a chino [puedes leer un poco sobre entornos de programación](https://www.linuxito.com/programacion/237-el-modelo-de-desarrollo-testing-y-produccion)). Cuando termine la instalación, echamos un ojo al `package.json` y se habrá añadido esta configuración:

```json
  "devDependencies": {
    "gulp": "^4.0.0"
  }
```

Además notaremos que se ha creado una carpeta en el proyecto `node_modules` donde se instalarán los paquetes de npm. Normalmente no queremos que esta carpeta forme parte de nuestro control de versiones, así que **la incluiremos en nuestro `.gitignore`**.

El `package.json` se usa para saber qué paquetes (dependencias) tiene el proyecto. ¿Para qué? Porque si alguien se clona tu proyecto no va a tener todo el código de las dependencias (la carpeta `node_modules`) pero en el `package.json` está toda esa información. Simplemente ejecutando `npm install` se instalarán todas esas dependencias y se añadirán a la carpeta `node_modules`.

Ahora solo nos falta crear el fichero de configuración de Gulp llamado `gulpfile.js`. Vamos a crear un fichero con ese nombre y meter este código de configuración (si miráis con atención ¡es JavaScript!):

```javascript
const gulp = require('gulp');

gulp.task('default', function(done) {
  console.log('Hola Gulp');
  done();
});
```

> **NOTA**: No vamos a entrar por el momento en detalle ni explicaciones, simplemente queremos que lo probéis y os vayáis familiarizando. Usad el botón de copiar de gitbook para evitar copiar caracteres extraños.

Para probar el código anterior, en la terminal escribiremos el siguiente comando:

`gulp`

Como resultado aparecerá el mensaje 'Hola Gulp' en nuestra terminal. Lo que hace el comando `gulp` es buscar el archivo `gulpfile.js` en la ruta en la que estamos situados desde la terminal. Si existe ejecutará la función asociada a la tarea `'default'` de Gulp, que en este caso hace un `console.log`.

Pero esto no es muy útil. Vamos a usar ahora otro _gulpfile_ más complejo que nos permita convertir Sass a CSS. Pero primero tendremos que instalar otro paquete que nos permite hacer esto:

`npm install --save-dev gulp-sass`

Ahora usaremos este gulpfile:

```javascript
const gulp = require('gulp');
const sass = require('gulp-sass');

gulp.task('default', function(done) {
  gulp
    .src('scss/index.scss') // Leo el archivo scss
    .pipe(sass()) // Convierto el contenido del archivo index.scss a CSS
    .pipe(gulp.dest('css')); // El CSS generado lo guardamos en la carpeta css
  done();
});
```

Lo que hace es coger `scss/index.scss` y generar a partir de él un archivo CSS en la carpeta `css`. Para probarlo, creamos en nuestro proyecto una carpeta `css` vacía y otra `scss` con un fichero llamado `index.scss` en el que escribiremos lo siguiente:

```scss
$primary-color: magenta;

body {
  background: $primary-color;
}
```

Ahora ejecutamos `gulp` en la terminal y el resultado debería ser que se crea un fichero `ìndex.css` con

```css
body {
  background: magenta;
}
```

**¡Enhorabuena!¡Has ejecutado tu primera tarea con Gulp!**

### Tareas con _watch_

Hasta ahora hemos creado una tarea que convierte nuestro Sass a CSS, pero solo una vez. Si volvemos a modificar el fichero Sass tendremos que volver a ejecutar el comando `gulp` para convertirlo a CSS. ¿Pero esto es un poco rollo, no?

Escribiendo en la terminal `gulp` en realidad hemos ejecutado la tarea por defecto (`default`) del archivo `gulpfile.js`. Si veis en el `gulpfile`, creamos una tarea con `gulp.task` y el nombre de la tarea. La tarea por defecto tiene el nombre especial `default`. Pero podemos ejecutar otras tareas con `gulp nombre_tarea`.

Vamos a crear una tarea `watch` que está todo el rato observando nuestros ficheros Sass y al modificarlos genera a partir de su contenido un archivo CSS. Para eso, usamos este `gulpfile`:

```javascript
const gulp = require('gulp');
const sass = require('gulp-sass');

gulp.task('default', function(done) {
  gulp.src('scss/index.scss') // Leo el archivo scss
    .pipe(sass()) // Convierto el contenido del archivo index.scss a CSS
    .pipe(gulp.dest('css')); // El CSS generado lo guardamos en la carpeta css
    done();
});

// Tarea que observa cambios en 'scss'
// En su primera ejecución lanzará también las tareas que pasamos como segundo parámetro en la función, default en este caso
gulp.task('watch', gulp.series(['default'], function(done) {
  gulp.watch('scss/*.scss', gulp.series(['default']));  // Lanza la tarea 'default' cuando observa cambios en cualquier scss
  done();
}));
```

Ahora ejecutamos nuestra nueva tarea `gulp watch`. Una vez ejecutada, lo primero que hará será ejecutar `default` porque le hemos dicho que lo ejecute antes de comenzar `watch`. Tras ejecutar `default`, el proceso se quedará corriendo en la terminal y si realizamos algún cambio en alguno de los archivos Sass de nuestro proyecto veremos cómo en la terminal aparecen unos mensajes que muestran que se ha vuelto a ejecutar la tarea `default`. Si en algún momento queremos parar este proceso, podremos pulsar `Ctrl + C` en el teclado y el proceso terminará en ese momento.

Prueba a modificar el fichero Sass y ver que el CSS se modifica automáticamente.

#### EJERCICIO 1

Ahora vamos a trabajar con un proyecto que ya tiene configurado Gulp. Primero tendremos que clonarlo en nuestro ordenador y en la carpeta ejecutar `npm install` para instalar las dependencias.

https://github.com/Adalab/testing-Gulp

Luego probamos a ejecutar la tarea por defecto `gulp` y la tarea `gulp watch`. Observamos el resultado en la carpeta CSS. Investigad un poco el código y probad a comentar cosas para averiguar qué hacen las 2 nuevas funcionalidades que hemos añadido.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

Vamos a trabajar con otro proyecto para ver la verdadera utilidad de gulp. En este caso, vamos a trabajar con ficheros HTML parciales, es decir, porciones de HTML que vamos a poder incrustar en otro HTML. De esta forma vamos a poder trabajar con ficheros más pequeños, por ejemplo, tener en un fichero la cabecera que podremos importar en todas las páginas de nuestra web.

https://github.com/Adalab/testing-gulp-html-partials

Probamos a ejecutar la tarea `gulp html`, que inserta los parciales en el HTML y deja el resultado en una nueva carpeta `docs`. También probad a ejecutar la tarea por defecto con `gulp`, que se queda observando los cambios en el HTML y los parciales para crear el HTML resultado en `docs`. Observamos el resultado en la carpeta `docs`. Investigad un poco el código y ahora vamos a probar a:

- añadir contenido al fichero HTML principal y observar el resultado en `docs`
- modificar los parciales del proyecto y observar el resultado en `docs`
- identificar cómo podemos pasar información a los parciales a través de los atributos HTML
- crear un nuevo parcial para el footer

\_\_\_\_\_\_\_\_\_\_

### Bueno, ¿y ahora?

Ahora os hemos preparado un proyecto que os podéis descargar y donde integrar vuestros proyecto y ejercicios en Adalab:
[Adalab Web Starter Kit](https://github.com/Adalab/Adalab-web-starter-kit)

## Adalab Web Starter Kit

Hemos preparado una base para hacer proyectos o ejercicios durante el curso.
Usa Gulp para ejecutar una serie de tareas (procesar los scss, gestionar las imágenes, los JS...) y vamos a tener una estructura un poco diferente, más adaptada a un proyecto real.

Tendremos tres carpetas (por defecto solo viene una en el kit):

- **\_src/**: Donde tendremos nuestros archivos de trabajo: html, scss, js e imágenes
- **public/**: será donde se genere una versión de desarrollo, nosotras trabajaremos sobre los archivos de trabajo y gulp se encargará de pasarlos correctamente a esta carpeta. El servidor web se ejecutará aquí.
- **docs/**: esta es opcional y nos dejará generar una versión de producción de nuestro proyecto para que activemos GitHub Pages.

#### EJERCICIO 3

¿Quién sabe decir qué hace la tarea **styles**?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

¿Que diferencias hay entre la tarea **styles** y **styles-dist**?

\_\_\_\_\_\_\_\_\_\_

### Tareas incluidas

En el archivo `README.md` del proyecto tenéis información más detallada pero en resumen este kit tiene dos tareas principales:

- `gulp`
- `gulp docs`

### `gulp`

La tarea por defecto lanza un servidor web con BrowserSync y varios watchers estarán pendientes de los archivos SCSS/JS/HTML de la nueva carpeta **public/** para recargar el navegador cuando se necesite.
Además, aplica automáticamente autoprefixer a nuestros estilos, es decir, que añade todos los vendor prefixes adecuados `moz-`, `webkit-`, etc. Además agrupa todas la mediaqueries que hayamos creado en los SCSS y las coloca al final del documento CSS, de esta manera podemos escribir mediaqueries donde las necesitemos y ya Gulp se ocupará de agruparlas y colocarlas en su sitio.

### `gulp docs`

Esta tarea se ejecuta una sola vez y no lanza servidores web ni watchers, pero genera una versión lista para producción (para subirla a un servidor, activar GitHub Pages o enviar a nuestra clienta) en la carpeta **docs/**.

## Cómo usar el kit en nuestros proyectos

Hay dos formas de usar el kit, elegid la que más os guste:

Clonando el repo:

1. Desde un terminal clona el repo como ya hemos hecho en anteriores lecciones: `git clone <url-del-repo-de-github>`.
1. Entra en la carpeta que acabas de crear: `cd <caperta-del-repo>`.
1. Lista todos los ficheros y carpetas, incluidos los ocultos: `ls -a -l`.
1. Verás que hay una carpeta que se llama `.git`. Si la borramos, esta carpeta dejará de estar enlazada con el repo de GitHub.
1. Borra la carpeta `.git` con el comando `rm -rf .git`.
1. Ejecuta `npm install` para instalar las dependencias del proyecto.
1. Ejecuta `gulp` para arrancar el proyecto.
1. Empieza a utilizar el kit creando o copiando ficheros dentro de `_src`, editando el README.md...

Descargando el repo en un fichero:

1. Entra en GitHub y junto a la opción de clonar está la opción de descargar el repo en un ZIP.
1. Descárgalo a tu ordenador y descomprímelo.
1. Ejecuta `npm install` dentro de la carpeta del proyecto para instalar las dependencias.
1. Ejecuta `gulp` para arrancar el proyecto.
1. Empieza a utilizar el kit creando o copiando ficheros dentro de `_src`, editando el README.md...

En ambos casos, si quieres conectar el proyecto que acabas de crear con un repositorio en GitHub debes hacer lo que aprendimos en lecciones anteriores... (pista: `git remote ...`).

#### EJERCICIO 5

Seguiremos los pasos anteriores para crear un nuevo proyecto usando el kit de Adalab. Después, en esta misma carpeta meteremos un ejercicio de la sesión de responsive para probar que se lanza el navegador que se actualiza solo con los cambios que hacemos en el HTML o CSS. Comprobad que la carpeta donde debemos meter el código de nuestro proyecto es **\_src**.

Una vez terminado, vamos a probar una opción muy chula del kit: la posibilidad de trabajar con ficheros parciales de HTML. Para eso, mirad el ejemplo de la carpeta `_src/templates` donde hay un fichero `index.html` que carga 2 ficheros parciales con trozos de HTML. En vuestro proyecto cread esta misma estructura y sacad la cabecera y el pie de página de la web a un parcial.

Para terminar, vamos a publicar la web usando GitHub Pages. Para eso usaremos la tarea `gulp docs` que genera una carpeta docs con la web preparada para subirla a GitHub Pages.

\_\_\_\_\_\_\_\_\_\_

## Rutas de ficheros en Starter Kit

Las rutas que escribimos en un fichero, por ejemplo en un scss escribimos `background-image: url('../images/logo-adalab-80px.png')`, nos sirven para relacionar dos ficheros. En el fichero de origen se indica dónde está el fichero de destino. Si las rutas están bien, el navegador sabrá dónde ir a buscar el fichero de destino.

Con las rutas se puede trabajar de dos maneras:

**Con rutas absolutas:** para mostrar la imagen de fondo, en `_src/assets/scss/main.scss` podríamos poner la ruta absoluta `http://localhost:3000/assets/images/logo-adalab-80px.png`. Esta es una ruta absoluta porque indica la dirección completa del fichero.

**O con rutas relativas:** en el fichero `_src/assets/scss/main.scss` tenemos la ruta relativa `../images/logo-adalab-80px.png`. Esto nos indica el siguiente camino o ruta:

1. Estamos el fichero `main.scss`.
1. `../` indica que subimos a la carpeta madre, es decir `assets/`.
1. Desde `assets/` buscamos el fichero `images/logo-adalab-80px.png`.

Esta ruta es relativa porque relaciona ficheros de la carpeta `sccs/` con ficheros de la carpeta `images/`, independientemente de dónde estén estas dos carpetas. Siempre que estas dos carpetas sean hermanas, la ruta funcionará y el navegador encontrará la ruta de destino.

Siempre preferimos rutas relativas porque las rutas absolutas solo funcionan en el servidor local `localhost:3000`. Si publicamos nuestro proyecto en un servidor para todo el mundo la web no se vería correctamente.

Como ya hemos visto, al hacer `gulp` en la terminal se crea una carpeta dentro de nuestro proyecto llamada `public/` con todos nuestras carpetas y ficheros. La carpeta `public/` funciona como servidor web. Con los ficheros `config.json` y `gulpfile.js` hemos hecho que la estructura de carpetas y ficheros de `_src/` se replique exactamente igual en `public/`.

Pero esto no siempre es así :(

A veces queremos (o necesitamos) que la estructura de carpetas en `public/` sea diferente. Y por ello tenemos que cambiar las rutas en nuestro código.

> **IMPORTANTE**: las rutas deben estar correctamente escritas en el código que esté en `public/`, porque ese es el código que estará en el servidor, esos son los ficheros que verán las usuarias de la web.

#### EJERCICIO 6

Hoy a venido la desarrolladora DevOps de la empresa y nos pide que la carpeta de imágenes se tiene que llamar `img/` porque así está en el resto de proyectos de la empresa, y le simplifica la gestión de los servidores. Para ello:

1. Arranca el proyecto con `gulp` y busca la carpeta `images/` dentro de la carpeta `public/`. Observa dónde se ha creado.
1. Para `gulp` y borra la carpeta `public/`.
1. Edita el fichero `config.json` > `images` > `dest` cambiando `public/assets/images/` por `public/assets/img/`.
1. Vuelve a arrancar el proyecto y busca en qué carpeta se han creado ahora las imágenes.
1. Como siempre, después de cualquier cambio tenemos que comprobar que no se ha roto nada. Mira la página en el navegador y verás que la imagen de fondo con el logotipo de Adalab ha desaparecido. OMG!! pues tenemos que arreglarlo.
1. Abre el _Devtools_ de _Chrome_, entra en la pestaña de _Console_ y mira el mensaje de error que aparece. ¿Qué nos está diciendo?
1. Arregla este error sin modificar el fichero `config.json`.

\_\_\_\_\_\_\_\_\_\_

## BONUS: Más plugins de Gulp

Hasta ahora hemos usado plugins de Gulp para trabajar con Sass y CSS. Plugins son todas las pequeñas librerías que hemos ido instalando con `npm install` como `gulp-sass`. Pero existen plugins para otras muchas funcionalidades. Vamos a ver algunos.

### Plugins para JavaScript

También existen tareas de Gulp que nos permiten mejorar nuestro flujo de trabajo con JavaScript. Algo habitual es tener varios ficheros JavaScript en un proyecto, pero en producción siempre es mejor que el navegador cargue uno solo. Para eso existe una tarea para concatenar (`concat`) todos los ficheros JS en uno solo. También suele ser habitual minificar el código (eliminar espacios, cambiar nombres de variables a una letra, etc.) para que vaya más rápido.

Podéis ver un ejemplo de cómo trabajar con esto en este repositorio que preparó un voluntario del curso: https://github.com/luisddm/Gulp-adalab

### Plugins de linting

Un _linter_ es un programa que detecta errores de uso y/o estilo en un código. Ahora mismo en el propio Code tenemos instalados varios linters que nos informan de errores en el código o en su estilo (llaves que no cierran, etc.). También podemos usar esos linters desde una tareas de Gulp, de forma que nos digan errores antes de, por ejemplo, subir un código a producción. Algunos ejemplos son [JSLint](http://www.jslint.com/) o [CSSLint](http://csslint.net/).

### Plugins para trabajar con imágenes

Existen plugins para optimizar imágenes, es decir, que pesen menos para nuestra web, por ejemplo, `gulp-imagemin`.

### Plugins para trabajar con ficheros

Plugins para copiar ficheros, por ejemplo, copiar las fuentes a nuestra carpeta con el proyecto para producción. O renombrarlos, por ejemplo, los ficheros minificados suelen llevar un `.min.` antes de su extensión. También borrar ficheros intermedios que ya no queremos.

## Recursos externos

- [Documentación oficial de Gulp](https://Gulpjs.com/)
- [Gulp for beginners](https://css-tricks.com/Gulp-for-beginners/)

