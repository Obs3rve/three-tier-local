# Three-tier-local
This project involves building and deploying a three-tier application to a Minikube cluster, simulating a real-world multi-environment setup.


The goal of this read me is to explain the stepsa in a way it can be replicated as it's aimed at people with little to no knowledge. I'll also provide tutorials and guides at each point.

Prerequisiete 
Docker - https://docs.docker.com/get-started/introduction/get-docker-desktop/
Minikube - https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fbinary+download
Docker Hub Account - https://hub.docker.com/

Project 1: Deploying to Minikube

   

1. Build and Containerize Your Application

To achieve this, I used a simple three-tier app (frontend, backend, database) provided by docker - https://docs.docker.com/get-started/introduction/develop-with-containers/. The dockerfile is also already written to containerize the app.

##What the setup contains
React frontend - a Node container that's running the React dev server, using Vite.
Node backend - the backend provides an API that provides the ability to retrieve, create, and delete to-do items.
MySQL database - a database to store the list of the items.
phpMyAdmin - a web-based interface to interact with the database that is accessible at http://db.localhost.
Traefik proxy - Traefik is an application proxy that routes requests to the right service. It sends all requests for localhost/api/* to the backend, requests for localhost/* to the frontend, and then requests for db.localhost to phpMyAdmin. This provides the ability to access all applications using port 80 (instead of different ports for each service).


All files can also be found here in this repo - git clone https://github.com/Obs3rve/three-tier-local.git

Simply use this command to clone/download the files - git clone https://github.com/docker/getting-started-todo-app
Use docker-compose to ensure all the services connect - docker compose watch
*(Psss you need to be in the same folder to run docker-compose. If you are not, use this command before docker compose "cd getting-started-todo-app"). 

Once done you should see the status
![Screenshot 2024-09-25 at 1 33 56 am](https://github.com/user-attachments/assets/0a8d3d70-b37c-4e7b-97a6-ae4cc9d3f197)


##Containerize the app
In the section we will build the image and push it to dockerhub.

First, go to your dockerhub account and create a new repository.
![Screenshot 2024-09-25 at 1 54 09 am](https://github.com/user-attachments/assets/ce453f7f-ef5b-4d0c-bb72-06acd105b46c)


The next step would be to build Image
docker build -t <DOCKER_USERNAME>/todoapp .
(psss the full stop is important :))
![Screenshot 2024-09-25 at 2 06 32 am](https://github.com/user-attachments/assets/70b93c85-9658-417f-bc3d-72b09b84d02b)

Our image is built. To confirm run the command "docker image ls"

you can now push it to dockerhub.
docker push <DOCKER_USERNAME>/getting-started-todo-app
![Screenshot 2024-09-25 at 2 10 21 am](https://github.com/user-attachments/assets/30d4bf7c-0cce-4856-a439-70edfab91a44)


We have successfully built and pushed our image to dockerhub

The next step would be to deploy our app to Kubernetes. For the local section of this guide, we will be using Minikube which is a lite version of Kubernetes.


2. Set Up Minikube

To install Minikube please follow this guide 

https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fbinary+download


#I'll continue tomorrow 


3. Deploy to Minikube

Deploy your containerized services to the minikube cluster.
Use Kubernetes manifests to define your deployments, services, ConfigMaps, and Secrets.
4. Set Up GitHub Actions CI/CD

Automate your deployment with GitHub Actions to push changes to different environments (dev, staging, prod) based on your branch.
Create pipelines for building, testing, and deploying your application.
