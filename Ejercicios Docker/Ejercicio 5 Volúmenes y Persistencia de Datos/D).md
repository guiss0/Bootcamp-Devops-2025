¿Es posible eliminar todos aquellos volúmenes creados que no se estén ocupando?

Sí, Docker permite eliminar los volúmenes que no están asociados a ningún contenedor utilizando el siguiente comando:
``` bash
docker volume prune
```

Este comando pedirá confirmación antes de eliminar los volúmenes no utilizados. Para forzar la operación sin confirmación, agrega el flag -f

``` bash
docker volume prune -f
```