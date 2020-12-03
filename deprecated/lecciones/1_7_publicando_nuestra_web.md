# Publicando nuestra web

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
- [EJERCICIO 12](#ejercicio-12)

<!-- /TOC -->

## Introducción

La lección de hoy es amplia y variada. Vamos a aprender a trabajar con la terminal, una herramienta fundamental en la programación. También vamos continuar avanzando con nuestros conocimientos de Git y GitHub. Y al final de la lección vamos a aprender cómo publicar nuestra web en el servidor de GitHub Pages.

> **Nota:** La lección de hoy es doble, en ella hablamos de la terminal y de Git / GitHub. Debemos repartir nuestro tiempo de estudio entre ambas partes.

## La terminal

> **Nota:** Antes de comenzar a trabajar con la terminal debes haber realizado la [Guía de instalación de la terminal](../instalacion/instalacion_de_la_terminal.md).

**La terminal, también llamada consola de comandos, es una herramienta fundamental** para la programación. Su finalidad es ejecutar **comandos u órdenes** mediante instrucciones. Estos comandos son similares a las interacciones que haríamos en una aplicación normal (clics, escribir en campos, cambiar de sección, etc.) pero en este caso se hacen **escribiendo órdenes** en una terminal de comandos.

Muchas de las herramientas para programación están hechas sin interfaz porque son **tan sencillas que no merece la pena** hacer un interfaz o **son tan complejas que no se puede hacer un interfaz gráfica** que tenga todas las funcionalidades posibles. La solución es usar la terminal.

Cuando una persona utiliza un programa como VS Code o Chrome está utilizando **una interfaz gráfica que transforma nuestras acciones en órdenes** que le envía al sistema operativo a través de una terminal. Es decir las aplicaciones son intermediarias. Cuando utilizamos la terminal directamente **no hay nada que se interponga entre el sistema operativo y nosotras**. Tenemos todo el poder, y toda la responsabilidad claro ;)

![Terminal de ubuntu](assets/images/1-7/terminal-ubuntu.png)

Como vemos en la imagen, la terminal nos muestra una línea, el **prompt**, a partir de la cual podemos escribir nuestros comandos. El prompt está compuesto por:

- Nombre del usuario con el que hemos iniciado sesión en el ordenador.
- @
- Nombre del equipo u ordenador.
- Ruta de la carpeta en la que está ahora mismo la terminal:
   - Puede ser la ruta absoluta de una carpeta.
   - Puede ser `~` que es una abreviatura de la carpeta **home** del usuario.
- Por último el símbolo del dólar, que es simplemente para saber dónde termina el prompt y dónde podemos empezar a escribir un comando.

Ejemplos:

```shell
ubuntu@ubuntu: ~$
```

```shell
maricarmen@portatil-del-trabajo: /mnt/c/Users/maricarmen/Desktop/Adalab/ejercicios$
```

> **Nota:** A veces, en nuestros materiales o en Internet, encontraremos ejemplos de comandos precedidos por el símbolo del dólar, por ejemplo `$ pwd`. Es una manera de decir que es un comando de terminal. Nosotras no debemos escribir el `$` en la consola.

Y ya que hemos hablado de las rutas no podemos continuar con la explicación de la terminal, sin antes explicar lo qué son la rutas absolutas y relativas.

### Rutas absolutas

Las rutas absolutas indican la **dirección completa** de una carpeta o fichero:

- Siempre empiezan con `/`. La `/` es la ruta raíz del ordenador.
- Si usamos una ruta absoluta **indicamos el camino que hay que recorrer desde la carpeta raíz** del ordenador a una carpeta o fichero.
- Por ejemplo `/user/maricarmen/adalab/proyectos/modulo-1/`.
- Por ejemplo `/user/maricarmen/adalab/proyectos/modulo-1/index.html`.
- Por ejemplo `/mnt/c/Users/maricarmen/adalab/proyectos/modulo-1/index.html`.

### Rutas relativas

- Las rutas relativas indican **el camino que hay que recorrer** para ir desde la carpeta en la que estoy ahora mismo a otra carpeta o fichero.
- La ruta relativa más simple es `../` (dos puntos barra). Esta ruta **indica la carpeta madre o carpeta superior respecto a la carpeta actual**. Si la ruta relativa es el camino a recorrer, escribiendo la ruta `../` vamos de la carpeta actual a la carpeta madre. Si escribimos la ruta `../../` vamos de la carpeta actual a la carpeta abuela. Y así sucesivamente...
- Otra ruta relativa muy simple es `./` (punto barra). Esta ruta indica la carpeta en la que estoy, mi carpeta actual. Si la ruta relativa es el camino a recorrer, escribiendo la ruta `./` vamos de la carpeta actual a la carpeta actual. Esto parece que no tiene mucho sentido, en seguida veremos que sí lo tiene.

