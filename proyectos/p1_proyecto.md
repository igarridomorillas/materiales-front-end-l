# Proyecto 1: Contact us!

<!-- TOC START min:2 max:3 link:true update:true -->

- [Resumen (TL;DR)](#resumen-tldr)
- [Objetivos](#objetivos)
- [Caso de uso](#caso-de-uso)
- [Especificaciones](#especificaciones)
- [Hitos](#hitos)
- [Entrega](#entrega)
- [Recursos](#recursos)

<!-- TOC END -->

## Resumen ([TL;DR](https://spanish.stackexchange.com/questions/15317/hay-alg%C3%BAn-equivalente-en-castellano-al-ingl%C3%A9s-tldr))

En este proyecto vamos a desarrollar nuestra primera web colaborativa. Para ello crearemos una web con la información social de todos los miembros del equipo. De cara a vuestro CV online (o LinkedIn) es muy importante dar visibilidad de que habéis hecho trabajo en equipo. ¡Esta será vuestra primera experiencia de trabajo en equipo relacionada con programación!

## Objetivos

1. Consolidar el aprendizaje de las tecnologías del módulo Hola Mundo (HTML, CSS, diseño responsive, GitHub pages, Sass, grid, gulp)
1. Utilizar control de versiones en equipo para aprender las ventajas y conflictos que genera
1. Implementar Scrum como marco de referencia para el desarrollo del producto, basándonos siempre en los valores de Agile como puntos clave del trabajo en equipo y la mejora continua
1. Mejorar la comunicación entre los miembros del equipo
1. Mejorar vuestras habilidades de comunicación en público al presentar el trabajo y exponer el resultado como parte de los Sprint Reviews y la presentación final de proyecto

## Caso de uso

Con esta web del equipo podréis ilustrar este primer proyecto realizado en Adalab en vuestro perfil de LinkedIn, añadiendo al resto de compañeras y el enlace al código en GitHub. De esta forma, las empresas podrán ver que, durante el programa Adalab, habéis adquirido experiencia de trabajo en equipo y podrán acceder fácilmente al código que habéis desarrollado.

## Especificaciones

Se desarrollará una página web con las siguientes características:

- Uso de HTML y Sass (al principio usaréis CSS pero la versión final debe usar Sass)
- Uso de mediaqueries y otras técnicas de diseño _responsive_ para que la web se adapte al tamaño de pantalla de distintos dispositivos
- Uso de git para el control de versiones del proyecto
- Publicación del resultado en Internet usando GitHub Pages

La web tendrá varias páginas:

- una página principal (_Home_) con la información principal sobre el equipo
- una página de contacto con un formulario para que puedan ponerse en contacto con vosotras
- opcionalmente, una página por cada componente del equipo con información más detallada sobre cada una

Todas las páginas tendrán una cabecera (header) y un pie de página (footer). En la cabecera aparece el nombre del equipo y un menú de navegación que debe mantenerse fijo en la parte superior de la ventana al hacer scroll. En el pie de página aparece el copyright, otro menú y el logo de Adalab.

![Home](assets/images/s1-home-1200.png)

En la página principal, aparece

- una foto del equipo
- la frase (_claim_) del equipo
- una sección "equipo" con la descripción del mismo (por qué os identificáis como equipo, cosas que tenéis en común) y vuestras fortalezas y debilidades
- una sección de "quiénes somos" con información resumida de cada miembro del equipo: nombre, foto, breve bio y enlaces sociales (Twitter, LinkedIn, GitHub y correo)

![Contact](assets/images/s1-contact-1200.png)

En la página de contacto habrá un formulario que recoge información de contacto como nombre completo, email, teléfono y mensaje, y un botón para poder enviarlo.

Las páginas principal y de contacto tienen un diseño establecido, al que debéis ajustaros lo máximo posible. El diseño está realizado para 3 tamaños de dispositivo:

- móvil, por debajo de 768px
- tablet, desde 768px hasta 1200px
- desktop, a partir de 1200px

Para las páginas de cada componente del equipo, el diseño es libre pero siguiendo la guía de estilo del resto de la web.

Podéis descargar un [archivo ZIP](assets/zip/proyecto1.zip) con los diseños e indicaciones en tres carpetas:

- **pantallas**, con los diseños
- **medidas** con indicaciones de dimensiones, márgenes y paddings
- **tipografía** con indicaciones de los tamaños, colores y fuentes de cada elemento.

### Logo, iconos tipografía y paleta

El logo de Adalab se puede descargar de [aquí](assets/images/logo-adalab.png)

Los iconos sociales los podéis sacar de [Font Awesome](https://fontawesome.com/), donde también podéis aprender a cómo usarla.

Las tipografías usadas en el diseño son Open Sans y Rubik, disponibles en Google Fonts.

#### Colores

- Verde oscuro: #099d8d
- Verde claro: #14d9c4
- Blanco: #ffffff
- Negro: #000000
- Gris oscuro: #54585a
- Gris claro: #b8b8b9
- Gris de fondo: #f1f1f1

### Zeplin

**Zeplin** es una aplicación para poder compartir un diseño con desarrolladores sin necesidad de que usen aplicaciones como Sketch, Illustrator o Photoshop, y con mucha más información que unos pantallazos.

Podéis ver un pequeño [tutorial en Youtube](https://www.youtube.com/watch?time_continue=12&v=tbKZAGthUgQ).

Se puede acceder al diseño directamente desde el navegador para lo que necesitaréis una cuenta de zeplin (que se puede conseguir de forma gratuita desde su página).

URL del proyecto: https://zpl.io/aXkApkx

## Planificación del proyecto

### Sprints

Para la realización de este proyecto trabajaremos en _2 sprints_ (2 iteraciones) de 7 sesiones cada iteración. Siguiendo los principios ágiles, estableceremos pequeños ciclos iterativos de forma que al final de cada uno generemos valor perceptible por nuestros usuarios (los visitantes de la web). Dedicaremos el primer día a la planificación del sprint (_sprint planning_) y el resto a trabajar en el desarrollo del proyecto. Al final de cada sprint haremos un _Sprint Review_ (_demo_) del proyecto para presentar los resultados conseguidos y recoger feedback, al igual que una _retrospectiva_ (_retro_) para evaluar cómo ha ido el sprint, además de valorar vuestro trabajo en equipo de cara a mejorar en el siguiente sprint.

Por tanto, al final del primer sprint tendremos un _Sprint Review_ corto, de no más de 5 minutos, para presentar el resultado del trabajo al resto de las compañeras y profesores. Lo importante es mostrar el sotfware funcionando, sin necesidad de presentación que lo sustente. Siempre se debe mostrar la página funcionando en GitHub Pages, ya que es un entorno de producción real. No debemos hacer la demostración mostrando la página directamente desde una carpeta de nuestro ordenador.

También haremos una _retro_ corta revisando los _working agreements_ que hemos acordado al inicio del proyecto y añadiendo cualquier otro feedback que nos permita mejorar el proyecto.

Al final del segundo sprint (que coincidirá con el final del proyecto), haremos una sesión de presentación más completa, más allá de lo que sería un _Sprint Review_. Estará limitada a 5 minutos de contenido con otros 5 minutos de preguntas, seguida posteriormente de una retrospectiva usando una dinámica similar a las usadas en los equipos de desarrollo Scrum.

### Historias de usuario

Para la gestión del proyecto, usaremos _historias de usuario_, que es una herramienta para definir las características de un producto que veremos en detalle durante el curso.

#### Primera. Versión móvil de la web

- Desarrollar la versión para móvil de la web (página principal) con HTML y CSS
- Crear el contenido de la web: textos e imágenes
- Crear la infraestructura necesaria: repositorio en GitHub y con acceso para todos los miembros del equipo

> **NOTA**:
> Para considerar terminada esta historia y todas las siguientes debéis tener publicada la web en GitHub Pages.

#### Segunda. Versión responsive de la web

- Hacer la web para el resto de tamaños de pantalla (tablet, desktop)

#### Tercera. Mejora de tecnología

- Integración con gulp para automatización de tareas
- Dividir HTML en partials
- Pasar el CSS a Sass (también usando partials)
- Aplicar las técnicas avanzadas aprendidas en la parte final del curso:
  - Grid en la sección de "quiénes somos"
  - Opcionalmente añadir animaciones y transiciones

#### Cuarta. Formulario de contacto

- Realizar el formulario de contacto para todos los dispositivos
- Hacer que funcione el envío usando el servicio [formspree.io](https://formspree.io) ([Cómo usar Formspree.io](#formspree))

## Entrega

El formato de entrega de este proyecto será mediante la subida de este a la plataforma de GitHub. Para subirlo, se creará un repositorio **en la organización de Adalab**. El nombre del repositorio deberá estar compuesto de las siguientes partes, todo ello separado por guiones:

- La palabra **project**.
- Letra de la promoción **promo-k**.
- Número del módulo **module-1**.
- Número del equipo **team-1**.

Por ejemplo:

- Adalab/project-promo-k-module-1-team-1
- Adalab/project-promo-k-module-1-team-3

De manera adicional, se deberá activar "GitHub Pages" en el proyecto para que este pueda ser visualizado como una web, es decir, que en el caso anterior, si alguien introdujese la dirección https://beta.adalab.es/project-promo-k-module-1-team-1 en un navegador web, este mostraría la web que se genera con el código del repositorio.

- **Entrega del primer sprint (sprint review):** 14 de septiembre
- **Entrega del segundo sprint (sprint review):** 23 de septiembre
- **Demo del proyecto (presentación final):** 30 de septiembre

En las sprint review se revisarán que se hayan solucionado todas las tareas técnicas asociadas a la entrega de esos sprints, si algo quedara pendiente se arrastraría al siguiente sprint. 

Los días entre la presentación del segundo sprint y la demo final deben ser para hacer retoques y preparar la presentación del proyecto para vendérsela al cliente.

## Presentación

El último día del módulo presentaréis la versión final de este proyecto a vuestras compañeras y al equipo de Adalab. Cada equipo realizará una presentación de 5 minutos y posteriormente habrá 5 minutos de feedback por parte del público. En este caso, la audiencia podría ser más variada pues no sólo estarán los profesores.

El objetivo es que practiquéis la realización de las demos de los proyectos que habéis desarrollado, explicándolo desde un punto de vista técnica y también desde la perspectiva del producto, mejorando además vuestras habilidades de exposición, objetivo de desarrollo profesional del curso.

Para que la presentación salga bien es imprescindible una buena preparación. Por ello, durante el segundo sprint del módulo tendréis que asignar responsabilidades dentro del equipo relacionadas con la preparación de ésta. A continuación incluimos algunos elementos que os pueden ayudar a enfocar la presentación:

- En el público habrá personas con conocimientos técnicos y no técnicos.
- La parte central de la presentación será mostrar el software desarrollado funcionando, a ser posible en directo de forma dinámica o a través de un vídeo (si no fuera posible, como plan B).
- En este módulo, de los diferentes elementos adicionales que os proponemos, sería útil incluir una breve presentación de los diferentes integrantes del equipo desde un punto de vista profesional. Se trata de practicar vuestro "relato" profesional en versión muy corta. Que las personas asistentes conozcan quienes sois como profesionales. Os será también útil para las entrevistas de trabajo.
- Todas las participantes del equipo deben hablar en la presentación (sin práctica no hay mejora).

Además de esto, para mejorar vuestras habilidades de exposición en público y hacer la presentación más rica, podréis incorporar otros elementos adicionales (son solo ideas, sentíos libres de innovar y ser creativas):

- Dejar muy claro quién ha sido vuestro cliente y qué fue lo que os pidió.
- Explicar qué necesidades cubre o qué problemas soluciona el producto, cuál es el beneficio principal que aporta y qué lo hace único comparado con otros productos parecidos del mercado.
- Aportaciones "únicas y diferenciadoras" de cada equipo al proyecto.
- Cómo ha sido la organización del equipo, el reparto de tareas y la coordinación a la hora de trabajar todas en el mismo código.
- Cuál de las tareas o los puntos ha sido el que más esfuerzo ha requerido.
- Cuál de las tareas o partes de la web es la que hace que el equipo esté más orgulloso.
- Las tecnologías qué habéis utilizado y para qué sirven, y algunas partes del código que habéis desarrollado que merezca la pena resaltar.
- La presentación debe tener un "buen inicio y un buen cierre" que nos haga a todos estar atentos y aplaudir... ahí os dejamos que echéis a volar vuestra imaginación.
- No habléis en primera persona de lo que habéis hecho, hablad del equipo.
- No mencionéis problemas, sino "retos" que os han hecho aprender y crecer.
- Os aconsejamos utilizar un lenguaje ni demasiado formal y técnico, ni demasiado informal. Nuestra audiencia puede ser muy variada. Recordad que si usais lenguaje técnico, hacedlo con fundamento y reflajando el conocimiento adquirido.

## Recursos

Para este proyecto hemos preparado un listado de recursos que os pueden servir de ayuda.

### Formspree

[Formspree.io](https://formspree.io) es un servicio gratuito para recoger la información de formularios simples:

1. Formspree nos proporciona una url para el atributo `action=""` de nuestro formulario que incluye el email en el que queremos recibir los datos
1. La primera vez nos pedirá que confirmemos la dirección de email

Puedes probarlo en este [codepen](https://codepen.io/adalab/pen/mvNNeL).

### Cómo diseñar una web desde cero

Saber diseñar una web no es un requisito previo para este curso. Tampoco es un objetivo del curso que aprendáis a hacerlo ni os lo exigiremos, por eso hemos preparado una breve guía para aprender a diseñar, para que os sirva como referencia para realizar el diseño de las página individuales y para daros los pasos y la información necesaria para llevar a cabo un diseño básico.

[Guía para diseñar una web desde cero](./p1_anexo.md)
