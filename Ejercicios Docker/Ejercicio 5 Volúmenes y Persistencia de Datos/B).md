¿Cómo podrías usar un volumen para persistir datos en un contenedor de MySQL?

Puedes montar un volumen al iniciar un contenedor de MySQL especificando el volumen en el comando docker run y asignándolo al directorio donde MySQL guarda sus datos (generalmente /var/lib/mysql).

`docker run -d \ --name mysql-container \ -e MYSQL_ROOT_PASSWORD=root_password \ -v mysql-data:/var/lib/mysql \ mysql:latest`

Esto asegura que los datos de MySQL se guarden en el volumen `mysql-data`, incluso si el contenedor se elimina.