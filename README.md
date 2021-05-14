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

## Conceptos importantes

* Directorio de trabajo: Entorno de desarrollo personal, lo que se ve en el explorador de archivos, también conocidos como ```untracked```.
* Área de preparación o ```staging```: Espacio en la RAM donde se almacenan los archivos que rastrea Git, también conocidos como ```tracked```.
Se añaden archivos a este espacio usando ```git add```.
* Repositorio local: Archivos en la base de datos que se encuentra en la carpeta .git. Al usar ```git commit```, se mueven todos los cambios en ```staging``` al repositorio local.
* Repositorio remoto: Repositorio almacenado en un servidor en internet.
Se puede descargar como repositorio local usando ```git clone```.
Los cambios del repositorio local se mueven a él usando ```git push```.
Se pueden recibir los cambios usando ```git fetch``` + ```git merge``` o usando ```git pull```.

* ```HEAD```: Es el lugar donde se está trabajando en el momento actual.
* ```master```:
* ```origin```: Es el nombre del repositorio remoto por defecto, que aparece al usar ```git clone```.

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

## Ver todas las configuraciones actuales

Existen 2 formas de hacerlo:

```
git config -l
```
```
git config --list
```

## Ver las configuraciones actuales y el archivo donde se encuentran

```
git config --list --show-origin
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
Se crea un área ```staging``` en la memoria RAM.
Se crea el repositorio en la carpeta ```.git```.
Por defecto, todos los archivos al momento de inicializar serán ```untracked```.

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

Los archivos añadidos con ```git add``` se vuelven ```tracked``` y se mueven a ```staged```.
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

## Remover todos los cambios realizados del ```staging```

```
git reset
```

Estos cambios se marcarán como ```untracked```.


## Remover un archivo específico del ```s ing```

```
git reset <archivo>
```

## Remover todos los cambios realizados y mantener staging

```
git reset --soft
```

## Remover todos los cambios realizados del disco

```
git reset --hard
```

## Hacer un commit con un mensaje

```
git commit -m "<mensaje del commit>"
```

El commit confirma todos los cambios ```staged``` al momento de realizarlo.
Los cambios confirmados se mueven a la carpeta ```.git```.
El mensaje debería describir en qué consistió el cambio.

## Hacer commit sin un mensaje

```
git commit
```

En realidad, no se puede hacer un commit si un mensaje.
Git mostrará un mensaje por defecto indicando que el usuario debe escribir el mensaje del commit y le pedirá que lo ingrese.
Se pedirá escribir el mensaje utilizando el editor Vim.

## Uso básico de Vim

Para comenzar a escribir texto se debe pulsar Escape + I, con lo cual se cambia al modo ```INSERTAR```.
Para salir de esta pantalla se debe pulsar Escape Shift Z Z, lo cual guarda el archivo y realiza el commit.
Si se deja el mensaje del commit en blanco, se aborta.

## Ver el historial de commits realizados

```
git log
```

## Listas largas de información

Si Git tiene demasiada información que mostrar con comandos como ```git log```, entonces no podrá mostrarla toda en pantalla al mismo tiempo.
Se puede pulsar Intro para mostrar la próxima línea, siempre que no aparezca ```(END)``` al final.
También se pueden usar las flechas para moverse por el archivo.
Para salir, se debe escribir ```q``` en el terminal.

## Ver el historial de commits compacto

```
git log --oneline
```

Esto reducirá los detalles que se muestran sobre cada commit.

## Ver historial de commits que alteraron un archivo específico

```
git log <archivo>
```

## Ver historial de cambios mostrando un resumen de los archivos modificados en cada usando

```
git log --stat
```

## Revisar el estado actual del repositorio

```
git status
```

El estado mostrará la rama actual y su estado al compararla con la rama remota, si esta existe.
Luego mostrará los cambios que tiene la base de datos, los cuales se separan en los cambios a archivos en ```staged```, los archivos que han recibido cambios pero todavía no están en ```staged``` y los archivos nuevos, que todavía no son parte del repositorio.

## Revisar las líneas cambiadas en el último comit

```
git show
```

## Agregar archivos de cierta extensión en el directorio actual

```
git add *.<extensión>
```

## Agregar archivos de cierta extensión de todo el repositorio

```
git add "*.<extensión>"
```

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
git commit -am "<mensaje del commit>"
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

Para los archivos binarios sólo se indica que difieren, ya que las diferencias son incomprensibles comparadas con el texto plano.

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

También se puede usar el hash ```#``` para escribir comentarios en el .gitignore.

