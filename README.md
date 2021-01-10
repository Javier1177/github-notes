# Git

## Introducción

Git es un sistema que almacena y modela la información. Su propósito es llevar un registro de los cambios en archivos y coordinar el trabajo que varias personas realizan sobre archivos compartidos mediante el uso de ramas.

Las ramas son utilizadas para desarrollar funcionalidades aisladas unas de otras. La rama master es la rama por defecto cuando creas un repositorio. Se suelen crear nuevas ramas durante el desarrollo cuando queremos introducirle mejoras o nuevas funciones a la rama principal, de esta manera si no nos funciona, no estropeamos el código de la rama master (la principal).

![Branch example](C:/Users/Javi/Boostnote/images/branches.png)


## Utilización github

### Trabajando en nuestro repositorio
En primer lugar, para utilizar git debemos ir al terminal. Una vez lo hemos abierto, debemos **crear el directorio** donde vamos a tener el repositorio de los archivos del proyecto.

<pre>
mkdir nombre_carpeta
</pre>

Una vez creado el directorio del proyecto, vamos a **iniciar git** (estando dentro de la carpeta):

<pre>
git init
</pre>

Esto lo que hace es crearle un nuevo subdirectorio llamado .git que tiene todos los archivos necesarios del repositorio (Inicializar git en una carpeta). Los archivos que crea están ocultos.

Por otro lado, al iniciar el git en nuestro directorio, nos aparecerá a la izquierda la rama en la que estamos. Por defecto, la primera es master.

![Where am I?](C:/Users/Javi/Boostnote/images/command1.png)

Ahora que tenemos iniciado git en nuestro directorio, debemos subirle los ficheros del proyecto. Para ello metemos los ficheros en la carpeta y hacemos lo siguiente:

<pre>
git add -A ----> añadir todos los ficheros al seguimiento.

git commit -m "descripción de la actualización"
</pre>

Ahora que ya tenemos iniciado git en el proyecto, vamos a crear una nueva rama para que los cambios no vayan directamente a la master. **La segunda rama siempre la llamaremos developer.** 

Cabe decir que se pueden crear tantas ramas como queramos, y crear ramas a partir de ramas. Para **crear una nueva rama**:

<pre>
git branch developer ----> Crear rama de forma normal.

git checkout -b developer  ----> Crear rama entrando en ella automáticamente.
</pre>

Si queremos **cambiar a una rama que tengamos** ya creada debemos ejecutar lo siguiente: 

<pre>
git checkout nombre_rama
</pre>

Si lo que queremos es **ver las ramas que tengo creadas** y donde me encuentro actualmente:

<pre>
git branch
</pre>

Ahora que ya sabemos movernos por git y como tener una base, vamos a trabajar con él.

Cuando quiero hacer una **modificación en algún archivo del proyecto**, antes de nada debemos crear una rama a partir de la rama develop, estando dentro de dicha rama. ***Siempre trabajaremos a partir de develop, solo uniremos los nuevos cambios al master cuando estemos listos para hacer el release.***

<pre>
git checkout -b nombre_rama
</pre>

Una vez hayamos creado la rama, haremos aquí las modificaciones que deseemos. Cuando lo hayamos modificado/creado los archivos, **añadiremos los archivos al seguimiento de github.**

<pre>
git add -A ----> añadir todos los ficheros al seguimiento.

git add nombre_fichero.txt ----> añadir fichero deseado al seguimiento.
</pre>

Para **ver el estado de los ficheros de la rama**, podemos hacer lo siguiente

<pre>
git status
</pre>

Ahora que ya tenemos añadido el archivo deseado, debemos **unirlo a la rama en la que estamos trabajando**.

<pre>
git commit -m "descripción sobre lo que he realizado"
</pre>

Para **ver los commits que he hecho y su id**:

<pre>
git log
</pre>

Como ya he realizado todos los cambios que quería hacer, vamos a unirlos a la rama develop. Para ello nos movemos a la rama donde vamos a traer los ficheros modificados y ejecutamos lo siguiente:

<pre>
git merge nombre_rama_que_queremos_traer
</pre>

Una vez cerrada una rama a la que hemos hecho un commit, **debemos eliminarla** (menos develop):

<pre>
git branch -D nombre_rama
</pre>

Ahora ya estamos seguros de que no queremos hacer ningún cambio mas (de momento), vamos a añadirlo a la rama master.

