# Manual git
## Aprende los comandos basicos de git

Lo primero que se debe hacer es intalar git, muchos ordenadores lo tienen ya instalado de serie. 
Para comprobralo introducir en terminal: `git --version` este nos mostrará la versión actual de git instalada.

Una vez tengamos git deberemos configurarlo. Git permite realizar distintos "chekpoints" (commits) en nuestros proyectos, estos se veran así:
```
commit 90a3edcb6ccf2c681b82944d9d1a0fdcdfffc8df (HEAD -> master)
Author: nombre <correo@example.com>
Date:   Fri Nov 29 21:27:00 2019 +0100

    Esto es un commit
```
Como veremos mas adelante estos commits guardan mucha información, entre otras cosas el nombre del autor y su correo
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

Para ello disponemos de distintas areas:

- **Working directory**: este area es la que usamos con y sin git, en ella trabajamos, hacemos modificaciones y guardamos nuestros archivos en su estado actual.

- **Staged area**: esta es una fase previa de nuestro archivo, esta nos permite "guardar cambios" mientras seguimos modificando nuestro archivo, y si decidimos volver atras podemos deshacer todos los cambios realizados a excepcion de los localizados en esta zona, para ver que archivos estan en esta zona se usa el comando: `git status`. Este nos muestra algo así: 



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

-**Commited**: Una vez hayamos avanzado en nuestro proyecto y querramos indicar un momento de este realizaremos un commit, tras desarrollar tres funciones que consideras de gran relevancia decides que este estado del proyecto es relevante, entonces realizas un commit, este "punto de gurdado" en tu proyecto te permitirá volver a él, deshacerlo o simplemente guardar el conetino *staged area* de forma permanente, de tal forma que esta se vacia y poder acumular en ella nuevos cambios. A la hora de realizar un *commit*  es importente escribir bien su descripción ya que nos servira más adelante para saber que se guardo en dicho commit y saber si queremos volver a trabajar desde él o no (si por que todos nos equivocamos y a veces es más facil volver a cierto punto de nuestro proyecto que pasarte horas y horas buscando un fallo).


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
Vemos que nso indica varias cosas: el nombre del autor que realizo el commit, cuando solo nosostros trabajamos esto no tiene mucha importancia pero en un proyecto colaborativo si es muy interesante saber quien ha realizado cada cambio.
También nos indica la fecha y hora cuando se realizó el commit. Se puede leer: `(HEAD -> master)` esto nos indica en que rama estamos (de ramas se hablará más adelante) y que estamos en el último commit ya que pone *HEAD* . Cada commit tiene un código de identificación asociado (el número largo) y por último el comemtario de este.


- `git checkout`
Este comando es muy polivalente, puede tener distintos usos, por ejemplo para eliminar los cambios del *working directory* indicando a que archivos se quiere realizar: `git checkout -- <file>...`
También nos permite viajar a los distintos commits: `git checkout código_identificación`
Otro uso es crear una nueva rama:`git checkout -b nombre_rama` o simplemente viajar a una existente: `git checkout nombre_rama`

Ahora que ya conoces los comandos báscos solo te queda practicar, probar y experimentar, una vez entiendas estos puedes ver nuevos mediante el comando `git --help`

## Ramas
En git tenemos la opotunidad de establecer distintas ramas, esto quiere decir que podemos tomar caminos alternativos para nuestro proyecto y escoger el que ,más nos convenga:

![foto de ramas en git](https://github.com/arejula27/Manual-git/blob/master/assets/ramas.png)
