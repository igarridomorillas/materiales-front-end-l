# Refactorización

## Contenidos

<!-- TOC depthFrom:4 depthTo:4 -->

- [EJERCICIO 1](#ejercicio-1)

<!-- /TOC -->

## Introducción

Como ya sabemos, _Refactorizar_ código consiste en modificar un código para mejorar su estructura pero sin añadir nuevas funcionalidades. En esta sesión vamos a usarla íntegramente para practicar refactorización de código usando una _kata_.

### Refactorización

Se pueden aprender muchas estrategias de cómo refactorizar y son temas avanzados, por ejemplo, usar _patrones de diseño de software_ para mejorar nuestro código. Además, se necesita experiencia para aprender a distinguir código bueno de código mejorable. Normalmente, cuando un código nos parece que puede mejorarse es que detectamos un _olor de código_ (en inglés _code smell_) que nos indica que algo no está hecho de la manera más simple y semántica. Algunos ejemplos de _code smells_ son

- duplicidad: si veo trozos de código que son casi iguales
- usar _números mágicos_ (_magic numbers_): que es usar números en nuestro código sin explicar lo que son (mejor definirlos en una variable para darles un nombre)
- funciones muy largas con muchos parámetros
- mal nombrado de variables y funciones

Esta parte de refactorización requeriría todo un curso en sí misma. Pero lo que sí queremos que entiendas es la importancia de tener tests para refactorizar, porque nos permiten cambiar cosas comprobando que nuestra aplicación sigue funcionando (no se rompe). Haremos un ejercicio específico para demostrar esta afirmación.

#### EJERCICIO 1

Para comprobar que se refactoriza mucho mejor con tests, os pasamos un ejercicio que ya tiene tests pero un código malísimo. Nuestro objetivo es mejorar el código que nos dan sin modificar el comportamiento (refactorizar) y que los tests sigan pasando. Se trata de la famosa [kata _Gilded Rose_ con JavaScript](https://github.com/gootyfer/gilded-rose-js-with-tests).

\_\_\_\_\_\_\_\_\_\_
