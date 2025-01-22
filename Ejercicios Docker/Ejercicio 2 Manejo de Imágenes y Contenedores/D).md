Armar un script para listar las imágenes disponibles en el sistema ordenadas por peso de mayor a menor. En el resultado debe estar el peso de la imagen y el nombre de la imagen con el tag.

``` bash
#!/bin/bash

echo -e "[!] Listando las imagenes del sistema"

echo -e "[!] NOMBRE, TAG Y PESO DE LA IMAGEN;"
docker images | sort -k6 | awk {'print $1, $2,$7'} | grep -v "TAG"

```