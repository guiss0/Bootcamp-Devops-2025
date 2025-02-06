
Crearemos un contenedor con la aplicacion web Jenkins, para eso es necesario el siguiente comando. 

``` bash
docker run -d --name jenkins --user 1000 -p 127.0.0.1:8080:8080 -v jenkins_home:/var/jenkins_home jenkins/jenkins:latest
```

El comando `docker run` permite correr un contenedor a partir de una imagen dada. Las opciones que estamos utilizando:

- `-d`: Ejecuta el contenedor en segundo plano (detached mode).
- `--name <nombre_del_contenedor>`: Asigna un nombre al contenedor, lo que facilita su gestión (iniciar, detener, eliminar, etc.).
- `--user <UID>`: Especifica el **UID** del usuario que ejecutará el contenedor. Los usuarios del sistema suelen tener UID del 0 al 999, mientras que los usuarios creados por humanos generalmente tienen un UID mayor a 1000. Docker solo permite especificar el contenedor con un UID de usuario.
- `-p 127.0.0.1:8080:8080`: Mapea el puerto **8080** del contenedor al puerto **8080** de nuestro **localhost**. Esto asegura que el contenedor solo pueda ser accedido desde la máquina local, sin exponer el puerto en la red.
- `-v jenkins_home:/var/jenkins_home`: Crea un volumen llamado `jenkins_home` en el directorio **host**. Este volumen almacena los datos del contenedor, permitiendo realizar copias de seguridad, restauraciones y facilitar la persistencia de los datos de Jenkins incluso si el contenedor se reinicia o elimina.
-  `--network="nombre de la red"`: Designamos al contenedor a tener una red en especifico
-------

## Configuracion del Jenkins

Una vez iniciado el contenedor con el Jenkins corriendo, al entrar al localhost:8080 , nos pedira una password, la cual conseguiremos en el directorio 

`/var/jenkins_home/secrets/initialAdminPassword`

La conseguiremos con el siguiente comando; 

``` bash
docker exec -it jenkins bash 

# Con esto lograremos entrar a la bash del contenedor para poder ejecutar el siguiente comando; 

cat /var/jenkins_home/secrets/initialAdminPassword

# Esto nos mostrara la password para poder iniciar la configuracion del Jenkins

```

----
## Ejecutar scripts y verificar datos del Contenedor

Luego de configurar el Jenkins, creamos nuestro script para que haga lo que queremos 

``` bash
#!/bin/bash

echo -e "Primer script lanzado en Jenkins"

``` 

Luego de ejecutar nuestro primer script en Jenkins, entraremos al contenedor como usuario root

```bash
docker exec --it --user root jenkins
# Con esto entraremos como root al contenedor
# Luego de entrar como root, podremos ejecutar lo siguiente; 

apt install net-tools -y
apt install iputils-ping -y

# Luego de esto podriamos modificar el Jenkins con los comandos;

ifconfig 

# Podriamos probar pinguear alguna red

ping -c 5 "IP"

# Podriamos probar localmente con nuestra IP o podriamos generar otro contenedor

```

``` bash
docker run -d --name nginx nignx:latest 

docker exec -it nginx bash

apt install net-tools -y
apt install iputils-ping -y

# Con las herramientas instaladas ya podriamos verificar la ip dentro del contenedor 

# Otra forma de comprobar las redes es usando el comando 

docker inspect "nombre del contenedor"

# Con esto deberiamos de ver la red y la ip que el contenedor tiene, por defecto tienen la red bridge los contenedores, asi que deberian de poder verse. 

docker run -d --name nginx --network="none" nginx:latest

# Asi el contenedor no tendra conexion a internet

```
----

## Detener y borrar todos los contenedores


``` bash

# Si queremos detener un contenedor utilizamos el siguiente comando
docker stop "nombre del contenedor"

# Si queremos parar todos los contenedores
docker stop $(docker ps -a -q)

####################################################

# Si queremos borrar los contenedores 
docker rm "nombre del contenedor"

# Si queremos borrar todos
docker rm $(docker ps -a -q)

```

----

## Borrado de volumenes 

``` bash

# Prmero tenemos que ver los volumenes de los contenedores creados 

docker volume ls

# Luego de verlo, podemos elegir si los borramos todos o solo los que no estan en uso

docker volume prune 

# Borrara todos los volumenes que no esten en uso

docker volume rm $(docker volume ls)

# Borrara todos los volumenes

```

