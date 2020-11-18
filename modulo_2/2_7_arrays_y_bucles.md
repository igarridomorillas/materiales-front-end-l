# Arrays y bucles

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

<!-- /TOC -->

## Introducción

En esta sesión nos centraremos en los arrays y los bucles.

Los arrays, también llamados arreglos o listas, nos permiten guardar una lista ordenada de datos en JavaScript. Algunos ejemplos: una lista de espera de un hospital, los objetos de una cesta de la compra, los usuarios que han dado _like_ a nuestra foto, etc.

```js
// Array con la lista de espera de los pacientes de un hospital
['Manuela Eufemia', 'Benigna Imelda', 'Isaías Paquito', 'Ximena Adán', 'Nicolás Emiliana'];
```

Durante esta sesión veremos cuales son las características principales de este tipo de estructura de datos y veremos cómo trabajar con ellos, modificarlos y obtener información de ellos.

También veremos los bucles, estructuras de control que, como su nombre indica, permiten repetir un código un número determinado de veces en función de si se cumple una condición. Esto es muy útil para realizar las tareas repetitivas que de otra forma tendríamos que escribir cientos de veces. Si pensamos en el típico castigo de colegio de "Escribe en una hoja 100 veces no volveré a dejarme los libros en casa", gracias al bucle `for` solo tendríamos que escribirlo una vez y decirle que se repita hasta que llegue a 100 veces. Imagina la cantidad de tiempo y código que permite ahorrarnos este recurso.

## ¿En qué casos se utilizan?

Si pensamos en una web, la mayoría de los datos vienen en una lista (solo hace falta recordar la de `ul`s y `li`s que hemos puesto hasta ahora).
Algunas de las aplicaciones más típicas de los arrays son:

- los resultados de búsqueda
- la lista de coordenadas de un mapa
- los artículos de un carrito de la compra
- las tareas de una lista de tareas
- los contactos de una lista de contactos.

Todos estos ejemplos anteriores se suelen almacenar en arrays para poderlos modificar (por ejemplo ordenar por orden alfabético o añadir un nuevo elemento), trabajar con ellos de forma sencilla y mostrarlos en nuestra web.

Los bucles se utilizan para repetir código, por ejemplo:

- Si tenemos 48 contactos, por cada contacto mostrar una tarjeta de contacto en la página
- Mostrar el total de un carrito de la compra sumando todos los precios de los artículos
- Mostrar todas las fechas hasta la actualidad en un select de un formulario

## Array

Un array es la estructura que utilizamos en JavaScript para almacenar listas de datos ordenados.

Un array puede contener cualquier tipo de dato (`string`, `number`, `boolean`, `object` incluso otros `arrays`). De hecho, un mismo array puede contener datos de distinto tipo mezclados, aunque es algo poco recomendable.

Cada elemento dentro de un array irá asociado a un índice, ese índice nos permitirá obtener el dato de una determinada posición del array o modificarlo. Un dato importante a tener en cuenta es que **el índice de los arrays empieza por el número 0**, por lo que el primer elemento tendrá índice 0, el segundo tendrá 1, el tercero 2 y así sucesivamente.

```js
// Array donde el orden es importante
const weekdays = ['Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes', 'Sábado', 'Domingo'];
```

En este ejemplo, 'Lunes' está en la posición 0 del array, y 'Domingo' en la posición 6.

> **NOTA:** Por lo general es poco recomendable mezclar varios datos diferentes en un array, en esos casos es mejor usar un objeto.

```js
// Un array con distintos datos (poco recomendable)
const madrid = ['Madrid', 40.4893538, -3.6827461];

// Tiene más sentido como objeto
const madrid = {
  name: 'Madrid',
  latitude: 40.4893538,
  longitude: -3.6827461
};
```

## Trabajando con arrays

A continuación vamos a ver cómo trabajar con arrays, cuáles son sus principales propiedades y métodos y cómo realizar operaciones básicas con ellos.

