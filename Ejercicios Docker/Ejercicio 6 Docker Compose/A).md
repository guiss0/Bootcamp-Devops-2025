¿Qué estructura básica debería tener un archivo "docker-compose.yml"?

```YML
version: "3.8" # Especifica la versión del esquema de Compose (recomendado usar la última estable)

services: 
  nombre_del_servicio_1: # Nombre del servicio (e.g., web, db, redis)
    image: nombre_de_la_imagen:tag # Imagen de Docker (puedes usar imágenes públicas o propias)
    ports: # Mapeo de puertos (host:contenedor)
      - "puerto_host:puerto_contenedor"
    environment: # Variables de entorno
      - VARIABLE1=valor1
      - VARIABLE2=valor2
    volumes: # Montaje de volúmenes
      - ruta_host:/ruta_contenedor
    networks: # Red personalizada
      - nombre_de_la_red
    depends_on: # Dependencias entre servicios
      - nombre_del_servicio_2

  nombre_del_servicio_2:
    image: otra_imagen:tag
    volumes:
      - otro_volumen:/otra_ruta
    environment:
      - DATABASE_USER=usuario
      - DATABASE_PASSWORD=contraseña
    networks:
      - nombre_de_la_red

networks: # Definición de redes
  nombre_de_la_red:
    driver: bridge # El tipo de red, por defecto es 'bridge'

volumes: # Definición de volúmenes
  nombre_del_volumen:
```
