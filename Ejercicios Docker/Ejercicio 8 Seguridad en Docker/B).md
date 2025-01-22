¿Qué parámetros usarías para limitar el uso de CPU y memoria de un contenedor?

``` bash
docker run --cpus="1.5" <contenedor> 
# Define la cantidad de nucleos del CPU

docker run --memory="512m" my-container
# Limita el uso de la memoria 

docker run --cpus="1.5" --memory="512m" --memory-swap="1g" my-container
# Limitar ambos recursos


--cpus="1.5" # Limita el CPU
--memory="512m" # Limita la memoria que el conetenedor puede usar
--memory-swap="1g" # Limita la ram del contenedor a 1GB


```


