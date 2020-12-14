# Express: servidor de estáticos

## Qué es un servidor de estáticos

- Básicamente aquel servidor que devuelve páginas web o ficheros estáticos, que no se modifican al vuelo.
- Un servidor de dinámicos es un API o un servidor que devuelve html personalizado o un generador de facturas en PDF

## Servidor de estáticos

- Vídeo
   - Express tiene un middleware que genera un servidor de estáticos
   - Funciona indicando la carpeta donde están los estáticos
   - La carpeta se puede llamar como queramos
   - Abrir la URL /, /contact.html y main.css
   - Es como si express hiciera app.get(/) >> devuelvo el index.html
   - Es como si express hiciera app.get(/contact.html) >> devuelvo el contact.html
   - Es como si express hiciera app.get(/assets/css/main.css) >> devuelvo el main.css

## Gestión de errores 404

- Vídeo
   - Mostrar el error 404 por defecto de express
   - Si el fichero que pedimos no existe dentro de public Express intenta gestionarlo con el siguiente endpoint
   - Ponemos `app.get('*', (req, res) => { ... })` para capturar todo

## Los endpoints antes que el servidor de estáticos

- Vídeo
   - Si tenemos que poner endpoints los ponemos antes