### Declaración de un array

Al igual que las cadenas y los números, podemos usar un `array` sin asignarlo a una variable `[1, 2, 3]`, pero normalmente crearemos una variable o constante para guardar su valor.

La sintaxis para declarar una variable o constante y asignarle como valor un array es la siguiente:

```js
// Crea una variable con un array vacío
const arr1 = [];

// Crea un array con dos números
const arr2 = [1, 2];

// Crea un array con cuatro datos
const arr3 = ['Laura', 'Pedro', 'Marta', 'Diego'];
```

> **NOTA:** Cuando un array contiene varios elementos suele ponerse en cada uno de ellos en una nueva línea como se ve en `arr3`, para facilitar su lectura.

### Obtener información de un array

Bien, ahora que sabemos cómo crear un array, es el momento de descubrir cómo podemos obtener información a partir de él. Como hemos comentado anteriormente, los arrays contienen una lista de datos y cada uno de esos datos va asociado a un número, un índice.

Sabiendo esto, si queremos obtener el valor que hay en una posición concreta de un índice, lo único que deberemos hacer será indicar la variable que contiene el array seguida del índice del valor que buscamos, que irá entre corchetes:

```js
const fruits = ['pera', 'manzana', 'naranja', 'plátano'];
console.log(fruits); // Muestra el array completo: 'pera', 'manzana', 'naranja', 'plátano'
console.log(fruits[1]); // Muestra 'manzana' (recordemos que el primer índice es 0)
console.log(fruits[3]); // Muestra 'plátano'
```

Un dato importante es que para obtener el valor que queremos del array podemos utilizar una variable en vez de un número. Imaginemos que queremos hacer una aplicación que simule el típico sorteo en el que cada uno de los participantes saca un papel de una urna y tiene un premio asociado. Si quisiéramos hacerlo con JavaScript, podríamos hacer algo parecido a lo siguiente:

```html
<label for="lotteryNumber">Introduce un número del 1 al 4</label> <input id="lotteryNumber" type="text" />
```

```js
const options = ['coche', 'viaje', 'crucero', 'llavero'];
const lotteryNumberInput = document.querySelector('#lotteryNumber');

function handleLotteryNumberChange(event) {
  const input = event.currentTarget;
  const selectedNumber = parseInt(input.value);
  const ind = selectedNumber - 1; // El índice empieza en 0
  const result = options[ind]; // Utilizamos una constante que contiene un número como valor
  console.log('Premio: ', result);
}

lotteryNumberInput.addEventListener('keyup', handleLotteryNumberChange);
```

### Añadir un elemento

Para añadir un elemento simplemente asignaremos un valor a un índice de un array:

```js
const arr = []; // Creamos un array vacío
arr[0] = 'Hola'; // Añadimos un elemento en el índice 0, la primera posición del array
arr[1] = '¿qué tal?'; // Añadimos un elemento en el índice 1, la segunda posición del array

// Tras los pasos anteriores arr será igual a  ['Hola', '¿qué tal?']
```

> **NOTA:** Es importante saber que si asignamos un valor a un índice más alto que la longitud del array, se crearán espacios vacíos:

```js
const arr = [1, 2, 3];
arr[8] = 24; // Saltamos del índice 2 al 7 (5 espacios) para añadir un valor en el 8

console.log(arr); // Muestra 1,2,3,,,,,,24 (un array con 5 espacios vacíos)
```

### Modificar un valor

Para modificar unos de los valores del array utilizaremos la misma sintaxis que para añadir un nuevo elemento. A la hora de escribirlo no habrá diferencia, pero el funcionamiento será distinto ya que en este caso estaremos sobrescribiendo el valor anterior.

```js
const arr = ['plátano', 'manzana', 'pera']; // Creamos un array con tres elementos
arr[1] = 'limón'; // Sobrescribimos el valor que hay en la segunda posición del array

// Tras los pasos anteriores arr será igual a  ['plátano', 'limón', 'pera']
```

