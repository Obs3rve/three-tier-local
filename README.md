# Getting Started Todo App

This project involves building and deploying a three-tier application(todo list application from Docker) to a Minikube cluster, simulating a real-world multi-environment setup.


## Purpose of This README
The goal of this README is to explain the steps to replicate this project, particularly for those who might have little to no knowledge of the subject. I’ll provide tutorials and guides along the way.

### Prerequisites
Before we jump into the project, make sure you have the following installed on your machine:

1. **Docker**: You can get started here: [Get Docker Desktop](https://docs.docker.com/get-started/introduction/get-docker-desktop/).
2. **Minikube**: Install it from this guide: [Minikube Start](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fbinary+download).
3. **Docker Hub Account**: Sign up here: [Docker Hub](https://hub.docker.com/).

---

## Project 1: Deploying to Minikube

### 1. Build and Containerize Your Application

For this step, we’ll use a three-tier app (frontend, backend, and database) provided by Docker. Check out the official Docker documentation for a quick start: [Develop with Containers](https://docs.docker.com/get-started/introduction/develop-with-containers/). The Dockerfile is already written to containerize the app.

#### What’s in Our Setup?
- **React Frontend**: A Node container running the React development server, using Vite.
- **Node Backend**: Provides an API to retrieve, create, and delete to-do items.
- **MySQL Database**: Stores the list of items.
- **phpMyAdmin**: A web-based interface to interact with the database, accessible at [http://db.localhost](http://db.localhost).
- **Traefik Proxy**: Routes requests appropriately, sending requests for `localhost/api/*` to the backend, requests for `localhost/*` to the frontend, and requests for `db.localhost` to phpMyAdmin, allowing access through port 80.

All files can be found in this repository: 
```bash
git clone https://github.com/Obs3rve/three-tier-local.git
```

Use the following command to clone/download the files:
```bash
git clone https://github.com/docker/getting-started-todo-app
```

To ensure all services connect, run:
```bash
docker compose watch
```
*(Psst! You need to be in the same folder to run `docker-compose`. If you are not, use this command before running Docker Compose: `cd getting-started-todo-app`).*

Once you execute the above command, you should see the status:
![Screenshot 2024-09-25 at 1 33 56 am](https://github.com/user-attachments/assets/0a8d3d70-b37c-4e7b-97a6-ae4cc9d3f197)

### 2. Containerize the App
Now, we will build our image and push it to Docker Hub.

1. **Create a New Repository**: First, go to your Docker Hub account and create a new repository. 
   ![Screenshot 2024-09-25 at 1 54 09 am](https://github.com/user-attachments/assets/ce453f7f-ef5b-4d0c-bb72-06acd105b46c)

2. **Build the Image**: Use the following command:
   ```bash
   docker build -t <DOCKER_USERNAME>/todoapp .
   ```
   *(Psst! The full stop is important.)*
   ![Screenshot 2024-09-25 at 2 06 32 am](https://github.com/user-attachments/assets/70b93c85-9658-417f-bc3d-72b09b84d02b)

3. **Check Your Image**: Run the following command to confirm everything went smoothly:
   ```bash
   docker image ls
   ```

4. **Push it to Docker Hub**: Once confirmed, push it to Docker Hub using:
   ```bash
   docker push <DOCKER_USERNAME>/getting-started-todo-app
   ```
   ![Screenshot 2024-09-25 at 2 10 21 am](https://github.com/user-attachments/assets/30d4bf7c-0cce-4856-a439-70edfab91a44)

You have successfully built and pushed your image to Docker Hub.

### 3. Set Up Minikube
Now that we’re set with our image, it’s time to deploy our app to Kubernetes. For the local section of this guide, we’ll be using Minikube. If you haven’t installed Minikube yet, follow this guide: [Minikube Start](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Fx86-64%2Fstable%2Fbinary+download).

---

### I’ll continue tomorrow.
Stay tuned for more details on the deployment process!

--- 

```
