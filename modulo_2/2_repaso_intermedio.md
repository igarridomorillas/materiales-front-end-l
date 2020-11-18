# Repaso intermedio módulo 2

## Sonríe… o no

Nos han encargado una pequeña aplicación web donde podremos mostrar si tenemos un buen día o si es mejor no pasarse hoy por nuestra mesa.
Dispondremos de toda la ventana del navegador para pintar una carilla con un fondo. En la parte baja de la pantalla tendremos un select donde podremos elegir entre dos estados, sonriente o triste, y un botón de actualizar.

![Guía de diseño](assets/images/2-6/bonus.png)

**Funcionamiento**
Por defecto vamos a intentar ir de buenas y se mostrará a la criatura sonriente sobre un fondo de un amarillo correcto #ffcc00.

- Con el select podremos cambiar nuestro estado de ánimo
- El boton `Update` hará varias cosas:
  - Recogerá el nuevo estado del select y lo pintará en lugar del actual
  - Generará un número aleatorio de 100 como máximo y si es un número par colocará el color de fondo del amarillo correcto (#ffcc00) y si es impar, usaremos el naranja fuego chileno (#ff9900).

**¿Cómo va lo del número aleatorio?**

Todos los lenguajes de programación tienen sus formas de generar número aleatorios, y JavaScript no iba a ser menos.

Puedes leer cómo va [la función Random de JS en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random). Echa un ojo con cuidado que hay varios ejemplos para generar números aleatorios con un máximo, con mínimos y máximos, excluidos o incluídos :)

## Resumen del módulo

Para llevar a cabo este ejercicio pondremos en uso todo lo que hemos aprendido hasta ahora en el módulo:

![Resumen del módulo](assets/repaso/js.png)

**¡Al turrón!**
