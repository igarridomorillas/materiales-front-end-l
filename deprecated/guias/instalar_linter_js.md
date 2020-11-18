# Instalación de un linter de JavaScript

Un linter es una herramienta que nos ayuda a prevenir errores y tener un formato homogéneo en nuestro código. Existen linters para varios lenguajes de programación, pero aquí veremos ESLint que es un linter para JavaScript.

En un linter definimos una serie de reglas en un fichero de configuración que son las que queremos comprobar en el código. Luego el programador que usa un linter ejecutará esas reglas, normalmente el propio editor (Atom) lo hace por ti, y si no se cumplen te mostrará un error o un warning (aviso).

Hemos creado una configuración específica de linter para vosotras, adalabers, porque queremos que os ayude a detectar algunos errores y a escribir código con un estilo correcto. Algunas de estas reglas son:

- da error si no se pone ; al final de una sentencia
- da error si no se usa indentación correcta
´da warning si dejáis console.log() en el código
- da warning si dejáis una función vacía

Para usarlo en un proyecto, tenéis que

- descargar el fichero de configuración .eslintrc.json de [este repositorio](https://raw.githubusercontent.com/Adalab/Adalab-web-starter-kit/master/.eslintrc.json)

	> "Descargar como" y guardar con el nombre .eslintrc.json


- instalar ESLint de forma global mediante `npm install -g eslint`

- **en el editor Atom** tendremos que tener instalado el plugin [linter-eslint](https://atom.io/packages/linter-eslint), y activa la opción `Use Global Eslint`
- **en el editor VS Code** necesitaremos el paquete [ESLint
](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- una vez configurado, al abrir un fichero JS en Atom o Code nos aparecen los errores y warnings, y para los errores solucionables, un botón para resolverlo.

![Linter Atom](../modulo_2/assets/images/2-10/linter-atom.png)

A veces nos resultará molesto tener algunos errores o warnings en el editor porque, por ejemplo, queremos usar un console.log para algo. Podemos deshabilitar el uso del linter en una línea concreta usando [las instrucciones de configuración](https://eslint.org/docs/user-guide/configuring).
