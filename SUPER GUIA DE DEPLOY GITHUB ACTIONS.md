------------------

Una breve introduccion a lo que necesitaremos setear para poder seguir adelante esto.

1. Precisaremos crear un runner de actions en nuestra maquina local, para eso tendremos que ir a la configuracion de nuestro repositorio y hacer algo asi: 
   
   Settings > Code and automation > Actions > Runners 
   
   Ahi tendremos un boton que dira "New self-hosted runner"
   
   Aqui es muy facil, solo elegimos el sistema operativo en el cual queremos correr el runner y ejecutamos los comandos que nos da, en mi caso utilice linux. 
   
``` Bash
# Create a folder
$ mkdir actions-runner && cd actions-runner
# Download the latest runner package
$ curl -o actions-runner-linux-x64-2.322.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.322.0/actions-runner-linux-x64-2.322.0.tar.gz
# Optional: Validate the hash
$ echo "$HASH_QUE_SE_GENERA"  actions-runner-linux-x64-2.322.0.tar.gz" | shasum -a 256 -c
# Extract the installer
$ tar xzf ./actions-runner-linux-x64-2.322.0.tar.gz


# Create the runner and start the configuration experience  
$ ./config.sh --url $TU_REPOSITORIO --token $TOKEN_GENERADO

# Last step, run it!  
$ ./run.sh
```

2. Luego de eso, generamos una pipeline en actions, para ir tendremos que ir a donde dice Actions en la barra de arriba del repositorio, cerca de Settings. 
   
   Generamos un workflow manual y creamos algo asi; 
   
``` BASH
name: Build, Push and Deploy to Kubernetes

on:
  push:
    branches: [main]

env:
  IMAGE_NAME: html-app
  REGISTRY: ${{ secrets.DOCKER_USERNAME }}

jobs:
  build-push-deploy:
    runs-on: self-hosted  # Especificamos que debe usar el runner local

    steps:
      - name: Login to Docker Hub
        run: |
           echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
              
      - name: Build and Push Docker Image
        run: |
          docker build -t $REGISTRY/$IMAGE_NAME:latest .
          docker push $REGISTRY/$IMAGE_NAME:latest
          
      - name: Setup kubectl and deploy
        run: |
          echo "$KUBE_CONFIG_DATA" | base64 -d > kubeconfig
          export KUBECONFIG=$PWD/kubeconfig
          kubectl version --client
          
      - name: Deploy to Kubernetes
        run: |
          cat deploy-html-app.yaml
          kubectl apply -f deploy-html-app.yaml
```

Estas son las instrucciones que seguira nuestro runner al momento de que hagamos un push en nuestro repo. 

Luego de esto, tendremos que setear los siguientes secrets para que nuestra pipeline funcione correctamente. 


###### Secrets a generar: 

###### DOCKER_USERNAME
Nuestro username de Docker
###### DOCKER_PASSWORD 
Es un token generado una vez iniciada la sesion en Docker
 https://app.docker.com/settings/personal-access-tokens
###### KUBE_CONFIG_DATA 
Esto es nuestro kubeconfig, dependiendo del cluster que usemos es donde lo tendremos, en mi caso uso k3s, y para verlo es algo asi 
``` BASH
cat /etc/rancher/k3s/k3s.yaml | base64 -w 0
```

Lo pasamos a base64 para que sea mejor de manipular y ademas le agrega seguridad.
Esto nos dara nuestro KUBE_CONFIG_DATA que setearemos para acceder al cluster de kubernetes desde el runner
###### DOCKER_REGISTRY_SECRET 
Esta no se en la pipeline, pero es del deployment de kubernetes, lo seteamos asi;

``` BASH
 kubectl create secret docker-registry docker-registry-secret \
   --docker-server=https://index.docker.io/v1/ \
   --docker-username=docker_username \
   --docker-password=tu_token_generado_en_docker\
   --docker-email=tu_email
```

Eso lo corremos localmente y para verlo utilizamos el siguiente comando 

``` bash
kubectl get secret docker-registry-secret -o yaml 
```

Lo copiamos y lo pegamos en el secret.


Los secrets se acceden mediante:
Settings > Secrets and Variables > Actions 

Y una vez ahi, creamos con "New repository secret" y generamos los secrets anteriores mencionados.

3. Una vez seteado el runner y los secrets, nos queda colocar los archivos para hacer el deploy, en este caso es un Dockerfile, index.html y el Deploy de kubernetes. 
   
   (Copien los de este repositorio y cambien la imagen del deploy) 
   
    guiss0/html-app:latest  -- Sera esta la que aparece, la cambiamos por el nombre de la build que generemos con el docker build mas nuestro usuario de Docker, podriamos manejarlo como secret, pero en este caso no lo hice debido a que preferia hardcodearlo para mostrarlo mucho mejor. 


Y una vez tengamos todo esto seteado, cada push que le hagamos al repositorio, este correra esta pipeline, ademas cada cambio que le hagamos al index.html , lo reflejara generando una nueva imagen, haciendo que este este constantemente actualizado. 