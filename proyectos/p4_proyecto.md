# Proyecto 4: Servidor del Awesome profile cards

- [Resumen (TL;DR)](#resumen-tl-dr)
- [Objetivos](#objetivos)
- [Caso de uso](#caso-de-uso)
- [Especificaciones](#especificaciones)
- [Planificación del proyecto](#planificacin-del-proyecto)
- [Entrega](#entrega)

## Resumen ([TL;DR](https://spanish.stackexchange.com/questions/15317/hay-alg%C3%BAn-equivalente-en-castellano-al-ingl%C3%A9s-tldr))

En este proyecto vamos a desarrollar nuestro primer servidor web. Durante el módulo 3 hemos desarrollado una web que usaba un servidor creado por las profesoras de Adalab, que para nosotras es una caja negra. **Hasta ahora no sabíamos cómo funcionaba por dentro.**

Ahora queremos que crear un servidor que tenga la misma funcionalidad que el servidor creado por las profesoras de Adalab. **Al finalizar el desarrollo podremos utilizar la página del módulo 3 con el servidor realizado en este módulo.**

Para saber que el nuevo servidor está bien programado, **este debe responder con exactamente los mismos datos y ficheros con los que responde el servidor creado por las profesoras de Adalab**.

## Objetivos

1. Consolidar el aprendizaje de las tecnologías Node JS y Express JS para aprender a escuchar peticiones desde los navegadores.
1. Consolidar el aprendizaje de SQL para trabajar con bases de datos y guardar los datos de las usuarias de forma persistente.
1. Consolidar el aprendizaje de API Rest para saber cómo estructurar y organizar las comunicaciones entre un navegador y un servidor de forma óptima.
1. Ser capaces de realizar un proyecto web completo, sin necesidad de solicitar ayuda a ningún otro equipo de desarrollo.
1. Ser capaces de poner en producción un proyecto completo: front end + back end.
1. Mejorar la comunicación entre los miembros del equipo y con otros equipos de desarrollo.

## Caso de uso

Con este servidor podréis demostrar que tenéis un perfil **full stack** (front end + back end) y que sois desarrolladoras versátiles capaces de trabajar en cualquier departamento técnico de una empresa de desarrollo.

## Especificaciones

En el módulo 3 hemos utilizado un servidor desarrollado por las profesoras de Adalab. Puesto que el objetivo de este proyecto es replicar la funcionlidad de dicho servidor, vamos a utilizarlo de guía para saber qué debemos desarrollar.

Si analizamos qué comunicaciones se realizan entre la web y el servidor desarrollado por las profesoras de Adalab del proyecto **Awesome profile cards** vemos que:

### API

La web envía una [petición con datos al servidor para crear una tarjeta](p2_anexo.md). Por cada una de estas peticiones el servidor debe:

- Comprobar que los datos recibidos desde el navegador son correctos.
- En caso de que los datos **no** sean correctos, el servidor debe devolver una respuesta de error.
- En caso de que los datos **sí** sean correctos, el servidor debe:
   - Guardar los datos en base de datos.
   - Generar una URL para que cuando se acceda a ella se visualice la tarjeta creada por la usuaria.
   - Devolver una respuesta al navegador con esta URL.

### Motor de plantillas

Cada vez que desde la web se crea una tarjeta, el servidor asocia una URL a cada tarjeta.

Una URL de ejemplo creada por el servidor de Adalab es https://us-central1-awesome-cards-cf6f0.cloudfunctions.net/card/-MQpvB55_XYh95upMAKy. Una URL de ejemplo creada por vuestro servidor debería ser algo como https://url-de-nuestro-servidor/card/-MQpvB55_XYh95upMAKy.

Cuando se accede a esta URL el servidor debe mostrar una página con los datos de la tarjeta:

- Datos de la usuaria
- Foto de la usuaria
- Colores de la tarjeta

### Servidor de estáticos

En el módulo 3 estamos utilizando el servidor GitHub Pages para publicar nuestras web. Ahora vamos a crear nuestro propio servidor. No tiene sentido utilizar GitHub Pages para la parte front y otro servidor para la parte de back.

- Una vez acabado nuestro servidor debemos poder meter dentro de nuestro servidor los ficheros de nuestra página hecha en el módulo 3 de React.
- En la página del módulo 3 solo debemos hacer un cambio en el código:
   - Este cambio es únicamente cambiar la URL del `fetch`.
   - En el módulo 3 la web se comunicaba con el servidor programado por las profesoras de Adalab, es decir, con https://us-central1-awesome-cards-cf6f0.cloudfunctions.net.
   - En el módulo 4 la web se debe comunicar con el servidor que vamos a crear, es decir, con https://url-de-nuestro-servidor.

### Servidor de producción

Una vez finalizado el servidor lo publicaremos o lo desplegaremos (que es lo mismo) en un servidor real, para que cualquier usuaria pueda acceder a nuestra página.´

En módulos anteriores hemos usado GitHub Pages que es un servidor para front. En este módulo desplegaremos nuestro servidor en [Heroku](https://heroku.com), que es un servidor para front + back.

## Planificación del proyecto

### Sprints

Para la realización de este proyecto trabajaremos en _1 sprint_ (1 iteración) de 5 sesiones. Siguiendo los principios ágiles, estableceremos pequeños ciclos iterativos de forma que al final de cada uno generemos valor perceptible por nuestros usuarios (los visitantes de la web). Dedicaremos el primer día a la planificación del sprint (_sprint planning_) y el resto a trabajar en el desarrollo del proyecto. Al final del único sprint haremos un _Sprint Review_ (_demo_) del proyecto para presentar los resultados conseguidos y recoger feedback, al igual que una _retrospectiva_ (_retro_) para evaluar cómo ha ido el sprint, además de valorar vuestro trabajo en equipo de cara a mejorar en futuros sprints.

Por tanto, al final del único sprint tendremos un _Sprint Review_ corto, de no más de 5 minutos, para presentar el resultado del trabajo al resto de las compañeras y profesores. Lo importante es mostrar el sotfware funcionando, sin necesidad de presentación que lo sustente. Siempre se debe mostrar la página funcionando en nuestro servidor de producción de **Heroku**, ya que es un entorno de producción real. No debemos hacer la demostración mostrando la página directamente desde una carpeta de nuestro ordenador.

También haremos una _retro_ corta revisando los _working agreements_ que hemos acordado al inicio del proyecto y añadiendo cualquier otro feedback que nos permita mejorar el proyecto.

Al final del curso, haremos una sesión de presentación más completa, más allá de lo que sería un _Sprint Review_. Estará limitada a 5 minutos de contenido con otros 5 minutos de preguntas, seguida posteriormente de una retrospectiva usando una dinámica similar a las usadas en los equipos de desarrollo Scrum.

### Historias de usuario

Para la gestión del proyecto, usaremos _historias de usuario_, que es una herramienta para definir las características de un producto que veremos en detalle durante el curso.

#### Primera. API

- Creación de un servidor básico.
- Creación de un API Rest para poder crear tarjetas, guardándolas en un array del servidor.

#### Segunda. Servidor de estáticos

- Creación de un servidor de estáticos para poder servir la página del módulo 3 desde el nuevo servidor.

#### Tercera. Motor de plantillas

- Creación de un motor de plantillas para poder visualizar las tarjetas creadas.

#### Cuarta. Bases de datos

- En la primera historia hemos guardado las tarjetas creadas en un array del servidor.
- En esta historia debemos guardar las tarjetas en base de datos.
- Cuando una usuaria visualice una tarjeta debemos recuperar esa información de base de datos para poder mostrarla.

## Entrega

El formato de entrega de este proyecto será mediante la subida de este a la plataforma de GitHub. Para subirlo, se creará un repositorio **en la organización de Adalab**. El nombre del repositorio deberá estar compuesto de las siguientes partes, todo ello separado por guiones:

- La palabra **project**.
- Letra de la promoción **promo-l**.
- Número del módulo **module-4**.
- Número del equipo **team-X**.

Por ejemplo:

- Adalab/project-promo-l-module-4-team-1
- Adalab/project-promo-l-module-4-team-3

De manera adicional, se deberá enlazar este repositorio con el servidor de Heroku.

- **Entrega del primer sprint (sprint review):** 17 de marzo
- **Demo del proyecto (presentación final):** 18 de marzo

En las sprint review se revisarán que se hayan solucionado todas las tareas técnicas asociadas a la entrega del sprint.

El día entre la presentación del sprint y la demo final deben ser para hacer retoques y preparar la presentación del proyecto para vendérsela al cliente.

## Presentación

El último día del módulo presentaréis la versión final de este proyecto a vuestras compañeras y al equipo de Adalab. Cada equipo realizará una presentación de 5 minutos y posteriormente habrá 5 minutos de feedback por parte del público. En este caso, la audiencia podría ser más variada pues no sólo estarán los profesores.

El objetivo es que practiquéis la realización de las demos de los proyectos que habéis desarrollado, explicándolo desde un punto de vista técnica y también desde la perspectiva del producto, mejorando además vuestras habilidades de exposición, objetivo de desarrollo profesional del curso.

Para que la presentación salga bien es imprescindible una buena preparación. Por ello, durante el sprint del módulo tendréis que asignar responsabilidades dentro del equipo relacionadas con la preparación de ésta. A continuación incluimos algunos elementos que os pueden ayudar a enfocar la presentación:

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
