 ¿Cómo podrías detener y eliminar un contenedor en ejecución? ¿Es posible hacer esto en un solo comando? 

``` bash
docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)
```
en docker ps -a -q, se podria poner solo los contenedores especificos si se quisiera, pero el comando ayuda a que sea mas facil borrando todo en este ejemplo

