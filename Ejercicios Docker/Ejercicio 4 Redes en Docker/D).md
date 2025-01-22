¿Cómo podrías comprobar si dos contenedores en la misma red pueden comunicarse entre sí?


``` bash
docker network ls

# Ver la red a la cual esta conectada el contenedor
docker inspect <nombre del contenedor1> | grep -i Network 
docker inspect <nombre del contenedor2> | grep -i Network 

# Luego de verificar que los contenedores tienen la misma red, puedo ejecutar un ping de un contenedor al otro, en el inspect conseguire la IP asignada de cada uno de los contenedores. 

docker exec -it <nombre de contenedor1> bash 
#Con esto conseguire una shell en el contenedor 1 y ahi ejecuto:

ping <ip del contenedor2>

# Puede hacerse tambien asi; 

docker exec <nombre_del_contenedor_1> ping <ip_o_nombre_del_contenedor_2>


# Fijarse antes de ejecutar estos comandos, que el contenedor los soporte, algunas distro ligeras no aguantan estos comandos.

```