```
# Este es un comentario
```

Se puede utilizar el símbolo de exclamación ```!``` para indicar algo que no se debe ignorar dentro de un directorio ignorado.

```
content
!content/README.md
```

Generalmente, se usa .gitignore para ignorar los siguientes tipos de archivos:

* Documentos que no son de texto plano
* Archivos binarios como imágenes, sonidos o videos
* Archivos con contraseñas o llaves de APIs, SSH, etc
* Configuraciones del entorno de ejecución
* Archivos compilados o usados sólo durante el proceso de compilación
* Archivos externos
* Logs o trazas
* Archivos que genera el sistema operativo
* Archivos que pueden contener información personal
* Archivos comprimidos como por ejemplo .zip, .tar.gz, .7z o .rar

## Borrar un archivo ```tracked``` del repositorio, sin removerlo del disco

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

Esto cambiará los archivos del directorio a los de la rama especificada.

## Crear una rama y conectarse a ella

```
git checkout -b <rama>
```

Básicamente es lo mismo que ```git branch``` seguido de ```git checkout```.

## Ver la lista de ramas creadas

```
git branch
```

La rama activa se mostrará en verde.

## Ver lista de ramas, incluyendo las remotas

```
git branch -a
```

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

Los commits siempre irán desde la rama escrita a la rama activa.
Los cambios se reciben en un nuevo commit, el cual también debe tener un mensaje.
Es por este motivo que al usar ```git merge```, se abrirá el editor Vim.
Sin embargo, en la mayoría de los casos el mensaje por defecto es suficiente.
Después de fusionar, se añade el nuevo commit a la rama activa y se traen todos los commits nuevos de la rama especificada.

## Conflictos

Git nunca borra nada.
En caso de que ocurra un conflicto, por ejemplo cuando 2 commits en 2 ramas distintas modifiquen la misma línea del código, este conflicto deberá ser gestionado manualmente.
La rama activa pasará a ser una rama temporal con el nombre ```<rama activa>|MERGING``` para indicar que la operación ```git merge``` no se pudo completar.

## Sintaxis de un conflicto

```
<<<<<<<< HEAD
<línea en la rama actual>
========
<línea en la rama que se quiere fusionar>
>>>>>>>> <rama que se quiere fusionar>
```

En los conflictos, ```<<<<<<<<``` indica el commit de la rama actual, ```>>>>>>>>``` indica el commit de la rama que se quiere fusionar y ```========``` actúa como un separador entre ambas versiones.

## Revisar el estado de los conflictos

```
git status
```

El comando ```git status``` que se mencionó anteriormente también indica los conflictos solucionados y los no solucionados.

## Solución de Conflictos

Los conflictos deben solucionarse editando los archivos manualmente, decidiendo qué cambios se dejan.
Se debe realizar un commit para confirmar la fusión, los cambios deben volver a añadirse usando ```git add```.
Cuando se solucione el conflicto, la rama activa pasa de ser ```<rama activa>|MERGING``` a ```<rama activa>``` y la rama temporal se borra.

## Cancelar una fusión en caso de conflictos

```
git merge --abort
```

## Comparar 2 commits

```
git diff <hash del commit origen> <hash del commit destino>
```

