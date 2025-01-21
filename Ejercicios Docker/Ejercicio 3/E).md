 ¿Cual es la diferencia entre CMD, ENTRYPOINT y RUN?

`RUN`:
- **Propósito:** Ejecutar comandos durante el proceso de construcción de la imagen (en la creación de capas).
    
- **Uso principal:** Instalar software, copiar archivos, configurar el sistema o preparar el entorno dentro de la imagen.
    
- **Cuándo se ejecuta:** Durante la **construcción** de la imagen.
- EJEMPLO; RUN apt-get update && apt-get install -y nginx
- Los cambios realizados con `RUN` quedan permanentemente en la imagen.


`CMD`:
- **Propósito:** Especificar el comando por defecto que se ejecutará al iniciar un contenedor.
    
- **Uso principal:** Definir el comando o script principal que debe ejecutarse en el contenedor.
    
- **Cuándo se ejecuta:** Al **correr** el contenedor (es decir, con `docker run`).
EJEMPLO: 
CMD ["nginx", "-g", "daemon off;"]
- **Características clave:**
    
    - Se puede sobrescribir al usar un comando explícito en `docker run`. Por ejemplo:
        
        `docker run <imagen> echo "Hola Mundo"`
        
    - Solo puede haber un `CMD` en un Dockerfile. Si hay múltiples, solo el último será efectivo.


`ENTRYPOINT`:
- **Propósito:** Similar a `CMD`, pero diseñado para ejecutar un programa específico como el punto de entrada del contenedor.
    
- **Uso principal:** Garantizar que siempre se ejecuta el comando especificado, incluso si se pasan argumentos adicionales a `docker run`.
    
- **Cuándo se ejecuta:** Al **correr** el contenedor.
    
- **Ejemplo:**
`ENTRYPOINT ["nginx", "-g", "daemon off;"]`
**Características clave:**

- Es más rígido que `CMD`. Incluso si pasas argumentos adicionales a `docker run`, se ejecutará el programa definido en `ENTRYPOINT` con esos argumentos.
- Puede combinarse con `CMD` para proporcionar argumentos predeterminados: