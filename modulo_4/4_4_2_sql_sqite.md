# SQL / SQLite

## La gran familia SQL

Ya sabemos que hay muchos tipos bases de datos:

- Bases de datos que guardan los datos en **colecciones de tipo JSON**.
- Bases de datos que guardan los datos en **tablas tipo Excel**.
- Otros tipos de bases de datos.

En Adalab os vamos a enseñar a trabajar con bases de datos de **tipo tabla**. Dentro de este tipo, hay muchas bases de datos. La más famosa y usada por más empresas es **SQL** (Structured Query Language).

Dentro de SQL a su vez hay muchas versiones o familias de bases de datos, porque en programación cada uno coge algo que ya existe, lo cambia un poquito, dice que ha reinventado la rueda y pide dinero a cambio ;)

Por ejemplo dentro de la familia **SQL** están: MySQL, Microsoft SQL, SQLite...

Lo bueno es que si aprendes a usar una de estas familias, ya sabes usar el resto de familias porque de una a otra cambian muy muy pocas cosas.

En Adalab concretamente os vamos a enseñar a trabajar con **SQL + SQLite**, ya que SQLite está muy bien para aprender y para ser usada en proyectos pequeños.

## Instalación de SQLite Browser

Para usar una base de datos SQLite dentro de nuestros proyectos de Node JS instalaremos un paquete de NPM. Ya veremos cuál.

Pero para trabajar de una forma cómoda necesitamos un programa que tenga un entorno gráfico amigable. Vamos a instalar en nuestro ordenador [**SQLite Browser**](https://sqlitebrowser.org/), que podemos decir que es un visualizador de bases de datos o el DevTools de SQLite. Para ello:

### Instalación desde Windows

Entra en la [página de descargas de SQLite browser](https://sqlitebrowser.org/dl/) y descarla e instala la última versión. Seguramente sea la que pone **DB Browser for SQLite - Standard installer for 64-bit Windows**.

### Instalación desde Mac

Entra en la [página de descargas de SQLite browser](https://sqlitebrowser.org/dl/) y descarla e instala la última versión. Puedes hacerlo:

- Descargando e instalando la aplicación o...
- Ejecutando `brew install --cask db-browser-for-sqlite` desde una terminal de tu Mac.

> **Nota:** a lo mejor tienes que usar `sudo`.

### Instalación desde Ubuntu

Entra en la [página de descargas de SQLite browser](https://sqlitebrowser.org/dl/), apartado **Ubuntu and Derivatives** y verás que te pide que ejecutes los siguientes comandos en una terminal:

```bash
sudo add-apt-repository -y ppa:linuxgndu/sqlitebrowser
```

```bash
sudo apt-get update
```

```bash
sudo apt-get install sqlitebrowser
```

### Abrir SQLite browser

Para saber que lo has instalado bien abre desde tu ordenador SQLite browser y verás este programa:

![SQLite broser](./assets/images/sqlite-browser.png)

## Nuestra primera base de datos

Ahora que ya tenemos instalado **SQLite browser** abre la aplicación desde tu ordenador para que puedas seguir los pasos que damos en este vídeo.

> **Nota:** si sigues los pasos de este vídeo borra la base de datos que está en `./src/dababase.db` que hay en el ejercicio, para crearla tú desde cero.

{% embed url="https://www.youtube.com/watch?v=l34svW5Amf4" %}

> [Ejercicio del vídeo](https://github.com/Adalab/ejercicios-de-los-materiales/tree/main/promo-l/4-4-2-sql-intro)

> **Importante:** os recordamos que cada vez que cambiamos algo en la base de datos desde SQLite browser hay que pulsar en **Guardar datos**.

## Diferencias entre base de datos, tablas y registros

- **Una base de datos en un conjunto de tablas**, lo que sería un documento de Excel que contiene varias hojas de Excel. Una aplicación de tamaño normal solo tiene una base de datos.
   - Si la aplicación es muy grande puede tener varias bases de datos.
   - Si la aplicación es todavía más grande puede combinar bases de datos de diferentes tipos.
- **Una tabla es un conjunto de columnas y regisros**, lo que sería una hoja de Excel. Vamos a tener una tabla por cada una de las cosas que queramos guardar, como por ejemplo en una tienda online tendremos una tabla para usuarios, otra tabla para productos, otra tabla para pedidos...
- **Un registro es cada una de las filas de una tabla**, lo que sería una fila de una hoja de un documento de Excel. Cada registro guarda uno de nuestros usuarios, uno de nuestros productos, uno de nuestros pedidos... En cada columna guardamos un dato de cada registro, en la tabla de usuarios en una columna guardamos el email, en otra la contraseña, en otra el nombre...
- **Un campo en cada dato o de un registro**, lo que sería una celda de una fila de una hoja de un documento de Excel. Para cada campo o celda podemos configurar qué tipo de dato guarda: texto, número entero, número con decimales, booleano...

Cada vez que hacemos una **consulta** a base de datos para leer o escribir lo llamamos **hacer una query**.

Así que cuando penséis y habléis de bases de datos debéis usar las palabras adecuadas en cada caso.