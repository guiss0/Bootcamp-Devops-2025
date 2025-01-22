

1. ¿Qué comando utilizarías para verificar si Docker está instalado correctamente? ¿Existe alguna forma que provea docker para saber si se pueden levantar los containers de forma correcta?

``` bash
docker --version 
#Al ver la version de docker, sabremos que esta instalado correctamente
```

```bash
docker images
# Al ver las imagenes, podemos saber que se pueden levantar con Docker run "imagen" , esto nos mostraria 
```

2. ¿Cómo habilitamos el servicio de Docker para que se inicie automáticamente al arrancar el sistema?
``` bash
sudo systemctl start docker
# Este comando arrancaria el servicio de docker en el sistema, haciendo que se inicie cada vez que se prenda. 

docker run --restart=always "imagen"
# Con este comando podremos hacer que el contenedor se levante, cada vez que se reinicia el sitema
```
3. ¿Qué información proporciona el comando "docker info"? Describe al menos tres aspectos clave.

``` bash
docker info

# Aspectos claves;
# Server, muestra los contenedores que estan en el sistema, los que estan corriendo, los que estan pausados y los que estan parados.
#Security options, muestra las opciones de seguridad que tiene el sistema con docker
# Imagees, muestra las imagenes en el sistema actual

### 1. **Información del entorno del servidor Docker**

- **Versión del motor de Docker**: Muestra la versión exacta del Docker Engine que se está utilizando.
- **Cgroups y controladores de almacenamiento**: Indica qué subsistema de control de recursos (Cgroups v1 o v2) y qué controlador de almacenamiento (como overlay2 o aufs) se están utilizando.
- **Tiempo de actividad del servidor**: Proporciona información sobre cuánto tiempo lleva ejecutándose el servicio Docker.

---

### 2. **Recursos del sistema**

- **CPU y memoria disponibles**: Muestra la cantidad de CPUs y memoria asignadas al daemon de Docker.
- **Número de contenedores**: Informa sobre el número total de contenedores en diferentes estados, como:
    - **Running** (en ejecución).
    - **Paused** (pausados).
    - **Stopped** (detenidos).
- **Número de imágenes**: Muestra cuántas imágenes están disponibles localmente en el sistema.

---

### 3. **Configuración de red y seguridad**

- **Configuración de redes**: Enumera las redes disponibles (bridge, host, none) y cualquier red personalizada creada.
- **Rootless mode**: Indica si Docker está ejecutándose en modo rootless (sin privilegios de superusuario).
- **Seccomp y AppArmor**: Muestra si estas características de seguridad están habilitadas, las cuales restringen las llamadas al sistema que pueden hacer los contenedores para mejorar la seguridad.

```
