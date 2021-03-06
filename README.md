# Manual git
## Aprende los comandos básicos de git

Lo primero que se debe hacer es intalar git, muchos ordenadores lo tienen ya instalado de serie. 
Para comprobralo introducir en terminal: `git --version` este nos mostrará la versión actual de git instalada.

Una vez tengamos git deberemos configurarlo. Git permite realizar distintos "chekpoints" (commits) en nuestros proyectos, estos se veran así:
```
commit 90a3edcb6ccf2c681b82944d9d1a0fdcdfffc8df (HEAD -> master)
Author: nombre <correo@example.com>
Date:   Fri Nov 29 21:27:00 2019 +0100

    Esto es un commit
```
Como veremos más adelante estos commits guardan mucha información, entre otras cosas el nombre del autor y su correo
Para evitar que git nos pregunte por estos datos continuamente cada vez que realizamos una acción se deberá configurar de la siguiente manera
```
$ git config --global user.name "nombre"
$ git config --global user.email correo@example.com
```

También sería interesante configurar el editor de texto por defecto, este es VIM, y dado a que mucha gente se siente mas cómodo con otros, podemos seleccionar el que queramos mediante la siguiente instrucción:
`$ git config --global core.editor mi_editor`
yo personalmente uso visual studio code or lo que puse `code`.

## Entendiendo git:
Git es un sistema de control de versiones, esto quiere decir que nos ayudará a guardar las distintas etapas de nuestro proyecto, a hacer deshacer y tomar distintos "caminos" (branches).

Para ello disponemos de distintas áreas:

- **Working directory**: este área es la que usamos con y sin git, en ella trabajamos, hacemos modificaciones y guardamos nuestros archivos en su estado actual.

- **Staged area**: esta es una fase previa de nuestro archivo, esta nos permite "guardar cambios" mientras seguimos modificando nuestro archivo, y si decidimos volver atras podemos deshacer todos los cambios realizados a excepción de los localizados en esta zona, para ver que archivos estan en esta zona se usa el comando: `git status`. Este nos muestra algo así: 



```On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   first_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   first_file.txt

```
Vemos que aparece nuestro archivo *first_file.txt* en ambas zonas, esto es debe a que he creado un archivo y he escrito en el, tras esto lo he guardado en la *staged area*, después he vuelto a cambiar el archivo sin añadir estos cambios a la *staged area*. De esta forma podremos deshacer todos los cambios del *working directory* sin cambiar los que nosotros queramos, también prodremos hacer un commit permante de estos.
Es muy importante trasladar los cambios de zona en el momento adecuado, sino puede que cuando querramos echar marcha atras deshagamos mas de la cuenta.
Veremos mas adelante como hacer estos cambios, ahora solo explico las zonas.

-**Commited**: Una vez hayamos avanzado en nuestro proyecto y querramos indicar un momento de este realizaremos un commit, tras desarrollar tres funciones que consideras de gran relevancia decides que este estado del proyecto es relevante, entonces realizas un commit, este "punto de gurdado" en tu proyecto te permitirá volver a él, deshacerlo o simplemente guardar el conetino *staged area* de forma permanente, de tal forma que esta se vacia y poder acumular en ella nuevos cambios. A la hora de realizar un *commit*  es importente escribir bien su descripción ya que nos servirá más adelante para saber que se guardo en dicho commit y saber si queremos volver a trabajar desde él o no (si por que todos nos equivocamos y a veces es más facil volver a cierto punto de nuestro proyecto que pasarte horas y horas buscando un fallo).


## Comandos básicos:

- `git init`
Este comando inicializa un repositorio git en un directorio, es decir, crea una carpeta *.git* en nuestro directorio atual, es recomendable realizar este comando en el directorio principal de nuestro proyecto. Tamién es recomendable tener un repositorio por proyecto, ya que de esta forma todo estará mas organizado y no da pie a equivocaciones entre proyectos.