#### EJERCICIO 1

**Películas**

Vamos a hacer este ejercicio en parejas. ¿Listas? La primera de la pareja con el teclado va a crear un array `movies` con un listado de 3 películas que le gusten. Será un array de cadenas (`strings`).

Ahora toma el teclado la otra compañera y añade al array anterior otra película más que le guste. No vale modificar la declaración del array, sino que añadiremos la nueva película en la posición 3 del array (recordad que se empiezan a numerar desde el 0). Para comprobar que funciona, tienes que mostrar el array completo en la consola.

El teclado vuelve a la primera de la pareja. Tienes que modificar la película que menos te guste de las que hay en el array (¿podría ser la que ha puesto tu compañera? :P) por el nombre de otra que te guste más. Para comprobar que funciona, tienes que mostrar el array completo en la consola.

El teclado vuelve a la segunda de la pareja. Ahora es tu turno de modificar la película que menos te guste del array por otra. De nuevo, muestra el array completo en la consola para comprobar que funcionó.

Para terminar este ejercicio, vamos a encapsular todo el código que hemos creado en una función que no toma parámetros y que llamaremos `workWithMovies`. Ejecutamos la función para comprobar que se muestran los mensajes en la consola correspondientes.

\_\_\_\_\_\_\_\_\_\_

### Los arrays son un tipo de datos especial

Una cosa importante a tener en cuenta es que cuando asignamos un array a una constante (o variable) realmente no asignamos a la constante ese valor sino un un _enlace a ese array_. Es exactamente lo mismo que nos sucedía con los objetos, ¿lo recuerdas? Y es que técnicamente el tipo de dato de los arrays, las funciones y los objetos literales ¡es `object`!

Así en el caso de los arrays creamos un dato y cuando lo asignamos a una constante en lugar de almacenar ese dato almacenará la referencia (enlace) que apunta al dato.

Y te estarás preguntando, ¿y en qué me afecta esto a mí? Imaginemos que creamos un array llamado `arr`:

```js
const arr = [1, 2, 3, 4];
```

En ese caso estaremos creando un array `[1, 2, 3, 4]` y la constante `arr` apuntará a ese array.

Si más tarde guardamos `arr` en otra constante llamada `arr2` de esta forma:

```js
const arr2 = arr;
```

Lo que estamos diciendo es que `arr2` va a guardar la información que tiene `arr` y por tanto, al igual que `arr` apuntará al array que hemos creado anteriormente.

Bien, el problema viene ahora, ambas constantes apuntan al mismo array por lo que si modificamos una estaremos modificando también la otra, ya que lo que va a hacer JavaScript es modificar el array al que apuntan.

```js
const arr = [1, 2, 3, 4];
const arr2 = arr;

arr[4] = 5;

console.log(arr[4]); // Imprime 5 en la consola
console.log(arr2[4]); // Imprime también 5 en la consola
```

Este tipo de comportamiento de guardar un _enlace_ a un dato, en lugar del dato como tal, se llama asignación por referencia y así es como almacena JavaScript los arrays. Tener esto en cuenta es muy importante ya que si lo aprendemos evitaremos bastantes problemas en el futuro a la hora de guardar arrays en constantes (o variables) y copiarlos.

### La propiedad length

Como los arrays son un tipo especial de objetos, tienen propiedades y métodos. Gracias a las propiedades podremos obtener información del array y gracias a los métodos podremos generar acciones sobre ellos para modificar sus datos u obtener un nuevo resultado.

La propiedad `length` sirve para obtener la longitud del array o en otras palabras cuántos elementos contiene. Como cualquier otra propiedad, para utilizarla simplemente escribiremos el nombre del array seguido por un punto y a continuación `length`:

```js
const arr = [1, 2, 3];

console.log(arr.length); // Mostrará un mensaje con la longitud del array (3)
```