El hash del commit es el que aparece al usar ```git log```.
Se puede usar el hash corto o el hash largo, pero se recomienda usar el largo si es posible.
Los cambios mostrados son los cambios que se harían para ir del commit origen al commit destino.

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

## Mostrar los cambios ocurridos en todas las ramas

```
git log --all
```

## Mostrar los cambios en todas las ramas junto a un gráfico

```
git log --all --graph
```

## Mostrar los cambios en todas las ramas junto a un gráfico decorado

```
git log --all --graph --decorate --oneline
```

## Añadir una etiqueta

```
git tag <etiqueta> <hash del commit>
```

Las etiquetas generalmente se usan para marcar versiones.

## Añadir etiqueta con más detalles

```
git tag -a <etiqueta> -m "<mensaje>" <hash del commit>
```

## Mostrar una lista de todas las etiquetas

```
git tag
```

## Mostrar las etiquetas y sus referencias

```
git show-ref --tags
```

Son distintas a las referencias del commit que marcan.

## Revisar el repositorio en el estado que tenía en una etiqueta

```
git checkout <etiqueta>
```

## Revisar un archivo en específico en el estado que tenía en un commit

```
git checkout <hash del commit> <archivo>
```

## Revisar un archivo en específico en el estado que tiene en una rama

```
git checkout <rama> <archivo>
```

## Revisar un archivo en específico en el estado que tiene en una etiqueta

```
git checkout <etiqueta> <archivo>
```

## Regresar un archivo a una versión anterior

```
git checkout <hash del commit> <archivo>
git add <archivo>
git commit -m "<mensaje>"
```

## Añadir un repositorio remoto

```
git remote add origin <url>
```

El nombre ```origin``` es el más usado, pero se puede cambiar a lo que se desee.

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
git remote add origin <url>
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

Es importante recordar que esta clave es muy importante, ya que añade otro nivel de seguridad.
No se debe compartir con nadie.
Se pedirá esta clave regularmente.

## Generar clave SSH manualmente

Se debe ingresar a la carpeta home del usuario actual.
En caso de usar Windows, se recomienda hacer todo este proceso desde Git Bash.

```
ssh-keygen -t <algoritmo> -b <grado de encriptación> -C "<email>"
```

En este ejemplo se usará el algoritmo de encriptación RSA.

```
ssh-keygen -t rsa -b 4096 -C "<email>"
```

Después, pedirá la ubicación donde se guardará.
Se recomienda dejar la ubicación por defecto.
Luego pide un passphrase, como una capa de seguridad adicional.
Una passphrase es una contraseña que acepta espacios dentro de ella.
El archivo sin extensión es la llave privada y el archivo .pub es la llave pública.

Después se debe añadir la llave, para que el sistema operativo la reconozca.
El nombre del archivo varía dependiendo del método de encriptación empleado.

```
ssh-add ~/.ssh/id_rsa
```

Se debe añadir la clave privada, no la pública.
Es importante crear una clave privada para cada equipo y cada usuario.
Importante: NO SE DEBE MOVER NI COPIAR DE UNO A OTRO.

Copiar la llave pública SSH.

```
clip < ~/.ssh/id_rsa.pub
```

## Cambiar origen existente de un repositorio

Se puede usar para pasar de HTTP a SSH o viceversa.

```
git remote set-url origin <url nueva>
```

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

## Recibir cambios del repositorio remoto, aunque este inició de una forma distinta al actuales

```
git pull <repositorio> <rama> --allow-unrelated-histories
```

Esto sirve para casos en los que el repositorio remoto se inició con otros archivos, como por ejemplo un ```README.md``` o un ```.gitignore```.

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

## Borrar una etiqueta

```
git tag -d <etiqueta>
```

## Borrar una etiqueta del repositorio remoto

