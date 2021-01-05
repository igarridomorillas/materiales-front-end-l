# Postman

Es muy frecuente que cuando programamos un servidor no tengamos programada la correspondiente web que va a comunicarse con el servidor.

En ese momento tenemos el problema de programar un servidor y no tener la web para probar que lo que estamos programando funciona bien.

Para ello existe una herramienta muy útil que nos permite hacer cualquier petición a un servidor. Es como si fuera una web universal que se puede comunicar con cualquier servidor del mundo.

![](assets/images/postman.png)

Esa herramienta se llama Postman y es muy muy útil mientras estamos programando.

## Instalación de Postman

Para instalar Postman en tu ordenador:

1. Descarga e instala Postman en tu ordenador:
   - Desde Windows o Mac entra en la [página de descargas de Postman](https://www.postman.com/downloads/).
   - Desde Ubuntu accede al instalador de aplicaciones desde el menú, busca **Postman** e instálalo.
1. Ábrelo:
   - Si al abrirlo te pide que te registres, debes saber que no hace falta. Sáltate este paso pulsando en **Skip signing in and take me straight to the app**.
1. Abre una nueva pestaña pulsando en el icono **+**.
1. Empieza a hacer peticiones a un servidor como si hubiera un mañana. Recuerda que el servidor debe estar arrancado para que conteste a las peticiones.

## ¿Cómo usar Postman?

- Vídeo:
   - Qué es postman
   - Cuándo es útil
   - Abro postman y elijo:
      - Verbo
      - Url
      - Llamo a https://google.es
      - Y datos si es necesario
   - Para probar mi servidor:
      - Descargo, instalo y arranco el servidor
      - Cómo hacer una petición normal /users
      - Cómo hacer una petición enviando datos /new-user
        - Petición con datos

[Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-basic)

Un pequeño recordatorio: cuando hacemos una petición POST y queremos enviar datos tenemos que:
  -

## Ejercicios

### 1. Usando Postman

1. Descarga, instala y arranca el [ejercicio de la lección de Intro a Express JS](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-2-express-basic).
1. Abre la página http://localhost:3000.
1. Abre Devtools > Network y mira qué peticiones se hacen cuando pulsamos en los botones de la página.
1. Realiza las mismas peticiones desde Postman. Para ello debemos indicar:
   - El verbo: GET, POST...
   - La dirección del endpoint `http://localhost:3000/users`, `http://localhost:3000/new-user`...
   -