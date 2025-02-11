# Curso de Git Gopher La Paz Bolivia

## Instalar Git:

Para Instalar git tenemos que descargarlo ya sea para 
windows o linux o mac. 

https://git-scm.com/downloads

Cada uno tiene su instrucciones desde que windows es solo
descargar un exe hasta utilizar brew para mac/linux

## Configurar Git 

Una ves necesitaremos correr `git version` ya sea en nuestra terminal
o git bash

```
mike@Mike-Laptop:~$ git version
git version 2.43.0
```
Una ves Instalado tenemos que configurar nuestro usuario y correo
```
git config --global user.name “<name>”
git config --global user.email “<email>”
```

Para ver que configuramos correct tenemos que correr  `git config --global --list`

Ejemplo:
```
mike@Mike-Laptop:~$ git config --global --list
user.email=michael.ramirez@pluto.tv
user.name=michaelr
```

## Repositorios

Git maneja repositorios. Cada Proyecto iniciado es un repositorio
Que nos permita manejar el control de la historia de cada proyecto

con `git init -b <branch-name>` Iniciamos un repositorio del direcotorio


`-b` Signficia `--initial-branch=<branch-name>`

Ejemplo: 
```
mike@Mike-Laptop:~/personal/git-course$ git init -b master
Initialized empty Git repository in /home/mike/personal/git-course/.git/
```
Una ves initializado nuestros comando vemos que se crea la carpeta

`.git` Que por defecto esta oculto. Esta carpeta se encuentra toda 
la informacion necesaria para que Git pueda funcionar. NO SE TIENE QUE MODIFICARLA!!

## Commits
Un commit es en realidad una version de nuestro proyecto. Mientras mas commits tengamos
mas versiones tendremos y podremos ir por la historia de commits.

### Pasos para hacer un buen commit 

#### git status
Siempre es bueno saber que vamos a commitear antes de aniadirlo al commit. Y 
es con el comando `git status` este git status nos dara la informacion de 
que no queremos comitear

Ejemplo: 
```
mike@Mike-Laptop:~/personal/git-course$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .idea/
        go.mod
        readme.md

nothing added to commit but untracked files present (use "git add" to track)
```
En aca vemos 4 pasos para la informacion

`On branch master`  Quiere decir en que branc estamos

`No commits yet` Quiere decir que no tenemos nada que aniadir 

`nothing added to commit but untracked files present (use "git add" to track)` Aca nos dice que no tenemos 
nada adianido. 

#### git add 

Este comando nos da el poder para decidir que archivos podemos aniadir.

`git add <file-name>` Solo aniadira un archivo a nuestro commit

`git add <file-name> <file-name>` Puedes aniadir multiples archivos

`git add -A` el flag `-A` quiere decir aniadir todo los archivos 

`git add .` Esto es es como el comando `git add -A` la unica diferencia buscara
los archivos de la raiz que agregamos este comando

Ejemplo
```
mike@Mike-Laptop:~/personal/git-course$ git add -A
mike@Mike-Laptop:~/personal/git-course$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   .idea/.gitignore
        new file:   .idea/git-course.iml
        new file:   .idea/modules.xml
        new file:   .idea/vcs.xml
        new file:   go.mod
        new file:   readme.md
```
Aqui vimos el primer comando `git add -A` y el segundo comando `git status`
Despues de eso vemos todo lo que tenemos que comitear 

### git reset
Que pasa si queremos eliminar un archivo o directorio de nuestro commit?
`git reset` es uno de los comando nos permitira hacerlo. 

En este escenario vamos a eliminar todo el directorio de `.idea` de nuestro commit
Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git reset .idea/
mike@Mike-Laptop:~/personal/git-course$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   go.mod
        new file:   readme.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .idea/
```

Nuestro git status nos muestra que ahora el directorio `.idea/` no esta
en nuestro commit. Tambien hay otros comandos como `git restore` 

### .gitignore
Que pasa si no queremos ciertos archivos que se guarden en nuestro directorio?
Seria molestoso que cada ves que queramos aniadir un archivo nuevo tengamos 
que hacer un `git reset` en donde esta nuestro raiz de nuestro archivo vamos
aniadir el archivo `.gitignore` para decirle que archivo no queremos que nos 
trackee y sea ignorado. 

Creamos el archivo `.gitignore` y en su contendio ponemos el archivo o directorio
que queremos ignorarlo `.idea` 

Una ves creado el archivo incluso si no lo adiadimos en nuestro commit git 
ya sabe que archivos no tiene que trackear

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   go.mod
        new file:   readme.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
```
Con esto podemos ver que `.idea` directorio no va a ser trackeado