```
git push origin :refs/tags/<etiqueta>
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

## Borrar una rama remota

```
git push origin :<rama>
```

## Relacionar automáticamente las ramas de un repositorio local con uno remotos

```
git push -u <repositorio remoto> <rama>
```

Esto permite usar ```git push``` para enviar todos los cambios que se hagan en el futuro, en vez de tener que escribir el repositorio y la rama otra vez.

## Mostrar todas las ramas y su historia

```
git show-branch
```

## Mostrar todas las ramas y su historia, incluyendo las remotas

```
git show-branch --all
```

## Git Flow

Git Flow es un programa distinto de Git, pero que funciona de manera muy similar.

## Iniciar repositorio Git Flow

```
git flow init
```

Esto permite seleccionar los nombres de las ramas ```master```, ```develop```, ```feature```, ```release```, ```bugfix```, ```hotfix``` y ```support```.
En general, se recomienda mantener los nombres por defecto.
Se crearán las ramas ```master``` y ```develop```.

## Iniciar una rama de característica

```
git flow feature start <rama de característica>
```

Una rama de característica se usa para añadir una nueva funcionalidad al programa.
Estas ramas tendrán el prefijo ```feature/``` por defecto.
Se basan en los commits que se tenían en ```develop``` al momento de usar el comando.

## Finalizar una rama de característica

```
git flow feature finish <rama de característica>
```

Esto realiza 3 cosas: une los cambios a ```develop```, cambia a esa rama y borra la rama de característica.

## Mostrar historial de cambios incluyendo todas las ramas

```
git log --oneline --decorate --all --graph
```

## Mostrar historial de cambios detallado incluyendo todas las ramas

```
git log --decorate --all --graph
```

## Propagar cambios de la rama ```develop``` a la rama de característica

```
git checkout feature/<rama de característica>
git merge develop
```

## Iniciar una rama de lanzamiento

```
git flow release start <rama de lanzamiento>
```

Una rama de lanzamiento es una versión casi terminada de ```develop```.
Estas ramas tendrán el prefijo ```release/``` por defecto.
Se basan en los commits que se tenían en ```develop``` al momento de usar el comando.

## Finalizar una rama de lanzamiento
```
git flow release finish <rama de lanzamiento>
```

Esto realiza 3 cosas: une los cambios a ```develop```, cambia a esa rama y borra la rama de lanzamiento.

## Iniciar una rama de bugfix

```
git flow bugfix start <rama de bugfix>
```

Una rama de ```bugfix``` es una rama de correción de errores de una rama de ```release```.
Estas ramas tendrán el prefijo ```bugfix/``` por defecto.
Se basan en los commits que se tenían en ```develop``` al momento de usar el comando.

## Finalizar una rama de bugfix
```
git flow bugfix finish <rama de bugfix>
```

Esto realiza 3 cosas: une los cambios a ```develop```, cambia a esa rama y borra la rama de bugfix.

## Iniciar una rama de hotfix

```
git flow hotfix start <rama de hotfix>
```

Una rama de ```hotfix``` es una rama de correción de errores de ```master```.
Estas ramas tendrán el prefijo ```hotfix/``` por defecto.
Se basan en los commits que se tenían en ```develop``` al momento de usar el comando.

## Finalizar una rama de hotfix
```
git flow hotfix finish <rama de hotfix>
```

Esto realiza 3 cosas: une los cambios a ```develop```, cambia a esa rama y borra la rama de hotfix.

## Publicar una rama de característica al repositorio remoto

```
git flow feature publish <rama de característica>
```

## Recibir ramas de tipo feature

```
git flow feature pull origin
```

## Terminar una rama de característica y borrarla del repositorio remoto

```
git flow feature finish -F <rama de característica>
```

## Recibir ramas de tipo bugfix

```
git flow bugfix pull origin
```

## Terminar una rama de bugfix y borrarla del repositorio remoto

```
git flow bugfix finish -F <rama de característica>
```

## Recibir ramas de tipo hotfix

```
git flow hotfix pull origin
```

## Terminar una rama de hotfix y borrarla del repositorio remoto

```
git flow hotfix finish -F <rama de característica>
```