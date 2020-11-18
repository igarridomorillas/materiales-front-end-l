![Git](assets/images/git-logo.jpg)

## Qué es Git

Git es un sistema de **control de versiones** de código además de una **herramienta para compartir** código.

El control de versiones nos sirve para ver el histórico de cambios que hemos hecho en el código. Es útil pasar saber por ejemplo que hace un mes nuestra compañera MariCarmen añadió un determinado código al proyecto. **Git nos dice quién, cuándo, por qué y dónde se cambió el código del un proyecto.**

También es una herramienta para compartir código entre nuestra compañeras de programación de los proyectos de Adalab, nuestros profes o la empresa en la que trabajaremos. **Es como el Drive o Dropbox de los programadores.**

## Qué es GitHub

Si Git es el sistema o programa para compartir código, [GitHub](https://github.com) es una de tantas empresas que hay para usar Git. A través de su página podemos crear proyectos y compartirlos con otras personas. También funciona como red social de programación.

**¡¡¡Gracias a Git y GitHub vamos a poder trabajar fácilmente en remoto desde el primer día!!!**

## Instalación de Git

Lo primero que tenemos que hacer es instalar Git en nuestro ordenador.

### Instalación en Ubuntu

Abre una terminal y ejecuta las siguientes líneas de una en una:

```bash
sudo apt update
```

```bash
sudo add-apt-repository ppa:git-core/ppa
```

```bash
sudo apt install git
```

### Instalación en Windows

Abre una terminal y ejecuta las siguientes líneas de una en una:

```bash
sudo apt update
```

```bash
sudo add-apt-repository ppa:git-core/ppa
```

```bash
sudo apt install git
```

Por último descarga e instala [Git para Windows](https://git-scm.com/download/win).

### Instalación en Mac

Descarga e instala [Git para Mac](https://git-scm.com/download/mac).

### Comprobando si lo hemos instalado bien

Una vez terminada la instalación de Git desde cualquiera de los 3 sistemas operativos debemos comprobar que todo ha ido bien. Para ello ejecutaremos en la terminal la siguiente línea:

```bash
git --version
```

Y la terminal debe mostrar la versión de Git instalada, algo como `git version 2.17.1`. Si por el contrario la terminal muestra el mensaje `No se ha encontrado la orden «git»...` es que algo hemos hecho mal. Vuelve a repetir todos los pasos y si no te funciona consulta a tu profesor.

## Configuración de Git

Una vez instalado Git tenemos crearnos una cuenta en GitHub y configurar nuestro ordenador para que **el Git de nuestro ordenador y nuestra cuenta de GitHub estén enlazados**:

1. Entra en [GitHub](https://github.com).
1. Crea una cuenta.
1. Cuando elijas tu nombre de usuaria ten en cuenta que las empresas te pedirán tu perfil de GitHub para ver cómo programas. No pongas un nombre de usuario demasiado informal.
1. Configura Git en tu ordenador:

### Configuración del nombre y email

En los 3 sistemas operativos tenemos que configurar el nombre de usuario y el email. Para ello abre una terminal y escribe los siguientes comandos un por uno. Sustituye el nombre y el email por tus datos:

```bash
git config --global user.name "Maria del Carmen"
```

```bash
git config --global user.email "lamary@gmail.com"
```

### Configuración en Ubuntu

Para poder almacenar la contraseña de GitHub en Ubuntu, abrimos una terminal y escribimos los siguientes comandos uno por uno:

```bash
sudo apt-get install libsecret-1-0 libsecret-1-dev
```

```bash
cd /usr/share/doc/git/contrib/credential/libsecret
```

```bash
sudo make
```

```bash
cd -
```

```bash
git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```

Al hacer esto, la próxima vez que introduzcamos nuestra contraseña de GitHub, esta se almacenará de forma segura en nuestro ordenador y no será necesario volver a introducirla de nuevo.

### Configuración en Windows

Para poder almacenar la contraseña de GitHub en Windows, abrimos una terminal y escribimos los siguientes comandos uno por uno:

```bash
sudo apt-get install libsecret-1-0 libsecret-1-dev
```

```bash
cd /usr/share/doc/git/contrib/credential/libsecret
```

```bash
sudo make
```

```bash
cd -
```

```bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager.exe"
```

Al hacer esto, la próxima vez que introduzcamos nuestra contraseña de GitHub, esta se almacenará de forma segura en nuestro ordenador y no será necesario volver a introducirla de nuevo.

### Configuración en Mac

Para poder almacenar la contraseña de GitHub en Mac, abrimos una terminal y escribimos el siguiente comando:

```shell
git config --global credential.helper osxkeychain
```

Una vez hayamos realizado ese paso, no necesitaremos hacer ningún cambio más.

## Clonar y crear un repositorio

Con el objetivo de empezar a trabajar de manera óptima en remoto desde el primer día de curso vamos a aprender lo básico sobre Git y GitHub. Para lo cuál os pedimos que veáis y sigáis los pasos de estos dos vídeos:

#### Cómo clonar un repositorio de Git

{% embed url="https://www.youtube.com/watch?v=iPM_yuknDjM" %}

Los comandos utilizados en [este vídeo](https://www.youtube.com/watch?v=iPM_yuknDjM) son:

```bash
git clone url_del_repositorio
```
```bash
git pull
```

#### Cómo crear un repositorio de Git

{% embed url="https://www.youtube.com/watch?v=UazjdwT9Xvg" %}

Los comandos utilizados en [este vídeo](https://www.youtube.com/watch?v=UazjdwT9Xvg) son:

```bash
git add -A
```
```bash
git commit -m "Mensaje del commit"
```
```bash
git push
```

### Estructura de carpetas

Os recomendamos que vuestro repositorio de `ejercicios-de-adalab` cumpla con las siguientes características:

- Cada ejercicio que hagamos en una carpeta. **Nunca se deben hacer dos ejercicios en la misma carpeta**, da muchos errores.
- El nombre de la carpeta que sea `modulo-x-leccion-y-ejercicio-z-descripcion`. Por ejemplo:
  - `modulo-1-leccion-04-ejercicio-03-flexbox`
  - `modulo-1-leccion-12-ejercicio-10-grid`
- Si todas las alumnas seguís este patrón es muy fácil compartir ejercicios y códigos entre vosotras.
