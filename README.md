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

//Publish and Detached modes
docker container run docker/getting-started  // se descarga y ejecuta el contenedor pero no es accesible
docker container stop <nombre o id>  // detiene la ejecución del contenedor
docker container ls // lista los container
docker run -d -p 8080:80 docker/getting-started  // ejecuta el container y mapea el puerto 8080 de mi equipo con el 80 del contenedor
docker container start <nombre o id>  // se vuelve a ejecutar el container en el mismo puerto con que se ejecutó anteriormente
docker container prune // Elimina todos los contenedores detenidos
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
- []()
- []()
- []()
- []()
- []()
- []()
- []()
