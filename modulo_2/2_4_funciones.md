# Funciones

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

## Funciones

Una función es un bloque de código que definimos una vez y lo reutilizamos las veces que queramos; un conjunto de instrucciones a las que podemos pasar diferentes datos para que nos devuelva resultados distintos.

Durante esta sesión veremos cuáles son las principales características de este recurso de programación y cómo utilizarlo en nuestro código para sacarle el máximo partido.

## ¿Para qué sirve lo que vamos a ver en esta sesión?

Las funciones son muy útiles a la hora de crear un código único para usarlo en distintas partes de nuestro programa. El beneficio de esto es que si en el futuro queremos modificar algo de ese código lo haremos en un único sitio aunque se utilice en decenas de sitios diferentes. Las funciones se ejecutan en distintos momentos y con distintas características gracias a los _parámetros_ y a los _argumentos_.

Otra de las ventajas de las funciones es que devuelven un valor, es decir, realizan una operación y pueden devolver un dato. Ese dato podemos asignárselo a una variable o usarlo dentro de otra operación. O incluso podemos prescindir de él si no nos interesa para nada.

Las funciones son una forma de agrupar código que vamos a usar varias veces permitiéndonos además, pasar diferentes valores para obtener diferentes resultados.

Podemos intentar hacer un paralelismo con el café, más o menos todo el mundo sabe hacer un café, desde los ingredientes a los diferentes pasos. Y cada vez que queramos uno seguimos todos los pasos uno a uno, y al final tendremos un café.

Ahora, las funciones serían como estas cafeteras modernas, a las que dependiendo de la cápsula que uses te hace un café diferente. Cuando activo la cafetera (llamo a la función) detecta qué tipo de capsula he introducido (parámetros) y me hace (me devuelve) un café u otro:

- Si utilizo una de estas cápsulas de hipster purista tendré un café de esos que no te dejan tomar si no llevas camisas de cuadros, patinetes y unas gafas de pasta.
- Si utilizo una cápsula más divertida que añada espuma, caramelo y coco pues tendré que huir de los hispters de antes porque para ellos este tipo de café debería ser ilegal.

Un ejemplo de esto sería:

```javascript
function makeMeCoffee(coffeeName) {
  return `Aquí tiene su ${coffeeName}, que lo disfrute`;
}
```

De manera que podemos llamar varias veces a la función y obtener "cafés" diferentes:

```javascript
makeMeCoffee('Café hipster con cuerpo de minotauro y esencia de madera y oro');
// devuelve "Aquí tiene su Café hipster con cuerpo de minotauro y esencia de madera y oro, que lo disfrute"

makeMeCoffee('Café con coco, nata y un toque de menta');
// devuelve "Aquí tiene su Café con coco, nata y un toque de menta, que lo disfrute"
```

## ¿En qué casos se utiliza?

Por ejemplo, en los siguientes casos:

- Si tenemos un código que convierte la primera letra de un texto a mayúsculas y vamos a usar ese código en varias partes de nuestro programa, creamos una función y ejecutamos la función en cada uno de los sitios necesarios
- Si queremos añadir varias clases a diferentes elementos HTML en función de la medida de la página web podemos crear una función y utilizarla en cada uno de ellos
- Si queremos enviar datos a un servidor, la mayoría de las veces es muy parecido y sólo cambian unos datos. Podríamos hacer una función y reutilizarla y usar distintos datos en cada una mediante los parámetros de la función (que veremos durante esta sesión)

## Declaración y uso de funciones

Para utilizar una función debemos declararla en algún sitio de nuestro código.

La estructura para declarar una función es

- primero la palabra reservada `function` seguida del nombre de la función
- después entre paréntesis `( )` los parámetros de la función separados por comas `,`, si no tiene parámetros estará vacío
- un bloque de código entre llaves `{ }` con las instrucciones de código de la función

```javascript
//Función sin parámetros
function hi() {
  return 'Hola';
}

//Función con parámetros
function sum(a, b) {
  return a + b;
}
```

Si añadimos las declaraciones anteriores de funciones a nuestra página, no veremos ningún efecto. Esto es porque solo estamos declarando las funciones, es decir, diciendo que existen pero nada más.

