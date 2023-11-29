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
# descargar la imagen con tag jammy
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

## Sección 3: Volúmenes y Redes

Para hacer persistente el contenido de los contenedores, es necesario moverlos a volúmenes.

- Ejercicio sin volúmenes - Montar Base de Datos

1. Montar la imagen de MariaDB con el tag jammy, publicar en el puerto 3306 del contenedor con el puerto 3306 de nuestro equipo, colocarle el nombre al contenedor de **world-db** (--name world-db) y definir las siguientes variables de entorno:
   - MARIADB_USER=example-user
   - MARIADB_PASSWORD=user-password
   - MARIADB_ROOT_PASSWORD=root-secret-password
   - MARIADB_DATABASE=world-db

```sh
# descargar la imagen con tag jammy (realmente no es necesario pues el próximo comando descarga el docker sino existe)
docker pull mariadb:jammy

# ejecutar el contenedor en el puerto 3306 local y usar el docker `mariadb` con tag `jammy`
docker container run \
--name world-db \
-e MARIADB_USER=example-user \
-e MARIADB_PASSWORD=user-password \
-e MARIADB_ROOT_PASSWORD=root-secret-password \
-e MARIADB_DATABASE=world-db \
-dp 3306:3306 \
mariadb:jammy

```

2. Conectarse usando Table Plus a la base de datos con las credenciales del usuario (NO EL ROOT)
3. Conectarse a la base de datos `world-db`
4. Ejecutar el query de creación de tablas e inserción proporcionado (https://import.cdn.thinkific.com/643563/courses/2100309/world-221207-123207.sql)
5. Revisar que efectivamente tengamos la data (Cmd + R para refrescar Table-plus y ver las tablas)

```sh
docker container ls
docker container rm -f <id-del-container>
```

---

- Tipos de volúmenes

  - Named volumes
  - Bind volumes
  - Anonymouse volumes

```sh
# Crear un volumen (world-db)
docker volume create world-db

# Listar los volumenes
docker volume ls

# Ver detalles del volumen
docker volume inspect world-db

# crear volumen (https://hub.docker.com/_/mariadb)
docker container run \
--name world-db \
--env MARIADB_USER=example-user \
--env MARIADB_PASSWORD=user-password \
--env MARIADB_ROOT_PASSWORD=root-secret-password \
--env MARIADB_DATABASE=world-db \
-dp 3306:3306 \
--volume world-db:/var/lib/mysql \
mariadb:jammy
```

Sí se borra el contenedor, los datos se mantienen persistentes en `/var/lib/mysql` gracias a la opcion `--volume world-db:/var/lib/mysql`

- PHPMyAdmin

```sh

# crear volumen (https://hub.docker.com/_/phpmyadmin/tags) con tag `5.2.0-apache`
docker container run \
--name phpmyadmin \
-d \
-e PMA_ARBITRARY=1 \
-p 8080:80 \
phpmyadmin:5.2.0-apache

# Abrir phpmyadmin en el browser cargado en el contenedor (no es necesario tener datos persistentes)
browser http://localhost:8080
# El contenedor no tiene acceso al de la base de datos de world-db con mariaDB al no estar el segundo expuesto.

# Conectar el contenedor de phpmyadmin con el de mariaDB con word-db (dos conetenedores)

```

## Recursos

- [https://hub.docker.com/\_/hello-world](https://hub.docker.com/_/hello-world)
- [https://hub.docker.com/\_/mariadb](https://hub.docker.com/_/mariadb)
- [https://hub.docker.com/\_/postgres](https://hub.docker.com/_/postgres)
- [Instalaciones necesarias](https://gist.github.com/Klerith/3f611ff0e5c15b733ac63365ab310a35)
- [Guías de atajos Docker](https://devtalles.com/files/docker-cheat-sheet.pdf)
- [Guías de atajos Docker Local](docs/docker-cheat-sheet.pdf)
- [Repositorio de imagenes](https://hub.docker.com/)
