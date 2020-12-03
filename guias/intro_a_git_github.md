# Introducción a Git y GitHub

Con el objetivo de empezar a trabajar de manera óptima en remoto desde el primer día de curso vamos a aprender lo básico sobre Git y GitHub. En los primeros días de clase también os lo explicaremos en detalle.

## Qué es Git

![Git](assets/images/git-logo.jpg)

[Git](https://git-scm.com/) es un sistema de **control de versiones** de código además de una **herramienta para compartir** código.

El control de versiones nos sirve para ver el histórico de cambios que hemos hecho en el código. Es útil pasar saber por ejemplo que hace un mes nuestra compañera Mari Carmen añadió un determinado código al proyecto. **Git nos dice quién, cuándo, por qué y dónde se cambió cada línea de código de un proyecto.**

También es una herramienta para compartir código entre nuestras compañeras de programación de los proyectos de Adalab, nuestros profes o la empresa en la que trabajaremos. **Es como el Drive o Dropbox de los programadores.**

## Qué es GitHub

![Git](assets/images/github-logo.png)

Si Git es el sistema o programa para compartir código, [GitHub](https://github.com) es una de tantas empresas que hay para usar Git. A través de su web podemos crear proyectos y compartirlos con otras personas. También funciona como red social de programación.

## Cómo clonar un repositorio de otra persona

Vamos a empezar por clonar un repositorio de otra persona. En concreto vamos a clonar el repositorio donde las profes subimos los ejercicios hechos en clase. De esta forma, al acabar cada clase podrás descargarte el código de dichos ejercicios:

{% embed url="https://www.youtube.com/watch?v=iPM_yuknDjM" %}

Los comandos utilizados en [este vídeo](https://www.youtube.com/watch?v=iPM_yuknDjM) son:

```bash
git clone https://github.com/adalab/ejercicios-en-clase-X
```

```bash
git pull
```

Ahora que ya sabes clonar un repositorio de otra persona, te recomendamos que te clones todos los repositorios que usaremos durante el curso. Las direcciones de estos repositorios están en la [sección Información de interés](../instalacion/antes_de_empezar_el_curso.md).

## Cómo crear mi repositorio de Git

A continuación te pedimos que crees tu propio repositorio en GitHub donde durante el curso irás subiendo los ejercicios que hagas en clase:

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

- Cada ejercicio que hagamos en una carpeta. **Nunca se deben hacer dos ejercicios en la misma carpeta**, da muchos errores. **Insistimos, nunca haremos dos ejercicios en la misma carpeta.**
- El nombre de la carpeta que sea `modulo-x-leccion-y-ejercicio-z-descripcion`. Por ejemplo:
  - `modulo-1-leccion-04-ejercicio-03-flexbox`
  - `modulo-1-leccion-12-ejercicio-10-grid`
- Si todas las alumnas seguís este patrón es muy fácil compartir ejercicios y códigos entre vosotras.

## Git status

Ya sabemos usar los comandos de Git `clone`, `add`, `commit`, `pull` y `push`. Solo nos queda por aprender un comando importante: `git status`.

`git status` nos dice el estado actual en el que está nuestro repo.