> **NOTA:** Un error que suele producirse a menudo es que escribimos _lenght_ en lugar de _length_. La segunda sería la forma correcta. Es importante tener cuidado, y cuando sea posible utilizar el autocompletado de nuestro editor, porque es un error que es difícil de percibir y bastante molesto.

### La función isArray

Hasta ahora ya conocíamos la función `typeof()` que nos devolvía el tipo de una variable. Para saber si una variable es un array o no, existe el método `Array.isArray()` que nos devuelve `true` o `false` dependiendo de qué variable le pasemos. Con un ejemplo se entiende mucho mejor:

```javascript
const list = [1, 2, 3];
Array.isArray(list); // true
const name = 'Ada';
Array.isArray(name); // false
```

Para más información leed la defición del [método `Array.isArray()` (2 minutos)](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Array/isArray).

## Bucles

Sirven para ejecutar un mismo código un número determinado de veces. _Haz esto x veces_.

### Bucle `for`

Tiene la siguiente estructura:

- podemos identificarlo por usar al comienzo la palabra `for`
- después irá la _configuración_ del bucle entre paréntesis `( )` que tiene 3 partes, separadas por punto y coma `;`:
  - _inicialización_ será una declaración y asignación de variable (ej: `let i = 1`, se suele usar `i` por la palabra index)
  - _condición_ será la condición que debe cumplirse para que se ejecute el bloque de código (ej: `i < 20`)
  - _actualización_ será la operación que se realizará al final de cada iteración del bucle (ej: `i++`, que es la abreviación de `i = i + 1`)
- al final definimos un _bloque de código_ entre llaves `{ }` que se va a ejecutar si se cumple la condición

```js
for (let i = 0; i < 20; i++) {
  console.log('Me encantan los bucles 💪');
}
```

En este ejemplo de código, hacemos aparecer 20 veces en la consola el texto `Me encantan los bucles 💪`. Funciona de la siguiente forma:

1. Se ejecuta el código de inicialización (`let i = 0`)
2. Se comprueba que la condición se cumple (`i < 20`), en este caso el resultado es `true`
3. Como la condición se cumple, se ejecuta el código que hay dentro del bloque entre las llaves (`{}`), es decir el `console.log`
4. Se ejecuta la actualización del bucle (`i++`) y la variable `i` pasa a valer 1
5. Vuelta al paso 2
6. Cuando la variable `i` llega al valor de 20, la condición ya no se cumple (20 no es menor que 20), por lo tanto el bloque que contiene el console log no se ejecuta y el bucle acaba

Otro aspecto interesante de los bucles `for` es que dentro del bloque de código que se repite (el que va entre llaves `{ }`) podemos usar la variable `i`. Por ejemplo:

```js
for (let i = 0; i < 20; i++) {
  console.log('Voy por la vuelta ' + i);
}
```

Este ejemplo hará aparecer 20 veces, en la consola, el texto:

- Voy por la vuelta 0
- Voy por la vuelta 1
- Voy por la vuelta 2

...

- Voy por la vuelta 19

#### EJERCICIO 2

Partiendo el ejemplo anterior, crea un bucle que muestre 10 veces, en la consola, el texto `Voy por la vuelta X` siendo el número de vueltas desde 1 hasta 10 (no desde 0 hasta 9).

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

Vamos a partir de una variable `acc` con valor 0. Construiremos un bucle que se ejecute 10 veces y sume 2 a la variable `acc` en cada iteración del bucle. Al acabar el bucle, mostraremos en la consola el texto `El resultado es: X`, siendo X el valor de la variable `acc`.

> NOTA: Este tipo de variables como `acc` que se va actualizando y al final tiene el resultado de varias operaciones se llama _acumulador_. Puede ser de tipo numérico pero también de tipo cadena si vamos acumulando una cadena cada vez más larga.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

