# drupal8-docker
Learning Docker step by step until build a Drupal 8 Docker compose file.
# Aprendiendo Docker paso a paso.
_De un servidor sencillo con Dockerfile a un Docker compose para una aplicación web con Drupal 8._

## Primero: Dockerfile con apache 🚀

_El primer paso es un servidor sencillo con apache y un index.html fijo._

### Crear Dockerfile y código de ejemplo
Se utiliza la imagen oficial de [Apache](https://hub.docker.com/_/httpd): **httpd:2.4**. Los pasos a seguir serían:
* Crear una carpeta específica para el proyecto, por ejemplo _drupal8_.
* Crear un archivo llamado _Dockerfile_, sin extensión, con el siguiente contenido:
```
FROM httpd:2.4
COPY ./public-html/my-index.html /usr/local/apache2/htdocs/
```
* Crear una carpeta llamada _public-html_.
* Crear un fichero llamado _my-index.html_ dentro de la carpeta a _public-html_, con el siguiente contenido:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Probando Docker</title>
</head>
<body>
    <h1>Primera prueba con Docker</h1>
    <p>Ésta es la primera prueba con Dockerfile.</p>
    <h2>Segunda prueba con Docker</h2>
    <p>Ésta es la segunfa prueba con Dockerfile usando volúmenes bind.</p>
    <p>Enlace a otra página: <a href="./test2.html">Test 2</a></p>
</body>
</html>
```
* Usando la terminal, situarse en la carpeta del proyecto y ejecutar la sentencia para construir la imagen:
```
docker build -t drupal8 .
```
* Ejecutar el comando para iniciar el contenedor a partir de la imagen anterior:
```
docker run -dp 8080:80 --name my-apache drupal8
```
* Abrir el navegador y visitar [http://localhost:8080/my-index.html](http://localhost:8080/my-index.html).

### Modificar el código de ejemplo
Si se quiere modificar el archivo _index.html_ hay que:
* Detener el contenedor y borrar la imagen (por separado o en una sola línea:
```
docker rm -f [id del contenendor]
```
* Modificar el fichero _index.html_
* Construir de nuevo la imagen
* Levantar el contenedor de nuevo y visitar [http://localhost:8080/my-index.html](http://localhost:8080/my-index.html).
