¿Qué mecanismo propone docker para simplificar la conexión entre contenedores sin la necesidad de ocupar las IP de los contenedores?

Docker propone el uso de **nombres de contenedor y DNS interno** para simplificar la conexión entre contenedores sin necesidad de utilizar sus direcciones IP. Este mecanismo se basa en las capacidades de red virtual de Docker y su sistema de resolución de nombres integrado.

### ¿Cómo funciona este mecanismo?

1. **Resolución de nombres mediante DNS interno**:
    
    - Docker incluye un servicio de DNS interno que permite a los contenedores dentro de la misma red comunicarse usando los nombres de los contenedores como si fueran hostnames.
    - Por ejemplo, si tienes un contenedor llamado `web` y otro llamado `db` en la misma red, el contenedor `web` puede comunicarse con `db` simplemente usando `db` como hostname.
2. **Redes personalizadas**:
    
    - Para habilitar este mecanismo, los contenedores deben estar en la misma red Docker. Puedes crear una red personalizada con:
        
        `docker network create my-network`
        
    - Luego, al iniciar los contenedores, los conectas a esa red:
        
  ``` bash 
   docker run --name web --network my-network nginx 
   docker run --name db --network my-network mysql
  ```
 Ahora `web` puede comunicarse con `db` usando su nombre.
3. **Aliases de red**:
    
    - Docker permite definir **alias** para los contenedores dentro de una red, lo que facilita aún más la conexión si necesitas nombres más amigables:
        
        `docker network connect --alias database my-network db`
        
    - Ahora el contenedor `web` puede comunicarse con `db` usando `database` como hostname.
