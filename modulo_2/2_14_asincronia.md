# Asincronía y temporizadores

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

<!-- /TOC -->

## Introducción

Durante esta sesión vamos a ver cómo se ejecutan las órdenes en JavaScript para entender mejor cómo funciona el lenguaje, para ello veremos qué es eso de la asincronía y por qué es una de las características más importantes de JavaScript.

## ¿Qué es la asincronía?

Imaginemos que tenemos un conjunto de tareas a realizar. En los lenguajes tradicionales, ese conjunto de instrucciones se realizaba una tras otra, es decir, imaginemos que tenemos los siguientes pasos:

1. Mostrar un mensaje en la pantalla
2. Realizar una petición al servidor
3. Mostrar otro mensaje
4. Con la respuesta del servidor, mostrar "Respuesta: ..."

En un lenguaje tradicional, se ejecutarán de forma secuencial, es decir, una tarea tras otra. Primero el paso 1, cuando termine, el paso 2 y así sucesivamente. De esta forma si realizamos una petición en el paso 2, hasta que no se reciba la información (que podría tardar varios segundos), no podríamos mostrar el mensaje del paso 3.

Pensemos por un momento en qué supone que cada paso se ejecute uno detrás de otro en la web. En primer lugar, si solicitamos una información a un servidor, durante el tiempo entre que se pide esa información y la respuesta no se podrá ejecutar nada de JavaScript, porque estará parado el resto del código hasta el momento de recibir la información del servidor. Cuando decimos nada de JavaScript, esto también implica que si tenemos algo de código que se va a ejecutar al pulsar un botón este tampoco funcionará y eso se traduce en que no se podrá interactuar con la web.

Pensad en Google Maps o Google e imaginaos lo que supondría que cada petición que hace al servidor (cargar una parte del mapa o recargar un nuevo resultado) hiciese que la página se congelase. Sería algo totalmente contraproducente. De este hecho nació la necesidad de hacer algo que no parase nuestro código cuando se realiza la petición a un servidor, nació la asincronía.

JavaScript permite realizar tareas de forma asíncrona y concurrente, esto quiere decir que pueden realizarse tareas que no vayan en cadena y ejecutarse ambas a la vez y trabajar de forma independiente.

Si mantenemos el caso anterior, en el caso de JavaScript se hará lo siguiente. Se ejecutará el paso 1 para mostrar un mensaje en la pantalla, se realizará luego el paso 2, que hará una petición al servidor y aquí es donde recae la diferencia. Como hemos dicho antes, en JavaScript no puede quedarse una orden esperando hasta que se ejecute la actual cuando se trata de tareas de larga duración. Para resolver esto, el navegador delega algunas tareas en otros procesos y mientras continúa con las siguientes. Así que se ejecutarán el resto de tareas hasta que llegue la petición del servidor, cuando se ejecutará el código con el resultado.

### ¿Por qué es importante entender la asincronía?

Entender la asincronía en JavaScript será fundamental para saber en qué orden se ejecutará nuestro código y por tanto, poder lidiar con él mejor sin que tengamos problemas de que algún paso no se ejecute cuando lo necesitamos.

Además, la mayoría de las formas de hacer nuestra web interactiva (eventos) dependen de esa asincronía por lo que supone un conocimiento muy importante si queremos hacer que nuestra web sea interactiva y funcione correctamente.

### Ejecutar código pasado un cierto intervalo de tiempo

En esta sección vamos a ver cómo podemos ejecutar en JavaScript pasados determinados milisegundos. Esto nos será muy útil para realizar webs como Kahoot, en la que tenemos un máximo de tiempo y cada x segundos el contador de tiempo disminuye.

Otros ejemplos de uso podrían ser cerrar la sesión de una web transcurridos X segundos, por ejemplo. Cualquier cosa que dependa del tiempo en una página probablemente se ejecute con el código que vamos a ver a continuación.

### setInterval

En JavaScript podemos crear código para que se ejecute cada determinado tiempo, para ello utilizamos `setInterval()`.

Esta función recibe 2 parámetros:

- la función a ejecutar cada cierto tiempo (sin paréntesis como hacíamos en addEventListener, ya que no la ejecutamos nosotras)
- el tiempo en milisegundos

