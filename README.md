# Comandos Git

Este es un repositorio con una lista de comandos para escribir en el terminal de Git.
Los conceptos no se explican demasiado, se debe considerar más como una "cheat sheet".

Todos los comandos deben ejecutarse desde el directorio raíz del repositorio.
Las palabras entre <> se deben reemplazar por 

## Inicializar un repositorio con la rama "master" (por defecto)

    git init

## Inicializar un repositorio con otra rama

    git init -b <rama>

## Revisar el estado actual del repositorio

    git status

## Almacenar una copia local de un repositorio en internet

    git clone <url>

    git clone <usuario>@<host>:ruta

## Agregar cambios al próximo commit

    git add <archivo o carpeta>

## Agregar todos los cambios actuales

    git add .

    git add -all

## Agregar archivos de forma interactiva

    git add -i

## Hacer un commit con un mensaje

    git commit -m "<mensaje del commit>"

## Ver el historial de commits realizados

    git log