### git commit 
Una ves que tengamos todo listo podemos crear nuestro primer commit de 
nuestro repositorio con el commando `git commit`

`git commit -m "Mensaje del Commit"` La bandera `-m` significa por un mensaje
Es siempre tener mensajes claros y consisos de lo que hicimos ya que esto
va a ser una version de nuestro historial.
Ejemplo
```
mike@Mike-Laptop:~/personal/git-course$ git commit -m "Primer Commit"
[master (root-commit) 9c152d1] Primer Commit
 3 files changed, 191 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 go.mod
 create mode 100644 readme.md
```
Vemos que creamos el primer cambio y ya tenemos nuestro historial de commits

Y nuestro git status ya no nos dira que no podemos commitear

```
mike@Mike-Laptop:~/personal/git-course$ git status
On branch master
nothing to commit, working tree clean
```

## Branches 

En git tenemos la fuerza de crear `branch` que ayuda a orginzar y trabajar
en diferentes features, bugs, otros. Sin que otra persona intervenga en 
nuestro branch

### git branch 
Este comando listea todo nuestros branch que existe en nuestro repositorio

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git branch
* master
```
Como podemos ver aca solo tenemos un branch creado que es el master.
`*` Significa en el branch que estamos actualmente

### git branch <name-of-the-branch>
Con este comando crearemos un branch

Ejemplo
```
mike@Mike-Laptop:~/personal/git-course$ git branch feature
mike@Mike-Laptop:~/personal/git-course$ git branch
  feature
* master
```
Como Podemos ver aqui creamos un nuevo branch llamado `feature` sin 
embargo no estamos en ese branch actualmente seguimos en `master`

Si hacemos un `git log` veremos que tanto como `master` y `feature` apuntan
al mismo commit

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git log
commit 57d6334f87feaada0c9e34b65f18d696000266b5 (HEAD -> master, feature)
Author: michaelr <michael.ramirez@pluto.tv>
Date:   Tue Jan 21 16:47:46 2025 -0400

    aniadiendo mas info de los commits

commit 9c152d10610b1460dcd061aa539d80331549e26c
Author: michaelr <michael.ramirez@pluto.tv>
Date:   Tue Jan 21 16:46:44 2025 -0400

    Primer Commit
```

### git switch
Este comando sirve para cambiar entre ramas. En este caso usaremos 
para ir a feature `git switch feature`

Ejemplo: 
```
mike@Mike-Laptop:~/personal/git-course$ git switch feature
M       readme.md
Switched to branch 'feature'
mike@Mike-Laptop:~/personal/git-course$ git branch
* feature
  master
mike@Mike-Laptop:~/personal/git-course$ git log
commit 57d6334f87feaada0c9e34b65f18d696000266b5 (HEAD -> feature, master)
Author: michaelr <michael.ramirez@pluto.tv>
Date:   Tue Jan 21 16:47:46 2025 -0400

    aniadiendo mas info de los commits

commit 9c152d10610b1460dcd061aa539d80331549e26c
Author: michaelr <michael.ramirez@pluto.tv>
Date:   Tue Jan 21 16:46:44 2025 -0400

    Primer Commit
```
Podemos ver en este escenario que nos cambiamos a feature.
En `git branch` podemos ver que estamos apuntando a `feature`
y en `git log` vemos la diferencia que `HEAD` esta apuntando la rama `feature`

### git checkout -b <name-of-the-branch>
Este comando es en realidad es uno de lo mas usados en ves de usar 
`git branch` y `git swtich` usamos `git checkout -b <name-of-the-branch>`

`-b` significa branch creation ya que `git checkout` se puede usar 
mas cosas que se veran en adelante

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git checkout master
M       readme.md
Switched to branch 'master'
mike@Mike-Laptop:~/personal/git-course$ git checkout -b feature-2
Switched to a new branch 'feature-2'
mike@Mike-Laptop:~/personal/git-course$ git log
commit 57d6334f87feaada0c9e34b65f18d696000266b5 (HEAD -> feature-2, master, feature)
Author: michaelr <michael.ramirez@pluto.tv>
Date:   Tue Jan 21 16:47:46 2025 -0400

    aniadiendo mas info de los commits