Para utilizar (también se le puede llamar _ejecutar_ o _invocar_) una función simplemente usamos el nombre de la función seguida de paréntesis donde pasaremos los argumentos separados por comas `,`.

```javascript
console.log(hi());
//Muestra en la consola la palabra 'Hola'

console.log(sum(1, 4));
//Muestra en la consola un 5
```

> NOTA: Esta sintaxis para utilizar funciones te suena, ¿verdad? Hasta ahora hemos estado ejecutando algunas funciones ya declaradas en el navegador como `querySelector('.title')` a la que le pasamos por parámetro una cadena con el selector que buscamos y nos devuelve la referencia a dicho elemento en nuestro HTML.

Así, una función es como una máquina:

- Se construye una vez (declarando la función)
- Se utiliza muchas veces (ejecutando la función)

Se pueden crear funciones sin nombre, estas funciones se llaman _funciones anónimas_. Estas funciones se suelen emplear para cosas que veremos en el curso más adelante, como asignarlas a una propiedad de un objeto o pasarlas como un callback. Un ejemplos de función anónima:

```javascript
const sum = function(a, b) {
  return a + b;
};

// La llamamos con el nombre de la variable
sum(2, 3); // devuelve 5
```

> **NOTA:** os acordáis que hasta ahora hemos estudiado 3 tipos de variables: number, string y undefined. Pues aquí estamos asignando a la variable `sum` un valor que es una función. Así que aquí tenemos un cuarto tipo de variable. Si ejecutamos el código `console.log('El tipo de sum es: ' + typeof(sum));` se mostrará en la consola `"El tipo de sum es: function"`.

## Parámetros y valores de retorno

Los _parámetros_ son los datos que definimos en una función y que, a la hora de ejecutarla, serán sustituidos por los _argumentos_ que le pasemos. Por tanto, en la declaración de la función le llamamos parámetros y en la ejecución le llamamos argumentos. Las funciones pueden tener 0, 1 o más parámetros separados por comas `,`.

Una función puede devolver un valor utilizando la palabra clave `return` seguida del valor que queremos devolver. Para devolver una variable `result`, utilizaremos `return result;` en el código.

```javascript
function sum(a, b) {
  const result = a + b;

  return result;
}

const sumResult = sum(3, 4); //sumResult vale 7
```

En este ejemplo, la función `sum` tiene 2 parámetros, a los que damos como nombre `a` al primero y `b` al segundo. Al ejecutarla en `sum(3, 4)` le pasamos los argumentos 3 y 4, que se asignan a los parámetros de forma que `a = 3` y `b = 4`. El valor de retorno es la variable `result` que contiene la suma de a y b, es decir, 7 en este caso. Este valor de retorno se asigna a la variable `sumResult` que recoge el resultado de la ejecución de la función.

Por defecto, si en una función no indicamos un valor de retorno usando `return`, la función devolverá el valor `undefined`. El valor _undefined_ en JavaScript indica que una variable ha sido declarada pero no posee ningún valor, en este caso determina que la función no tiene asignado ningún valor de retorno y por eso devuelve `undefined`.

```javascript
function sum(a, b) {
  const result = a + b;
}

const sumResult = sum(3, 4); //sumResult vale undefined
```

Cuando ejecutamos una instrucción `return` dentro de una función, termina la ejecución de la función. Todo el código que se fuese a ejecutar después de ese `return` será ignorado, como si no existiese. Por tanto, debemos evitar escribir líneas de código después de un `return` y normalmente será la última línea de código de una función.

```javascript
function sayHi(name) {
  return 'Hi ' + name;

  return 'En un lugar de la Mancha'; //Esta línea nunca se llega a ejecutar
}

const result = sayHi('Ashley'); //result vale 'Hi Ashley'
```

Observa la siguiente imagen:

![Máquina funciones](assets/images/2-4/maquina-funciones.png)

- Al crear la máquina sum le hemos puestos tres tubos llamados a, b y c, estos son los **parámetros**.

```js
function sum(a, b, c) {
  return a + b + c;
}
```

- Cada vez que la usamos pasamos valores por los tubos, por ejemplo 3, 56, 12, estos son los **argumentos**, y la maquina nos devuelve un resultado.