Vamos a ver un ejemplo de rutas relativas:

```
adalab/
├ proyectos/
├─┬ modulo-1/
│ └┬─ css/
│  │  └─ styles.css
│  ├─ images/
│  │  └─ logo.jpg
│  └─ index.html
└─ modulo-2/
```

Pensemos que estoy en la carpeta `proyectos/` y quiero *caminar* hasta la carpeta `modulo-1/`. La ruta a usar es `./modulo-1/`. Es decir, desde `proyectos/` entro en `modulo-1/`.

Ahora pensemos que estoy en la carpeta `proyectos/` y quiero *caminar* hasta la carpeta `images/`. La ruta a usar es `./modulo-1/images/`. Es decir, desde `proyectos/` entro en `modulo-1/`. Después desde `modulo-1/` entro en `images/`.

Ahora pensemos que estoy en la carpeta `css/` y quiero entrar en la carpeta `images/`. La ruta a usar es `../images/`. Primero subo a la carpeta madre que es `modulo-1/` pero no necesito saber el nombre de la carpeta madre porque me vale con poner `../`. Desde la carpeta madre entro en la carpeta `images/`.

### Rutas dentro de ficheros

Cuando nos movemos por la terminal podemos usar rutas absolutas o relativas.

Pero **cuando escribimos la ruta desde dentro de un fichero a otro fichero debemos usar siempre rutas relativas**. Esto se debe a que cuando estamos programando una página, los ficheros están en mi ordenador. Pero si los subo a GitHub y una compañera se los baja, ella los tendrá en una ruta absoluta diferente a la mía.

Por ejemplo desde un `index.html` importamos la hoja de estilos usando `<link rel="stylesheet" href="./css/styles.css">`. Usamos `./css/` para ir desde `index.html` a `styles.css`.

Pasa lo mismo cuando desde un fichero `styles.css` usamos una ruta a una imagen de fondo `background-image: url('../images/hero.png);`. Usamos `../images/` para ir desde `index.html` a `styles.css`.

> **BRICONSEJO:** Acuérdate de este importante consejo. Cuando pongas la ruta de un fichero dentro de otro, la ruta debe empezar con `./` o `../`. Siempre. Sin excepciones. Si alguna vez no lo haces, antes o después tendrás problemas y acabarás acordándote de este briconsejo.

Y ahora que ya sabemos cómo funcionan las rutas podemos aprender los principales comandos de la terminal. Te recomendamos que abras una consola y los pruebes.

### pwd (print working directory)

Principalmente usaremos la terminal para movernos por el sistema de archivos y carpetas del ordenador. Así que es fundamental saber dónde estamos en cada momento. El comando `pwd`se encargará de mostrarnos en qué carpeta nos encontramos.

```shell
pwd
```

Devolverá la ruta absoluta de la carpeta en la que estemos, con este aspecto:

```shell
/user/nombre-de-usuario
```

Nos estaría indicando que nos encontramos en la carpeta `nombre-de-usuario`, que está dentro de `user`, que está en la carpeta raíz de nuestro equipo.

Si estás trabajando en un Ubuntu integrado dentro de Windows 10 y pruebas `pwd` verás que el resultado es:

```shell
/mnt/c/Users/nombre-de-usuario
```

