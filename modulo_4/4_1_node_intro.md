# Introducción a Node JS

![Node JS](assets/images/nodejs-logo.jpg)

[Node JS](https://nodejs.org) es un lenguaje programación que nos sirve para **ejecutar JavaScript en la terminal de un ordenador**.

Existen muchísimos lenguajes de programación de back end (como PHP, Java, Python, .NET...). Nosotras vamos a aprender Node JS porque ya sabemos JavaScript y sabemos el 80% de los conocimientos que se necesitan. Cuando en el futuro quieras aprender otro lenguaje de back end te costará mucho menos.

Hasta ahora estamos acostumbradas a ejecutar nuestro código JavaScript en un navegador como Chrome. Gracias a Node JS podemos ejecutar JavaScript en una terminal y que este haga tareas como leer y escribir en los ficheros del ordenador, o podemos crear una aplicación de servidor.

## Diferencias entre JavaScript y Node JS

Las diferencias entre un código de JavaScript ejecutado en un navegador y en una terminal son las características propias de cada uno de estos dos entornos. Por ejemplo:

- En un navegador las usuarias producen eventos (click, keyUp, scroll...) pero esto no tiene sentido en una terminal. Es decir, **una terminal no tiene una interfaz gráfica que puedan usar las usuarias**.
- **Una terminal tienen muchos más permisos para acceder a servicios del ordenador**, como acceder a los ficheros del ordenador, abrir puertos de Internet, instalar otros programas... todas estas cosas no se pueden hacer desde un navegador por temas de permisos y seguridad.
- Node JS no va a ejecutar o interpretar HTML, CSS, imágenes... Pero sí que los va a gestionar, a crear, a modificar, a servir a aquellas páginas web que los pidan. **En Node JS solo se ejecutan ficheros de JavaScript.**

## Similitudes entre JavaScript y Node JS

Todo lo demás es común entre JavaScript y Node JS. Es decir, en Node JS también vamos a trabajar con nuestras variables y constantes, nuestros ifs, nuestros **amados** arrays y bucles, vamos a dividir el código en diferentes ficheros que vamos a exportar e importar, vamos a poder **depurar** nuestras aplicaciones... También vamos a trabajar con **asíncronía** que es especialmente útil en un servidor.

En resumen, nos interesa aprender de Node JS aquellos conocimientos que son únicos de Node JS. También nos interesa aprender a pensar en cómo funciona un servidor.

## Qué es Node JS

En este [vídeo](https://www.youtube.com/watch?v=3rQggXHyjmU) explicamos qué es Node JS y ejecutamos nuestro primer programa:

{% embed url="https://www.youtube.com/watch?v=3rQggXHyjmU" %}

> Ejercicio del vídeo: [node-intro](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-1-node-intro)

## Y tú ¿has utilizado alguna vez Node JS?

{% embed url="https://www.youtube.com/watch?v=dO2cv7OpBGk" %}

Recuerda lo que hemos comentado en este [vídeo](https://www.youtube.com/watch?v=dO2cv7OpBGk), pulsando **Ctrl+C** en la terminal, puedes forzar que un programa de Node JS finalice.

## Acceso al sistema de ficheros

Otra funcionalidad muy útil y usada es el [**File system (también conocido como fs)**](https://nodejs.org/dist/latest-v14.x/docs/api/fs.html), que no es otra cosa que una librería interna de Node para acceder a los archivos y carpetas del ordenador donde se está ejecuando.

Vamos a ver varios ejemplos de cómo se usa:

> Ejercicio del vídeo: [node-intro](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-1-node-intro)

### Leer ficheros

{% embed url="https://www.youtube.com/watch?v=gHf6SXXdi_0" %}

> Ejercicio del vídeo: [node-fs-read-file](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-1-node-fs-read-file)

### Leer ficheros JSON

{% embed url="https://www.youtube.com/watch?v=A54Y8S9pdLI" %}

> Ejercicio del vídeo: [node-fs-read-file-json](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-1-node-fs-read-file-json)

### Escribir en ficheros

{% embed url="https://www.youtube.com/watch?v=YE09MWJcVLA" %}

> Ejercicio del vídeo: [node-fs-write-file](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-1-node-fs-write-file)

### Leer y escribir en ficheros

{% embed url="https://www.youtube.com/watch?v=yfsCFBGjQuc" %}

> Ejercicio del vídeo: [node-fs-read-and-write-file](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-1-node-fs-read-and-write-file)

## Ejercicios

### Suma

1. Crea un `index.js`.
1. Crea una función `add`:
   - La función debe recibir dos números como parámetros.
   - La función debe retornar el resultado de la suma.
1. Ejecuta y consolea el resultado.

### Escribir en un fichero

1. Crea un `index.js`.
1. Crea una constante con el texto que tú quieras, ej: **Lorem ipsum**.
1. Crea un objeto que tenga las siguientes propiedades:
   ```js
   {
      originalContent: 'Lorem ipsum',
      changedContent: 'LOREM IPSUM',
      textLenght: 11
   }
   ```
1. Consolea el objeto en modo objeto.
1. Guarda el objeto tal cual en el fichero de destino:
   - ¿Qué error te muestra?
1. Consolea el objeto en modo texto.
   - Pista: ¿Recuerdas lo que teníamos que hacer para guardar en el local storage un objeto en formato texto?
1. Guarda el objeto en modo texto en el fichero de destino y verás que sí funciona.

### Leer de un fichero, modificar los datos y escribirlos en otro fichero

1. Crea un fichero `input-file.txt` con un texto, ej: **Lorem ipsum**.
1. Crea un `index.js`.
   1. Lee el contenido del fichero `input-file.txt`.
   1. Crea en un objeto que tenga los siguientes campos:
   ```js
   {
      originalContent: 'Lorem ipsum',
      changedContent: 'LOREM IPSUM',
      textLenght: 11
   }
   ```
   1. Guarda el objeto en modo texto en un fichero de destino llamado `output-file.json`.

> **Pista:** la asincronía es importante, debes guardar en el fichero de destino después de leer del fichero de origen.