commit 9c152d10610b1460dcd061aa539d80331549e26c
Author: michaelr <michael.ramirez@pluto.tv>
Date:   Tue Jan 21 16:46:44 2025 -0400

    Primer Commit
```
Explicacion:

`git checkout master` significa que nos movemos a master

`git checkout -b feature-2` Creamos el branch `feature-2` y nos cambiamos
directamente a ese branch sin necesidad de usar `git switch`

`git log` Aca vemos que `HEAD` esta apuntando directamente a `feature-2` 

# Merge
Una ves terminado nuestros cambios en nuestro `branch` podemos 
`mergear` esos cambias a la rama principal. Hay dos tipos de merge
en git. `Fast Forward Merge` y `Three way Merge` vamos a explicarlo

## git merge <branc-name>
Para mergear nuestros cambios o mergear los cambios a nuestra rama
se usa el comando `git merge <nombre de la rama>`

1. Primero tenemos que estar en la rama que queremos nuestros cambios 
por ejemplo queremos que master este con los ultimos cambios de nuestra 
rama feature-2. Para eso necesitamos estar en master:
`git checkout master`
2. Una ves en nuestra rama master vamos a mergearlo con la rama feature-2
`git merge feature-2`
3. Finalizado nuestro proceso veremos que nos saldra que es un Merge
`Fast Forward Merge`

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git checkout master
Switched to branch 'master'
mike@Mike-Laptop:~/personal/git-course$ git merge feature-2
Updating 57d6334..211bbe0
Fast-forward
 readme.md | 146 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-- 
 1 file changed, 144 insertions(+), 2 deletions(-)
```

## Fast Forward Merge
Es el Merge mas conveniente ya que el HEAD no tiene disvergencia
con la rama que queremos mergear. No nos va a pedir un commit extra 
y generalmente no va a guardarselo en el historial

## Three Way Merge 
En este ejemplo veremos el Three Way Merge es los mismos pasos. 
Pero veremos un output diferente

1. Primero tenemos que estar en la rama que queremos nuestros cambios
   por ejemplo queremos que master este con los ultimos cambios de nuestra
   rama feature-2. Para eso necesitamos estar en master:
   `git checkout master`
2. Una ves en nuestra rama master vamos a mergearlo con la rama feature-2
   `git merge feature-3`
3. Finalizado nuestro proceso veremos que nos saldra que es un Merge
   `Merge made by the 'ort' strategy`
4. Y al final tendremos un commit en un historial
Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git merge feature-3
Auto-merging readme.md
Merge made by the 'ort' strategy.
readme.md | 2 +-
1 file changed, 1 insertion(+), 1 deletion(-)
```

Esta forma de mergear es la mas conocida y guarda un commit en nuestro
historial. Diciendo que se Mergeo la rama con nuestra rama. 

Git decide cuando usar entre `Fast Foward` y `Three way Merge`
El objetivo de `Three way merge` es la forma de saber cuando
hay conflicto entre las ramas

## Merge Conflicts
En un mundo ideal es cuando un Programador nunca toca la linea 
de codigo de otro Programador pero es algo muy dificil que pase. 

Un Merge Conflict es cuando en la misma rama se tocaron la misma 
linea y git te da a escoger. Si escogemos entre la rama en la
que estas. En La rama que estamos mergeando o hacemos una convinacion 
entre las dos. En este escenario veremos que pasa

1. Mergeamos la rama que queramoes en nuestra rama `git merge merge-conflict`
2. Solucionamos el Merge ya sea escogiendo los cambios de nuestra rama
o de la rama que estamos mergeando
3. Commiteamos el cambio: `git commit -m "Fix Merge"`
4. Vemos si no hay nada que Mergear `git merge continue`


Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git merge merge-conflict
Auto-merging readme.md
CONFLICT (content): Merge conflict in readme.md
Automatic merge failed; fix conflicts and then commit the result.
mike@Mike-Laptop:~/personal/git-course$ git commit -m "Fix Merge Conflict"
[master 8eaece3] Fix Merge Conflict
mike@Mike-Laptop:~/personal/git-course$ git merge continue
merge: continue - not something we can merge
```
Estos comandos que vemos a la hora de hacer Merge nos soltra
en nuestro archivo de esta manera:

