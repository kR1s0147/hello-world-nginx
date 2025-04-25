# Hello World Kubernetes Deployment with NGINX and Optional Argo CD Integration
## Overview 
**This Project demonstrates how to deploy a simple *nginx server* in k8 cluster in your local machine using Kind (k8 in docker)**
- *Build a Docker image serving a static HTML page.*

- *Set up a local Kubernetes cluster using Kind.*

- *Deploy the application to the cluster.*

- *Expose the application via a NodePort service.*

**Repositary Structure**
.  
├── app/  
│   └── index.html  
├── docker/  
│   └── Dockerfile  
├── k8s/  
│   ├── deployment.yaml  
│   └── service.yaml  
├── demo/  
│   └── video.mp4  
└── README.md  

## Requirements
- Docker
- kind (kubernets in Docker)
- kubectl (kubernetes client)

## Setting the Environment

**OS - Ubuntu24.04 LTS**

**Installing Requirements**
### Installing Docker  
*Docker is platform independent platform the enables developers to package applications and their dependecies  into standardised units called containers. These containers are lightweight and consistent across different enviroments.*  
  
`sudo apt-get update`  
`sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
  
### Installing kind 
*Kind (Kubernetes in Docker) is used to run local kubernetes clusters as nodes in docker container.*  
  
`curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64`  
`chmod +x ./kind`  
`sudo mv ./kind /usr/local/bin/kind`

## Deploying the Server in local k8 clusters

#### Building docker images
`sudo docker build -t hello-world-nginx .`  
  
#### Verifying the images in the docker
`sudo docker images`

#### Creating K8 clusters in kind   
`sudo kind create cluster --name hello-world`

#### Verifying the clusters
`sudo kind get clusters`

### Manifesting the Containers
#### Applying the Depolyment to container
**Deployment manages the desired state of your application by ensuring that a specified number of pod replicas are running at all times.**  
`sudo kubectl apply -f k8/deployment.yaml`

#### Applying the Service   
**Service Exposes application to other services or external users.**    
`sudo kubectl apply -f k8/service.yaml`

### Application Access 

**We can easily verify that our container is started or not using the following command.It lists all the services**  
`sudo kubectl get svc`

#### Output
`root@kR1s:/home/giridhar/Rust_Projects/hello-world-nginx# kubectl get svc`  
`NAME                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE`  
`hello-world-nginx   NodePort    10.96.131.129   <none>        80:30001/TCP   15s`  
`kubernetes          ClusterIP   10.96.0.1       <none>        443/TCP        73s`  
   
**WE CAN ACCESS THE WEB SERVER USING  https://localhost:30001**  






