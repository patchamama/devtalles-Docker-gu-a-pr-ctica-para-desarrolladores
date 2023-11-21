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

// Hola Mundo en Docker
docker pull hello-world
docker container run hello-world // ejecuta la imagen hello-work

// Borrar contenedores e imágenes
docker container --help // muestra la ayuda
docker container ls // Lista los comandos
docker container ls -a // Muestra todos los contenedores
docker container rm <CONTAINER IDs separados por espacio y pueden ser los primeros 3 caracteres> // Elimina un contenedor
docker container prune // Elimina todos los contenedores detenidos

docker image --help // lista ayuda con imagenes
docker image ls -a // lista todas las imágenes
docker image rm -f <IMAGE ID> // Imagen a borrar de forma forzada (sí se está ejecutando)
docker image rm hello-world

// Publish and Detached modes
docker container run docker/getting-started  // se descarga y ejecuta el contenedor pero no es accesible
docker container stop <nombre o id>  // detiene la ejecución del contenedor
docker container ls // lista los container
docker run -d -p 8080:80 docker/getting-started  // ejecuta el container y mapea el puerto 8080 de mi equipo con el 80 del contenedor
docker container start <nombre o id>  // se vuelve a ejecutar el container en el mismo puerto con que se ejecutó anteriormente
docker container prune // Elimina todos los contenedores detenidos
docker image rm <nombre o id> // elimina la imagen del contenedor

// Variables de entorno
docker pull postgres // https://hub.docker.com/_/postgres
docker run --name some-postgres -dp 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -d postgres  // se ejecuta la imagen en el puerto local 5432 y sí no está se descarga. User: postgres y pass: mysecretpassword

// Usar la imagen de Postgres
docker container ls // muestra los contenedores y puertos abiertos
// abrir tableplus.app y conectar
```

- []()
- []()
- []()
- []()
- []()
- []()
- []()
- []()
- []()

## Recursos

- [https://hub.docker.com/\_/hello-world](https://hub.docker.com/_/hello-world)
- [Instalaciones necesarias](https://gist.github.com/Klerith/3f611ff0e5c15b733ac63365ab310a35)
- [Guías de atajos Docker](https://devtalles.com/files/docker-cheat-sheet.pdf)
- [Guías de atajos Docker Local](docs/docker-cheat-sheet.pdf)
- [Repositorio de imagenes](https://hub.docker.com/)
- []()
- []()
- []()
- []()
- []()
- []()
