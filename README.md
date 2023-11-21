# devTalles - Docker: Guía práctica de uso para desarrolladores

Notas sobre el curso sobre Docker impartido por Fernando Herrera: https://cursos.devtalles.com/courses/docker-guia-practica

## Description

Aquí aprenderás Docker y para qué te puede servir, aprende a utilizar y crear imágenes, controlar el versionamiento y construcción automática de las mismas.

## Sección 1: Introducción

- [Instalaciones necesarias](https://gist.github.com/Klerith/3f611ff0e5c15b733ac63365ab310a35)
- [Guías de atajos Docker](https://devtalles.com/files/docker-cheat-sheet.pdf)
- [Guías de atajos Docker Local](docs/docker-cheat-sheet.pdf)

## Sección 2: Bases de Docker

```sh
## Hola Mundo en Docker
docker pull hello-world
# ejecuta la imagen hello-work
docker container run hello-world

## Borrar contenedores e imágenes
# muestra la ayuda
docker container --help
# Lista los comandos
docker container ls
# Muestra todos los contenedores
docker container ls -a
# Elimina un contenedor
docker container rm <CONTAINER IDs separados por espacio y pueden ser los primeros 3 caracteres>
# Elimina todos los contenedores detenidos
docker container prune
# lista ayuda con imagenes
docker image --help
# lista todas las imágenes
docker image ls -a
# Imagen a borrar de forma forzada (sí se está ejecutando)
docker image rm -f <IMAGE ID>
docker image rm hello-world

## Publish and Detached modes
# se descarga y ejecuta el contenedor pero no es accesible
docker container run docker/getting-started
# detiene la ejecución del contenedor
docker container stop <nombre o id>
# lista los container
docker container ls
# ejecuta el container y mapea el puerto 8080 de mi equipo con el 80 del contenedor
docker run -d -p 8080:80 docker/getting-started
# Abrir el navegador en el puerto 8080
browse http://localhost:8080/
# se vuelve a ejecutar el container en el mismo puerto con que se ejecutó anteriormente
docker container start <nombre o id>
#  Elimina todos los contenedores detenidos
docker container prune
# elimina la imagen del contenedor
docker image rm <nombre o id>

## Variables de entorno
# https://hub.docker.com/_/postgres
docker pull postgres
# se ejecuta la imagen en el puerto local 5432 y sí no está se descarga. User: postgres y pass: mysecretpassword
docker run --name some-postgres -dp 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d postgres

# Usar la imagen de Postgres
# muestra los contenedores y puertos abiertos
docker container ls
# abrir tableplus.app y conectar

## Multiples instancias de Postgres
# primera instancia de nombre postgres-alpha corriendo localmente en el puerto 5432
docker container run \
--name postgres-alpha \
-e POSTGRES_PASSWORD=mypass1 \
-dp 5432:5432 \
postgres
# segunda instancia de nombre postgres-alpha1 corriendo localmente en el puerto 5433
docker container run \
--name postgres-alpha1 \
-e POSTGRES_PASSWORD=mypass1 \
-dp 5433:5432 \
postgres:14-bookworm
# listar contenedores activos
docker container ls -a
# parar ambos contenedor y removerlos
docker container rm -f id1 id2

## Logs del contenedor
docker container logs <container id>
# va mostrando live el log mientras se actualiza
docker logs --follow CONTAINER
# descargar la imagen
docker pull mariadb:jammy
# ejecutar el contenedor en el puerto 3307 local (el 3306 está ocupado)
docker container run \
-e MARIADB_RANDOM_ROOT_PASSWORD=yes \
-dp 3307:3306 \
mariadb:jammy
# obtener listado de contenedores activos
docker container ls -a
# me permite ver el password generado automáticamente (con usuario root)
docker container logs <container id> | grep PASSWORD
# abrir tableplus.app y conectar

## Tarea - Borrar todas las imágenes de Postgres
# Detener imágenes que están corriendo
docker container ls -a
docker container stop <id>
# Eliminar todas las imágenes que tengo de postgres
docker image ls -a
docker image rm <id>
```

## Recursos

- [https://hub.docker.com/\_/hello-world](https://hub.docker.com/_/hello-world)
- [https://hub.docker.com/\_/mariadb](https://hub.docker.com/_/mariadb)
- [https://hub.docker.com/\_/postgres](https://hub.docker.com/_/postgres)
- [Instalaciones necesarias](https://gist.github.com/Klerith/3f611ff0e5c15b733ac63365ab310a35)
- [Guías de atajos Docker](https://devtalles.com/files/docker-cheat-sheet.pdf)
- [Guías de atajos Docker Local](docs/docker-cheat-sheet.pdf)
- [Repositorio de imagenes](https://hub.docker.com/)
