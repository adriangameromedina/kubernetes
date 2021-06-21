# Kubernetes
Aplicación Django con base de datos Postgres, ejecutada en un clúster de kubernetes. (Google Cloud)

## 1. Crear clúster en Google Cloud.

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