- `git add <files>`
Este comando introduce los archivos seleccionados en la *stage area*, podemos escribir uno o varios archivos, si queremos guardar todos los cambios del directorio actual usar `git add .`

- `git commit` 
Este comando realiza el commit de la actual *staged area* es recomendable usarlo de la siguiente manera:
`git commit -m "Esto es el comentario del commit`
De esta forma escribimos el comentario en el propio comando, sino se abrira el editor de texto por defecto en git donde deberemos poner el comentario

- `git log`
Este comando nos muestra el historial de todos los commits realizados en el proyecto, en el formato del commit mostrado al principio del manual:
```
commit 90a3edcb6ccf2c681b82944d9d1a0fdcdfffc8df (HEAD -> master)
Author: nombre <correo@example.com>
Date:   Fri Nov 29 21:27:00 2019 +0100

    Esto es un commit
```
Vemos que nos indica varias cosas: el nombre del autor que realizo el commit, cuando solo nosostros trabajamos esto no tiene mucha importancia pero en un proyecto colaborativo si es muy interesante saber quien ha realizado cada cambio.
También nos indica la fecha y hora cuando se realizó el commit. Se puede leer: `(HEAD -> master)` esto nos indica en que rama estamos (de ramas se hablará más adelante) y que estamos en el último commit ya que pone *HEAD* . Cada commit tiene un código de identificación asociado (el número largo) y por último el comemtario de este.


- `git checkout`
Este comando es muy polivalente, puede tener distintos usos, por ejemplo para eliminar los cambios del *working directory* indicando a que archivos se quiere realizar: `git checkout -- <file>...`
También nos permite viajar a los distintos commits: `git checkout código_identificación`
Otro uso es crear una nueva rama:`git checkout -b nombre_rama` o simplemente viajar a una existente: `git checkout nombre_rama`

Ahora que ya conoces los comandos báscos solo te queda practicar, probar y experimentar, una vez entiendas estos puedes ver nuevos mediante el comando `git --help`

## Ramas
En git tenemos la opotunidad de establecer distintas ramas, esto quiere decir que podemos tomar caminos alternativos para nuestro proyecto y escoger el que más nos convenga:

