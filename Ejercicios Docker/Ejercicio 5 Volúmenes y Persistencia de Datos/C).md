¿Cómo verificamos los detalles de un volumen creado?

Para ver los detalles de un volumen, se utiliza el comando:
``` bash
docker volume inspect <nombre_del_volumen>

docker volume inspect mysql-data
```

Este comando mostrará información como el punto de montaje del volumen en el host, su nombre y opciones de configuración.