```
<<<<<<< HEAD
entre las dos. En este escenario veremos que pasa

=======
entre las dos. Esto Provocora un Merge Conflicto
>>>>>>> merge-conflict
```

Nos va a decir Primero en donde estra el conflict
`<<<<<<< HEAD` Signfica que es lo que tenemos NOSOTROS
y se separa con los iguales `=======` que es lo que tienen
ellos `>>>>>>> merge-conflict` 
Ahora hay herramientas como visual studio code y demas 
que te ayudan a ser mas visual esto. Ya es decicion de cada uno

# Git Reposiotorios Remoto

Por ahora esuvimos trabajando solo en nuestras maquinas. Pero el fuerte
de git son los Repositorios Remoto. Y hay diferentes servicios que nos 
dan esa capcidad los mas conocidos
1. Github
2. Bitbucket
3. GitLab

## Github != Git
GitHub es solo un servicio en la nube para hostear nuestros repositorios
remotamente. Muchos confunden que github es git. Si lo se, pero no es asi.
En este curso vamos a usar Github pero al final el uso de comandos es lo 
mismo para los otros repositorios remotos.

## Authentication in Github SSH

Una forma de `authenticate` y la mas usada es usar `ssh` (Secure Shell).
El beneficio de usar `ssh` sobre `https` es que no tenemos que poner nuestro
usario y password cada ves. Es una configuracion de una sobre otra. Ademas 
cuando usamos con Pipeplines y otros. Podemos usar el `ssh authentication`

### Crear tu ssh key 
Para poder crear tu `ssh-key` ya sea en Windows o Linux necesitamos tener 
instalado `ssh-keygen` en Windows `git bash` ya lo tiene si tu distro de Linux
no lo tiene es simplemente instalar eso. 

Puedes seguir los pasos en esta pagina https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

O seguir estos pasos que son lo mismo
1. Generar la Llave
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Esto te genera ciertos promt que tenemos que llenarlos. 
2. En nuestro home directory veremos que hay una carpeta `.ssh`
```
mike@Mike-Laptop:~/.ssh$ pwd
/home/mike/.ssh
mike@Mike-Laptop:~/.ssh$ ls
id_ed25519  id_ed25519.pub  known_hosts  known_hosts.old
```
En ese lugar se encuentra nuestra llave generada. Son dos llaves
y el que tenemos que aniadir a nuestra cuenta de git es el con extension 
`.pub` de llave publica. 
4. Aniadimos nuestra llave publica a este link https://github.com/settings/ssh/new

Con esto tenemos configurado nuestro ssh!!

## Creando un repositorio Remoto en Github
Es muy facil crear un repositorio en Github solo tenemos que ir a la 
pagina:

https://github.com/new

Y Crear con el nombre que queramos. Esto puede ser publico y privado.
Puedes tener N repositorios publicos pero solo 5 privados en Github.

## Conectarse a nuestro Reposiorio Remotamente. 
Una ves creado nuestro repositorio tenemos dos opciones de conexion `ssh`
o `http` en este escenario vamos a usar solo `ssh`. 

## git remote 
Este comando nos ayuda para aniadir, remover o cambiar nuestro repositorio 
remoto. En este escenario solo vamos a cubir aniadir.

`git remote add origin <url-repositorio-remoto>`
Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git remote add origin git@github.com:Gatusko/git-course.git
mike@Mike-Laptop:~/personal/git-course$ git remote
origin
```

## origin
Enimatico keyword que tenemos en git pero que pocos entienden su significado
en resumen estamos linkeando la palabra `origin` con nuestro repositorio. 
Mas adelante vamos a ver como seria sin usar la palabra `origin`. 
El uso para `origin` es cuando tenemos que pushear a distintos repos del mismo
codigo. Generalmente cuando hacemos un `fork` se puede aniadir pero generalmente
tenemos solo un repositorio remoto.

## git push
Este comando es para `pushear` o `subir` nuestros cambios a nuestro repositorio
este ejemplo es de este mismo curso vamos a subir todos nuestros cambios a Github

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git push origin master
Enumerating objects: 42, done.
Counting objects: 100% (42/42), done.
Delta compression using up to 32 threads
Compressing objects: 100% (40/40), done.
Writing objects: 100% (42/42), 7.05 KiB | 3.52 MiB/s, done.
Total 42 (delta 27), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (27/27), done.
To github.com:Gatusko/git-course.git
 * [new branch]      master -> master
```
Aqui vemos que pusheamos solo nuestra rama master.

