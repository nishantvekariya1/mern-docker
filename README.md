# Building and Deploying a Dockerized User Profile App

## Introduction
Docker is a powerful tool that simplifies the process of packaging, distributing, and running applications. In this guide, we'll walk through building and deploying a user profile app using Docker. By containerizing our app's components, we'll make it portable, scalable, and easy to deploy.

## Prerequisites
- Basic understanding of Docker and Docker Compose.
- Node.js installed.
- Familiarity with MongoDB.

## Setting Up with Docker
Let's start by setting up our environment using Docker. We'll need to create a Docker network for our containers to communicate effectively.

### Step 1: Create Docker Network
Create a Docker network named `mongo-network`.

docker network create mongo-network

### Step 2: Start MongoDB
Run MongoDB container with authentication enabled.

docker run -d -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=password \
    --name mongodb \
    --net mongo-network \
    mongo

### Step 3: Start Mongo Express
Launch Mongo Express to manage MongoDB through a web interface.

docker run -d -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
    --net mongo-network \
    --name mongo-express \
    -e ME_CONFIG_MONGODB_SERVER=mongodb \
    mongo-express

### Step 4: Open Mongo Express
Visit http://localhost:8081 in your browser to access Mongo Express.

### Step 5: Create User-Account Database
Using Mongo Express, create a database named "user-account" and a collection named "users".

### Step 6: Start Node.js Application Locally
Navigate to the app directory, install dependencies, and start the Node.js server.
cd app
npm install
node server.js

### Step 7: Access the Application UI
Open http://localhost:3000 in your browser to interact with the app.

## Using Docker Compose
Alternatively, Docker Compose simplifies managing multi-container applications.

### Step 1: Start MongoDB and Mongo Express
Start MongoDB and Mongo Express containers using Docker Compose.

docker-compose up

### Step 2: Create Database and Collection
Access Mongo Express at http://localhost:8080 to create a database and collection.

### Step 3: Start Node Server
Navigate to the app directory, install dependencies, and start the Node.js server.

cd app
npm install
node server.js

### Step 4: Access the Application
Visit http://localhost:3000 to use the application.

## Building and Deploying the Docker Image
Once the app is ready, build and push it to a Docker repository for deployment.

### Step 1: Build Docker Image
Build the Docker image for the app.

docker build -t (docker hub repo name) .

### Step 2: Push to Repository
Log in to Docker Hub and push the image to a repository.

docker login
docker push <repository_name>

## Conclusion
Dockerizing our user profile app streamlines development and deployment. It offers portability and scalability, allowing us to focus on building great applications. Experiment with Docker and unleash the full potential of containerized apps in your projects.

## Blog Link
[Blog Link](https://medium.com/@vekariyanishant1/building-and-deploying-a-dockerized-user-profile-app-ea21588ddc8b)