```js
const amount = sum(3, 56, 12);
console.log('Cantidad', amount);

const totalAges = sum(35, 26, 30);
console.log('totalAges', totalAges);

console.log('Exercises completed', sum(2, 6, 9));
```

Ahora que ya hemos visto bastante teoría sobre funciones vamos a ver un poco de práctica. Os hemos preparado un [ejercicio global grabado](./2_ejercicio_global_tienda_de_camisetas.md) donde cada día vamos a ir aplicando los conocimientos que vamos aprendiendo.

#### EJERCICIO 1

**Función multiplicación**

Crea una función que reciba como argumentos dos valores y devuelva como valor de retorno la multiplicación de ambos. Haz tres pruebas con distintos números para comprobar que funciona correctamente y muestra el resultado en la consola usando `console.log()`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 2

**Función media**

Crea una función con 4 parámetros numéricos que devuelva como valor la media de todos ellos. Haz tres pruebas con distintos números para comprobar que funciona correctamente y muestra el resultado en la consola.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 3

**Ticket con IVA**

Crea una función que reciba por parámetro un número, que representará un precio, y devuelva un texto en el que ponga el precio sin IVA, el IVA (21%) y el total. Por ejemplo, si pasamos por parámetro un 10, la función pintará en la consola `"Precio sin IVA: 10, IVA: 2,1 y Total: 12,1"`.

Para probar que funciona, ejecuta la función recogiendo el resultado en una variable e imprímela en la consola para comprobarlo.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 4

**Pares o nones**

Crear una función que reciba por parámetro un número y devuelva `true` si es par y `false` si es impar.

Ejecutala e imprime el resultado para comprobar que funciona.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 5

**`querySelector` para todas**

Estamos trabajando en un proyecto bastante grande, donde hay que recoger muchos elementos de HTML desde JavaScript para interaccionar con ellos. Para no tener que escribir `document.querySelector(...)` tantas veces una compañera ha sugerido hacer una función llamada `getEl`.

Esta función debe recibir por parámetro un selector de css y retornará el elemento de HTML correspondiente. Hemos quedado en que cuando llamemos a la función la sintaxis será tal que así:

```js
const btnEl = getEl('.btn');
```

> **Nota**: Prepara un HTML con varios elementos para poder probarla.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 6

**Logueando errores**

Nos hemos dado cuenta de que cuando llamamos a `getEl` a veces nos equivocamos escribiendo el selector (se nos olvida el punto de la clase, nos comemos una letra...), a partir de ahí todo falla y nos cuesta encontrar dónde está el error.

Vamos a mejorar nuestra función para que nos avise cuando esto ocurre. Dentro de ella:

- Al recoger el elemento de HTML vamos a guardarlo en una constante.
- Con un condicional vamos a comprobar si la constante no tiene ningún valor, y en ese caso vamos a imprimir un error en la consola que diga `No existe ningún elemento con clase, id o tag llamado {aquí-el-nombre-del-selector}`
- Finalmente tras nuestro condicional retornaremos la constante con el elemento.

> **Nota**: podemos imprimir/loguear errores con `console.error()`.

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 7

**Combinando funciones**

Partimos de un HTML con un párrafo que contiene un número. En nuestro fichero JavaScript nos copiamos la declaración de las funciones `getEl` y la que comprueba si un número es par o impar (ejercicio 5).

_Sin modificar estas dos funciones_, vamos a hacer lo siguiente:

- usando nuestra función `getEl` accedemos al párrafo, y recogemos su valor (con `innerHTML`)
- convertimos ese valor a número y lo asignamos a una constante
- usamos nuestra función del ejercicio 4 para saber si es par o impar
- escribimos en la consola 'Este número es PAR: ...' o 'Este número es IMPAR: ...'

\_\_\_\_\_\_\_\_\_\_

## Ámbito de las variables

Por defecto, una variable definida con `let` o `const` tiene un ámbito (en inglés, _scope_) que corresponde a su bloque, es decir, van a existir dentro de su bloque.

**¿Y qué es un bloque?** Un bloque es cualquier expresión con llaves `{}` como puede ser un `if` o una función :)

