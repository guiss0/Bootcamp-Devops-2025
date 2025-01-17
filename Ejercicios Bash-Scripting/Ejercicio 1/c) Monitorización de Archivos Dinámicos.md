ver las ultimas 20 lineas agregadas
cat syslog | tail -20 

y ver en tiempo real
watch -n 1 "cat syslog"



-- -- 
VARIANTES 


`sudo tail -f /var/log/syslog`

- **`-f`**: "Follow" permite observar las nuevas líneas que se agregan al archivo en tiempo real.
- **`/var/log/syslog`**: Es el archivo que estás monitoreando.


- -- ---

### Ver las últimas 20 líneas y observar en tiempo real

Puedes combinar ambos comandos para ver las últimas 20 líneas y luego continuar observando en tiempo real:

bash

Copiar código

`sudo tail -n 20 -f /var/log/syslog`

- **`-n 20`**: Muestra las últimas 20 líneas iniciales.
-- --

