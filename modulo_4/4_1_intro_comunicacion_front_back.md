# Comunicación entre front y back

Ahora mismo eres experta en programación front. Ya que vas a aprender cómo funciona la parte de back end, lo primero que tenemos que hacer es aprender cómo se comunican ambos mundos.

![](assets/images/comunicacion-entre-front-y-back.svg)

Vamos a ver este [vídeo](https://www.youtube.com/watch?v=knnzF-d0V1I) para entender cómo se comunica el front y el back:

{% embed url="https://www.youtube.com/watch?v=knnzF-d0V1I" %}

<!--
Guión para los vídeos

- Vídeo:
   - Bienvenidas al nuevo módulo de back end
   - Vamos a hacer una introducción explicando qué es el back y cómo se comunica con el front
   - Cuando hablemos de back end y de servidores es lo mismo
   - Qué es un servidor:
      - Es un ordenador que está siempre contectado a Internet
      - En muchos sitios del mundo (Madrid, Nueva Dely) hay edificions con cientos de ordenadores
      - En estos ordenadores hay programas que son servidores, es decir, contienen los ficheros y los datos de una página web.
      - Por ello si cualquier usuaria del mundo entra en un navegador y visita una página web, el navegador se conecta a través de Internet con el correspodiente servidor y este le envía los HTMLs, CSSs, imágenes que se necesitan para visualizar la página.
      - El navegador coge esos ficheros y compone la página para que se vea
      - Para saber con qué servidor se tiene que comunicar nuestro navegador utilizamos una dirección web, que está compuesta de
         - Protocolo
         - Subdominio
         - Dominio
         - Extensión de dominio
         - Puerto
         - Carpeta / Ficheros
      - Entrar en Adalab.es
   - Similitudes entre front y back:
      - Son programas escritos en lenguajes de programación
      - El front en HTML, CSS y JS
      - El back se puede escribir en muchos lenguajes como JAVA, Python, PHP o Node JS y muchos más
      - El back y el front en lo que se refiere a código es igual, lo vamos programar en el VS Code con Node JS.
   - Diferencias entre front y back:
      - La diferencia entre front y back hace referencia sobre dónde se ejecuta el código
         - El front se encarga de enseñar la página a la usuaria por ello se ejecuta en el navegador, es una interfaz gráfica, es algo visual.
         - El back o los servidores se encarga de gestionar las páginas y los datos de las usuarias, se va a ejecutar en la terminal de uno de esos ordenadores que están repartidos por el mundo.
      - Lo que programaremos en back va a funcionar igual para ser usado desde una web en un PC o desde una app nativa de un móvil
   - Back:
      - Con node JS vamos a montar aplicaciones de servidor
      - Cuando las desarrollemos vamos a ejecuarlas en local, al igual que las páginas >>> localhost
      - Cuando las terminemos las subimos a un servidor de verdad donde se ejecutarán >>> dominio.com. Es parecido a GitHub Pages pero con más funcionalidades.
      - Dentro de un servidor hay muchas partes o sub servidores. Lo más típicos son:
         - Servidor de estáticos:
            - Gestionan la visualización normal de una web, cuando una usuaria entra en ella
            - Es el navegador el responsable de solicitar de forma automática los HTMLs, CSSs, imágenes, vídeos y cualquier otro fichero, que muestra en la página
            - Uno de ellos es GitHub Pages
            - Mostrar adalab.es
            - Decimos que es de ficheros estáticos por que sirve ficheros
            - Son estáticos porque sirve los mismos ficheros sin modificar a todos usuarios, no cambian
            - Se encarga el navegador >>> mostrar devtools network
         - Servidor de dinámicos:
            - Es parecido al de estáticos
            - Hay una pequeña diferencia
            - Los ficheros html están customizados personalizados para cada usuaria
            - Mostrar la diferencia entre twitter.com/migueldelmazo y twitter.com/Adalab_Digital
            - Esto se consigue con un motor de plantillas o template engine
            - Es un html que es una plantilla y según qué usuario consulte esa página la plantilla se rellena con unos u otros datos.
            - Mostrar una plantilla html de los materiales
            - También se usa mucho para por ejemplo cuando te bajas una factura del gas
         - API
            - A las APIs con las que hemos trabajado hasta ahora
            - Las APIs son muy diferentes a los servidores de estáticos y dinámicos
            - Mientras los anteriores devuelven o sirven ficheros las APIs devuelve datos
            - En el 99% de los casos se intercambia la información entre un cliente y un API en formato JSON
            - Se realizan siempre con fetch
            - Están compuestas de una petición y una respuesta
            - Son las que más vamos a trabajar durante este módulo, ya que los servidores de estáticos y dinámicos no tienen mucho misterio
            - Las peticiones a un API envían datos en la petición y en la respuesta de muchas formas.
            - En próximas lecciones veremos cómo se envían y reciben dichos datos.
         - Bases de datos:
            - Es el sistema que utilizamos para guardar datos
            - Cuáles? todos:
               - Los emails y contraseñas de los usuarios registrados
               - Los pedidos de amazon
               - Los comentarios a un vídeo de youtube
               - El número de me gusta de Facebook
               - Los mensajes que nos intercambiamos por wasap
            - Hay muchos tipos de bases de datos y se diferencian por:
               - El formato de los datos que guardan
               - Hay unas que guardan los datos en un formato de tabla muy parecido a un excel
               - Hay otras que guardan los datos en un formato JSON
            - Como vemos en el diagrama los servidores de dinámicos y los del API necesitan datos, pues los leen y / o escriben en base de datos.
-->

### ¿Qué significa API Rest?

**Queremos hacer una pequeña aclaración:** hasta ahora a la API la hemos llamado API. Así la llama todo el mundo. API siginifica literalmente **Application Protocol interface** o **Application Programming Interface**. En cristiano, un protocolo para comunicar dos ordenadores o dispositivos. Por ejemplo front con back.

En concreto la API de la que vamos a hablar durante todo el módulo se llama **API Rest** o **API Restful**. Durante el módulo explicaremos más acerca de este protocolo.







