Por ejemplo:

```javascript
const globalVar = "Ey, I'm global";

if (2 === 2) {
  // ejemplo para asegurarnos de que entra en el bloque if
  const globalVar = "Ey, I'm not really global";
  const notGlobalVar = "Shirt, I'm not global :(";

  console.log(globalVar); // devuelve "Ey, I'm not really global"
  console.log(notGlobalVar); // devuelve "Shirt, I'm not global :("
}

console.log(globalVar); // devuelve "Ey, I'm global"
console.log(notGlobalVar); // da un error porque no está definida
```

Por supuesto, podemos acceder a las variables del ámbito superior:

```javascript
let globalVar = "Ey, I'm global";
if (2 === 2) {
  globalVar = "Ey, I'm STILL global";
  console.log(globalVar); // devuelve "Ey, I'm STILL global"
}
console.log(globalVar); // devuelve "Ey, I'm STILL global" que se cambió en el bloque if
```

De esta manera, una variable creada dentro del cuerpo de una función sólo será accesible desde dentro de esa función.

Desde dentro de una función podemos utilizar las variables que se hayan definido fuera de cualquier función, y gracias al ámbito de cada función también podemos crear, sin generar conflicto, nuevas variables que se llamen como variables de otras funciones.

Por ejemplo:

```javascript
function f1() {
  const item = 1;
  return item;
}

function f2() {
  const item = 2;
  return item;
}

console.log(f2()); // devuelve 2;
console.log(f1()); // devuelve 1;
```

Comprueba cuál será el resultado de las siguiente operaciones:

```javascript
// Usamos una variable de ámbito global

const secretLetter = 'y';
function mySecretLetter() {
  return secretLetter;
}
console.log(mySecretLetter()); // devuelve "y"
console.log(secretLetter); // devuelve "y"
```

```javascript
// modificamos una variable de ámbito global
let secretLetter = 'y';
function mySecretLetter() {
  secretLetter = 'x';
  return secretLetter;
}
console.log(mySecretLetter()); // devuelve "x"
console.log(secretLetter); // devuelve "x"
```

```javascript
// Usamos una variable de ámbito local que se llama igual que la global
const secretLetter = 'y';
function mySecretLetter() {
  const secretLetter = 'x';
  return secretLetter;
}
console.log(mySecretLetter()); // devuelve "x"
console.log(secretLetter); // devuelve "y"
```

```javascript
// intentamos usar una variable local fuera de su ámbito
function mySecretLetter() {
  const secretLetter = 'x';
  return secretLetter;
}
console.log(mySecretLetter()); // devuelve "x"
console.log(secretLetter); // da un error porque la variable solo está definida dentro del bloque de la función
```

#### EJERCICIO 8

Vamos a partir de uno de los ejemplos anteriores que usa una variable global, que luego se modifica desde una función.

```javascript
// modificamos una variable de ámbito global
let secretLetter = 'y';
function mySecretLetter() {
  secretLetter = 'x';
  return secretLetter;
}
console.log(mySecretLetter()); // devuelve "x"
console.log(secretLetter); // devuelve "x"
```

En el ejemplo anterior prueba a cambiar el orden del los `console.log`. ¿Qué está pasando? ¿Por qué no se imprime en la consola 2 veces "x"?

\_\_\_\_\_\_\_\_\_\_

## Arrow functions

Las arrow functions ("funciones flecha") de ES6 son una forma simplificada para declarar funciones anónimas. La sintaxis básica es la siguiente:

```javascript
const sum = (a, b) => {
  return a + b;
};

// y la ejecutamos usando la variable a la que la hemos asignado:
sum(2, 3); // devuelve 5;

// Anteriormente vimos esta misma función con la forma "normal"
const sum = function(a, b) {
  return a + b;
};
```

### Paréntesis opcionales

En las funciones flecha podemos evitar los paréntesis solo cuando la función tenga 1 único parámetro:

```javascript
const getWaitingTime = (minutes) => {
  return `Please, wait ${minutes} minutes`;
};

// equivale a
const getWaitingTime = minutes => {
  return `Please, wait ${minutes} minutes`;
};
```

