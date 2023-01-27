Ghost Blog on Kubernetes

This repository contains the configuration files necessary to deploy a Ghost blog on Kubernetes using a MySQL backend and an nginx-proxy for routing traffic.

Prerequisites
- A running Kubernetes cluster
- The kubectl command-line tool installed on your local machine

Workloads/Services/Secrets/ConfigMaps

kubectl apply -f namespace.yaml

kubectl apply -f volumes/ghost-blog-pv.yaml
kubectl apply -f volumes/ghost-blog-pvc.yaml
kubectl apply -f volumes/mysql-pv.yaml
kubectl apply -f volumes/mysql-pvc.yaml
kubectl apply -f volumes/nginx-proxy-pv.yaml
kubectl apply -f volumes/nginx-proxy-pvc.yaml

kubectl apply -f deployments/ghost-blog-deployment.yaml
kubectl apply -f deployments/mysql-deployment.yaml
kubectl apply -f deployments/nginx-proxy-deployment.yaml

kubectl apply -f services/ghost-blog-service.yaml
kubectl apply -f services/mysql-service.yaml
kubectl apply -f services/nginx-proxy-service.yaml

kubectl apply -f services/ingress-service.yaml

kubectl apply -f ~/config-map_secrets/ghost-blog-config-map.yaml
kubectl apply -f ~/config-map_secrets/ghost-blog-secrets.yaml
kubectl apply -f ~/config-map_secrets/mysql-config-map.yaml
kubectl apply -f ~/config-map_secrets/mysql-secrets.yaml


gcloud compute disks create --size=50GB --zone='us-central1-c ghost-blog-disk, mysql-disk, nginx-proxy-disk

This will create the necessary resources in the cluster, including a deployment for the Ghost app, a service for connecting to the MySQL server, and an ingress service for routing traffic to the Ghost app via the nginx-proxy with https and http.

Volumes
This configuration is using a Persistent Volume to store the Ghost blog data, this can be done by creating a persistent volume and persistent

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To create a Docker image of Ghost-Blog, you will need the following files:

A Dockerfile which contains the instructions for building the image.
A config.production.json file which contains the configuration settings for your Ghost blog.
The Ghost source files, which can be obtained by downloading the latest version of Ghost from the official website or by cloning the Ghost GitHub repository.
Here's an example of a basic Dockerfile that can be used to build a Ghost image:

bash
Copy code
FROM node:12

ENV NODE_ENV production

RUN mkdir -p /var/www/ghost
WORKDIR /var/www/ghost

COPY . .

RUN npm install --production

CMD ["npm", "start"]
You can build image with command:

perl
Copy code
docker build -t my-ghost-blog .
This command will create an image with the name 'my-ghost-blog' using the files in the current directory.

It is important to note that this is a basic example and you may need to make adjustments to the Dockerfile depending on your specific requirements.

And you also can use ghost official image from docker hub:

Copy code
docker pull ghost:3
and use your config file and custom theme with this command:

javascript
Copy code
docker run -d --name my-ghost-blog -p 2368:2368 -v /path/to/config.production.json:/var/lib/ghost/config.production.json -v /path/to/content:/var/lib/ghost/content ghost:3
This will start a container with the name 'my-ghost-blog', map port 2368 on the host to port 2368 in the container, and mount your config.production.json file and a custom theme to the appropriate locations in the container.