**Previsión para ver la _Luna del cazador_**

Cada 3 años se produce una luna llena completamente iluminada por el Sol durante unos minutos. Esta luna es conocida como la “Luna del cazador”. En el año 2017 se pudo ver esta luna el 5 de octubre y mucha gente se la perdió. Para que no nos pase los siguientes años vamos a crear un código que muestre en consola cuándo serán las 15 próximas lunas.

> NOTA: Vamos a realizar este ejercicio de forma que, antes de programar nada, escribamos el un papel el listado de las acciones (_algoritmo_) que tenemos que realizar para conseguir el resultado que buscamos. Una vez escrito este listado, ya nos pondremos a programarlo en JS.

\_\_\_\_\_\_\_\_\_\_

### Iterando sobre los elementos de un array

Cuando trabajamos con arrays es muy común que tengamos que realizar alguna operación sobre todos sus elementos para modificarlos o generar un nuevo array a partir de ellos. Por eso es muy normal que veamos usos de arrays combinados con el uso de bucles `for`. Veamos un ejemplo en el que combinaremos ambos. En este ejemplo, vamos a tener una lista de puntuaciones y vamos a sumarlas para saber cuál será la puntuación final obtenida:

```js
const scores = [4, 2, 7, 8, 6, 7, 9, 1, 2, 6, 7];

// Creamos una variable fuera del bucle para que no se sobrescriba en cada iteración
// En esta variable iremos sumando cada una de las puntuaciones
let acc = 0;

// La i empieza en 0 porque el índice de los arrays empieza en 0 también
for (let i = 0; i < scores.length; i++) {
  acc += scores[i];
  // Sumamos a `acc` el valor actual del array en cada iteración del bucle
  // acc += arr[i] es igual a acc = acc + arr[i]
}

console.log('La puntuación final es ' + acc);
```

#### EJERCICIO 5

**La media**

a) Vamos a crear un nuevo array `numbers` que contendrá 5 números cualesquiera. Vamos a recorrer el array mediante un bucle para calcular la media de los números (la suma de los números dividido por cuántos hay, es decir, 5). Necesitaremos una variable (_acumulador_) para ir almacenando la suma de todos los números y después poder hacer la media. Para comprobar si el resultado es correcto, vamos a _loguearlo_ en la consola.

b) Ahora vamos añadir un nuevo número al array y repetir el cálculo de la media. En este caso, para calcular la media habrá que sumar todos y dividir entre el total, que ahora es 6.

c) Vamos a generalizar el código anterior creando una función `average`. Esta función toma como parámetro un array `numbers`, calula la media del array (de cualquier longitud) y devuelve la media. Para poder trabajar con arrays de cualquier longitud, deberemos consultar la longitud del array mediante su propiedad `length`. Para comprobar que la función hace el cálculo correcto, la invocaremos (o ejecutaremos para que no suene tan esotérico) varias veces pasándole como argumento un array con diferente longitud cada vez y mostraremos el resultado en la consola del navegador.

\_\_\_\_\_\_\_\_\_\_

## Bucle `for...of`

El bucle `for...of` de ES6 nos permite recorrer un objeto iterable, como son los arrays, sin tener que escribir las condiciones de un `for`. Además, nos permite usar nombres mucho más reconocibles para los valores dentro del array.

```js
const bestAnimatedFeature2016Nominees = ['Zootopia', 'Kubo and the Two Strings', 'La tortue rouge', 'Ma vie de Courgette', 'Moana'];

// bucle for
for (let i = 0; i < bestAnimatedFeature2016Nominees.length; i++) {
  console.log(`"${bestAnimatedFeature2016Nominees[i]}" was nominated to 89th Academy Awards`);
}

// bucle for...of
for (const movie of bestAnimatedFeature2016Nominees) {
  console.log(`"${movie}" was nominated to 89th Academy Awards`);
}
```