### Llaves y return implícito

Escribir o no las llaves del bloque (`{}`) significa dos cosas distintas. Solo podremos no escribirlas cuando la función tenga una sola sentencia; es decir, cuando se ejecute una sola orden dentro (un console.log(), un cambio en un elemento HTML, un incremento en un contador, etc.). Cuando no escribimos las llaves, el valor que devuelve esa sentencia será el return de la función. Eso nos permite escribir en menos líneas funciones muy sencillas:

```javascript
const getWaitingTime = minutes => `Please, wait ${minutes} minutes`;
console.log( getWaitingTime(4) );
// devuelve "Please, wait 4 minutes"
};

// equivale a
const getWaitingTime = minutes => {
  return `Please, wait ${minutes} minutes`;
};
console.log( getWaitingTime(4) );
// devuelve "Please, wait 4 minutes"
```

#### EJERCICIO 9

**Arrow functions everywhere**

Vamos a rehacer alguno de los ejercicios anteriores con funciones flecha. ¡A lo loco!

\_\_\_\_\_\_\_\_\_\_

#### EJERCICIO 10

**Calculador de modelo de caja**

Como hemos visto en las clases anteriores, en CSS tenemos dos tipos de cálculo para las dimensiones de un elemento: `border-box` y `content-box`. Vamos a realizar un calculador al que le pasaremos 4 parámetros y nos devolverá el ancho del contenido, y el ancho total de la caja en una cadena como esta: `El ancho del contenido es: 30px y el ancho total de la caja es: 34px`.

La función tendrá 4 parámetros:

- el primero será un booleano para especificar si es `border-box` o no.
- el segundo será un número con el `width` de la caja.
- el tercero será un número con el `padding`.
- el cuarto será un número con el `border-size`.

Para probar que funciona, ejecuta la función recogiendo el resultado en una variable e imprímela en la consola.

\_\_\_\_\_\_\_\_\_\_

## Bonus: Funciones en todas partes

Se pueden ejecutar funciones dentro de otras funciones.

Se pueden pasar funciones como argumentos para otras funciones, devolver funciones como valores de otras funciones y guardar funciones en variables.

## Bonus: depurar JS

Depurar o debugging es **el arte de ejecutar el código de un programa línea a línea** para poder comprobar cómo está funcionando nuestro programa. Principalmente nos ayuda a entender por qué no funciona nuestro programa, nos ahorra muchísimo tiempo y frustración.

Además depurando se aprende mucho sobre cómo funciona JavaScript por dentro, nos muestra en directo lo que aprendemos en la teoría y nos enseña más que cualquier profesor.

Ahora que ya sabemos cómo programar con funciones es el momento en el que podemos empezar a sacarle mucho jugo al debugging. Un consejo, la diferencia entre una programadora que no usa el depurador y otra que sí es que una va gateando y la otra va corriendo ;)

Os hemos preparado un [vídeo explicando cómo funciona el debugging de DevTools](./2_sintaxis_de_js.md#debugger-y-console) para JavaScript.

## Recursos externos

### Curso de Ada Lovelace en Youtube

Este curso explica bastante bien y de forma breve qué son las funciones y como trabajar con ellas.

- [Funciones. Introducción](https://www.youtube.com/watch?v=PEfw6xuj8Y0&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=16)
- [Funciones anónimas](https://www.youtube.com/watch?v=GstPXAffmmI&index=17&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o)
- [Funciones. Parámetros y argumentos](https://www.youtube.com/watch?v=5VVBrfWQ2Wk&index=18&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o)
- [Ámbito de variables](https://www.youtube.com/watch?v=HlY2jF74s_c&list=PLI7nHlOIIPOJtTDs1HVJABswW-xJcA7_o&index=19)

### Libros Web

Si prefieres un recurso escrito para aprender, aquí tienes la explicación de las funciones y el ámbito de las variables en JavaScript de la mano del libro de Introducción a JavaScript por Libros Web.

- [Funciones](http://librosweb.es/libro/javascript/capitulo_4/funciones.html)
- [Ámbito de las variables](http://librosweb.es/libro/javascript/capitulo_4/ambito_de_las_variables.html)
