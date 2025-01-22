¿Cómo crearías una red personalizada en Docker?

``` bash
docker network create \   --driver bridge \   --subnet=182.18.0.0/24 \   --gateway=182.18.0.1 \   wp-mysql-network
```

**Explicación del comando:**

1. **`docker network create`**: Crea una nueva red en Docker.
2. **`--driver bridge`**: Especifica que la red usará el controlador `bridge`.
3. **`--subnet=182.18.0.0/24`**: Define la subred en formato CIDR (en este caso, desde 182.18.0.0 hasta 182.18.0.255).
4. **`--gateway=182.18.0.1`**: Configura la dirección del gateway de la red.
5. **`wp-mysql-network`**: Nombre de la red que estás creando.

``` bash
docker network inspect wp-mysql-network
```
Esto mostrará la configuración de la red, incluyendo el controlador, subred y gateway. Deberías ver algo similar a: