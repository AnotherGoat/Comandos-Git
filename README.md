# Comandos Git

Este es un repositorio con una lista de comandos para escribir en el terminal de Git.
Los conceptos no se explican demasiado, se debe considerar más como una "cheat sheet".

Todos los comandos deben ejecutarse desde el directorio raíz del repositorio.
Las palabras entre <> se deben reemplazar por el nombre del elemento que describen.

## Configuración inicial

Para poder realizar commits, Git necesita que su usuario registre su nombre y correo.

    git config --global user.name "<nombre>"
    git config --global user.email "<correo>"

## Verificar configuración inicial

    git config user.name
    git config user.email

## Inicializar un repositorio con la rama "master" (por defecto)

    git init

## Inicializar un repositorio con otra rama

    git init -b <rama>

## Almacenar una copia local de un repositorio en internet

    git clone <url>

La copia se almacenará en la carpeta actual.

## Almacenar una copia local en otra carpeta

    git clone <url> <carpeta>

## Agregar cambios hechos a archivos al próximo commit

    git add <archivo>

Los archivos añadidos con add serán marcados como "staged".

## Agregar todos los archivos dentro de una carpeta

    git add <directorio>

No se pueden agregar directorios vacíos.
Los directorios deben tener archivos para agregarlos.

## Agregar todos los cambios actuales

Hay 2 formas de hacerlo.

    git add .

    git add --all

## Hacer un commit con un mensaje

    git commit -m "<mensaje del commit>"

El commit confirma todos los cambios marcados como "staged" al momento de realizarlo.
El mensaje debería describir en qué consistió el cambio.

## Ver el historial de commits realizados

    git log

## Ver el historial de commits sin detalles

    git log --oneline

## Agregar archivos de cierta extensión en el directorio actual

    git add *.<extensión>

## Agregar archivos de cierta extensión de todo el repositorio

    git add "*.<extensión>"

## Revisar el estado actual del repositorio

    git status

El estado mostrará la rama actual y su estado al compararla con la rama remota, si esta existe.
También mostrará los cambios "staged", los archivos que han recibido cambios pero todavía no se marcan como "staged" y los archivos nuevos, que todavía no son parte del repositorio.

## Quitar un archivo de los cambios "staged"

    git restore --staged <archivo>

## Agregar archivos de forma interactiva

    git add -i

Esto inicia un menú para manejar los cambios.

## Ver todos los cambios en detalle, incluyendo los no registrados

    git diff

Se debe pulsar Ctrl+C para salir.

## Ver los cambios "staged" en detalle

    git diff --staged

Se debe pulsar Ctrl+C para salir.

## Deshacer el último commit local y mantener los cambios como "staged"

    git reset --soft HEAD^

## Deshacer el último commit local y borrar todos los cambios

    git reset --hard HEAD^

## Deshacer los últimos 2 commits locales y borrar todos los cambios

    git reset --hard HEAD^^

## Añadir archivos al último commit

    git add <archivo>
    git commit --amend -m "<Mensaje nuevo>"

El mensaje anterior se sobreescribirá.

## Ver el historial detallado de cambios de un archivo

    git blame <archivo>

Se debe pulsar Ctrl+C para salir.

## Borrar un archivo de Git y del disco

    git rm <archivo>

## Hacer que Git ignore archivos

Se debre crear el siguiente archivo en la carpeta raíz o donde están los archivos que se quieren ignorar.

    .gitignore

El archivo se modifica con cualquier editor de texto y los nombres de archivos o directorios dentro de él serán ignorados por Git.

## Borrar un archivo ignorado del repositorio, sin removerlo del disco

    git rm --cached <archivo>

Con archivo ignorado se refiere a los que aparecen en .gitignore, pero existen en el último commit.

## Crear una rama

    git branch <rama>

La rama creada será igual a la de origen y no estará activa.

## Cambiar la rama que se usa actualmente

    git checkout <rama>

## Crear una rama y conectarse a ella

    git checkout -b <rama>

Básicamente es lo mismo que branch seguido de checkout.

## Ver la rama activa

    git branch

## Ver la lista de ramas creadas

    git branch --list

La rama activa se mostrará en verde.

## Borrar una rama que no se está usando

    git branch -d <rama>

Si se tienen commits sin fusionar, se mostrarán errores.

## Forzar el borrado de una rama local

    git branch -D <rama>

Esto ignorará cualquier error.
Se debe tener cuidado al momento de usarlo.

## Cambiar el nombre de la rama activa

    git branch -m <nombre nuevo>

## Revisar las diferencias entre 2 ramas

    git diff <rama de origen> <rama de destino>

## Fusionar los commits de una rama a la rama activa

    git merge <rama>

## Comparar 2 commits

    git diff <id del commit 1> <id del commit 2>

## Conectar un repositorio remoto a uno local

    git remote add origin <url>

Las ramas remotas tendrán el nombre origin/<rama>.

## Ver el repositorio remoto

    git remote show origin

## Ver la lista de ramas remotas

    git branch -r

## Enviar los cambios locales al repositorio remoto

    git push

## Añadir una etiqueta

    git tag <etiqueta> <id del commit>

Las etiquetas generalmente se usan para marcar versiones.

## Mostrar una lista de todas las etiquetas

    git tag

## Revisar el repositorio en una etiqueta

    git checkout <etiqueta>

## Enviar etiquetas al repositorio remoto

    git push --tags

## Iniciar la interfaz gráfica

    gitk

## Iniciar un repositorio desde cero y subirlo a GitHub

Paso 1: Inicializar el repositorio local

    git init
    git add .
    git commit -m "<commit inicial>"
    git branch -m main

En GitHub, main es el nombre por defecto de la rama principal, en vez de master.

Paso 2: Crear el repositorio en GitHub y copiar su URL.

Paso 3: Añadir el repositorio remoto y subir los cambios

    git remote add origin <URL>
    git push --set-upstream origin main

Paso 4: Iniciar sesión en los logon que aparecerán

## Hacer que Git recuerde las credenciales del inicio de sesión en GitHub

Existen muchos métodos, pero el más seguro es usar SSH.

Paso 1: Generar una nueva clave SSH

     ssh-keygen -t ed25519 -C "<correo del usuario>"

Se debe pulsar Intro cuando pregunte donde guardarlo para que se guarde en la ubicación por defecto.
Después, se ingresa la passphrase que actúa como contraseña.
Es importante no olvidar esta contraseña.

Paso 2: Copiar el siguiente texto y guardarlo como un archivo de nombre ".profile" en la carpeta raíz de tu usuario del sistema operativo.

```
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2= agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env
```

Paso 3: Volver a iniciar Git Bash e ingresar la passphrase que se registró anteriormente.

Paso 4: Copiar la clave SSH

clip < ~/.ssh/id_ed25519.pub

Paso 5: Ir a GitHub > Settings > SSH and GPG keys > New SSH key y pegar la clave SSH

Es importante recordar que esta clave es muy importante.
No se debe compartir con nadie.