¿Cómo crearías un contenedor que utilice un usuario no root?

``` dockerfile
# Usar una imagen base
FROM ubuntu:20.04

# Crear un usuario no root (ejemplo: appuser)
RUN useradd -m -s /bin/bash appuser

# Cambiar al usuario no root
USER appuser

# Configurar el directorio de trabajo
WORKDIR /home/appuser

# Instrucción CMD o ENTRYPOINT
CMD ["bash"]
```

- `RUN useradd -m -s /bin/bash appuser`: Crea el usuario `appuser` con su directorio home.
- `USER appuser`: Cambia al usuario no root para todas las operaciones posteriores.
- `WORKDIR /home/appuser`: Establece el directorio base para las operaciones del contenedor.

docker build -t non-root-container . 
docker run -it non-root-container