Es decir, en Windows 10 las unidades de nuestro ordenador como `c:\` se montan dentro de `/mnt/`, por ello la ruta `c:\Users\maricarmen` corresponde con `/mnt/c/Users/maricarmen`.

### ls (list)

El comando `ls` nos muestra un listado de los archivos y carpetas que hay en la carpeta actual.

```shell
ls
```

Podemos usar la opción especial `ls -A` para listar también los ficheros y carpetas ocultos. Los ficheros y carpetas ocultos empiezan por `.` y por defecto no se ven ;). Por ejemplo un fichero oculto es `.gitignore`.

```shell
ls -A
```

### cd (change directory)

El comando `cd` nos ofrece diferentes posibilidades a la hora de cambiar de carpeta. Para entrar en una carpeta hija de la carpeta actual usamos:

```shell
cd nombre-de-carpeta-hija
```

O lo que es lo mismo:

```shell
cd ./nombre-de-carpeta-hija
```

Podemos encadenar varios nombres de subcarpetas separadas por `/` para llegar hasta una ruta más profunda:

```shell
cd nombre-de-carpeta-hija/carpeta-nieta/carpeta-bisnieta
```

También podemos escribir la ruta absoluta desde la raíz de nuestro equipo `/` a la carpeta a la que queremos entrar.

```shell
cd /ruta/absoluta/a/una/carpeta
```

Podemos escribir solo `cd` y nos mueve a la carpeta de nuestro usuario:

```shell
cd
```

`..` nos permite subir a la carpeta madre, esto es, ir a la carpeta que contiene nuestra carpeta actual

```shell
cd ..
```

O lo que es lo mismo:

```shell
cd ../
```

Y para ir a la carpeta hija de mi carpeta madre, lo que en cristiano significa ir a la carpeta prima:

```shell
cd ../carpeta-de-mi-prima-hermana
```

Este comando permite **deshacer o desandar** el último `cd` realizado. Vuelve a la localización anterior al último cambio de carpeta.

```shell
cd -
```

### mkdir (make directory)

Nos permite crear una carpeta. Pero no entra en la carpeta, solo la crea.

Para crear la carpeta `proyecto` escribimos el comando:

```shell
mkdir proyecto
```

Casi todos los comandos los podemos combinar con lo que ya sabemos de las rutas. Por ejemplo para crear una carpeta `proyecto` en la carpeta superior escribimos el comando:

```shell
mkdir ../proyecto
```

Y por ejemplo para crear una carpeta `proyecto` en la raíz del ordenador escribimos el comando:

```shell
mkdir /proyecto
```

### touch

Nos permite crear un nuevo archivo. Al igual que el comando `mkdir` se puede combinar con lo que ya sabemos sobre rutas. Para crear el fichero `index.html` usamos el comando:

```shell
touch index.html
```

En algunas terminales de Ubuntu y Windows también podemos limpiar usando los atajos de teclado `ctrl + l` o `ctrl + k`. Si estamos en Mac son `cmd + l` o `cmd + k`.

### cp (copy)

Para copiar ficheros (o carpetas) usamos el comando `cp` seguido del fichero (o carpeta) de origen, un espacio y la ruta del fichero (o carpeta) de destino:

```shell
cp fichero-de-origen.html ../carpeta-de-destino/fichero-de-destino.html
```

### mv (move)

Para mover ficheros (o carpetas) usamos el comando `mv` seguido del fichero (o carpeta) de origen, un espacio y la ruta del fichero (o carpeta) de destino:

```shell
mv fichero-de-origen.html ../carpeta-de-destino/fichero-de-destino.html
```

Este comando también sirve para renombrar, ya que renombrar un fichero de `a.html` a `b.html` es lo mismo que moverlo.

```shell
mv a.html b.html
```

### clear

A veces pasa que hemos introducido muchos comandos y sería genial poder limpiar la ventana. Para eso existe el comando `clear`.

```shell
clear
```

### Historial de comandos

Para movernos por los últimos comandos ejecutados usamos la teclas de flecha para arriba ⬆️ y para abajo ⬇️. Así nos ahorramos volver a escribir lo mismo muchas veces.

Si queremos buscar un comando en el historial, podemos usar `ctrl+r` y comenzar a escribir el comando para buscarlo.

### Ayuda y opciones

Si no sabemos cómo funciona un comando pediremos ayuda a la terminal. Por ejemplo para saber cómo funciona el comando `ls` escribimos:

```shell
ls --help
```

El terminal mostrará una explicación de cómo se utiliza el comando y las opciones que se pueden utilizar. Con esta información sabremos que para listar el contenido de un directorio en orden inverso podemos escribir:

```shell
ls --reverse
```

o

```shell
ls -r
```

Os aconsejamos que cada vez que aprendáis un comando nuevo miréis la ayuda para ver qué posiblidades tiene.

#### EJERCICIO 1

Utilizando solo la terminal, id a vuestra carpeta de ejercicios de esta lección y cread la siguiente estructura de carpetas y archivos (vacíos):

```txt
nombre
└┬─ datos
 │ └─ mis-datos.txt
 └─ proyecto
   └─ ruta-del-proyecto.txt
```

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

Desde la terminal, vamos a crear un nuevo proyecto en nuestra carpeta de ejercicios que se llame `rutas-relativas`, con la siguiente estructura

```
rutas-relativas/
├─ styles/
│  └─ styles.css
├─ images/
│  └─ mi-foto.jpg
└─ index.html
```

A continuación, editando el archivo `index.html` en VS Code se tiene que ver la imagen de dos formas:

1. Con un `<img>`.
1. Como fondo de un `div` del mismo tamaño que la imagen.
1. ¿Cómo es la ruta de ambas imágenes? ¿Absoluta? ¿Relativa?
1. ¿Es diferente en los dos casos? ¿Por qué?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

A través de la terminal entra en la carpeta del ejercicio 1 y investiga el comando `ls` para conseguir:

- Listar el contenido de la carpeta para ver los nombres, propietarios y tamaño de los ficheros y carpetas.
- Listar el contenido de la carpeta para mostrar solo el nombre de los ficheros y carpetas en formato columna.
- Listar (con un solo comando) el contenido de la carpeta para ver los nombres, propietarios y tamaño de los ficheros y carpetas, incluyendo las subcarpetas y subarchivos.
- Repertir los ejercicios anteriores pero además mostrando los ficheros ocultos.

En cada caso mira detenidamente toda la información que muestra la columna.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

A través de la terminal:

- Copia la carpeta `rutas-relativas` del ejercicio 2 en la carpeta `rutas-relativas-2`.
- Copia la carpeta `rutas-relativas` del ejercicio 2 en la carpeta `rutas-relativas-3` con la opción `verbose` y observa qué aparece en la terminal.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 5

A través de la terminal:

- Renombra (o mueve) la carpeta `rutas-relativas-2` del ejercicio anterior, y ponle el nombre `nuevas-rutas-relativas`.

\_\_\_\_\_\_\_\_\_\_

## Git y GitHub

> **Nota:** Antes de comenzar a trabajar con Git y GitHub debes haber realizado la [Guía de instalación de Git](../instalacion/instalacion_de_la_terminal.md).

Como hemos explicado anteriormente, [GitHub](https://github.com) es una **plataforma de desarrollo colaborativo** para alojar proyectos utilizando el sistema de control de versiones de Git. Está muy enfocada a proyectos de código abierto y la verdadera fuerza de GitHub está en la comunidad tan grande que se ha montado sobre la idea de código abierto u **open source** :)

Hay que tener en cuenta que GitHub es una empresa que ofrece el servicio de repositorios Git, pero hay muchas otras plataformas que hacen lo mismo como por ejemplo [Bitbucket](https://bitbucket.org/) o [GitLab](https://gitlab.com).

#### EJERCICIO 6

Poneros, ambas compañeras, una imagen de perfil en vuestras cuentas de GitHub. No tiene por qué ser una fotografía.

\_\_\_\_\_\_\_\_\_\_

### Crear un repositorio

Con Git hay dos formas de crear un repositorio, lo podemos crear en nuestro ordenador y luego enlazarlo con GitHub o bien lo podemos crear en GitHub y luego clonarlo en nuestro ordenador. Es más cómoda la segunda opción, así que vamos a ver un [vídeo sobre cómo crear un repositorio en GitHub](https://www.youtube.com/watch?v=MGf3K6qxptg):

{% embed url="https://www.youtube.com/watch?v=MGf3K6qxptg" %}

En este vídeo hemos aprendido a clonar un repo:

```bash
git clone url-del-repositorio
```

### Añadir cambios a un repositorio

Una vez que hemos creado y clonado un repo, vamos a empezar a trabajar con él en [este vídeo](https://www.youtube.com/watch?v=QQOHttHNtY0):

{% embed url="https://www.youtube.com/watch?v=QQOHttHNtY0" %}

En este vídeo hemos aprendido a añadir todos los cambios al futuro commit:

```bash
git add -A
```

O añadir los cambios solo de algunos ficheros al futuro commit:

```bash
git add index.html
```

También hemos aprendido a crear una nueva versión de nuestro código, a la que llamamos commit:

```bash
git commit -m "Commit message"
```

> **IMPORTANTE:** Antes de hacer un commit debemos repasar que el código que vamos a subir está bien, es decir, debemos limpiarlo con el fin de tener el historial de Git lo mejor posible. ¿Y qué es limpiar el código? Pues, por ejemplo, eliminar comentarios que no hagan falta, borrar propiedades CSS duplicadas, reorganizar el código para que sea más fácil de leer por otra persona, formatear el cógido...

**Mensaje del commit**

Hemos visto que cada commit lleva su mensaje. Este mensaje debe ser suficientemente corto para que no sea una locura leerlo y, a la vez, explique qué cambio se ha hecho de forma clara.

Normalmente **trabajamos con otras compañeras** en un mismo proyecto y **es fundamental que todas entiendan qué se ha hecho en cada paso** para poder trabajar de forma más rápida y no tener que estar preguntando qué es cada cosa. Crear mensajes claros en los commits, nos servirá también para que si volvemos a ver un commit del pasado, podamos entender qué es lo que hicimos.

A la hora de escribir un mensaje para un commit hay múltiples maneras de plantearlo e infinidad de guías. Como estamos empezando tengamos en cuenta sólo la siguiente serie de normas para crear un mensaje lo suficientemente bueno:

- Debe estar escrito en **inglés**.
- Tiene que ser corto. Máximo 72 caracteres.
- Debe explicar brevemente y a nivel general los cambios que se han hecho (añade el footer, corrige los enlaces del artículo, etc.).
- No tiene que detallar los cambios hechos en el código, sino en general. Recordemos que ya tenemos un control de versiones que muestra, exactamente, qué se ha hecho. (Ejemplo: no pongáis "Add 2 paragraph tags", poned mejor "Add introduction text").
- **Usaremos el imperativo** (Ejemplo: `Change header styles` - Cambia los estilos del header) para decir qué hace el commit.

Un ejemplo de un buen commit:

```
$ Git commit -m "Fix typo in article title"
```

Hemos aprendido a subir el código al repo remoto:

```bash
git push
```

Y por último hemos aprendido a bajar el código desde repo remoto:

```bash
git pull
```

Madre mía qué útil es el comando status, lo uso sin parar:

```bash
git status
```

> **Nota:** Hemos creado una [guía sobre Git](../guias/git_github.md) donde recopilamos todos los contenidos que aprendemos durante el curso.

#### EJERCICIO 7

1. Vamos a crear un repositorio en GitHub, al que llamaremos `testing-git`.
1. Lo clonamos en nuestro ordenador.
1. Dentro de él, creamos un archivo `index.html` con un título en el `<head>` en el que ponga "Testing Git" y un `h1` con el mismo texto.
1. Además, crearemos un archivo para los estilos (`main.css`) dónde añadiremos un estilo para que la familia de texto que se use en la web sea `sans-serif`. Organizaremos el proyecto siguiendo la estructura de siempre:
    ```txt
    testing-git
    ├─ styles
    │  └─ main.css
    └─ index.html
    ```
1. Vamos a añadir los cambios al futuro commit con `git add`.
1. A continuación creamos el primer commit con `git commit`.
1. Subimos nuestro código al repositorio remoto con `git push`.
1. Observa si se han subido los cambios a GitHub.

#### EJERCICIO 8

Modificar el archivo `index.html` para que en el título de la página ponga "My first Git project" y en el texto de la cabecera aparezca una sonrisa `:)`. Añadir los cambios y hacer un commit para guardarlos.

> **Nota:** El mensaje del commit deberá explicar de forma clara los cambios que hemos realizado.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 9

Vamos a realizar un tercer cambio dónde añadiremos un archivo `README.md` en la raíz de nuestro proyecto. Este archivo se utiliza para poner información acerca de nuestro código y, por defecto, la web GitHub lo muestra en la página principal de nuestro proyecto. Dentro de ese archivo escribiremos el siguiente texto:

```markdown
## My first Git project