Vamos a ver un ejemplo: un contador que se incrementa cada segundo y se muestra en pantalla.

```html
<p class="time">0</p>
```

En el HTML tenemos un párrafo con la clase `time`.

```javascript
let counter = 0;

const incrementAndShowCounter = () => {
  counter++;
  const time = document.querySelector('.time');
  time.innerHTML = counter;
};

setInterval(incrementAndShowCounter, 1000);
```

En JavaScript definimos una variable global que será nuestro contador. También una función que incrementa el contador y lo muestra en el HTML, que será la que ejecutemos cada cierto tiempo. Finalmente ejecutamos la llamada a `setInterval` pasando como primer parámetro la función y luego 1000 para indicar que se ejecute cada segundo.

> NOTA: En el ejemplo anterior pasamos a `setInterval` la función `incrementAndShowCounter` como argumento, sin ejecutarla. A estas funciones en JavaScript se les suele llamar _callbacks_.

Podéis [jugar con el código de este ejemplo en Codepen](https://codepen.io/adalab/pen/POLdmN?editors=1010#0).

Para obtener más información acerca de `setInterval`, consultaremos la [documentación de setInterval en MDN](https://developer.mozilla.org/es/docs/Web/API/WindowTimers/setInterval).

#### EJERCICIO 1

Partiendo del ejemplo anterior, vamos a realizar un temporizador que empiece en 0 y cada 2 segundos se incremente.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

Todos sabemos lo que pasó en Canal Sur hace unos años, en mitad de las campanadas pusieron anuncios y aguaron la noche a millones de personas. Para estar preparados, vamos a crear un contador de uvas. Este contador empezará en 0 y cada segundo incrementará en 1, así hasta 12, en ese momento terminará la cuenta y se dejará de contar más.

La cuenta se mostrará en la pantalla con números y si lo deseas puedes añadir una imagen de una uva cada vez que pase un segundo.

> PISTA: la función se puede seguir ejecutando con setInterval pero para que se pare en 12 basta con dejar de pintar en el HTML en el momento adecuado.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

Vamos a realizar el típico mensaje que aparece en un blog con la información de hace cuanto se escribió un post. Por ejemplo, con el texto: "escrito hace 30 segundos". Al principio escribiremos en pantalla "escrito hace 1 segundo" e iremos aumentando el número de segundos. Cuando lleve más de 59 segundos queremos que ponga "escrito hace 1 min".

\_\_\_\_\_\_\_\_\_\_

### setTimeout

El método `setTimeout()` es muy similar a `setInterval()` pero a diferencia de este solo ejecuta una vez la función que le pasemos. Sirve entonces para retrasar determinados milisegundos una operación.

Por ejemplo, vamos a crear un texto de aviso de que algo se ha guardado correctamente. Este mensaje se borrará pasados 6 segundos.

```html
<p class="msg">Se ha guardado correctamente</p>
```

En HTML sólo tenemos un párrafo con el mensaje de confirmación y la clase `msg`.

```javascript
const removeMsg = () => {
  const msg = document.querySelector('.msg');
  msg.innerHTML = '';
};

setTimeout(removeMsg, 6000);
```

En JavaScript definimos la función que elimina el mensaje de la pantalla. Luego llamamos a `setTimeout` para que ejecute esa función pasados 6 segundos.

Podéis [jugar con este ejemplo el Codepen](https://codepen.io/adalab/pen/EbMeOM).

Para obtener más información acerca de `setTimeout()`, consultaremos la documentación de MDN:

- [Documentación de setTimeout en MDN](https://developer.mozilla.org/es/docs/Web/API/WindowTimers/setTimeout)

#### EJERCICIO 4

Con JavaScript, crear un código para mostrar una ventana en nuestro navegador una vez transcurridos 15 segundos que ponga "su sesión ha expirado" (creada usando HTML y CSS).

\_\_\_\_\_\_\_\_\_\_

### Cancelar eventos de setInterval y setTimeout

En algunas ocasiones querremos dejar de realizar una tarea que hemos configurado con `setInterval` para que se realice cada determinado tiempo o cancelar una tarea programada con `setTimeout`. Para ello utilizaremos los métodos `clearTimeout` y `clearInterval`.

Vamos a partir del ejemplo anterior del contador que se actualizaba cada segundo. Queremos que a los 10 segundos se pare, eliminando la ejecución de la función con setInterval.

```javascript
let counter = 0;
let temp;

const incrementAndShowCounter = () => {
  counter++;
  const time = document.querySelector('.time');
  time.innerHTML = counter;
  if (counter === 10) {
    clearInterval(temp);
  }
};

temp = setInterval(incrementAndShowCounter, 1000);
```

Hemos hecho sólo un par de cambios en JavaScript. En primer lugar hemos guardado el identificador del temporizador en una variable `temp` para que luego sea accesible desde la función. El segundo cambio es que ahora en la función hacemos una comprobación y si el contador llega a 10 ejecutamos el `clearInterval` y la función deja de ejecutarse cada segundo.

Podéis [jugar con este ejemplo el Codepen](https://codepen.io/adalab/pen/ooVPOg).

Para obtener más información:

- [clearInterval](https://www.w3schools.com/jsref/met_win_clearinterval.asp)
- [clearTimeout](https://www.w3schools.com/jsref/met_win_cleartimeout.asp)

#### EJERCICIO 5

Vamos a modificar nuestra solución del ejercicio 2 para que, en lugar de seguir ejecutando la función indefinidamente, detengamos su ejecución con `clearInterval`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

Crear un cronómetro que vaya aumentando en segundos y cuando se pulse el botón de parar deje de aumentar. Cuando pulsemos el de continuar, vuelva a empezar de nuevo.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 7

Crear una página con un botón que transcurridos 10 segundos te pregunte: "¿te has dormido?". Si pulsas en el botón la cuenta volverá a cero y otra vez, si transcurren 10 segundos sin pulsar volverá a preguntar de nuevo "¿te has dormido?"

\_\_\_\_\_\_\_\_\_\_

En los videos que enlazamos a continuación, se explica de forma más detallada qué es la asincronía y cómo funciona ésta en JavaScript.

- [Asincronía en JavaScript - Parte 1 - Sincronía y Concurrencia](https://www.youtube.com/watch?v=PndHsDpEfhU)
- [Asincronía en JavaScript - Parte 2 - Event loop](https://www.youtube.com/watch?v=rgmej4Jx4WM)

#### EJERCICIO 8

Usando la herramienta [loupe](http://latentflip.com/loupe/?code=!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D) que se utiliza en el video (ver el vídeo), realizar en JavaScript las siguientes tareas para ver en qué orden se reproducen:

TAREAS A

1. Crear una función `funA` que contenga un `console.log('hola')`
2. Crear otra función `funB` que ejecute `funA`
3. Ejecutar la función `funB`

TAREAS B

1. En un if comprobar si "Hello" y "hello" son iguales
2. Si lo son, ejecutar un `console.log` que diga "lo son"
3. Si no lo son, ejecutar un `console.log` que diga "no lo son"

TAREAS C

1. Crear una función `pulsado()` que guarde en una variable el texto "pulsado" y luego muestre esa variable con un `console.log`
2. Crear un botón que llame a la función anterior. Podemos editar el HTML en el panel inferior izquierdo. Usaremos una sintaxis propia del programa en lugar de `addEventListener`:
   `$.on("button", "click", pulsado);`

3. Añadir un `console.log` al final que muestre el texto "empezamos"

¿Sabrías explicar por qué se ejecutan en ese orden? En caso de no ser así consulta y debate con el resto de tus compañeras.

\_\_\_\_\_\_\_\_\_\_

## Resumen
En esta lección hemos profundizado un poco más en el concepto de asincronía y hemos conocido los temporizadores:

- `setInterval` nos permite ejecutar una función cada x milisegundos, y puede ser cancelada con `clearInterval`

- `setTimeout` nos permite ejecutar una función pasados x milisegundos, y puede ser cancelada con `clearTimeOut`

## Recursos adicionales

- [Javascript Asíncrono: La guía definitiva](https://lemoncode.net/lemoncode-blog/2018/1/29/javascript-asincrono)
