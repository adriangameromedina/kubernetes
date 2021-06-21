# Kubernetes


## 1. Crear clúster en google cloud.

## 2. Kubernetes en nuestra máquina y vincular nuestra cuenta, proyecto y cluster de google cloud.

```
gcloud auth login
gcloud config set project [PROJECT_ID]
gcloud container clusters get-credentials [CLUSTER_NAME] --zone=[ZONE]
```
