# Condicionales

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)
- [EJERCICIO 2](#ejercicio-2)
- [EJERCICIO 3](#ejercicio-3)
- [EJERCICIO 4](#ejercicio-4)
- [EJERCICIO 5](#ejercicio-5)
- [EJERCICIO 6](#ejercicio-6)
- [EJERCICIO 7](#ejercicio-7)
- [EJERCICIO 8 BONUS](#ejercicio-8-bonus)

<!-- /TOC -->

## Introducción

Utilizando aplicaciones y webs, muchas veces nos encontramos con casos en los que no se nos permiten determinadas acciones, por ejemplo, añadir un elemento más al carro de la compra si hemos superado el límite.

Las condicionales permiten tomar decisiones y realizar acciones en función de una serie de datos. Gracias a ellas diremos qué pasos queremos que siga la aplicación en cada momento para que se cumpla el objetivo que deseamos alcanzar.

Durante esta sesión veremos cómo controlar qué parte de nuestro código se ejecuta y cuál no. Aprenderemos a dar instrucciones a nuestras aplicaciones para realizar acciones en función de datos. Estableciendo normas al estilo si sucede esto haz esto otro y si no haz una orden alternativa. El condicional es una de las estructuras de control más básicas e importantes de cualquier lenguaje de programación.

¿Sabrías decir si en CSS hemos aprendido algún tipo de propiedad condicional?

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Los tipos de datos booleanos sirven para tener datos que representen verdadero o falso, como por ejemplo, saber si una condición se cumple o no. Los condicionales se basan en condiciones, es decir, la base fundamental para que funcionen correctamente son los booleanos y sin ellos no serían viables.

La mejor forma de explicar para qué sirven las condicionales es explicar cómo sería la programación sin ellas. En un mundo sin éstos tendríamos que escribir en nuestro código todos los pasos a llevar a cabo, uno a uno y no podríamos ejecutar un código u otro en función de una serie de datos. Por ejemplo no podríamos comprobar si un formulario tiene todos los campos rellenos para enviarlo; ni comprobar si hemos hecho scroll hasta una sección concreta de nuestra página para mostrar un elemento o activar una animación. Es decir, no habría distintas vías, sólo un posible camino, cosa que haría prácticamente imposible ejecutar un código realmente útil.

Las condiciones nos permiten evaluar algo y tomar un camino u otro.

## ¿En qué casos se utiliza?

Veamos algunos ejemplos donde se utiliza lo que vamos a ver durante esta sesión.

Los booleanos se utilizan para almacenar datos verdaderos o falsos, o convertir comparaciones a verdadero o falso:

- Guardar información del estilo, si el usuario está registrado o no, el campo se ha rellenado o no, etc.
- Guardar info sobre si un número es mayor o menor, si dos strings son iguales o no, si una variable existe, si una cadena de texto está vacía, etc.

Los condicionales se usan para realizar o no un código en función de una condición:

- Mostrar un mensaje de error si falta un campo obligatorio por rellenar en un formulario.
- Mostrar el símbolo de usuario verificado en Twitter si la cuenta está verificada.
- Mostrar una película en favoritos si está marcada como favorita.

## Booleanos

Los booleanos son tipos de datos de JavaScript que guardan información del tipo verdadero o falso. Solo pueden tener los valores `true` o `false`. Por ejemplo:

```js
const filled = false; // Este booleano es falso
const solved = true; // Este booleano es verdadero
```

Los booleanos son muy útiles para representar valores que solo pueden ser verdadero o falso. Por ejemplo, para representar si un usuario tiene o no avatar. O también para representar el resultado de una comparación. Por ejemplo, el número de tareas que tenemos que completar es menor que 5.

## Truthy y Falsy

En Javascript un **valor verdadero** o `Truthy` es un valor que se considera verdadero aunque su tipo no sea `boolean`. Todos los valores son verdaderos a no ser que estén en la lista de los definidos como "Falsy".

Los valores `Falsy` son aquellos que aun no siendo de tipo booleano, al evaluarse en un contexto booleano, se comportan como los booleanos de valor falso.

Los valores falsy son:

- false
- null
- undefined
- 0
- NaN
- ''
- ""

## Operadores de comparación

Podemos obtener también un booleano como resultado de una operación booleana, por ejemplo, una comparación. Siempre devuelven un valor booleano (`true` o `false`). Vamos a ver algunos operadores de comparación que devuelven booleanos.

### Igualdad

El operador comparación de igualdad es `===` (_strict equal_ o _estrictamente igual_) comprueba si dos valores son iguales y son del mismo tipo. Usaremos siempre esta versión para comparar si algo es igual. Existe también una versión `==` que solo compara el valor (no el tipo de datos) pero que NO debemos usar.

Ejemplo:

```js
const currentVegetable = 'lettuce';
const isLettuce = currentVegetable === 'lettuce'; // true
console.log(isLettuce);
const isTomato = currentVegetable === 'tomato'; // false
console.log(isTomato);
```

### Desigualdad

El operador de comparación de desigualdad es `!==` (_strict not equal_ o _estrictamente diferente_) comprueba si dos valores son diferentes en valor y tipo. Usaremos siempre esta versión para comparar si algo es distinto. Existe también una versión `!=` que solo compara el valor (no el tipo de datos) pero que NO debemos usar.

Ejemplo:

```js
const result = 5;
console.log(result !== 4 + 5); // true
console.log(result !== 0 + 5); // false
```

Otros operadores de desigualdad para comparar números:

- `<` (_less than_ o _menor que_) comprueba si el número a la izquierda del operador es menor que el que está a su derecha
- `>` (_greater than_ o _mayor que_) comprueba si el número a la izquierda del operador es mayor que el que está a su derecha
- `<=` (_less than or equal_ o _menor o igual que_) comprueba si el número a la izquierda del operador es menor o igual que el que está a su derecha
- `>=` (_greater than or equal_ o _mayor o igual que_) comprueba si el número a la izquierda del operador es mayor o igual que el que está a su derecha

Ejemplo:

```js
const result = 5;
console.log(result >= 4 + 5); // false
console.log(result >= 0 + 5); // true
console.log(result >= 4 - 5); // true
```

> **Nota**: Los operadores de comparación se ejecutan siempre después de los operadores numéricos, es decir, si tenemos `5 * 1 - 4 !== '3'`, primero se hará la multiplicación, luego la resta y finalmente se hará la operación de comparación.

## Operadores lógicos

Normalmente se usan con valores booleanos, en estos casos siempre devuelven `true` o `false`. Pero `&&` y `||` devuelven el valor de uno de los operandos, de manera que si estos no son booleanos, el valor devuelto tampoco lo será.

### Negación

Uso --> `!expression`

El operador `!` (_NOT_) devuelve el valor contrario al valor dado. Por ejemplo:

```js
const emptyNameField = true; // true
const nameIsFilled = !emptyNameField; // false
```

Cuando aplicamos una negación a un valor `truthy` o `falsy`, JavaScript primero lo convierte a booleano y después nos devuelve el valor contrario, esto es muy útil por ejemplo para saber si una variable está definida, o si tiene un string que no está vacío (que no es `''` o `""`).

```js
const nameField = document.querySelector('.input-name').value; // Accedemos al valor de un input que está en la página, y está vacío (falsy)
const emptyNameField = !nameField; // true
const nameIsFilled = !emptyNameField; // false
```

Podemos realizar la misma operación con el atajo `!!` (doble exclamación) que significa negar 2 veces. O lo que es lo mismo convertir un valor no booleano a uno booleano: _truthy_ en `true` o _falsy_ en `false`.

```js
const nameField = document.querySelector('.input-name').value; // '' (falsy)
const nameIsFilled = !!nameField; // false
```

Un truco para utilizar el operador `!` es pensar en humano. Para usarlo podemos hacer planteamientos de este tipo:

- ¿Tiene `nameField` un valor falso?

  La respuesta nos la dará su negación,`!nameField`.

  Cuando `!nameField` devuelve `true`, la respuesta es SI, `nameField` tiene un valor falso.

  Cuando `!nameField` devuelve `false`, la respuesta es NO, `nameField` tiene un valor verdadero.

- ¿Tiene `nameField` un valor verdadero?

  La respuesta nos la dará su doble negación, `!!nameField`.

  Cuando `!!nameField` devuelve `true`, la respuesta es SI, `nameField` tiene un valor verdadero.

  Cuando `!!nameField` devuelve `false`, la respuesta es NO, `nameField` tiene un valor falso.

> **Nota**: Trabajar con el operador `!` puede parecer un poco lioso al principio, no te preocupes si aún no tienes claro cómo aplicarlo, irá asentándose poco a poco con su uso.

### _AND_

Uso --> `expression1 && expression2`

El operador `&&` (_AND_) devuelve la primera expresión si esta es `falsy`, de lo contrario devuelve la segunda expresión.

Cuando trabajamos con booleanos devuelve verdadero **SOLO** si ambas condiciones son verdaderas. Por ejemplo:

```js
const name = 'María';
const age = 35;

name === 'María' && age >= 30; // true
name === 'Marta' && age >= 30; // false
name === 'María' && age >= 40; // false
name === 'Marta' && age >= 40; // false
```

Cuando trabajamos con no booleanos `&&` es muy útil para asignar valores a constantes y variables de manera condicional.

```js
const isModerator = true;
const isAdmin = false;
const userName = 'Layla';

// Como la primera expresión es `truthy`, se devuelve la segunda expresión
const moderatorName = isModerator && userName; // Layla

// Como la primera expresión es `falsy`, se devuelve esta, y la segunda ni siquiera llega a evaluarse.
const adminName = isAdmin && userName; // false
```

### _OR_

Uso --> `expression1 || expression2`

El operador `||` (_OR_) devuelve la primera expresión si esta es `truthy`, de lo contrario devuelve la segunda expresión.

Cuando trabajamos con booleanos devuelve verdadero si **AL MENOS** una condición se cumple. Por ejemplo:

```js
const name = 'María';
const age = 35;

name === 'María' || age >= 30; // true
name === 'Marta' || age >= 30; // true
name === 'María' || age >= 40; // true
name === 'Marta' || age >= 40; // false
```

Cuando trabajamos con no booleanos `||` devuelve la primera expresión si esta es verdadera, de lo contrario devuelve la segunda expresión.

```js
const welcomeMessageElement = document.querySelector('.welcome__text');

const isAdmin = false;
const adminText = isAdmin && 'administradora';
const isModerator = true;
const moderatorText = isModerator && 'moderadora';

// Como la primera expresión es `falsy`, se devuelve la segunda expresión
welcomeMessageElement.innerHTML = `Bienvenida ${adminText || moderatorText}. ¡Es genial verte de nuevo!`;
```

> **Nota**: Aunque no lo hemos puesto en los ejemplos se pueden evaluar más de 2 condiciones seguidas, por ejemplo: `name === 'María' && age >= 30 && career === 'adalaber' && favoriteLanguaje === 'JavaScript'`

#### EJERCICIO 1

**Nadie sin avatar**

Partiendo de estas bases de html y js, vamos a realizar un programa para completar el perfil de un usuario.

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="utf-8" />
    <title>Mi primer código JavaScript</title>
  </head>
  <body>
    <div class="user">
      <h1 class="user__name">Bill</h1>
      <img class="user__avatar" />
    </div>
    <script type="text/javascript" src="main.js"></script>
  </body>
</html>
```

```js
'use strict';

// avatar por defecto
const DEFAULT_AVATAR = 'http://placehold.it/300x300';
// avatar que eligió el usuario al registrarse
let userAvatar = 'http://www.fillmurray.com/300/300';
```

Paso a paso:

1. Hagamos la lógica para añadir, desde javascript, la imagen `userAvatar` a la etiqueta de HTML `img`.
2. Ahora vamos a plantear que `userAvatar` pueda no contener una URL porque, por ejemplo, cuando el usuario se registró no encontraba ninguna foto molona y decidió que la subiría en otro momento. Para ello tenemos que cambiar el contenido de `userAvatar` a comillas vacías `let userAvatar = '';`. ¡Ahora no debería verse ninguna imagen en la página!
3. Vamos a mejorar nuestro programa para que la ficha de usuario tenga una imagen sí o sí, de manera que:
   - si tenemos el avatar del usuario se muestre este.
   - si no tenemos datos del avatar del usuario, se muestre el avatar por defecto

> **NOTA**: En este ejercicio aún no vamos a usar condicionales `if`/`else`, tenemos que apoyarnos en el operador _OR_ para asignar al atributo `src` de la etiqueta `img` un valor u otro ;)

> **NOTA**: Cambia manualmente el valor de `userAvatar` ('http://www.fillmurray.com/300/300' o '') para comprobar que el programa funcionará para los usuarios que añadieron su foto y para los que no lo hicieron.

\_\_\_\_\_\_\_\_\_\_

## Condicionales

Los condicionales son estructuras de control de JavaScript que sirven para ejecutar un código u otro (o ninguno) en función de si se cumple o no una condición.

_Si esta condición es verdadera, haz esto, y si no, esto otro_. La condición que escribamos siempre se va a convertir en `true` o `false`.

### If...else

La estructura simple de un condicional es la siguiente:

- usamos la palabra `if` para definirlo
- después indicamos entre paréntesis `( )` una condición
- a continuación definimos un bloque de código entre llaves `{ }` que se va a ejecutar si se cumple la condición

Podemos pensar en ellos como un _"Si...haz..."_.

```js
const age = 35;

if (age > 30) {
  console.log('Tienes más de 30 años'); //Esta línea se ejecuta solo si se cumple la condición
}
```

Existe otra estructura para el condicional que nos permite ejecutar otro código cuando no se cumpla la condición. Partiendo de la estructura simple, añadimos:

- usamos la palabra `else` para definir qué hacer cuando NO se cumple la condición
- a continuación definimos un bloque de código entre llaves `{ }` que se va a ejecutar si NO se cumple la condición

Podemos pensar en ello como un _"Si...haz...si no haz..."_.

```js
const age = 35;

if (age > 30) {
  console.log('Tienes más de 30 años'); //Esta línea se ejecuta solo si se cumple la condición
} else {
  console.log('Como mucho tienes 30 años'); //Esta línea se ejecuta solo si NO se cumple la condición
}
```

#### EJERCICIO 2

**Control de acceso**

En este ejercicio vamos a crear un control de acceso. Para ello prepararemos una variable y le asignaremos un nombre. Posteriormente, si el nombre es el tuyo o el de tu compañera mostraremos el mensaje "Bienvenida, (tu nombre aquí)". Si el nombre es diferente al tuyo deberá mostrar "Lo siento pero el usuario que has introducido no está registrado".

> **Nota**: cambia el valor de la variable y comprueba que todo funciona como esperas.

\_\_\_\_\_\_\_\_\_\_

Podemos complicar incluso más la estructura del condicional cuando queremos que se ejecute un código si NO se cumple la primera condición pero SOLO si se cumple una segunda condición. En este caso, a la estructura del condicional simple le añadimos:

- usamos la palabra `else` para definir qué hacer cuando NO se cumple la condición
- usamos la palabra `if` para definir una nueva comprobación
- después indicamos entre paréntesis `( )` una segunda condición
- a continuación definimos un segundo bloque de código entre llaves `{ }` que se va a ejecutar si se cumple esta segunda condición

Podemos pensar en ello como un _"Si...haz...si no si...haz..."_.

```js
const age = 35;

if (age > 30) {
  console.log('Tienes más de 30 años'); // Esta línea se ejecuta solo si se cumple la condición
} else if (age >= 20) {
  console.log('Tienes entre 20 y 30 años'); // Esta línea se ejecuta solo si se NO cumple la primera condición y SÍ se cumple la segunda
}
```

Si necesitamos una estructura más complicada, siempre podemos poner un `else` al final para ejecutar código cuando no se ha cumplido ninguna de las condiciones. Además, podemos incluir todas las condiciones que queramos con `else if`.

```js
const age = 35;

if (age > 30) {
  console.log('Tienes más de 30 años'); //Esta línea se ejecuta solo si se cumple la condición
} else if (age >= 20) {
  console.log('Tienes entre 20 y 30 años'); //Esta línea se ejecuta solo si se NO cumple la primera condición y SÍ se cumple la segunda
} else if (age >= 10) {
  console.log('Tienes entre 10 y 19 años'); //Esta línea se ejecuta solo si se NO cumplen la primeras condiciones y SÍ se cumple la última
} else {
  console.log('Eres un niño entre 0 y 9 años'); //Esta línea se ejecuta solo si se NO cumplen ninguna de las condiciones anteriores
}
```

> **Nota**: Los bloques de un condicional son excluyentes, es decir, solo se va a ejecutar el código de un bloque (if, else if o else). En ningún momento se ejecutará el código de dos bloques ya que si se cumple una condición se ejecuta el código de su bloque y se ignoran las posteriores condiciones.

#### EJERCICIO 3

**Completa las condiciones**

Prepara una variable cuyo valor será un número.
Escribe las condiciones para el siguiente ejercicio y utilizando la variable haz pruebas para ver que estas se cumplen.

```js
if (/* condición 1 */) {
  console.log('El número es 0')
} else if (/* condición 2 */) {
  console.log('El número es negativo')
} else if (/* condición 3 */) {
  console.log('El número más 2 es mayor que 13 pero menor o igual que 20')
} else if (/* condición 4 */) {
  console.log('El número es mayor que 20 pero menor que 50')
} else {
  console.log('el número no es 123123125')
}
```

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

**Conversor de edad de perro a humano**

Te habrá pasado varias veces de ir por la calle y que alguien te pregunte "perdona, tienes a mano un conversor de edad de perros a humanos" y tener que contestar con vergüenza que no y que esa persona te mire raro... ¡hasta ahora! Vamos a crearla para evitar esto que pasa tan a menudo. Para ello, las reglas son las siguientes:

- El primer año de un perro equivale a 15 años de humano
- El segundo año de un perro equivale a nueve años de humano
- A partir del tercero, cada año de perro equivale a 5 años de humano.

> **Nota**: Prueba que el código funciona correctamente con distintos años (1, 2, 12...). Imagina el alcance de los daños si la próxima vez que te pare una persona para preguntarte por el conversor... ¡no funciona correctamente!

\_\_\_\_\_\_\_\_\_\_

### classList.contains

Vamos a ver un método nuevo de `classList` que es muy útil cuando trabajamos con condicionales, para ello vamos a plantear una posible situación. Imaginemos que tenemos un botón que sirve para mostrar y ocultar un elemento de nuestra página. De momento no vamos a ver cómo hacer que cuando pulses en un botón, se haga algo pero sí vamos a ver cómo podríamos ocultar un elemento sólo en el caso de que no estuviese oculto antes. Tendríamos que tener una forma de comprobar si un elemento tiene una clase o no, aquí es donde entra en juego `classList.contains()`. Con este método podremos comprobar si un elemento contiene una clase y nos devolverá un booleano (`true` o `false`).

Veamos el caso que estábamos comentando, tenemos un elemento que puede o no tener la clase `.hidden`. Vamos a comprobar si la tiene y en caso de ser así se la quitaremos y en caso de no tenerla se la añadiremos. Esto huele a `if` ¿verdad? :). Veamos el código:

```js
const activableSection = document.querySelector('.activable-section');

// Si contiene la clase hidden
if (activableSection.classList.contains('hidden')) {
  // Elimina la clase
  activableSection.classList.remove('hidden');
} else {
  // Si no, en caso contrario
  // Añade la clase hidden
  activableSection.classList.add('hidden');
}
```

#### EJERCICIO 5

**Notificaciones arcoiris**

Crea un div que contenga un título "NOTIFICACIÓN" y un texto "Mensaje por defecto".
Crea también tres clases:

- La primera, `.success`, aplicará un borde verde oscuro, un fondo verde claro y el color de fuente verde oscuro
- La segunda, `.error`, igual pero sustituyendo el verde por rojo
- La tercera, `.warning`, lo mismo pero usando el color amarillo

Usando JavaScript, haremos que:

- Si contiene la clase warning, el título sea 'AVISO' y el texto sea: 'Tenga cuidado'
- Si contiene la clase error, el título sea 'ERROR' y el texto sea: 'Ha surgido un error'
- Si contiene la clase success, el título sea 'CORRECTO' y el texto sea: 'Los datos son correctos'

Cambia la clase en HTML y comprueba que el código de JavaScript funciona.

\_\_\_\_\_\_\_\_\_\_

### Operador condicional o ternario

Podemos pensar en él como un atajo del `if...else` más sencillo.

La estructura de un ternario es la siguiente:

- Escribimos `?` y el código que se va a ejecutar si se cumple la condición
- Escribimos `:` y el código que se va a ejecutar si NO se cumple la condición

Solo debemos utilizar el operador ternario cuando:

- Queremos guardar un valor en una variable o constante.
- Solo queremos hacer una operación o sentencia dentro del `?` y del `:`. Si queremos hacer más cosas utilizaremos el `if - else`.
- Queremos hacer una operación dentro del `?` y otra dentro del `:`. Si no queremos hacer nada en el `:`, es decir el `else`, no podemos usar un operador ternario.

```js
const theme = 'hallowen';
const fontColor = theme === 'hallowen' ? '#ff5722' : '#000';
```

## Expresiones (expressions) y sentencias (statements).

Una expresión es cualquier unidad de código que produce un valor.

```js
myVar;

3 + x;

true ? 'Access allowed' : 'You may not pass';

'' || 'OneEyedMan';
```

Una sentencia realiza una acción.

```js
let avocados;
const avocadoPrice = 1.5;
const money = 33;

if (money >= avocadoPrice) {
  avocados = money / avocadoPrice;
} else {
  avocados = 0;
}
```

Normalmente cuando JavaScript espera una sentencia podemos escribir una expresión, pero no al revés. Por ejemplo podríamos haber escrito la sentencia `if...else` con un _ternario_, pero no podemos poner entre los paréntesis del if como condición otro if, ya que aquí JavaScript espera una expresión que produzca un valor `true`/`false`.
Si en este punto el concepto de expresión y sentencia es confuso, no te preocupes, es natural. Es un primer acercamiento a un concepto teórico y se irá aclarando con el tiempo ;)

#### EJERCICIO 6

Reescribe el código del ejemplo anterior (no del ejercicio anterior) utilizando un ternario en lugar de un `if...else`.

## Switch

Ya sabemos hacer varios **if...else** encadenados para comprobar una condición, y sabemos que si la primera condición es falsa, comprobamos la siguiente, y si esta también es falsa comprobamos la siguiente... hasta que comprobamos una condición que es verdad, o hasta que llegamos hasta el **else** final.

Algunas veces nos encontramos en que todas estas comprobaciones son "parecidas", es decir, **una parte de la comparación es la misma y la otra parte de la comparación cambia**.

En el siguiente ejemplo la parte izquierda de la comparación es la misma, siempre comparamos la constante `todayDate` con otras cosas. La parte derecha de la comparación cambia. Por ejemplo:

```js
const todayDate = 'Viernes';

if (todayDate === 'Lunes') {
  console.log('Hoy me tomo un café con Maricarmen');
} else if (todayDate === 'Martes') {
  console.log('Bajar al perro');
} else if (todayDate === 'Miércoles') {
  console.log('Vamos al cine a ver una peli');
} else if (todayDate === 'Jueves') {
  console.log('Juernesss');
} else if (todayDate === 'Viernes') {
  console.log('Cumpleaños de Paco');
} else if (todayDate === 'Sábado') {
  console.log('Comida con los suegros');
} else {
  console.log('Dormir hasta las 12');
}
```

Para trabajar con este tipo de condiciones disponemos de la herramienta **switch**. El código anterior con if...else hace lo mismo que el siguiente con switch:

```js
const todayDate = 'Viernes';

switch (todayDate) {
  case 'Lunes':
    console.log('Hoy me tomo un café con Maricarmen');
    break;
  case 'Martes':
    console.log('Bajar al perro');
    break;
  case 'Miércoles':
    console.log('Vamos al cine a ver una peli');
    break;
  case 'Jueves':
    console.log('Juernesss');
    break;
  case 'Viernes':
    console.log('Cumpleaños de Paco');
    break;
  case 'Sábado':
    console.log('Comida con los suegros');
    break;
  default:
    console.log('Dormir hasta las 12');
}
```

**Switch es un tipo de condicional**, en el cual:

1. JavaScript obtiene el valor de la variable o constante que pongamos dentro del primer paréntesis. En el ejemplo `switch (todayDate)`, que en este caso es 'Viernes'.
1. A continuación JavaScript compara este valor con cada uno de los valores de los `case`. Primero con `Lunes`, después con `Martes`...
1. Cuando el valor comparado `todayDate`, coincida con uno de los valores `case`, en el ejemplo `case 'Viernes'` se ejecutarán las líneas de código que hay desde el `case` hasta el siguiente `break`, en el ejemplo se ejecutará la línea `console.log('Cumpleaños de Paco');`.
1. Si ninguno de los valores del valor comparado `todayDate` coincide con un valor de `case`, JavaScript ejecutará la acción por defecto, es decir el código que está a continuación de `default`.

Algunas consideraciones:

* JavaScript compara los case en el orden en el que estén escritos.
* JavaScript solo ejecuta el primer `case` que coincida. Si escribimos más de un `case` que coincida, solo se ejecutará el primero.
* Entre un `case` y el siguiente `break;` puede haber una línea o las líneas de código que queramos.
* La opción `default` equivale al último else de un if...else.
* La opción `default` no es obligatoria.
* **Al igual que un operador ternario, un switch es un tipo específico de condicional.** Todo operador ternario y todo switch se puede reescribir como la combinación de varios if...else.

#### ¿Qué tengo que hacer hoy?

Vamos a practicar un poco, copia el switch de ejemplo que tenemos arriba, mételo en un fichero de JavaScript y ejecútalo para ver qué se muestra en consola.

A continuación cambia el día de la semana para ver qué se pinta en consola. Puedes añadir más *consoles* donde quieras.

#### EJERCICIO 7

Vamos a hacer un pequeño programa que te sugiera una receta en función del ingrediente que le pasemos.

Para resolverlo nos dan una variable en la que podemos declarar un ingrediente a elegir entre estos tres: pollo, merluza o espinacas, por defecto si no hay ingrediente pondrá 'Nada en la nevera' y según el ingrediente que le pasemos el programa nos devolverá un mensaje por consola diciéndote el ingrediente que has elegido y con las siguientes sugerencias de receta:
Filete con patatas / Merluzita en salsa verde / Espinacas rehogadas. Ejemplo: Tu ingrediente es pollo. Puedes freirte un filete con patatas.

```js
let ingredient = 'Pollo';

// aquí tu código
```

\_\_\_\_\_\_\_\_\_\_

## BONUS

### Módulo

El operador de resto (`%`), también llamado operador de módulo (_module_), es un operador especial utilizado en JavaScript para obtener el resto de la división entre dos valores. Si escribimos `5 % 2` en nuestro código, este nos devolverá el resto de esa operación, 1.

```js
0 % 80; // Devuelve 0
4 % 5; // Devuelve 4
13 % 5; // Devuelve 3
9 % 3; // Devuelve 0
```

El operador de módulo tiene el mismo orden de ejecución que los operadores de multiplicación y división.

> **Nota**: este operador es muy util para saber si un número es par o impar. Como recordatorio todos los números cuya división entre dos tienen como resto 0 son pares.

#### EJERCICIO 8 BONUS

Calcular cuál va a ser el siguiente año bisiesto

Vamos a escribir un pequeño programa que nos permita saber cuál será el siguiente año bisiesto. Para aportar un poco de información, sabemos que los años bisiestos se producen cada cuatro años a partir del año 0. El primer año bisiesto fue 4, el segundo 8 y así progresivamente. La idea de este ejercicio es que, si estuviésemos en el año 3, al ejecutarlo apareciese en la consola el texto "4", ya que el año 4 sería el siguiente año bisiesto.

**Pista:** Tenemos que escribir el año en el que estamos en una constante.

\_\_\_\_\_\_\_\_\_\_

Por cierto en CSS los media queries son una especie de condicional. Si el usuario tiene un pantalla de menor de 768px aplicamos una propiedad CSS, si están en una pantalla mayor aplicamos otras propiedades.

## Recursos externos

### Videos de Ada Lovelace en YouTube

En este canal tenemos varios vídeos que explican muy bien lo que necesitamos aprender en esta sesión con ejemplos y de forma bastante sencilla:

- [Operadores de comparación](https://www.youtube.com/watch?v=ICZXkflN-CA&index=11&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o)
- [Operadores lógicos](https://www.youtube.com/watch?v=S6qx7TCM4hU&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=12)
- [Condicionales. Sentencias If-Else](https://www.youtube.com/watch?v=9hUlwVjBSco&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=20)

### Introducción a JavaScript de Libros Web

- [Operadores](http://librosweb.es/libro/javascript/capitulo_3/operadores.html)
- [Elementos verdaderos y falsos](https://librosweb.es/libro/fundamentos_jquery/capitulo_2/elementos_verdaderos_y_falsos.html)
- [Estructuras de control de flujo](http://librosweb.es/libro/javascript/capitulo_3/estructuras_de_control_de_flujo.html)

> **Nota:** De las estructuras de control de flujo, no vamos a ver `for` de momento y muestra algunas cosas con arrays que por el momento tampoco veremos hasta dentro de un algunas sesiones.
