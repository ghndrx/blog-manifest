Ghost Blog on Kubernetes
This repository contains the configuration files necessary to deploy a Ghost blog on Kubernetes using a MySQL backend and an nginx-proxy for routing traffic.

Prerequisites
A running Kubernetes cluster
The kubectl command-line tool installed on your local machine
Deployment

kubectl apply -f namespace.yaml
kubectl apply -f blog-config-map.yaml

kubectl apply -f deployments/ghost-blog-deployment.yaml
kubectl apply -f deployments/mysql-deployment.yaml
kubectl apply -f deployments/nginx-proxy-deployment.yaml
kubectl apply -f services/ghost-blog-service.yaml
kubectl apply -f services/ingress-service.yaml
kubectl apply -f services/mysql-service.yaml
kubectl apply -f services/nginx-proxy-service.yaml

kubectl apply -f volumes/nginx-pv.yaml
kubectl apply -f volumes/nginx-pvc.yaml
kubectl apply -f volumes/mysql-pv.yaml
kubectl apply -f volumes/mysql-pvc.yaml
kubectl apply -f volumes/blog-pv.yaml
kubectl apply -f volumes/blog-pvc.yaml

This will create the necessary resources in the cluster, including a deployment for the Ghost app, a service for connecting to the MySQL server, and an ingress service for routing traffic to the Ghost app via the nginx-proxy with https and http.

Volumes
This configuration is using a Persistent Volume to store the Ghost blog data, this can be done by creating a persistent volume and persistent volume claim, and then referencing it in the ghost-blog-deployment.yaml file.

ingress-service.yaml
In this example, $(VAR_HOST) and $(SECRET_NAME) are variables that are stored in a configMap and a Secret, respectively. These variables can be managed and updated separately from the YAML files, making it easier to update and maintain your configuration.

To use variables in your YAML files, you'll first need to create a configMap and a Secret that contains the variables you need. You can do this using the kubectl