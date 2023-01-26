Ghost Blog on Kubernetes
This repository contains the configuration files necessary to deploy a Ghost blog on Kubernetes using a MySQL backend and an nginx-proxy for routing traffic.

Prerequisites
A running Kubernetes cluster
The kubectl command-line tool installed on your local machine
Deployment
To deploy the Ghost blog, run the following commands:

Copy code
kubectl apply -f namespace.yaml 
kubectl apply -f ghost-blog-deployment.yaml
kubectl apply -f ghost-blog-service.yaml
kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml
kubectl apply -f ingress-service.yaml
This will create the necessary resources in the cluster, including a deployment for the Ghost app, a service for connecting to the MySQL server, and an ingress service for routing traffic to the Ghost app via the nginx-proxy with https and http.

Volumes
This configuration is using a Persistent Volume to store the Ghost blog data, this can be done by creating a persistent volume and persistent volume claim, and then referencing it in the ghost-blog-deployment.yaml file.

# ingress-service.yaml
In this example, $(VAR_HOST) and $(SECRET_NAME) are variables that are stored in a configMap and a Secret, respectively. These variables can be managed and updated separately from the YAML files, making it easier to update and maintain your configuration.

To use variables in your YAML files, you'll first need to create a configMap and a Secret that contains the variables you need. You can do this using the kubectl command-line tool.

For configMap, you can create it with the following command:

Copy code
kubectl create configmap my-config-map --from-literal=VAR_HOST=example.com
And for Secret:

Copy code
kubectl create secret generic my-secret --from-literal=SECRET_NAME=mysecret
Once you've created the configMap and Secret, you can reference them in your YAML files using the $(VAR_NAME) syntax.

You can also manage and update the variables in the configMap and Secret using kubectl commands.

It's important to note that configMap and Secret are not the only way to use variables in Kubernetes, you can also use other tools like Helm or Kustomize.

# 