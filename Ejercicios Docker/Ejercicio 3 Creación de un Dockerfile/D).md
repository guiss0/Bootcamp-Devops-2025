 ¿Cuál es la diferencia entre COPY y ADD?

`COPY`
 - Copia archivos del directorio host al contenedor directamente

`ADD`
- Es lo mismo que el COPY pero mas versatil, permitiendo copiar achivos de internet, directamente de URL's, si hay zips los descomprime al pasarlos al contenedor. 


Si los archivos no son zips, tar, o los tenes en tu directorio local, es mejor usar COPY. ADD, se usaria en casos donde el archivo sea un zip,tar o esten en internet, para evitar posibles problemas.