Pero esto causa un problema. Si tenemos N ramas tendriamos que hacer
este comando por las N Ramos ir cambiando una por una. Para pushear
todo el historial local el comando

`git push origin --all`

Subira toda nuestra historia.

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git push origin --all
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:Gatusko/git-course.git
 * [new branch]      feature -> feature
 * [new branch]      feature-2 -> feature-2
 * [new branch]      feature-3 -> feature-3
 * [new branch]      merge-conflict -> merge-conflict
```
## Subir nuestros cambios
Como vimos `git push origin <nombre-de-la-rama>` es para subir nuestros
cambios. Entonces el orden general para subir nuestros commits son estos:

1. `git status` Para ver que vamos a subir y no subir archivos inncesarios
2. `git add .` o `git add <file-name>`
3. `git commit -m "nombre de commit"`
4. `git push origin <nombre-de-la-rama>`

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.md

no changes added to commit (use "git add" and/or "git commit -a")
mike@Mike-Laptop:~/personal/git-course$ git add .
mike@Mike-Laptop:~/personal/git-course$ git commit -m "Anidiendo Git Remote"
[master 98a76b3] Anidiendo Git Remote
 1 file changed, 131 insertions(+)
mike@Mike-Laptop:~/personal/git-course$ git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 32 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 2.38 KiB | 2.38 MiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:Gatusko/git-course.git
   1a60fac..98a76b3  master -> master
```
En este escenario vimos que Aniadimos los ultimos cambios del `readme.md`

## Clonar un repositorio Remoto 
Generalmente tenemos que clonarnos repositorios remotos y tenemos que trabajar
sobre ellos. El comando `git clone origin <repositorio:sobre ssh o https>` 
nos ayudara en eso. 

Ejemplo:
```
Michael Ramirez@Mike-Laptop MINGW64 ~/comunidad
$ git clone git@github.com:Gatusko/git-course.git
Cloning into 'git-course'...
remote: Enumerating objects: 45, done.
remote: Counting objects: 100% (45/45), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 45 (delta 29), reused 45 (delta 29), pack-reused 0 (from 0)
Receiving objects: 100% (45/45), 9.96 KiB | 1.42 MiB/s, done.
Resolving deltas: 100% (29/29), done.
```
En esto clonamos git-course caserito a nuestra carpeta principal.

## git fetch
Este comando es para que nuestro repositorio actual tenga los ultimos cambios.
Git no hace nada automatico tenemos que hacerlo manualmente nosotros para 
obtener los ulitmos cambios remotos a nuestro repositorio local

Ejemplo:
```
mike@Mike-Laptop:~/personal/git-course$ git fetch
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 253 bytes | 253.00 KiB/s, done.
From github.com:Gatusko/git-course
 * [new branch]      feature-4  -> origin/feature-4
```
Al hacer un git fetch hacemos que nuestro repositorio local tenga
los ultimos cambios. 

Es muy importante este comando veremos en errores comunes.


## git pull
Git pull es el comando para obtener los ultimos cambios a diferencia
de git fetch esto aplica nuestros cambios haciendo un merge. En resumida
git pull es dos comandos en uno:

`git pull` = `git fetch` + `git merge` o `git rebase`

Nostros cuando trabajamos en la rama siempre tenemos que hacer un git pull
de esa rama. 

Por que hace un `git merge` o un `git rebase`?

Si n  personas trabajan en la misma rama tiene que existir una conciliacion 
a la hora de obtener el trabajo de uno o del otro. Y puede existir que exista 
conflictos. Veremos dos Ejemplos

Happy Path: Usuario actualiza la rama master y el no trabajo en esa rama.
```
$ git pull origin master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 2), reused 3 (delta 2), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 927 bytes | 185.00 KiB/s, done.
From github.com:Gatusko/git-course
 * branch            master     -> FETCH_HEAD
   5013c1a..9c33dac  master     -> origin/master
Updating 5013c1a..9c33dac
Fast-forward
 readme.md | 42 +++++++++++++++++++++++++++++++++++++++++-
 1 file changed, 41 insertions(+), 1 deletion(-)
```
Aqui vemos que hicimos un FF merge el happy path y lo que todo queremos. 

