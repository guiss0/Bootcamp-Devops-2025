sed -i '316{H;d};519G' dockerScript.sh


### **Explicación:**

1. **`316{H;d}`**:
    
    - En la línea 316:
        - **`H`**: Guarda la línea 316 en el buffer de retención.
        - **`d`**: Elimina la línea 316 temporalmente.
2. **`519G`**:
    
    - En la línea 519:
        - **`G`**: Inserta el contenido del buffer de retención (línea 316) después de la línea 519.
3. Esto no modifica el archivo original, solo muestra el resultado. Para sobrescribir el archivo:

