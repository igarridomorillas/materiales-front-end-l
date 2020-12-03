En esta guía **estamos recopilando todo lo que enseñamos en el curso** sobre Git y GitHub. Mucha de esta información y de estos vídeos están también en algunas de las lecciones de los módulos 1 y 2.

> **Nota:** no es necesario que leas esta guía antes de empezar el curso de Adalab, te lo iremos enseñando poco a poco. La idea es que vengas aquí para resolver problemas puntuales.

Git es una herramienta que **se aprende con el uso y la práctica**.

Está guía está dividida en dos partes: principales comandos de Git y vídeos.

# Principales comandos de Git

## git *command* --help

Obtener ayuda sobre un comando:

```bash
git clone --help
```

```bash
git commit --help
```

## git clone

Clonar un repo en nuestro ordenador desde un repo remoto:

```bash
git clone url-de-repo-en-github
```

## git add

Añadir todos los ficheros modificados al próximo commit:

```bash
git add -A
```

Añadir algunos ficheros modificados al próximo commit:

```bash
git add nombre-de-fichero
```

```bash
git add nombre-de-una-carpeta/*
```

## git commit

```bash
git commit -m "Add footer styles"
```

## git push

Subir uno o varios commits al repositorio remoto:

```bash
git push
```

Subir los últimos commits al remoto después de crear una rama:

```bash
git pull -u origin nombre-de-rama
```

## git pull

Bajar los últimos commits desde el repositorio remoto:

```bash
git pull
```

## git status

Ver el estado de nuestro repo local:

```bash
git status
```

## git fetch

Sincroniza la información (de commits, ramas...) desde el repo remoto al local, sin hacer ningún cambio en nuestro código ni en nuestro historial local de commits, lo podemos hacer siempre que queramos:

```bash
git fetch
```

## git clean

A veces, creamos ficheros que no hacen falta y no van a ir a ningún commit. Si queremos limpiar nuestro repositorio de esos ficheros podemos usar ```git clean```:

```bash
git clean -f .
```

También podemos usar ```git clean -i .``` para que nos vaya preguntando cuál fichero borrar y cuál no.

Si esos ficheros extra no queremos que vayan en ningún commit pero no los vamos a borrar porque son necesarios (por ejemplo, ficheros de configuración o el directorio de configuración de VisualStudio Code) podemos incluir sus nombres (con su ruta relativa) en el fichero ```.gitignore``` uno por línea. Si ```.gitignore``` no existe, podemos crearlo. Después, hacemos add y commit de ```.gitignore``` y a partir de entonces git no los tendrá en cuenta.

## git reset

Si lo que queremos es deshacer todos los cambios que hemos hecho desde el último commit y quedarnos con el directorio "limpio de cambios", ejecutaremos:

```bash
git reset --hard
```

Usando ```git reset``` en conjunto al comando anterior ```git clean```, que nos quedará el directorio de trabajo igualito a lo que había hasta el último commit.

## git branch

Listar las ramas locales:

```bash
git branch
```

Listar las ramas remotas:

```bash
git branch -r
```

Crear una rama (sin movernos a ella):

```bash
git branch nombre-de-la-nueva-rama
```

## git checkout

Movernos desde la rama actual a otra rama:

```bash
git checkout nombre-de-otra-rama
```

Crear y movernos a una rama en un solo comando:

```bash
git checkout -b nombre-de-la-nueva-rama
```

## git merge

Mover el código desde la rama de origen hacia la rama en la que estoy:

```bash
git merge nombre-de-rama-origen
```

## git log

Ver el listado de commits realizados:

```bash
git log
```

Para salir de `git log` y volver a la terminal hay que pulsar `q`. Para ver más resultados, pulsa el espacio.

## git diff

Sirve para ver los ficheros modificados y sus diferencias desde el último commit:

```bash
git diff
```

Aunque lo podemos usar para ver las diferencias entre dos commits:

```bash
git diff hash-commit-más-antiguo hash-commit-más-nuevo
```

