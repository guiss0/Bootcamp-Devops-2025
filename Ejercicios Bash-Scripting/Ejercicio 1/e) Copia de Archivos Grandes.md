cp -r --force $(find -type f -size +4k) ~/pruebaBootcamp1  

- cp -r --force: Copia todos los archivos de manera recursiva creando subdirectorios en caso de dentro de la carpeta seleccionada y el --force es para forzarlo en caso de que algo moleste de por medio
- $(find -type f -size +4k): Esto al estar $() es para que tome los argumentos que da ese comando para poder ejecutarlos en el otro, comando, es decir que va a generar una lista de archivos que pesen mas de 4kb y se lo pase al cp, evitando asi escribir archivo por archivo.

<PRUEBABOOTCAMP1 SERIA LA CARPETA A DONDE MANDARLO>