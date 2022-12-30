# Docker Container

# Creating a Dockerfile for Node.JS 

## Create a Dockerfile within directory 

    // downloading base image
    FROM node:16-alpine 
    
    //create working directory within Docker Container
    WORKDIR /app 

    //copy package.json into that workdir in Container
    COPY package.json ./ 

    // install dependencies
    RUN npm install 

    // copy rest of files into Docker Container
    COPY ./ ./ 

    // define starting command
    CMD ["npm", "start"] 

## Create .dockeringnore

Create a .dockeringore and add node_modules into the file

# Docker commands in terminal

### Build image based on dockerfile in current directory with tag [my docker name]/[name of service]

    docker build -t internadine/posts .

### Create a start a container based on provided image id or tag

    docker run internadine/posts

### Create and start container, but also override default command (e.g. run shell)

    docker run -it internadine/posts sh 

### Print out information about all running containers

    docker ps 

### Execute given comman in running container

    docker exec -it internadine/posts sh

### Print out logs from given container

    docker logs internadine/posts

## Types of Services (=> Objects)

* Cluster IP = Set up easy to remember URL to access a pod. Only exposes pods in the cluster.
* Load Balancer = Makes a pod accessible from outside the cluster. 
* Node Port = Makes a pod accessible from outside the cluster. Usually only used for dev purposes. 