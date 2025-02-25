# Git Config Commands Summary


| Command                                                                    | Description                                                                                              |
|----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| `git config --global user.name “<name>”`<br>`git config --global user.email “<email>”` | Aniadimos globalmente nuestro usuario y correo para que se vean en el commit                             |
| `git config --global --list`                                               | Vemos nuestra configuracion global                                                                       |
|  `git config user.name “<name>”`<br>`git config user.email “<email>”`      | Si usamos esto en nuestro repositorio local entonces va a usar esta configuracion en ves de las globales |
|  `git config --list`                                                                        | Ve la configuracion del reporistorio actual si esta usando la global o tiene algo configurado            | |                                                                                                          |     |


# Git Repositories Summary

| Command                         | Description                                                 |
|---------------------------------|-------------------------------------------------------------|
| `git init -b <branch-name>`     | Iniciamos el reposoitorio local.                            |
| `git status`                    | Vemos los files que fueron modificados o <br/> son nuevos   |
| `git add <file-name>`           | Aniade el archivo que queremos que este en el commit        |
| `git add .`                     | Aniade todos los archvis que modificaomos o<br/> son nuevos |
| `git commit -m "mi mensaje`     | Commit!  YA esta guardado en nuestro repositorio local      |
| `git push origin <branch-name>` | Subimos nuestros cambios al repositorio remoto!             |


# Git Branchs Summary 

| Command                              | Description                                                          |
|--------------------------------------|----------------------------------------------------------------------|
| `git checkout -b <nombre-del-branch` | Creamos y nos vamos a la nueva rama                                  |
| `git merge <branch-mame>`            | Mergamos la rama que queramos a nuestra rama que estamos acutalmente |
| `git pull origin <branch-name>`       | Obtenemos los cambios que estan en el respositorio remoto            |

# Git Repository Remote Summary 

| Command                                            | Description                                             |
|----------------------------------------------------|---------------------------------------------------------|
| `git remote add origin <url-repositorio-remoto>`   | Aniadimos la conexion url de nuestro repositorio remoto |
| `git clone origin <repositorio:sobre ssh o https>` | Clonamos el respositorio remoto a nuestra maquina       |
| `git fetch`                                         | Obtenemos todos los cambios del Repositorio Remoto      |
