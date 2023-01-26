Ghost Blog on Kubernetes

This repository contains the configuration files necessary to deploy a Ghost blog on Kubernetes using a MySQL backend and an nginx-proxy for routing traffic.

Prerequisites
- A running Kubernetes cluster
- The kubectl command-line tool installed on your local machine

Workloads/Services/Secrets/ConfigMaps

kubectl apply -f namespace.yaml

kubectl apply -f volumes/traefik-pv.yaml
kubectl apply -f volumes/ghost-blog-pv.yaml
kubectl apply -f volumes/mysql-pv.yaml

kubectl apply -f volumes/mysql-pvc.yaml
kubectl apply -f volumes/traefik-pvc.yaml
kubectl apply -f volumes/ghost-blog-pvc.yaml

kubectl apply -f deployments/ghost-blog-deployment.yaml
kubectl apply -f deployments/mysql-deployment.yaml
kubectl apply -f deployments/traefik-proxy-deployment.yaml

kubectl apply -f services/ghost-blog-service.yaml
kubectl apply -f services/mysql-service.yaml
kubectl apply -f services/traefik-proxy-service.yaml

kubectl apply -f services/LoadBalancer-traefik.yaml

kubectl apply -f ~/config-map_secrets/ghost-blog-config-map.yaml
kubectl apply -f ~/config-map_secrets/ghost-blog-secrets.yaml
kubectl apply -f ~/config-map_secrets/mysql-config-map.yaml
kubectl apply -f ~/config-map_secrets/mysql-secrets.yaml



kubectl apply -f services/ingress-service.yaml

This will create the necessary resources in the cluster, including a deployment for the Ghost app, a service for connecting to the MySQL server, and an ingress service for routing traffic to the Ghost app via the nginx-proxy with https and http.

Volumes
This configuration is using a Persistent Volume to store the Ghost blog data, this can be done by creating a persistent volume and persistent