Dummy project to learn Git basics.
```

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 10

1. Vamos a clonarnos el repositorio que ha hecho nuestra compañera.
1. A continuación modificamos su index.html añadiendo un párrafo con el texto: **¡¡¡Esto es un proyecto colaborativo!!!**.
1. Subimos el código al repositorio remoto.

> **Nota:** si al intentar subirlo te da un error diciendo que no tienes permisos, la propietaria del repo debe ir al repo de GitHub > Settings > Manage access > Invitar a su compañera al repositorio.

\_\_\_\_\_\_\_\_\_\_

### Crear un repo en local y conectarlo

Algunas veces, vamos a querer crear un repositorio en local y conectarlo con GitHub. Os vamos a explicar cómo hacerlo. Esta es una opción que se usa poco, por ello queremos que sepáis que existe, para que si algún día necesitamos hacerlo, en ese momento, buscamos la información en esta lección o en Internet, lo aprendemos en el momento y lo hacemos.

Básicamente tenemos que **crear un repositorio en una carpeta de mi ordenador** con el comando `git init`:

```bash
git init nombre-de-carpeta
```

A continuación entramos en la carpeta creada y empezamos a trabajar. Cuando queramos hacemos `git add -A` y `git commit -m "My message"`. No podemos hacer `git push` porque no tenemos un repo remoto donde subir el código.

A continuación creamos un repo en GitHub y lo enlazamos con el repo de nuestro ordenador, con el comando:

```bash
git remote add origin url-del-repositorio-que-me-da-github
```

A partir de este momento ya podemos trabajar normalmente y hacer `git push`, `git pull` o lo que queramos.

## GitHub Pages

Como hemos comentado previamente, GitHub ofrece un servicio llamado [GitHub Pages](https://pages.GitHub.com) que pueden utilizar los usuarios como hosting gratuito para los proyectos que estén alojados en GitHub.

Un hosting es un servicio de almacenamiento de ficheros para poder tener tu web en un servidor y que esté disponible en Internet y esto es lo que ofrece exactamente GitHub Pages.

Para activar el servicio de GitHub Pages en un repositorio hay que:

1. Ir al repositorio en GitHub.
1. Ir a la pestaña settings.
1. Ir al apartado GitHub Pages.
1. Seleccionar la opción **Master branch**.
1. Al hacerlo nos genera una URL donde podemos ver nuestro repositorio.
1. Normalmente tarda 5 minutos en publicar el repositorio, así que espera 5 minutos y...
1. Entra en la URL que ha generado, verás tu página.
   - Si ves el contenido del README.md es porque no tienes un fichero `index.html`.
1. Para facilitarle la vida a los usuarios que vean tu repo vamos poner la URL en la portada del repo:
   1. Vamos a la página principal del repo.
   1. Debajo de la pestaña de **Settings** hay un botón que pone **Edit**, púlsalo.
   1. Ahí puedes editar la descripción y URL del proyecto.
   1. Pega la URL que te ha generado GitHub Pages en Website.

#### EJERCICIO 11

Publica tu repo `testing-git` con GitHub Pages y pon la URL en la portada del repo.

## Github Classroom

GitHub Classroom es un "módulo" de GitHub que permite automatizar el control de acceso y la creación de repositorios. Durante este curso lo usaremos para asignar ejercicios.

#### EJERCICIO 12

Haz clic en el siguiente enlace [https://classroom.github.com/a/cdZUSdeT](https://classroom.github.com/a/cdZUSdeT) para crear tu primer repositorio a través de GitHub Classroom, y luego:

1. Clónalo en tu equipo.
1. Crea un archivo `README.md`.
1. Dentro, escribe tu nombre precedido de un `#`: `# PEPA HERRERA`.
1. Haz `add` y `commit`.
1. Haz un `push` al repo remoto :)

\_\_\_\_\_\_\_\_\_\_

## Recursos extra

##### Personaliza la terminal

- [Prompt coloreado](https://www.howtogeek.com/307701/how-to-customize-and-colorize-your-bash-prompt/)
- [Prompt con información del repo GIT](https://sujipthapa.co/blog/Git-pro-tip-show-your-branch-on-linux-ubuntu-terminal)

##### Pro Git

Como recurso extra para aprender Git, el libro de "Pro Git" es uno de los mejores. Está escrito por dos desarrolladores que trabajaron en implementar libgit, el sistema que utiliza GitHub en el núcleo de su plataforma para lidiar con Git. Aparte, ambos han formado parte del desarrollo de Git y la comunidad que mantiene este software, por lo que saben muy bien de lo que hablan. El libro está explicado de forma sencilla y fácil de entender y es gratuito.

> **Nota:** Es un libro bastante denso pero los capítulos 1 y 2 se centran en lo básico, por lo que puede ser interesante leer estos y en el futuro leer el resto.

- [Enlace a la página del libro Pro Git (versión inglesa y más actual)](https://Git-scm.com/book/en/v2)
- [Enlace a la página del libro Pro Git (versión española, menos actual y no disponible para descargar)](https://Git-scm.com/book/es/v2)
