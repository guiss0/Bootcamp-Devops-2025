
comm -23 <(seq 1 254 | awk '{print "192.168.88." $1}' | sort -u) <(cat archivo.conf | grep host | awk '{print $7}' | tr -d ';}' | sort -u)



1. **`sort -u`**:
    
    - Al aplicar `sort -u` a ambas listas (las IPs generadas y las extraídas de `archivo.conf`), nos aseguramos de que las IPs estén ordenadas y sin duplicados.
    - Esto evitará que se repitan las IPs en ambas listas antes de compararlas.
2. **`comm -23`**:
    
    - Compara las dos listas ordenadas y muestra solo las IPs que están en el rango `192.168.88.1` a `192.168.88.254` pero no en `archivo.conf`.
3. **Flujo de trabajo**:
    
    - **`seq 1 254 | awk '{print "192.168.88." $1}'`**: Genera las IPs del rango `192.168.88.1` a `192.168.88.254`.
    - **`cat archivo.conf | grep host | awk '{print $7}' | tr -d ';}'`**: Extrae las IPs del archivo `archivo.conf`, eliminando los caracteres `;` y `}`.
    - **`sort -u`**: Elimina las IPs duplicadas en ambas listas.
    - **`comm -23`**: Compara las listas y muestra las IPs que están en el rango, pero no en `archivo.conf`.
