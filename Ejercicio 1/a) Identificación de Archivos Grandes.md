ESTO ES EL TOTAL DE TODO LO QUE HAY, LISTA DIRECTORIOS Y ARCHIVOS

``` bash
du -hs * | grep -v '^d'|sort -rh -k1 | head -n 6
```


```bash
du -h 
```
Lista todos los archivos que hay en el directorio y muestra su respectivo tamanio con G,M,K , interepretandolos correctamente 

```bash
sort -rh -k1 
```
Arregla la primera columna haciendo que -r ordene en orden descendente de mayor a menor, el h que interprete las G,M,K y -k1 que sea la primera columna del output dado

``` bash
head -n 6
```
Que muestre solo los primeros 6 resultados, como el primer resultado es el peso actual del directorio, por ende sorteamos por 6 para que muestre los 5 primeros asi evitando que muestre los 5 utilizando el output del directorio actual

--------
LISTA LOS 5 ARCHIVOS MAS GRANDES DE LA CARPETA
```BASH
ls -lhS | grep -v '^d' | head -n 6 | awk '{print $5,$9}'
```
l- **`ls -lhS`**: Lista los archivos y directorios en formato legible, ordenados por tamaño (`-S`).
- **`grep -v '^d'`**: Excluye directorios (solo archivos).
- **`head -n 5`**: Muestra los 5 archivos más grandes.
- awk '{print $5,$9}' : Hace que solo muestre el tama;o y el nombre del archivo
-- --- --

VARIANTES

### Opción 1: Usando `find`, `xargs`, y `ls`

bash

Copiar código

`find . -maxdepth 1 -type f -exec ls -lh {} + | sort -rh -k5 | head -n 5`

- **`find . -maxdepth 1 -type f`**: Encuentra todos los archivos en el directorio actual (sin recursividad).
- **`ls -lh`**: Lista los detalles de cada archivo en formato legible por humanos.
- **`sort -rh -k5`**: Ordena por la columna de tamaño (5ta columna en `ls -lh`).
- **`head -n 5`**: Muestra los 5 archivos más grandes.


¡Entendido! Aquí tienes tres alternativas que **no utilizan `du`** pero logran un resultado similar (listar los 5 archivos o directorios más grandes dentro de un directorio):

---

### Opción 1: Usando `find`, `xargs`, y `ls`

bash

Copiar código

`find . -maxdepth 1 -type f -exec ls -lh {} + | sort -rh -k5 | head -n 5`

- **`find . -maxdepth 1 -type f`**: Encuentra todos los archivos en el directorio actual (sin recursividad).
- **`ls -lh`**: Lista los detalles de cada archivo en formato legible por humanos.
- **`sort -rh -k5`**: Ordena por la columna de tamaño (5ta columna en `ls -lh`).
- **`head -n 5`**: Muestra los 5 archivos más grandes.

---

### Opción 2: Usando `ls` directamente con `sort`

bash

Copiar código

`ls -lhS | grep -v '^d' | head -n 5`

- **`ls -lhS`**: Lista los archivos y directorios en formato legible, ordenados por tamaño (`-S`).
- **`grep -v '^d'`**: Excluye directorios (solo archivos).
- **`head -n 5`**: Muestra los 5 archivos más grandes.

----------
### Opción 3: Usando `find` con `stat` y `sort`

bash

Copiar código

`find . -maxdepth 1 -type f -exec stat --printf="%s %n\n" {} + | sort -rn | head -n 5`

- **`find . -maxdepth 1 -type f`**: Encuentra todos los archivos en el directorio actual.
- **`stat --printf="%s %n\n"`**: Muestra el tamaño en bytes seguido del nombre del archivo.
- **`sort -rn`**: Ordena en orden descendente por tamaño.
- **`head -n 5`**: Muestra los 5 archivos más grandes.