![foto de ramas en git](https://github.com/arejula27/Manual-git/blob/master/assets/ramas.png)

Como vemos esto nos permite poder realizar distintas "historias de guardado" esto nos puede ser de gran utilidad a la hora de depurar, ya que podemos realizar todos los cambios sin perder el fichero original, también a la hora de desarrollar nuevas fases del proyecto, ya que si estas "rompen" la anterior, el proyecto orignal no sufre cambios.
La rama central se denomina *master*, mientras que las demás pueden llevar el nombre que escojamos, por supuesto, en cualquier momento podemos fusionar dos ramas uniendo así todos los cambios (una vez solucionado el problema en la rama de depuración la unimos a master, estando así la rama central arreglada).
Los comados necesarios son:
- `git branch` Nos permite ver el listado de ramas
- `git checkout <branch name>` Nos permite viajar a una rama
- `git checkout -b <branch name> Crea una rama y viaja a ella
- `git merge <bramch name>` Fusiona la rama actual con la escogida, si estamos en *master* y fusionamos una rama, todos los cambios de esa rama iran a master, mientras que si estamos en cualquier rama y fusionamos con master esa rama se "actualizara" con los cambios de master. También se puede hacer `git merge` entre ramas que no sean master.
Habra veces que nos avise de un *merge confict* esto significa que al fusionar dos ramas se ha realizaod un cambio en la misma linea, por lo que no sabe cual dejar en la fusión. Únicamente deberemos decirle si queremos conservar los cambios de la rama atcual (current changes) o los datos de la rama que viene (incoming changes), tras esto habrá que hacer un commit y tendrías las ramas fusionadas.
Esto resulta más sencillo con un editor de texto como vs code.

## Repositorios remotos:

Hasta ahora hemos aprendido a usar git en forma local (en nuestro ordenador) pero este también nos permite tenerlo en forma remota, es decir tener una copia en internet, hay muchos sitios donde poder hacer esto, yo personalmente los tengo en github.

Esto nos permite tener una copia de seguridad de nuestros proyectos, poder pasarlo de un ordendor a otro de forma sencilla o poder trabajar varias personas en un proyecto, ya que este se actualiza en el repositorio remoto. Para usarlos hay dos opciones, crear el repositorio remoto y luego pasarlo al ordenador o viceversa.
- Repo remoto a local:
En este caso debemos crear el repositorio remoto, una vez hecho eso debemos ir a la carpeta donde querramos ponerlo y usar el comando `git clone <url repo>` de tal forma que se crea una carpeta con el nombre del repo y todos sus ficheros y carpetas entro, esta ya estara unido al remoto.
- Repo local a remoto:
En este caso hemos desarrollado un repo local y queremos subirlo, para ello podemos usar aplicaciones como *github desktop* o crear un repo remoto vacío y usar el siguiente comado `git romote add origin <url repo>`
De esta forma ya estan unidos.

Ahora veremos dos comandos que nos permititan interactuar entre estos dos repos:
- `git pull` Este comando descarga todos los cambios que haya en el repo remoto a tu versión local, es * *funadamental* * realizar ese comando antes de ponerse a trabajar, ya que así podremos evitar posibles fallos y trabajar con la última versión. 
- `git push`  Este comando sube los cambios locales al repositorio remoto, es importante decir que para realizar esta acción el repo local debe estar actualizado (por ello es necesario realizar `git pull` como se ha dicho previemante).
Estas  intrsucciones únicamente suben o descargan los *commits* no los cambios que has hecho en el *working directory* ni en la *staged area.
Si usamos `git push --all`se neviaran los *commits* de todas las ramas mientras que si no usamos dicho flag, únicamente los de la rama actual.

## Trabajar sobre un repo que no he creado yo:

Cuando queramos colaborar en un repo remoto que hayamos creado hay distintas posibilidades:

- **Pull request**:
En este caso el propietario del repo no nos ha concedido permisos, para realizar cambios en él deberemos crear una copia de su proyecto (*fork*) y descargar esa copia en nuestro ordenador, una vez hechos los cambios haremos una *pull request*, es decir, le mandaremos una petición donde estan los cambio que queremos añadir, el propietario los leeá y podrá aceptarla o no.
- **Tener permisos**:
dentro de este caso hay dos opciones, descargar directamente el repo de dicha persona una vez nos haya concedido los permisos de escritura (con `git clone`) y hacer `pull`y `push`como si fuera nuestro, el único inconveniente es que trabajaremos todos con e mismo repo y no estará en nuestro perfil.
La otra oción es hacer una copia (*fork*) y descargarla, una vez hecho esto deberemos sincronizar nuestro repo local con nuestra copia (no es necesario por que se hace automático al hacer `git clone`) y sincronizarlo con el repo de dicha perosna, para ello ejecutar: `git remote add upstream <url del repo>` de esta forma ambos están sincronizados. ¿Por qué hacer esto?
Por que así podremos controlar los cambios que mandamos, igual usamos ramas auxiliares que no queremos mandar al repo central, de esta forma evitamos eso, subiendolas unicamente a nuestro repo, también tendremos una copia en nuestro propio pefil, luego a la hora de interactuar será mucho más sencillo.
Para actualizar ahora deberemos usar `git pull --all`para tomar los cambios de ambos repos.
A la hora de hacer push deberemos indicar a cual por lo que primero debermos hacer push al nuestro (*origin*) y luego al central (`git push upstream`), existe la opción de crear un alias para hacer los dos en el mismo comando:
`git config --global alias.pushall '!git remote | xargs -L1 git push --all` de esta forma al hacer `git pushall`se envian los cambios a ambos. 






