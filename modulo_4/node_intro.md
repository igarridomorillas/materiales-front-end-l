# Introducción a Node JS

![Node JS](assets/images/nodejs-logo.jpg)

[Node JS](https://nodejs.org) es un lenguaje programación que nos sirve para ejecutar JavaScript en la terminal de un ordenador.

## Qué es Node JS

- Vídeo
   - Explicar qué es Node JS
   - Explicar las diferencias entre Node JS y JS: eventos, acceso a ficheros, local storage
   - Explicar las similitudes entre Node JS y JS: asíncronía
   - Explicar que tiene versiones
   - Explicar que funciona con paquetes gracias a NPM
   - Explicar
   - Explicar que se puede utilizar para montar un servidor y para cosas que no son de un servidor

## Acceso al sistema de ficheros

- Explicar que hacemos este ejemplo para que veamos que no solo sirve para crear servidores
- Explicar qué es el sistema de ficheros

### Leer ficheros

- Vídeo
   - Explicar ejercicio node-file-system-read-file
   - Explicar que es asíncrono
   - Explicar que el nombre de los ficheros puede ser el que queramos
   - Explicar la sintaxis de `fs.readFile(fileName, 'utf8', (err, data)`. Es muy común que el primer argumento sea `err`
   - Explicar ejercicio node-file-system-read-json-file para ver que una cosa es leer del sistema de ficheros y a partir de ahí cómo lo usas es tu problema
   - Explicar que un JSON no es más que un texto con un formato concreto

### Escribir en ficheros

- Vídeo
   - Explicar ejercicio node-file-system-write-file
   - Explicar que es asíncrono

## Ejercicios

### Suma

1. Crear un index.js
1. Crear una función de suma
1. La función debe retornar el resultado
1. Consolear el resultado

### Escribir en un fichero

1. Crea un index.js
1. Crea una constante con el texto que tú quieras, ej: Lorem ipsum
1. Crea un objeto que tenga los siguientes campos:
   - originalContent: Lorem ipsum
   - changedContent: LOREM IPSUM
   - textLenght: 11
1. Consolea el objeto en modo objeto
1. Consolea el objeto en modo texto. Pista: ¿Recuerdas lo que teníamos que hacer para guardar en el local storage un objeto?
1. Guarda el objeto tal cual en el fichero de destino ¿Qué error te muestra?
1. Guarda el objeto en modo texto en el fichero de destino

### Leer de un fichero, modificar los datos y escribirlos en otro fichero

1. Crea un fichero input-file.txt con un texto, ej: Lorem ipsum
1. Crea un index.js
1. Lee el contenido del fichero
1. Crea un objeto que tenga los siguientes campos:
   - originalContent: Lorem ipsum
   - changedContent: LOREM IPSUM
   - textLenght: 11
1. Guarda el objeto en modo texto en el fichero de destino

Pista: la asincronía es importante, debes guardar en el fichero de destino después de leer del fichero de origen

