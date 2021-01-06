# Nodemon

[Nodemon](https://www.npmjs.com/package/nodemon) es un módulo de NPM que nos ayuda programar más rápido.

Recordáis que la extensión de VS Code **Live Server** lo que hace es observar cambios en los ficheros de nuestra página web y cuando algún fichero cambia, Live Server se da cuenta y nos refresca la página para que no tengamos que hacerlo nosotras manualmente. Pues Nodemon hace lo mismo pero para proyectos de Node JS.

## Instalar Nodemon

Vamos a instalar Nodemon de forma global en nuestro ordenador. De esta forma lo tendremos disponible para cualquier proyecto de Node JS. Abre una terminal y ejecuta:

```bash
sudo npm install -g nodemon
```

## Usar Nodemon

Hasta ahora hemos ejecutado cada ejercicio de node ejecutando en la terminal `node index.js`. A partir de ahora podemos ejecutar `nodemon index.js` y nuestro proyecto se ejecutará de la misma manera.

La diferencia es que a partir de ahora cada vez que modifiquemos el fichero `index.js` o cualquier otro fichero de nuestro proyecto, Nodemon parará el proyecto y volverá a ejecutarlo otra vez, evitándonos hacerlo nosotros mismo de forma manual.

**A partir de ahora te recomendamos usar siempre Nodemon para ahorrar tiempo.**

## Ejercicios

### 1. Prueba Nodemon

Abre un de ejercicio de los vídeos anteriores o uno que hayas creado tú y arráncalo con Nodemon. Haz algún cambio en tus ficheros y verás que al guardarlo, en la terminal se reiniciará tu proyecto.
