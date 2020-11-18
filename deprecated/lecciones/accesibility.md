## Accesibilidad web

¿Alguna vez no has podido usar el ratón de tu ordenador y has tenido que rellenar un formulario sólo pulsando el teclado?¿Has pensado alguna vez que puede sentir una persona invidente al navegar por una web que no está preparada para el uso de dispositivos de lectura?

La accesibilidad web va más allá de crear webs “usables” para personas con alguna discapacidad sensorial o motriz, es hacer que nuestros proyectos puedan ser usados por el mayor número de personas posibles, sea cual sea su situación física o las capacidades del dispositivo con el que navega. 

Pensemos en este lema:
> Mismas oportunidades sin importar habilidades o circunstancias.

La accesibilidad es algo a lo que todas las adalabers **deberíamos dar una gran importancia**, ya que aporta muchos beneficios a nuestras aplicaciones.

 - Como ya hemos comentado, **aumenta el número de usuarios potenciales de nuestras webs**.
 - **Mejora el SEO**, ya que los “crawlers” o arañas de los buscadores leen el mismo contenido que un dispositivo para invidentes.

 - **Por solidaridad y ética profesional**

 - **Genera un código más limpio, semántico y ordenado**.

  

## Me has convencido, ¿cómo mejoro la accesibilidad de mi web?

Esto tiene una respuesta sencilla, por un lado, escribiendo un **HTML semántico y bien ordenado**, vamos a daros unas pautas para que entendáis a qué nos referimos con esto. Por otro, mejorando la accesibilidad propiamente dicha.

**Pautas para mejorar la semántica de nuestro HTML**

 1.   HTML5 incorpora un montón de etiquetas nuevas que hacen que tu web sea mucho más semántica, lo que hace que puedas usar dichas etiquetas en función del significado más específico y correcto para su tarea. **No abuses del uso de la etiqueta div**, cuando tienes etiquetas HTML creadas especialmente para el tipo de contenido que van a agrupar. Por ejemplo `<input>`  dentro de etiquetas `<form>`, `<li>` en listas `<ul>` o `<ol>`...

 2.   **Mantener una estructura lógica de ordenación de contenidos en titulares**, por ejemplo cuando manejamos jerarquías de titulares, `<h1> <h2> <h3>`...
    
 3.   Utilizar las **listas para contenidos que siguen una pauta de repetición y constituyen un listado**:
	    - Menús (cada item es un elemento de lista `<li>`)
		-	Migas de pan
		-	Categorías/Tags...

 4. En etiquetas `<input>`, especificar siempre su `type`, `value` y `name`, además, asociar siempre etiquetas `<label>` a sus respectivos `<input>`.
 ```html
 <label for="male">Male</label>  
<input type="radio" name="gender" id="male" value="male">
 ```

 5. Incorporar **textos alternativos** en imágenes y vídeos

  

