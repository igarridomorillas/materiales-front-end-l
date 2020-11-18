# Proyecto 2: Awesome profile-cards

<!-- TOC START min:2 max:2 link:true update:true -->

- [Resumen (TL;DR)](#resumen-tldr)
- [Objetivos](#objetivos)
- [Caso de uso](#caso-de-uso)
- [Especificaciones](#especificaciones)
- [Diseño](#diseno)
- [Hitos](#hitos)
- [Entrega](#entrega)
- [Recursos](#recursos)

<!-- TOC END -->

## Resumen ([TL;DR](https://spanish.stackexchange.com/questions/15317/hay-alg%C3%BAn-equivalente-en-castellano-al-ingl%C3%A9s-tldr))

En este proyecto vamos a realizar una aplicación web que nos permite crear una tarjeta de visita personalizada. En la página web podemos introducir nuestros datos profesionales y obtener una vista maquetada con esta información. Lo bueno de este proyecto es que será una herramienta de la que os podréis beneficiar. Será una aplicación web interactiva creada por vosotras y que podéis usar para crear vuestras propias tarjetas de visita profesionales.

## Objetivos

1. Aprender los conceptos básicos de programación (variables, estructuras de datos, condicionales, funciones, etc.)
1. Comprender cómo manipular el DOM de una página y responder a eventos del usuario
1. Manejar estructuras de datos complejas, con arrays y objetos
1. Realizar peticiones al servidor y almacenar datos en local
1. Implementar Scrum como marco de referencia para el desarrollo del producto, basándonos siempre en los valores de Agile como puntos clave del trabajo en equipo y la mejora continua
1. Mejorar la comunicación entre los miembros del equipo
1. Mejorar vuestras habilidades de comunicación en público al exponer el proyecto en la sesión final

## Caso de uso

Con esta web podréis mostrar que, a parte de maquetar, podéis crear una página web con la que interactuar y sacar algo que vaya más allá de una página que solo muestra información. Esto os permitirá mostrar vuestras habilidades a la hora de trabajar con JavaScript en GitHub, algo que en las empresas se valora bastante a la hora de escoger candidatas para puestos de programadora front-end.

## Especificaciones

En el desarrollo de esta aplicación web usaremos las siguientes tecnologías:

- Uso avanzado de formularios HTML
- Maquetación usando CSS avanzado, como flex y grid
- Uso de mediaqueries para que el diseño sea adaptable al dispositivo usando la estrategia mobile first
- Gestión de eventos en el navegador (al hacer click, pasa x, etc.)
- Acceso y envío de datos a un servidor
- Almacenamiento en local usando LocalStorage
- Uso de git para el control de versiones del proyecto
- Publicación del resultado en Internet usando GitHub Pages

El proyecto consta de 2 páginas:

- Una página landing de bienvenida
- Una página con la aplicación de crear tarjetas

La aplicación funciona siguiendo estos pasos:

1. Permitir al usuario elegir el estilo de la tarjeta, eligiendo paleta de colores
2. Permitir al usuario que, mediante la introducción de información en un formulario, este texto se muestre maquetado automáticamente en un cuadro similar a una tarjeta de visita, que será la muestra del resultado final
3. Permitir que el usuario pueda crear una web con su tarjeta y compartirla por Twitter

![Awesome profile-cards versión tablet](assets/images/s2-tablet.png)

La tarjeta de visita deberá tener los siguientes campos (entre paréntesis el nombre del campo a usar):

- Nombre completo (full_name)
- Profesión (desarrolladora front-end ;) (job)
- Datos personales
  - Teléfono (phone)
  - Correo electrónico (email)
- RRSS
  - LinkedIn (linkedin)
  - GitHub (github)

Respecto a la interacción con la web:

- Los campos deberán tener restricciones para su formato indicado. Campo de teléfono para el móvil, mail para el correo, etc.
- Las modificaciones que hacemos en el formulario (diseño y contenido), aparecen automáticamente en la vista previa de la tarjeta
- Las 3 partes del proceso de creación serán elementos colapsables, que al hacer clic en el título se mostrará/ocultará solo mostrando una sección a la vez
- Toda la información del formulario debe almacenarse en LocalStorage (almacenamiento local del navegador), de forma que al recargar la página siga disponible y podamos borrarla con un botón de _Reset_. Para esto, debemos definir una estructura de datos compleja (con arrays y objetos) que es lo que guardaremos en el navegador
- Para compartir en Twitter seguiremos 2 pasos:
  1. Al hacer clic en el botón de "Enviar" enviaremos el formulario (_submit_) a un API que devolverá la URL de una web con la tarjeta de visita con la información rellena
  1. Mostraremos esta URL para que el usuario verifique si la tarjeta está bien definida y un botón de "Compartir" que enlazará a Twitter donde habrá un tweet con texto predefinido que incluye la URL de la tarjeta

## Diseño

El diseño lo podéis inspeccionar en [este proyecto de zeplin](https://zpl.io/bJ78X13). También podéis probar cómo funciona en este [prototipo online](https://sketch.cloud/s/O28AG/a/qkjwo3/play).

### Archivos

Podéis descargar los logos necesarios para completar el proyecto:

- [Logo de Adalab](assets/images/logo-adalab.png)
- [Logo de Awesome Profile-cards](assets/images/logo-awesome-profile-cards.svg)

### Creatividad

Aunque el diseño del proyecto está cerrado, hemos dejado algunos aspectos que podéis personalizar:

- Usar un logo personalizado del equipo (o nombre del equipo) en el pie de página, tras la información de copyright
- Utilizar un fondo personalizado en la previsualización de la tarjeta
- Añadir más paletas a las definidas en el diseño, pero no eliminar las que os proponemos ;)

## Planificación del proyecto

### Sprints

Para la realización de este proyecto trabajaremos en _2 sprints_ (2 iteraciones) de 7 sesiones cada uno. Siguiendo los principios ágiles estableceremos pequeños ciclos iterativos de forma que al final de cada uno generemos valor perceptible por nuestros usuarios (los visitantes de la web). Dedicaremos el primer día a la planificación del sprint (_sprint planning_) y el resto a trabajar en el desarrollo del proyecto. Al final de cada sprint haremos una _demo_ del proyecto para presentar los resultados conseguidos, y una _retrospectiva_ (_retro_) para evaluar nuestro trabajo en equipo y mejorar en el siguiente sprint.

Al final del primer sprint haremos una demo corta de 10 minutos (incluidas preguntas) para presentar el resultado del trabajo al resto de las compañeras y a las profesoras. También haremos una retro corta revisando los _working agreements_ que hemos acordado al inicio del proyecto.

Al final del segundo sprint (final del proyecto), haremos una demo de 10 minutos más preguntas, y una retrospectiva usando una dinámica similar a las usadas en los equipos de desarrollo que usan Scrum.

### Historias de usuario

Para la gestión del proyecto, usaremos _historias de usuario_, que es una herramienta para definir las características de un producto.

### Primera. Landing y UI de la herramienta

- Desarrollar la página de landing
- Desarrollar una primera versión básica de la web, con la maquetación de la estructura básica (para desktop y móvil) que incluye el formulario con los colapsables y la vista previa

> **NOTA**:
> Para considerar terminada esta historia y todas las siguientes debéis tener publicada la web en GitHub Pages.

### Segunda. Versión interactiva

- Formulario interactivo: al modificar un campo del formulario, tanto del diseño de la tarjeta como de los datos de usuario (excepto la foto), se actualiza la vista previa
- Realizar validaciones de datos del formulario: campos obligatorios, email, etc.

### Tercera. Compartir

- Actualización de la foto en la vista previa de la tarjeta, usando [el componente proporcionado](https://github.com/Adalab/Componente-de-foto-de-perfil-js)
- Añadir la funcionalidad de compartir en Twitter, enviando primero los datos al servidor para obtener la URL para compartir

### Cuarta. Versión offline

- Hacer que el contenido se almacene en LocalStorage del navegador

## Entrega

El formato de entrega de este proyecto será mediante la subida de este a la plataforma de GitHub. Para subirlo, se creará un repositorio **en la organización de Adalab**. El nombre del repositorio deberá estar compuesto de las siguientes partes, todo ello separado por guiones:

- La palabra **project**.
- Letra de la promoción **promo-k**.
- Número del módulo **module-2**.
- Número del equipo **team-1**.

Por ejemplo:

- Adalab/project-promo-k-module-2-team-1
- Adalab/project-promo-k-module-2-team-3

De manera adicional, se deberá activar "GitHub Pages" en el proyecto para que este pueda ser visualizado como una web, es decir, que en el caso anterior, si alguien introdujese la dirección "https://beta.adalab.es/project-promo-k-module-2-team-1/" en un navegador web, este mostraría la web que se genera con el código del repositorio.

- **Entrega del primer sprint (sprint review):** 13 de octubre
- **Entrega del segundo sprint (sprint review):** 22 de octubre
- **Demo del proyecto (presentación final):** 29 de octubre

En las sprint review se revisarán que se hayan solucionado todas las tareas técnicas asociadas a la entrega de esos sprints, si algo quedara pendiente se arrastraría al siguiente sprint.

Los días entre la presentación del segundo sprint y la demo final deben ser para hacer retoques y preparar la presentación del proyecto para vendérsela al cliente.

## Presentación

El último día del módulo presentaréis la versión final de este proyecto a vuestras compañeras y al equipo de Adalab. Cada equipo realizará una presentación de 10 minutos y posteriormente habrá 10 minutos de feedback por parte del público.

El objetivo es que practiquéis la realización de las demos del trabajo que estáis realizando que posteriormente tendréis que realizar en las empresas, y también que mejoréis vuestras habilidades de exposición en público, objetivo de desarrollo profesional del curso.

Para que la presentación salga bien es imprescindible una buena preparación. Por ello, durante el segundo sprint del módulo tendréis que asignar responsabilidades dentro del equipo relacionadas con la preparación de esta. Durante los dos últimos días de la evaluación final del módulo cada equipo tendrá asesoramiento durante 30 minutos por parte de la Especialista en Comunicación sobre la presentación del proyecto grupal. Para aprovechar bien este espacio, es necesario que antes cada equipo haya decidido las cuestiones clave para la presentación.

A continuación algunos elementos que os pueden ayudar a enfocar la presentación:

- En el público habrá personas con conocimientos técnicos y no técnicos.
- La parte central de la presentación será mostrar el software desarrollado funcionando, a ser posible en directo de forma dinámica o a través de un vídeo si no fuera posible.
- En este módulo, de los diferentes elementos adicionales que os proponemos, incluid qué necesidades cubre o qué problemas soluciona el producto, cuál es el beneficio principal que aporta y qué lo hace único comparado con otros productos parecidos del mercado.
- Todas las participantes del equipo deben hablar en la presentación (sin práctica no hay mejora).

Además de esto, para mejorar vuestras habilidades de exposición en público y hacer la presentación más rica, podréis incorporar otros elementos adicionales (son solo ideas, sentíos libres de innovar y ser creativas):

- Dejar muy claro quién ha sido vuestro cliente y qué fue lo que os pidió.
- Presentación de los diferentes integrantes del equipo desde un punto de vista profesional. Se trata de practicar vuestro "relato" profesional en versión muy corta. Que las personas asistentes conozcan quienes sois como profesionales.
- Aportaciones "únicas" de cada equipo al proyecto.
- Cómo ha sido la organización del equipo, el reparto de tareas y la coordinación a la hora de trabajar todas en el mismo código.
- Cuál de las tareas o los puntos ha sido el que más esfuerzo ha requerido.
- Cuál de las tareas o partes de la web es la que hace que el equipo esté más orgulloso.
- Las tecnologías qué habéis utilizado y para qué sirven, y algunas partes del código que habéis desarrollado que merezca la pena resaltar.
- La presentación debe tener un "buen inicio y un buen cierre" que nos haga a todos estar atentos y aplaudir... ahí os dejamos que echéis a volar vuestra imaginación.
- No habléis en primera persona de lo que habéis hecho, hablad del equipo.
- No mencionéis problemas, sino "retos" que os han hecho aprender y crecer.
- Os aconsejamos utilizar un lenguaje ni demasiado formal y técnico, ni demasiado informal. Nuestra audiencia puede ser muy variada.

## Recursos

Para este proyecto hemos preparado un listado de recursos que os pueden servir de ayuda.

### Ejemplo similar

Si en este punto algo no ha quedado del todo claro aquí tenéis un ejemplo similar con un generador de firmas de email para nuestra empresa.
Este es un ejemplo real en el que a través de un formulario actualizamos lo que luego será la firma de email para los empleados de esta empresa.

Está subido a GitHub y utiliza GitHub Pages para tenerlo online.

- [Generador de firmas de email](https://chucheria.github.io/EmailSignatureGenerator/index.html)