> **Nota**: si quisiéramos modificar los valores del array, tendríamos que hacer un bucle `for` como ya sabíamos. `for...of` solo nos permite leer los datos, ya que no nos da información sobre el índice.

#### EJERCICIO 6

**Tenemos mucho en común**

Usando `for...of` vamos a hacer un pequeño programa que le pregunte a la usuaria cuáles son sus dos películas o libros favoritos mediante un formulario. Cuando pulse el botón `enviar` guardaremos la información en un array, lo recorreremos y mostraremos este mensaje por cada obra: "¡A mí también me encantó "OBRA"! Tenemos mucho en común, humana.", donde OBRA será el nombre de la obra.

\_\_\_\_\_\_\_\_\_\_

### Combinando arrays con objetos

Como comentábamos anteriormente, podemos tener arrays dentro de objetos u objetos dentro de arrays porque ambos pueden ser tratados como un valor más:

```js
// Lista de contactos (array con objetos dentro)
const contacts = [
  {
    name: 'Raquel',
    phone: '915552323',
    email: 'raquel@inbox.com'
  },
  {
    name: 'Pedro',
    phone: '915554564',
    email: 'pedro@inbox.com'
  },
  {
    name: 'Laura',
    phone: '915555656',
    email: 'raquel@inbox.com'
  }
];

console.log(contacts[0].name); // Muestra el nombre del primer contacto (Raquel)
contacts[2].email = 'laura@inbox.com'; // Cambia el email del tercer contacto
console.log(contacts[2].email); // Muestra el email del tercer contacto ('laura@inbox.com')

// Tarea con participantes (objeto con array dentro)
const task = {
  name: 'Crear un repositorio',
  participants: ['Raquel', 'Pedro', 'Laura']
};

console.log(task.participants[0]); // Muestra el nombre del primer participante (Raquel)
task.participants.push('Diego'); // Añade un nuevo participante a la lista
task.participants[0] = 'Andrea'; // Cambia el nombre del primer participante
console.log(task.participants); // Muestra Andrea, Pedro, Laura, Diego
```

#### EJERCICIO 7

**A story `of` adalabers**

Estamos en una clase de Adalab, y queremos conocer algunas estadísticas sobre las adalabers de esa clase. Estos son sus datos:

- María, 29 años, diseñadora
- Lucía, 31 años, ingeniera química
- Susana, 34 años, periodista
- Rocío, 25 años, actriz
- Inmaculada, 21 años, diseñadora

En primer lugar, vamos a crear una estructura de datos en JavaScript para manejar estos datos. Usaremos arrays y objetos para crearla.

Después, vamos a crear varias funciones en JavaScript que nos permitan calcular de forma automática estadísticas sobre las adalabers. Todas ellas toman como parámetro un listado de adalabers similar a nuestra estructura de datos anterior.

1. Una función `countAdalabers` que devuelve el número de adalabers en el listado.
2. Una función `averageAge` que devuelve la media de edad de listado.
3. Una función `theYoungest` que devuelve el nombre de la adalaber más joven.
4. Una función `countDesigners` que devuelve el número de adalabers que son diseñadoras.

Según vayáis creando las funciones, debéis ir probando que funcionan invocándolas con nuestra estrucutra de datos como argumento. Al final, modificad la estructura de datos para añadir, modificar o quitar adalabers. Y probad que las funciones siguen devolviendo el valor correcto.

\_\_\_\_\_\_\_\_\_\_

## `querySelectorAll`

Hay muchas funciones nativas de JavaScript que retornan arrays. Son aquellas funciones que devuelven un listado de elementos, propiedades u otras cosas... Una de estas funciones es `querySelectorAll`.

Como hemos visto en sesiones anteriores, para recoger un elemento de HTML utilizamos el método `querySelector`. Pero ¿y si queremos recoger más de uno, por ejemplo todas las etiquetas que tengan una determinada clase? `querySelectorAll` al rescate.
Este método devuelve una lista de elementos que funciona de manera similar a un array. Podríamos hacer lo siguiente:

