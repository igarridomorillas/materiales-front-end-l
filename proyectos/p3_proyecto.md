# Proyecto 3: Un caso de código heredado

<!-- TOC START min:2 max:2 link:true update:true -->

- [Resumen (TL;DR)](#resumen-tldr)
- [Objetivos](#objetivos)
- [Caso de uso](#caso-de-uso)
- [Especificaciones](#especificaciones)
- [Planificación del proyecto](#planificacin-del-proyecto)
- [Entrega](#entrega)

<!-- TOC END -->

## Resumen ([TL;DR](https://spanish.stackexchange.com/questions/15317/hay-alg%C3%BAn-equivalente-en-castellano-al-ingl%C3%A9s-tldr))

En este proyecto vamos a trabajar con un caso muy típico que se suele producir en el mundo de la programación, un trabajo que nos viene dado, con código heredado, es decir escrito por otra persona y sobre el que tenemos que trabajar. En este caso es un poco especial porque vais a trabajar con código heredado pero vuestro: el código del proyecto del segundo módulo (el generador de tarjetas interactivas). **¡Sorpresa!**

## Objetivos

1. Lidiar con código heredado y ser capaces de refactorizarlo
1. Saber identificar y generar los componentes de una página, separarlos y crear componentes visualmente similares a partir de estos
1. Aprender a usar React para crear una aplicación web sencilla
1. Aprender a buscar información en la documentación de librerías externas
1. Implementar Scrum como marco de referencia para el desarrollo del producto, basándonos siempre en los valores de Agile como puntos clave del trabajo en equipo y la mejora continua
1. Mejorar la comunicación entre los miembros del equipo
1. Mejorar vuestras habilidades de comunicación en público al exponer el proyecto en la sesión final

## Caso de uso

La idea fundamental de este proyecto es que aprendamos a trabajar con un proyecto heredado. De esta forma desarrollaremos nuestra capacidad de adaptarnos a proyectos ya existentes. Esto nos preparará para, de cara al futuro, entrar en equipos nuevos de desarrollo con mayor rapidez, mejorar nuestra capacidad de modificación de código creado por otras personas y concienciarnos de la importancia de crear buen código visto desde la otra parte, la persona que lo recibe.

## Especificaciones

Se partirá de un proyecto funcional y se realizará una refactorización del código incluyendo el uso de React. _Refactorizar_ código consiste en modificar un código para mejorar su estructura pero sin añadir nuevas funcionalidades.

De cara a la refactorización, el proyecto debe utilizar estas tecnologías:

- Uso de Sass para los estilos
- Uso de ES6 y React para la estructuración del JS de la aplicación
- Uso de mediaqueries para que el diseño sea adaptable al dispositivo
- Desarrollo usando la estrategia mobile first
- Uso de git para el control de versiones del proyecto, con ramas y pull-requests para revisar los cambios de las compañeras
- Publicación del resultado en Internet usando GitHub Pages

La webapp deberá tener las siguientes nuevas características:

- Deberá usar transiciones y/o animaciones para mejorar interacciones con la aplicación

- Debe implementarse con una navegación entre distintas páginas de la aplicación usando React router

## Planificación del proyecto

### Sprints

Para la realización de este proyecto trabajaremos en _2 sprints_ (2 iteraciones) de 7 sesiones cada uno. Siguiendo los principios ágiles estableceremos pequeños ciclos iterativos de forma que al final de cada uno generemos valor perceptible por nuestros usuarios (los visitantes de la web). Dedicaremos el primer día a la planificación del sprint (_sprint planning_) y el resto a trabajar en el desarrollo del proyecto. Al final de cada sprint haremos una _demo_ del proyecto para presentar los resultados conseguidos, y una _retrospectiva_ (_retro_) para evaluar nuestro trabajo en equipo y mejorar en el siguiente sprint.

Al final del primer sprint haremos una demo corta de 10 minutos (incluidas preguntas) para presentar el resultado del trabajo al resto de las compañeras y a las profesoras. También haremos una retro corta revisando los _working agreements_ que hemos acordado al inicio del proyecto.

Al final del segundo sprint (final del proyecto), haremos una demo de 10 minutos más preguntas, y una retrospectiva usando una dinámica similar a las usadas en los equipos de desarrollo que usan Scrum.

### Historias de usuario

Para la gestión del proyecto, usaremos _historias de usuario_, que es una herramienta para definir las características de un producto. Usaremos las mismas historias de usuario que ya tenemos definidas del proyecto anterior. Aunque os daremos una planificación técnica para ayudaros a organizaros.

### Planificación técnica

#### Primero paso. Análisis del proyecto

- En este proyecto usaremos 2 repos:
  1. El repo del proyecto que nos hayan asignado, donde trabajaremos en una rama para entender y mejorar el código heredado. Esto quiere decir que sí podemos modificar el repo antiguo, pero sin tocar la rama **master**.
  1. Un nuevo repo con el proyecto de React.
- Analizar y probar el código y entender su estructura para poder adaptarla a nuestras necesidades y conocimientos.
- Solucionar errores detectados en el código.
- Implementar mejoras en el código heredado, sin modificar la funcionalidad (hacer las funciones más pequeñas, usar métodos funcionales, mejorar el nombrado, etc.).

#### Segundo paso. Maquetación con React de la página de la herramienta

- Definir la estructura de componentes React de la aplicación.
- Generar los componentes del proyecto y comunicar información mediante props.

> **NOTA**: No debéis copiar código de vuestro proyecto anterior, sino esforzaros por entender el que han creado otras compañeras. Para partes incompletas o que no funcionen podéis arreglarlas pero no re-hacerlas desde cero.

#### Tercero. Versión completa con React

- Realizar la interactividad, usando el estado y los eventos de React.
- Usar este [componente que os pasamos para la foto de perfil](https://github.com/Adalab/Componente-react-de-foto-de-perfil).
- Implementar la comunicación con el backend, la función de compartir y offline.

#### Cuarta. Mejoras finales

- Crear la página de landing.
- Implementar las rutas con React router.
- Revisión del código y pruebas.
- Podrán implementarse otras mejoras visuales si todo ya está terminado y acordado con el PO.

## Entrega

El formato de entrega de este proyecto será mediante la subida de este a la plataforma de GitHub. Para subirlo, se creará un repositorio **en la organización de Adalab**. El nombre del repositorio deberá estar compuesto de las siguientes partes, todo ello separado por guiones:

- La palabra **project**.
- Letra de la promoción **promo-k**.
- Número del módulo **module-3**.
- Número del equipo **team-x**.

Por ejemplo:

- Adalab/project-promo-k-module-3-team-1
- Adalab/project-promo-k-module-3-team-3

De manera adicional, se deberá activar "GitHub Pages" en el proyecto para que este pueda ser visualizado como una web, es decir, que en el caso anterior, si alguien introdujese la dirección "https://beta.adalab.es/project-promo-k-module-3-team-X/" en un navegador web, este mostraría la web que se genera con el código del repositorio.

- **Entrega del primer sprint (sprint review):** 12 de noviembre
- **Entrega del segundo sprint (sprint review):** 23 de noviembre
- **Demo del proyecto (presentación final):** 30 de noviembre

En las sprint review se revisarán que se hayan solucionado todas las tareas técnicas asociadas a la entrega de esos sprints, si algo quedara pendiente se arrastraría al siguiente sprint.

Los días entre la presentación del segundo sprint y la demo final deben ser para hacer retoques y preparar la presentación del proyecto para vendérsela al cliente.

## Presentación

El último día del módulo presentaréis la versión final de este proyecto a vuestras compañeras y al equipo de Adalab. Cada equipo realizará una presentación de 5 minutos y posteriormente habrá 5 minutos de feedback por parte del público.

El objetivo es que practiquéis la realización de las demos del trabajo que estáis realizando que posteriormente tendréis que realizar en las empresas, y también que mejoréis vuestras habilidades de exposición en público, objetivo de desarrollo profesional del curso.

Para que la presentación salga bien es imprescindible una buena preparación. Por ello, durante el segundo sprint del módulo tendréis que asignar responsabilidades dentro del equipo relacionadas con la preparación de esta.

A continuación algunos elementos que os pueden ayudar a enfocar la presentación:

- En el público habrá personas con conocimientos técnicos y no técnicos.
- La parte central de la presentación será mostrar el software desarrollado funcionando, a ser posible en directo de forma dinámica o a través de un vídeo si no fuera posible.
- En este módulo, de los diferentes elementos adicionales que os proponemos, incluid la explicación de algunas tecnologías qué habéis utilizado y para qué sirven, y algunas partes del código que habéis desarrollado que merezca la pena resaltar.
- Todas las participantes del equipo deben hablar en la presentación (sin práctica no hay mejora).

Además de esto, para mejorar vuestras habilidades de exposición en público y hacer la presentación más rica, podréis incorporar otros elementos adicionales (son solo ideas, sentíos libres de innovar y ser creativas):

- Dejar muy claro quién ha sido vuestro cliente y qué fue lo que os pidió.
- Presentación de los diferentes integrantes del equipo desde un punto de vista profesionales. Se trata de practicar vuestro "relato" profesional en versión muy corta. Que las personas asistentes conozcan quienes sois como profesionales.
- Qué necesidades cubre o qué problemas soluciona el producto, cuál es el beneficio principal que aporta y qué lo hace único comparado con otros productos parecidos del mercado
- Aportaciones "únicas" de cada equipo al proyecto.
- Cómo ha sido la organización del equipo, el reparto de tareas y la coordinación a la hora de trabajar todas en el mismo código.
- Cuál de las tareas o los puntos ha sido el que más esfuerzo ha requerido.
- Cuál de las tareas o partes de la web es la que hace que el equipo esté más orgulloso.
- La presentación debe tener un "buen inicio y un buen cierre" que nos haga a todos estar atentos y aplaudir... ahí os dejamos que echéis a volar vuestra imaginación.
- No habléis en primera persona de lo que habéis hecho, hablad del equipo.
- No mencionéis problemas, sino "retos" que os han hecho aprender y crecer.
- Os aconsejamos utilizar un lenguaje ni demasiado formal y técnico, ni demasiado informal. Nuestra audiencia puede ser muy variada.