Ejemplo 2: Los dos usuarios trabajan en la misma rama y los dos hacen 
el cambio provocando un conflicto. 

```
mike@Mike-Laptop:~/personal/git-course$ git push origin master
To github.com:Gatusko/git-course.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'github.com:Gatusko/git-course.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
Este es el primer error que nos sale ya que dos usuarios modificaron la rama 
y hay un conflict. Nos esta pidiendo que hagamos un `git pull`

```
mike@Mike-Laptop:~/personal/git-course$ git pull origin master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 2), reused 3 (delta 2), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 283 bytes | 283.00 KiB/s, done.
From github.com:Gatusko/git-course
 * branch            master     -> FETCH_HEAD
   9c33dac..5cb5ef6  master     -> origin/master
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```
Al hacer esto nos sale un error diciendo que tenemos que ver como reconciliar
nuestros cambios de nosotros con el de nuestro companiero.

Por defecto git va a tratar de ir siempre por el happy path de FF. 
Pero en este escenario no sera posible por que estamos trabajando en la misma rama
tenemos que decirle que nuestro pull tiene que ser sin FF


Comando `git pull origin <branch-name> --no-ff`
```
mike@Mike-Laptop:~/personal/git-course$ git pull origin master --no-ff
From github.com:Gatusko/git-course
 * branch            master     -> FETCH_HEAD
Auto-merging readme.md
CONFLICT (content): Merge conflict in readme.md
Automatic merge failed; fix conflicts and then commit the result.
```

Aqui ahora el error es un problema de merge que tenemos que solucionarlo

Una ves solucioando veremos podremos ver el commit del merge

```
mike@Mike-Laptop:~/personal/git-course$ git log --oneline
40af53e (HEAD -> master) Merge branch 'master' of github.com:Gatusko/git-course
5037929 more changes
5c8becc Git pull vs git push
5cb5ef6 (origin/master) Conflico en remoto
9c33dac Git pull example
5013c1a Change user name to user personal email
```

Veremos mas adelante con rebase este ejemplo

# Rebase
Bonito en teoria odiado en Practica. Es modificar nuestra historial de 
commit. Se puede "Mergear" Pero en realidad lo que hacemos es modificar
es historial de git. 

Hay muchos que dicen "Ni timas a rebase" En realidad si hacaces un rebase
local no deberia afectar. Sin embargo un Rebase remoto afecta y jode. 

De github(https://docs.github.com/en/get-started/using-git/about-git-rebase):

```
Warning

Because changing your commit history can make things difficult
 for everyone else using the repository, it's considered bad 
 practice to rebase commits when you've already pushed to a repository. 
 To learn how to safely rebase, see About pull request merges.
```

De BitBucket(https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)
```
Don't rebase public history
As we've discussed previously in rewriting history, 
you should never rebase commits once they've been pushed to a public repository.
The rebase would replace the old commits with new ones and it would look like that part of your project history abruptly vanished.
```

Y de muchos sources mas podriamos sacar esa informacion.

"Piro mi sinior mi dijo qui ribise es bueno" NOOO!! REBASE HACE QUE EXISTA LA POSIBILIDAD QUE SE PIERDA
LA HISTORIA YA QUE MODIFICAMOS LA HISTORIA!

Por mas que queramos tener un git tree sin commits y demas y perfecciontistas prefieran usar rebase.
El rebase causo muchos conflictos, es por eso que se sigue usando merge hasta el dia de hoy. 

Sin embargo daremos unos ejemplos de rebase.

# Git Merge con Rebase

En este escenario en ves de `merge` nuestra rama `feature-rebase` vamos a
hacer un `rebase`
Pasos:
1. Vamos a suponer que nuestra rama `feature-rebase` ya fue pusheada a nuestro
repositorio entonces vamos a tener que ir hacer un `git fetch`
```
mike@Mike-Laptop:~/personal/git-course$ git fetch
mike@Mike-Laptop:~/personal/git-course$ git log --all --graph --decorate --oneline --simplify-by-decoration
* c95c9b5 (origin/feature-rebase) new rebase
* 13b049b (HEAD -> master, origin/master) Git pull final
| * dd7dada (origin/feature-4) Test fetch
|/
* 5013c1a Change user name to user personal email
```
Aca vemos el commit c95c9b5 con este ID en la Rama despues del Rebase que pasara?
2. Sobre la rama de master hacemos un `git rebase`