...donde ```hash-commit-más-antiguo``` y ```hash-commit-más-nuevo``` son los identificadores de commit. Se ven después de hacer ```git commit``` o al listarlos con ```git log```. Los puedes copiar y pegar o escribir sólo las primeras 5 letras.

También se puede usar para ver los cambios entre dos ramas:

```bash
git diff rama-1 rama-2
```

...nos dirá los cambios de la rama-1 que no están en la rama-2 con un símbolo - al principio de la línea y los de la rama-2 que no están en la rama-1 con un símbolo +.

Hay un nombre de commit "especial" que es **HEAD**. Automáticamente, git asigna al nombre HEAD el último commit de la rama en la que estamos. Es útil para ver los cambios que hemos hecho hasta ahora:

```bash
git diff hash-de-commit-antiguo HEAD
```

## git commit --amend

Imaginaos que, por poco probable que parezca, nos hemos equivocado en el commit anterior: la descripción no es correcta o falta algún fichero. Podemos corregirlo modificando (enmendando) el último commit:

```bash
git commit --amend -m "Otra descripción"
```

```bash
git add fichero-que-me-deje.js
git commit --ammend
```

En el primer caso cambiamos la descripción del último commit y en el segundo añadimos un fichero más.

## git revert

Si el último commit no era correcto porque tenía bugs o fallos y queremos desestimarlo, podemos usar git revert:

```bash
git revert
```

Lo que hace es generar otro commit nuevo con los cambios inversos al último commit y con la descripción del último commit pero con la palabra Revert al principio y los archivos como estaban antes de ese commit:

```bash
ivan@adalab:~/ejemplo-git$ git log --oneline
6c14dda (HEAD -> master) Cambio chungo
43da3d1 Otro cambio
c725fe8 Un cambio

ivan@adalab:~/ejemplo-git$ git revert HEAD
[master 466e605] Revert "Cambio chungo"
 1 file changed, 1 deletion(-)

ivan@adalab:~/ejemplo-git$ git log --oneline
466e605 (HEAD -> master) Revert "Cambio chungo"
6c14dda Cambio chungo
43da3d1 Otro cambio
c725fe8 Un cambio
```

## git init

Crea un repositorio desde cero en nuestro ordenador, sin necesidad de crearlo previamente en GitHub:

```bash
git init
```

## git add remote

Enlaza un repositorio de nuestro ordenadro con un repositorio remoto:

```bash
git remote add origin url-del-repositorio-que-me-da-github
```

# Vídeos de Git

## Crear un repositorio

[Vídeo](https://www.youtube.com/watch?v=MGf3K6qxptg) sobre cómo crear y clonar un repositorio:

{% embed url="https://www.youtube.com/watch?v=MGf3K6qxptg" %}

## Añadir cambios a un repositorio

[Vídeo](https://www.youtube.com/watch?v=QQOHttHNtY0) sobre cómo añadir commits a un repositorio con los comandos `add`, `commit`, `push` y `pull`:

{% embed url="https://www.youtube.com/watch?v=QQOHttHNtY0" %}

## Merges blandos y duros

[Vídeo](https://www.youtube.com/watch?v=jDOVhbgc8Ec) sobre cómo trabajar dos personas en paralelo en un repositorio y cómo solucionar merges blandos (cuando ambas personas tocan diferentes líneas de código) y merges duros (cuando ambas personas tocan la misma línea):

{% embed url="https://www.youtube.com/watch?v=jDOVhbgc8Ec" %}

## Trabajar con varias ramas

[Vídeo](https://www.youtube.com/watch?v=MnaRLneoiSo) sobre cómo trabajar con varias ramas, movernos entre ramas, publicarlas y mergear una rama en otra:

{% embed url="https://www.youtube.com/watch?v=MnaRLneoiSo" %}

## Flujo de ramas

[Vídeo](https://www.youtube.com/watch?v=t-GbqNDrJ4A) sobre qué ramas debemos usar y cómo y cuándo debemos mover el código entre las diferentes ramas para mantener la mejor calidad de código:

{% embed url="https://www.youtube.com/watch?v=t-GbqNDrJ4A" %}
