sed -n '10,20p' dockerScript.sh >> dockerScript.sh && sed -i '10,20d' dockerScript.sh 

`sed -n '10,20p' dockerScript.sh >> dockerScript.sh`

- **¿Qué hace?**
    
    - **Extrae las líneas 10 a 20** del archivo `dockerScript.sh`.
    - Las **agrega al final del mismo archivo** utilizando `>>`.
- **Desglose del comando:**
    
    - **`sed -n`**:
        - Activa el modo "silencioso", lo que significa que `sed` no imprime todo el archivo, sino solo lo que se le indica.
    - **`'10,20p'`**:
        - Indica que solo las líneas desde la 10 hasta la 20 deben imprimirse (`p` = print).
    - **`dockerScript.sh`**:
        - Es el archivo de entrada que `sed` lee.
    - **`>> dockerScript.sh`**:
        - Redirige (en modo de anexar) las líneas extraídas al final del archivo `dockerScript.sh`.

---

### **2. Segunda parte:**

bash

Copiar código

`sed -i '10,20d' dockerScript.sh`

- **¿Qué hace?**
    
    - **Elimina las líneas 10 a 20** del archivo original.
- **Desglose del comando:**
    
    - **`-i`**:
        - Modifica el archivo original directamente (in-place).
    - **`'10,20d'`**:
        - Indica que las líneas 10 a 20 deben eliminarse (`d` = delete).
    - **`dockerScript.sh`**:
        - Es el archivo que se está modificando.