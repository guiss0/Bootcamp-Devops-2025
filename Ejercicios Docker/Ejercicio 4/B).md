 ¿Cómo iniciarías un contenedor y lo conectarías a una red personalizada?

```bash
docker run --name alpine-2 --network none -it alpine
```

**Explicación del comando:**

1. **`docker run`**: Crea y ejecuta un nuevo contenedor.
2. **`--name alpine-2`**: Asigna el nombre `alpine-2` al contenedor.
3. **`--network none`**: Conecta el contenedor a la red `none`. Esto significa que no tendrá conectividad de red.
4. **`-it`**: Ejecuta el contenedor en modo interactivo con acceso a la terminal.
5. **`alpine`**: Especifica que usará la imagen `alpine`


