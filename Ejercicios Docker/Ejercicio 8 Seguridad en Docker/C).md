Investiga y menciona al menos dos prácticas recomendadas para mejorar la seguridad en Docker.

## 1. Establecer un usuario no root en el contenedor 

``` bash
docker run -u 4000 alpine
```


``` dockerfile
FROM alpine
RUN groupadd -r myuser && useradd -r -g myuser myuser
#    <HERE DO WHAT YOU HAVE TO DO AS A ROOT USER LIKE INSTALLING PACKAGES ETC.>
USER myuser
```


###  2. Ejecutar Docker en modo no root
https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html#rule-11-run-docker-in-rootless-mode

### 3.Minimizar las capacidades del contenedor**

- **Descripción:** Reduce los privilegios del contenedor deshabilitando capacidades innecesarias y asegurándote de que no pueda realizar tareas sensibles.
- **Acciones específicas:**
    - Usa el parámetro `--cap-drop` para eliminar capacidades innecesarias.
    - Habilita solo las capacidades estrictamente necesarias con `--cap-add`.
`docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE imagen`


### 4. Usar redes personalizadas y seguras**

- **Descripción:** Los contenedores que comparten la misma red tienen comunicación directa. Usar redes personalizadas permite segmentar y aislar el tráfico.
- **Acciones específicas:**
    - Crea redes específicas para diferentes servicios con el driver adecuado (`bridge` o `overlay`).
    - Usa reglas de firewall para filtrar tráfico entre contenedores.

**Comando para crear una red personalizada:**
`docker network create --driver bridge mi-red-segura`
`docker run --network=mi-red-segura imagen`