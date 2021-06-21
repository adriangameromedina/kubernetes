# Kubernetes
Aplicación Django con base de datos Postgres, ejecutada en un clúster de kubernetes. (Google Cloud)

## 1. Crear clúster en Google Cloud.
En nuestra cuenta de google cloud, buscamos el servicio de Kubernetes Engine y creamos un nuevo clúster. En este caso sirve con el Estándar y en el margen derecho nos aparece la opción de mi primer cluster. Creamos ese tipo por defecto y no modificamos nada o el nombre si lo vemos necesario.

## 2. Kubernetes en nuestra máquina y vincular nuestra cuenta, proyecto y cluster de google cloud.
### 2.1 Instalar kubernetes (Ubuntu)
```
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

### 2.2 Establecer cuenta de gcloud, proyecto y cluster.
Si no se tiene instalado gcloud se instala como:
```
sudo snap install google.cloud-sdk --classic
```
Se continua con las siguientes 3 líneas para autenticarnos, seleccionar el proyecto y el clúster
```
gcloud auth login
gcloud config set project [PROJECT_ID]
gcloud container clusters get-credentials [CLUSTER_NAME] --zone=[ZONE]
```

### 2.3 Crear reglas firewall en GoogleCloud
Es necesario crear reglas de firewall para permitir el puerto 8000 en este caso que es el que usa la aplicación. Para ello en GoogleCloud en el menú navegamos a Red de VPC, en sus distintas secciones se selecciona firewall y ahí creamos una nueva regla. Indicamos Rango de IP 0.0.0.0/0, protocolos y puertos tcp:8000-8001, lo asignamos a la red default y lo aplicamos a todas las instancia de la red para este caso. Lo mejor sería solo asignarlo al clúster de kubernetes en este caso.

## 3. Ejecución
Tenemos los ficheros correspondientes al deployment y el servicio de la base de datos de Postgres (db) y otro para la aplicación Django (result). Para su ejecución se usa el comando 
```kubectl apply -f .```

## 4. Escalado 
Para realizar el escalado de nuestra aplicación se le puede asignar el numero de replicas al deployment en concreto que queramos con el siguiente comando:
```kubectl scale [DEPLOYMENT_NAME] --replicas=[NUMBER OF REPLICAS]```
