¿Cómo podrías reutilizar un volumen existente al iniciar un nuevo contenedor?

Para reutilizar un volumen existente, simplemente usa el flag -v y especifica el nombre del volumen al iniciar el nuevo contenedor.


``` bash
docker run -d \
--name new-mysql-container \
-e MYSQL_ROOT_PASSWORD=new_password \
-v mysql-data:/var/lib/mysql \
mysql:latest
```

En este caso, el contenedor new-mysql-container utilizará el volumen mysql-data, que ya contiene los datos previamente almacenados. Esto asegura que los datos se mantengan consistentes entre múltiples contenedores.