```js
// Guardamos una lista de todos los parrafos de la página
const paragraphs = document.querySelectorAll('p');

// Modificamos el primer párrafo
paragraphs[0].innerHTML = 'Soy el primero';

// Muestra el número de parráfos que hay en nuestra web
console.log(paragraphs.length);

// Iteramos sobre todos los párrafos para asignarles a todos una clase
for (let i = 0; i < paragraphs.length; i++) {
  paragraphs[i].classList.add('highlight');
}
```

#### EJERCICIO 8

**Botones de alarma**

Vamos a partir de un HTML que tiene 3 botones con el texto ALARMA en un fondo blanco. Vamos a hacer que al pulsar en cualquiera de ellos, el fondo de la pantalla se ponga rojo. Si volvemos a pulsar en cualquiera de ellos, el fondo se pondrá blanco. Y así sucesivamente. Vamos a hacer uso de `querySelectorAll` para evitar repetir mucho código.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 9

Vamos a practicar un poco más con el método `querySelectorAll`:

1. En esta misma página abrimos las herramientas para desarrolladoras de Chrome (DevTools) y seleccionamos la pestaña `Consola`.
1. Escribimos el siguiente código: `document.querySelectorAll('h1')`. ¿Qué está devolviendo este método?
1. Y si escribimos `document.querySelectorAll('h1')[0]` ¿qué está mostrando en consola este código?
1. Ahora escribimos `document.querySelectorAll('h1')[0].className`. ¿qué información nos muestra? ¿Y el código `document.querySelectorAll('h1')[0].innerText`?
1. Y por último ¿qué muestra el código `document.querySelectorAll('asdf')` y por qué?

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 10

Para finalizar la lección de hoy queremos hacer un ejercicio que muestre en consola el tipo datos que hay en un array. Dado el siguiente array:

```javascript
const items = [
  'Ada',
  1815,
  ['Informática', 'Matemática', 'Escritora'],
  {
    mother: 'Anna Isabella',
    father: 'Lord Byron'
  }
];
```

Escribid un script que recorra los datos de este array y pinte en consola por cada elemento: "El dato VALOR está en la posición X y es de tipo TIPO".

Por ejemplo "El dato Ada está en la posición 0 y es de tipo string".

\_\_\_\_\_\_\_\_\_\_

## Bonus `for...in`

Ahora que ya sabemos recorrer arrays, seguro que te estás preguntando si se pueden recorrer objetos. La respuesta es: claro que sí!

Imaginemos que tenemos el código HTML de login:

```html
<form>
  <label for="email">Email</label>
  <input type="text" name="email" class="js-email" />
  <label for="password">Contraseña</label>
  <input type="password" name="password" class="js-password" />
  <input type="submit" value="Enviar" />
</form>
```

Podemos prerellenar los campos del formulario con los datos de la usuaria para ella solo tenga que pulsar en el botón **Enviar**. Lo haríamos con el siguiente código:

```javascript
const userData = {
  email: 'info@email.com',
  password: 'mi-contraseña-super-secreta'
};
for (let item in userData) {
  const inputElement = document.querySelector(`.js-${item}`);
  inputElement.value = userData[item];
}
```

En la [documentación oficial](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Sentencias/for...in) podrás averiguar cómo funciona `for...in`.

## Recursos externos adicionales

- [3.05. Arrays I de Ada Lovelace](https://youtu.be/idhclogNzMU)
- [3.06. Arrays II de Ada Lovelace](https://youtu.be/nVNLcw70cso)
- [Sintaxis Básica V Arrays, Matrices, Arreglos. Píldoras informáticas](https://youtu.be/hTeFMke6F6Q)
- [Sintaxis Básica V. Arrays, Matrices, Arreglos II. Píldoras informáticas](https://youtu.be/yn-o0rxXW0o)
