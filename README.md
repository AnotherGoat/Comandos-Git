# Comandos Git

Este es un repositorio con una lista de comandos para escribir en el terminal de Git.
Los conceptos no se explican demasiado, se debe considerar más como una "cheat sheet".

Todos los comandos deben ejecutarse desde el directorio raíz del repositorio.
Las palabras entre <> se deben reemplazar por el nombre del elemento que describen.

## Importancia de Git

Git permite:

* Guardar sólo los cambios realizados a muchos archivos.
* Permitir que múltiples personas modifiquen el mismo archivo sin que se pierda el trabajo de ninguno.
* Saber qué persona cometió algún error.
* Revertir los cambios a una versión anterior.

## Instalar Git

Se debe descargar el instalador desde el [sitio web oficial](https://www.git-scm.com/downloads).
Para asegurarse de que se instaló correctamente, se puede usar el siguiente comando.

```
git --version
```

## Ver una pequeña introducción a Git

```
git
```

## Abrir documentación sobre un comando

```
git help <comando>
```

Esto abrirá la documentación sobre el comando en el navegador predefinido.

## Hacer la configuración inicial

Para poder realizar commits, Git necesita que su usuario registre su nombre y correo.

```
git config --global user.name "<nombre>"
git config --global user.email "<correo>"
```

## Verificar configuración inicial

```
git config user.name
git config user.email
```

## Iniciar la interfaz gráfica

```
gitk
```

## Inicializar un repositorio Git

```
git init
```

Por defecto, este repositorio se iniciará con la rama ```master```.

## Inicializar un repositorio en otra carpeta

```
git init <ruta>
```

## Inicializar un repositorio con otra rama

```
git init -b <rama>
```

## Cambiar el nombre de rama predeterminado

```
git config --global init.defaultBranch <rama>
```

Esto cambiará el nombre de la rama creada al usar ```git init```.
Un ejemplo de uso es para cambiar el valor por defecto ```master``` a ```main```, ya que gran parte de la comunidad de Git ha empezado a migrar a este nuevo nombre.

## Almacenar una copia local de un repositorio remoto usando HTTPS

```
git clone <url>
```

La copia se almacenará en la carpeta actual.

## Clonar usando SSH

```
git clone <usuario>@<host>:<ruta>
```

## Almacenar una copia local en una carpeta distinta

Usando HTTPS o SSH

```
git clone <url> <carpeta>
git clone <usuario>@<host>:<ruta> <carpeta>
```

## Hacer la configuración para el repositorio actual

```
git config --local user.name "<nombre>"
git config --local user.email "<correo>"
```

Esta configuración se guardará como local y sobreescribe la configuración global (sólo para los repositorios donde se haya configurado).

## Agregar cambios hechos a un archivo específico

```
git add <archivo>
```

Los archivos añadidos con ```git add``` se mueven a ```staged```.
Para confirmarlos, se usa el comando ```git commit```, que se explica más adelante.

## Agregar todos los archivos dentro de una carpeta

```
git add <directorio>
```

No se pueden agregar directorios vacíos.
Git sólo registra cambios hechos a archivos y añade directorios sólo cuando tienen archivos dentro de ellos.

## Agregar todos los cambios actuales

Existen 2 formas de hacerlo.

```
git add .
```

```
git add --all
```

Se agregan todos los archivos de la carpeta actual.

## Remover todos los cambios realizados

```
git reset
```

## Remover un archivo específico

```
git reset <archivo>
```

## Hacer un commit con un mensaje

```
git commit -m "<mensaje del commit>"
```

El commit confirma todos los cambios ```staged``` al momento de realizarlo.
El mensaje debería describir en qué consistió el cambio.

## Ver el historial de commits realizados

```
git log
```

## Salir de una lista larga de información

Si Git tiene demasiada información que mostrar con comandos como ```git log```, entonces no podrá mostrarla toda en pantalla al mismo tiempo.

Se puede pulsar Intro para mostrar la próxima línea, siempre que no aparezca ```(END)``` al final.

Para salir, se debe escribir ```q``` en el terminal.

## Ver el historial de commits compacto

```
git log --oneline
```

Esto reducirá los detalles que se muestran sobre cada commit.

## Agregar archivos de cierta extensión en el directorio actual

```
git add *.<extensión>
```

## Agregar archivos de cierta extensión de todo el repositorio

```
git add "*.<extensión>"
```

## Revisar el estado actual del repositorio

```
git status
```

El estado mostrará la rama actual y su estado al compararla con la rama remota, si esta existe.
Luego mostrará los cambios que tiene la base de datos, los cuales se separan en los cambios a archivos en ```staged```, los archivos que han recibido cambios pero todavía no están en ```staged``` y los archivos nuevos, que todavía no son parte del repositorio.

## Quitar un archivo de los cambios ```staged```

```
git restore --staged <archivo>
```

## Agregar archivos de forma interactiva

```
git add -i
```

Esto inicia un menú para manejar los cambios.

## Hacer un commit con todos los cambios hechos a archivos conocidos

Existen 2 formas de hacerlo. No es necesario usar ```git add``` de antemano.

```
git commit -a -m "<mensaje del commit>"
```

```
git commit --all -m "<mensaje del commit>"
```

Con "archivos conocidos" se refiere a los archivos que ya eran parte del repositorio en el último commit realizado y que tuvieron cambios desde la realización de éste.
En otras palabras, los archivos nuevos serán ignorados en este commit.

## Ver todos los cambios en detalle, incluyendo los no registrados

```
git diff
```

## Ver los cambios en ```staged``` en detalle

```
git diff --staged
```

## Deshacer el último commit local y mantener los cambios como ```staged```

```
git reset --soft HEAD^
```

## Deshacer el último commit local y borrar todos los cambios

```
git reset --hard HEAD^
```

## Deshacer los últimos 2 commits locales y borrar todos los cambios

```
git reset --hard HEAD^^
```

## Añadir archivos al último commit

```
git add <archivo>
git commit --amend -m "<mensaje nuevo>"
```

El mensaje anterior se sobreescribirá.

## Ver el historial detallado de cambios de un archivo

```
git blame <archivo>
```

## Borrar un archivo de Git y del disco

```
git rm <archivo>
```

Esto sólo funciona con los archivos que están presentes en el último commit realizado.

## Hacer que Git ignore archivos

Se debe crear el siguiente archivo en la carpeta raíz o donde están los archivos que se quieren ignorar.

```
.gitignore
```

El archivo se modifica con cualquier editor de texto y los nombres de archivos o directorios dentro de él serán ignorados por Git.

Por ejemplo, para hacer que Git ignore el archivo ```archivo.txt``` y todos los archivos de la carpeta ```test```, el .gitignore debe tener el siguiente contenido.

```
archivo.txt
test
```

## Borrar un archivo ignorado del repositorio, sin removerlo del disco

```
git rm --cached <archivo>
```

Con archivo ignorado se refiere a los que aparecen en ```.gitignore```, pero tenían una versión guardada en el último commit.
Al igual que ```git add```, esta operación será confirmada en el próximo commit.

## Crear una rama

```
git branch <rama>
```

La rama creada será igual a la de origen y no estará activa.

## Cambiar la rama que se usa actualmente

```
git checkout <rama>
```

## Crear una rama y conectarse a ella

```
git checkout -b <rama>
```

Básicamente es lo mismo que ```git branch``` seguido de ```git checkout```.

## Ver la rama activa

```
git branch
```

## Ver la lista de ramas creadas

```
git branch --list
```

La rama activa se mostrará en verde.

## Borrar una rama que no se está usando

```
git branch -d <rama>
```

Si se tienen commits sin fusionar, se mostrarán errores.

## Forzar el borrado de una rama local

```
git branch -D <rama>
```

Esto ignorará cualquier error.
Se debe tener cuidado al momento de usarlo.

## Cambiar el nombre de la rama activa

```
git branch -m <nombre nuevo>
```

## Revisar las diferencias entre 2 ramas

```
git diff <rama de origen> <rama de destino>
```

## Fusionar los commits de una rama a la rama activa

```
git merge <rama>
```

## Comparar 2 commits

```
git diff <hash del commit 1> <hash del commit 2>
```

El hash del commit es el que aparece al usar ```git log```.
Se puede usar el hash corto o el hash largo, pero se recomienda usar el largo si es posible.

## Regresar a un commit pasado temporalmente

```
git checkout <hash del commit>
```

En este estado, no se pueden hacer commits.

## Regresar a un commit pasado y crear una rama nueva

```
git checkout -b <rama> <hash del commit>
```

Esto permite hacer commits en una rama nueva que tendrá como último commit el del hash que se le entregó.

## Conectar un repositorio local a uno remoto

```
git remote add origin <url>
```

Las ramas remotas tendrán el nombre ```origin/<rama>```.

## Ver el repositorio remoto

```
git remote show origin
```

## Ver la lista de ramas remotas

```
git branch -r
```

## Enviar los cambios locales al repositorio remoto

```
git push
```

## Añadir una etiqueta

```
git tag <etiqueta> <hash del commit>
```

Las etiquetas generalmente se usan para marcar versiones.

## Mostrar una lista de todas las etiquetas

```
git tag
```

## Revisar el repositorio en el estado que tenía en una etiqueta

```
git checkout <etiqueta>
```

## Iniciar un repositorio desde cero y subirlo a GitHub/GitLab

Paso 1: Inicializar el repositorio local.

```
git init
git add .
git commit -m "<commit inicial>"
git branch -m main
```

En GitHub, main es el nombre por defecto de la rama principal, en vez de master.

Paso 2: Crear el repositorio en GitHub/GitLab y copiar su URL.

Paso 3: Añadir el repositorio remoto y subir los cambios.

```
git remote add origin <URL>
git push -u origin main
```

Paso 4: Iniciar sesión en los logon que aparecerán.

## Hacer que Git recuerde las credenciales del inicio de sesión en GitHub/GitLab

Existen muchos métodos, pero el más seguro es usar SSH.

Paso 1: Generar una nueva clave SSH en base al correo electrónico.

```
ssh-keygen -t ed25519 -C "<correo del usuario>"
```

Se debe pulsar Intro cuando pregunte donde guardarlo para que se guarde en la ubicación por defecto.
Después, se ingresa la passphrase que actuará como una contraseña.
Es importante no olvidar la passphrase.

Paso 2: Copiar el siguiente texto y guardarlo como un archivo de nombre ```.profile``` en la carpeta raíz de tu usuario del sistema operativo.

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

Paso 4: Copiar la clave SSH.

```
clip < ~/.ssh/id_ed25519.pub
```

Paso 5 (GitHub): Ir a GitHub > Settings > SSH and GPG keys > New SSH key y pegar la clave SSH.

Paso 5 (GitLab): Ir a GitLab > Preferences > SSH Keys > pegar la clave SSH y Add key.

Es importante recordar que esta clave es muy importante.
No se debe compartir con nadie.
Se pedirá esta clave regularmente.

## Recibir cambios desde el repositorio remoto

```
git fetch
```

Cualquier conflicto que se encuentre deberá ser solucionado usando ```git add```.

## Recibir cambios desde el repositorio remoto y fusionar

```
git pull
```

Los conflictos se solucionarán automáticamente, pero puede causar errores.
Básicamente es un ```git fetch``` seguido de un ```git merge```.

## Subir un cambio de la rama local al repositorio remoto y sincronizar

```
git push -u
```

Esto hará que se suban los cambios locales y hace que se relacionen las ramas locales con las remotas automáticamente.
Se recomienda usar ```git fetch``` o ```git pull``` antes de ```git push```, especialmente si se está trabajando con otras personas.

## Subir cualquier cambio hecho a la rama local después de conectar el repositorio remoto

```
git push
```

Este cambio sólo subirá los cambios de la rama activa.
Si es la primera vez que se suben cambios, se recomienda usar ```git push -u```.

## Enviar etiquetas al repositorio remoto

```
git push --tags
```

## Enviar todas las ramas y etiquetas

```
git push --all
```

## Revertir el repositorio local a un commit todavía no subido al repositorio remoto

```
git reset --hard <hash del commit>
```

Esto eliminará todos los cambios locales.
No se debe usar si todavía se tiene trabajo que se quiere mantener.

## Deshacer un commit subido al repositorio remoto

```
git revert <hash del commit>
```

Esto hará un commit que deshace los cambios.

## Deshacer múltiples commits en commits separados

```
git revert <hash del commit 1> <hash del commit 2> ...
```

Cada hash proporcionado creará su propio commit de reversión.

## Deshacer múltiples commits en un mismo commit

```
git revert --no-commit <hash del commit 1> <hash del commit 2> ...
git commit -m "<mensaje del commit>"
```

Esto permite juntar muchos ```git revert``` en un mismo commit.

## Añadir otro repositorio remoto

```
git remote add <nombre del repositorio> <url>
```

Al usar comandos como ```git clone```, el repositorio remoto creado por defecto se llama ```origin```.
Por este motivo, se acostumbra que el primer repositorio remoto tenga ese nombre.
Sin embargo, no es obligatorio.
Perfectamente, se pueden tener 2 repositorios remotos llamados ```github``` y ```gitlab```.

## Revisar todos los repositorios remotos

```
git remote -v
```

## Enviar los cambios hechos a un repositorio remoto en específico

```
git push <repositorio remoto> <rama>
```

## Enviar los cambios hechos a varios repositorios remotos

```
git push <repositorio remoto 1> <rama 1> && git push <repositorio remoto 2> <rama 2>
```
