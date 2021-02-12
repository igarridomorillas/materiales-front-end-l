# Depurar con Node JS

Depurar es ejecutar paso a paso cada una de las líneas del código de un programa para ver qué está haciendo en cada momento y comprobar si está haciendo lo que nosotras queremos.

**A estas alturas de vuestra vida ya sabreís que es importantísimo saber depurar las páginas web que programamos.**

Cuando programamos una página web con JavaScript le estamos diciendo al navegador lo que queremos que haga, pero ya sabemos que nuestro código nunca funciona bien a la primera. Si utilizamos el depurador, el navegador nos va a decir lo que está entendiendo y por lo tanto podemos saber en qué nos estamos equivocando.

El depurador nos enseña más que cualquier profesor sobre cómo se comporta el lenguaje de programación. Nos explica cómo funciona el lenguaje. Nos ayuda a escuchar y entender el lenguaje. **Nos dice al oído cómo se siente.**

Además nos ayuda a encontrar errores más rápido y a programar más deprisa. Dicho de otra forma, la programadora que no depura va andando. La programadora que sí depura va en moto.

¡¡¡Por favor os lo pedimos, aprended cuanto antes a depurar!!!

> **Nota:** Si quieres repasar [cómo se depura JS en Chrome mira este vídeo](https://www.youtube.com/watch?v=m5QGMBK_vIA).

## Depurar con Node JS

En esta lección vamos a aprender a depurar Node JS. Node JS es el mismo lenguaje que JavaScript, por ello lo único que necesitamos para saber cómo depurar es saber cómo arrancar el depurador de Node JS.

Así como el depurador de JavaScript está en las Devtools de Chrome, **el depurador de Node JS está integrado en el VS Code**.

Lo que vamos a ver en el siguiente ejercicio funciona para Mac y para Ubuntu, pero es necesario que lo veas aunque estés trabajando en Windows.

- Vídeo
    - Si ejecutamos un ejercicio normal nos muestra los consoles en la terminal.
    - Para ejecutar el ejercicio en modo depuración le damos a Run > Start debugging > Node JS (preview)
    - Esto nos ejecuta el programa de forma normal pero en la pestaña de Debug console.
    - Esto nos ejecuta el fichero que tengamos seleccionado.
    - Una vez que sabemos arrancar el depurador ya podemos hacer todo lo que hacemos normalmente en el depurador de las devtools de chrome
       - Podemos poner puntos de parada con el punto rojo
       - Podemos poner un `debugger;`
       - Podemos posarnos sobre una variable y saber lo que vale
       - Podemos ver lo que vale una variable ejecutándola en Debug console
       - Podemos darle al play, ejecutar paso a paso, entrar en una función, salir de una función, reiniciar el depurador...
    - Por cierto te has fijado que cuando estamos depurando la barra inferior del Code está naranja.
    - Cuando estamos depurando también podemos pulsar en la pestaña Run y ver
       - Las variables locales, el call stack

##### ¿Te ha gustado?

Por favor rellena este [formulario](https://adalab.typeform.com/to/Rc0bft9x) para darnos feedback sobre la calidad de esta mini lección.