**Pautas para mejorar la accesibilidad**

 1. **Los landmarks.** Se usan para identificar áreas de tu página y transmitir la naturaleza de la mismas. Así añadimos características útiles de navegación que transmiten información sobre la estructura de la página. Simplemente tenemos que añadir al elemento contenedor (el “div” por ejemplo) el código role=”[tipo_landmark]”. Por ejemplo, `<div role=”main”>` para marcar el "div" que contiene la zona de contenido principal. ¿Verdad que es sencillo? Hay varios tipos de landmarks dependiendo de la etiqueta HTML a la que acompañen los más importantes son los que os indicamos aquí abajo:

        <header> / banner
        <aside> / complementary
        <main> / main
        <footer> / contentinfo
        <nav> / navigation
        <form> / form

 Puedes  leer más sobre landmarks en [https://olgacarreras.blogspot.com/2014/03/navegacion-mas-accesible-y-semantica-en.html](https://olgacarreras.blogspot.com/2014/03/navegacion-mas-accesible-y-semantica-en.html)

 2. **Color**. Una buena práctica es ofrecer opciones de alto contraste en nuestra web para usuarios con problemas visuales. Si el diseño de nuestro proyecto se ve interferido por el uso de colores muy
        contrastados siempre podremos incorporar un pequeño botón que altere la gama de colores de manera que todo el mundo pueda leer el contenido de nuestra web. Para usuarios con problemas de percepción del color, deberíamos utilizar texturas adicionales como rayados o punteados.

 3. **Navegación con teclado**
    
	-	**Focussable buttons**: Hacer siempre los botones de nuestra web visualmente destacados cuando nos posicionemos sobre ellos a través del foco. No deberíamos quitar nunca el `:focus` de nuestros botones.
    
    -	**Tabbable elements:** Muchas veces el orden visual de los elemtnos de
    nuestras webs no se corresponde con el orden lógico en el que
    queremos que se navegue por ella, por ejemplo los campos de
    formulario. Para solucionar esto existe la propiedad `tabindex`.

```html
<a href="https://www.w3schools.com/" tabindex="2">W3Schools</a>  
<a href="http://www.google.com/" tabindex="1">Google</a>  
<a href="http://www.microsoft.com/" tabindex="3">Microsoft</a>
```

Puedes leer más sobre el uso correcto de tabindex en [https://developers.google.com/web/fundamentals/accessibility/focus/using-tabindex?hl=es](https://developers.google.com/web/fundamentals/accessibility/focus/using-tabindex?hl=es)

 4. **Etiquetas ARIA**. Las etiquetas ARIA sirven para añadir descripciones y etiquetas a elementos para volverlos accesibles cuando por sí mismos no lo son. Vamos a ver un ejemplo. más abajo se aplica estilo a un botón para que parezca un típico botón "cerrar", con una X en medio. Al no haber nada que indique que el propósito del botón es cerrar el diálogo, se usa el atributo `aria-label` para proporcionar una etiqueta a cualquier lector de pantalla.
```html
<button aria-label="Close" onclick="myDialog.close()">X</button>
```
Conoce más sobre este tipo de etiquetas en [https://developers.google.com/web/fundamentals/accessibility/semantics-aria/aria-labels-and-relationships?hl=es](https://developers.google.com/web/fundamentals/accessibility/semantics-aria/aria-labels-and-relationships?hl=es)

¡Vamos a practicar!

#### EJERCICIO 1
La empresa Bacon Yummy tiene una página anticuada que no sigue ninguna pauta de accesibilidad y semántica web, así que está perdiendo cada semana un montón de usuarios y clientes potenciales que ya no comprarán bacon para sus pizzas. Nos ha encargado reestructurar la semántica y accesibilidad de su web y nos ha dado su HTML, así que ¡vamos a ello!

```html
<!DOCTYPE  HTML>
<html>
<head>
<title>Best bacon for your pizza</title>
</head>
<body>
<div  class="header">
<div  class="menu">
<a  class="link"  href="#">Home</a>
<a  class="link"  href="#">What is bacon</a>
<a  class="link"  href="#">Contact</a>
</div>
</div>
<div  class="aside">
<div  class="aside-menu">
<a  class="link"  href="#">Oink</a>
<a  class="link"  href="#">Aside oink oink</a>
<a  class="link"  href="#">More oinks</a>
</div>
</div>
<div  class="main">
<div  class="article">
<h2>Bacon ipsum recipe</h2>
<p>
Bacon ipsum dolor amet shankle landjaeger flank jerky short loin drumstick tenderloin buffalo porchetta sausage. Burgdoggen flank pork belly, corned beef jerky cow capicola rump venison picanha frankfurter turducken hamburger cupim jowl. Rump tail pastrami short ribs picanha. Pig capicola shank t-bone pork belly turducken. Flank alcatra strip steak, pork loin jowl capicola prosciutto chicken pork belly pork chop.
</p>
</div>
</div>
<div  class="footer">
<h1>Visit us</h1>
Copyright 2019. Bacon Yummy. All right reserved.
</div>
</body>
</html>
```

> **Pista**: Sustituye cada div por su respectiva etiqueta HTML5