Si queremos **crear un tag** con el nombre de la version a la rama master, debemos ejecutar el siguiente codigo estándo en dicha rama:

<pre>
git tag v1.0.0
</pre>

Si queremos **ver los tags** que tenemos:

<pre>
git tag
</pre>

Para **añadir todo nuestro trabajo a un repositorio de github por primera vez**, debemos ejecutar lo siguiente:

<pre>
git remote add origin https://github.com/usuario/nombreproyecto.git ----> Unimos nuestra carpeta con el repositorio de github (el codigo lo pondrá en la pagina).

git push -u origin master ----> Subo los datos que tengo en el directorio al repositorio.
</pre>

En caso de que queramos realizar un cambio en el proyecto, deberiamos volver a hacer los pasos de crear una rama a partir de developer y hacer los cambios deseados.

Al acabar, como ya tenemos conectado el directorio del proyecto con el respositorio, solo deberiamos hacer los adds y los commits, unirlos a la rama developer y subirlos a github:

<pre>
git add -A

git commit -m "descripción actualización"

git push ----> Subo los datos al repositorio.
</pre>

En caso de que se nos haya borrado el proyecto y queramos **descargarlo de github**:

<pre>
git clone enlace_repositorio
</pre>

Aunque si queremos **eliminar el proyecto junto con su git**, ejecutaremos lo siguiente estando fuera de él:

<pre>
git rm -rf nombre_proyecto
</pre>

En cambio, para borrar un fichero del git:

<pre>
git rm nombre_fichero
</pre>

Cuando queramos **sincronizar los datos que tenemos en el directorio con los de github**:

<pre>
git pull
</pre>

Si lo que queremos **ver son los cambios que se han hecho en una rama** (al hacer merge):

<pre>
git diff
</pre>

Para **añadir una lista de los ficheros a ser ingorados**:

<pre>
touch .gitignore
</pre>

Por último, si lo que queremos es ver la config de nuestro git:

<pre>
git config --list
</pre>

### Trabajando en el repositorio de otra persona

Para empezar a trabajar con el repositorio de otra persona debemos hacer un [fork](https://geeksroom.com/2014/05/que-es-un-fork-y-como-trabajar-en-github/85588/). Por lo que debemos ir a su repositorio a través de github y darle a fork. Una vez hecho esto, debemos **sincronizar nuestro git con el repositorio de la otra persona**.

<pre>
git remote add upstream enlace_repositorio
</pre>

Ahora debemos **descargar los datos de ese repositorio**. El codigo tambien sirve por si quiero verificar que tengo el proyecto al dia. (Es como un pull de un repositorio de otra persona).

<pre>
git fetch upstream
</pre>

Seguidamente, **unimos los datos descargados a una rama**.

<pre>
git merge upstream/develop
</pre>

Ahora que ya tenemos su trabajo y hayamos hecho los cambios deseados, debemos hacer un push para tener los datos en nuestro repositorio, utilizando el push. Después, deberemos ir a nuestro fork de github y hacer click en new pull request.

Al hacer click en new pull request deberemos seleccionar la rama que queremos sugerirle y donde. Después haremos click en make pull request para que la otra persona pueda añadir o no los cambios que hemos hecho en su proyecto.

Una vez hecho esto, si quieres borrar las ramas de remoto, se usa lo siguiente:
<pre>
git push origin --delete feature/login
</pre>

**En caso de que nos hagan a nosotros el pull request**, deberemos descargar el pull request (pr) y ponerlo en una rama aparte para ver los cambios, esto debe hacerse ejecutando el siguiente codigo:

<pre>
git fetch upstream pull/id_del_pull_request/head:nombre_rama
</pre>

Por último, cuando ya tengo descargado el pull request en una rama, **debo ejecutar el siguiente codigo en develop** para ver los cambios:

<pre>
git merge upstream/develop
</pre>

### Versiones
Cuando queremos poner una versión, normalmente se ponen tres números:

<pre>
Ej. V1.0.0
      M.m.r
</pre>

Los numeros se dividen en tres grupos:
-	major: indica la versión principal del software, consistiendo en un conjunto de funcionalidades concretas que son recogidas y cubiertas en dicha versión.
- minor: indican funcionalidad menor cubierta en la versión de software entregada.
-	revision: se modifican cuando hay revisiones de código ante fallos de la aplicación.
