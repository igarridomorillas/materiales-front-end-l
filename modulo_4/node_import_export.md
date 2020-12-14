# Módulos en Node JS

## Qué son los módulos

- Vídeo
   - Qué es un módulo
   - Los hemos usado en React, pero aquí con require y module.exports
   - Para qué es: separar / organizar código en diferentes ficheros, crear librerías
   - Cuatro tipos de módulos:
     - Mis propios módulos
     - Nativos de Node JS
     - Instalados con NPM
     - JSON

## Módulos propios

- Vídeo
   - Explicar ejercicio node-modules-custom
   - Explicar la sintaxis, diferencias entre los nuevos y los viejos
   - El index.js no es un módulo porque no tiene un export. Un proyecto suele tener un index.js que no es un módulo y el resto de ficheros sí son módulos.
   - Cualquier fichero puede importar otros módulos
   - Hay varias formas de exportar pero nosotras solo vamos a ver module.exports
   - Podemos exportar una función, objeto...

## Módulos nativos

- Vídeo
   - Explicar que node tiene muchos módulos nativos
   - Uno de ellos es fs
   - Explicar ejercicio node-modules-native

## Módulos instalados con NPM

- Vídeo
   - Buscar paquetes en la página npm, los puede crear cualquier persona
   - Crear package.json con npm init
   - Instalar lodash
   - A partir de ahí lodash es como si fuera un módulo nativo
   - Explicar que lodash se suele representar con un guión bajo

## Módulos JSON

- Vídeo
   - Tipo especial de módulo
   - Node lo importa y lo transforma a objeto u array con JSON.parse
   - Muy usado para ficheros de configuración o ficheros de datos
   - De esa forma separamos los datos por un lado y la programación por otro
   - Explicar ejercicio node-modules-json

## Ejercicios

### Librería de file system

1. Mira, ejecuta y entiende los ejemplos node-modules-read-and-write-files-with-one-module y node-modules-read-and-write-files-with-two-modules
1. Piensa y justifica si te gusta más que las dos funciones estén en un solo módulo o separadas en dos

### Librería Math

1. Crea un index.js
1. Crea un math.js que es un módulo
1. Exporta dos funciones una para sumar y otra para restar
1. Desde index.js importa el módulo
1. Haz una suma y consolea el resultado
1. Haz una resta y consolea el resultado

### Librería Math avazado

1. Crea un index.js
1. Crea un math-add.js que es un módulo que exporta una función de suma
1. Crea un math-sub.js que es un módulo que exporta una función de resta
1. Crea un math.js que es un módulo que importa los dos módulos anteriores y los exporta dentro de un objeto
1. Exporta dos funciones una para sumar y otra para restar
1. Desde index.js importa el módulo
1. Haz una suma y consolea el resultado
1. Haz una resta y consolea el resultado

### Lodash: obetner la unión

1. Crea un index.js con los arrays [1, 2, 3] y [2, 3, 4]
1. Usa el módulo lodash para hallar la unión de estos dos ficheros
1. Si consoleas el resultado debería ser [2, 3]

### Lodash: ordenar una colección

Una colección es un array de objetos.

1. Crea un index.js con la colección:
   [
      {
        name: 'Sofía',
        promo: 'k'
      },
      {
        name: 'María',
        promo: 'l'
      },
      {
        name: 'Lucía',
        promo: 'j'
      },
      {
        name: 'Julia',
        promo: 'l'
      }
    ]
1. Usa el módulo lodash para ordenar este array primero por la letra de la promo y después por el nombre de la alumna
1. Si consoleas el resultado debería ser:
   [
      {
        name: 'Lucía',
        promo: 'j'
      },
      {
        name: 'Sofía',
        promo: 'k'
      },
      {
        name: 'Julia',
        promo: 'l'
      },
      {
        name: 'María',
        promo: 'l'
      }
    ]