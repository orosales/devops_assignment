## Multi-Container Docker Application with CI/CD: Calculator App Project

#### Complete Project Instructions: [DevOps Foundations Course/Project](https://github.com/shiftkey-labs/DevOps-Foundations-Course/tree/master/Project)

#### Submission by - Omar Rosales

### Project Overview

- **Brief project description:** What is the purpose of your application?

This project consists in a practical case using the knowledge learned in the DevOps Course:
Create an image of a Backend developed in Python
Create an image of a FrontEnd developed in React
Create a GitHub workflow to publish the images in DockerHub
Create a Docker Composer to local deployment

- **Which files are you implmenting? and why?:**

backend/Dockerfile -> Creates the image of the Backend in Pythong
frontend/Dockerfile -> Creates the image of the FrontEnd in React
github/workflows/github-ci.yml -> Creates the Pipelines to Create images in Docker Hub
docker-compose.yml -> Creates containers for my local environment


- _**Any other explanations for personal note taking.**_

Steps in Assigment.txt is a file that I created when you could find commands that I used to create local images and validate that the Dockerfile are right.


### Docker Implementation

**Explain your Dockerfiles:**

- **Backend Dockerfile** (Python API):
    - Image created based on python:3.9-slim
    - /app is my folder of the application in the container
    - Copy the files to the container to the folder /app
    - Install the libraries which are in requirements.txt 
    - I added the library flask-cors to support cors
    - Expose the port 5000 so the API is working in this port by default
    - Run app.py 


- **Frontend Dockerfile** (React App):
    - Image created based on node:23.3.0-slim 
    - /app is my folder of the application in the container
    - Copy the package.json and package-lock.json to the container to the folder /app
    - Install dependencies npm install
    - Copy the public and src folders to the container to the folder /app
    - Build the application with npm run build
    - I use the output of the Image of node as an input for nginx
    - Copy files from the builder of react to default directory of Nginx
    - Modify Nginx configuration to listen on port 3000 instead of 80
    - Run Nginx


**Use this section to document your choices and steps for building the Docker images.**


### Docker Compose YAML Configuration

**Break down your `docker-compose.yml` file:**

- **Services:** 
  backend -> Python App
  frontend -> FrontEnd App
- **Networking:** app-network type bridge
- **Volumes:** I do not use a volume
- **Environment Variables:** 
  FrontEnd
  REACT_APP_BACKEND_URL - URL for the Backend
- Create the local environment by running: docker-compose up -d


**Use this section to explain how your services interact and are configured within `docker-compose.yml`.**

backend runs in the port 5000 and it uses the network app-network
frontend runs in the port 3000 and it uses the network app-network


### CI/CD Pipeline (YAML Configuration)

**Explain your CI/CD pipeline:**

- Trigger the pipeline: push and pull_request 
- The stages are: Build, Test, and Push Docker Images
- To push images in Docker Hub, I do the following steps:
    - Log into Docker Hub - User and Password are secret and are configured in my GitHub (secrets.DOCKER_USERNAME &  secrets.DOCKER_PASSWORD)
    - Build BackEnd Docker Image
    - Test BackEnd Docker image by using curl to test the API
    - Stop the BackEnd container
    - Push the Backend Docker Image to Docker Hub
    - Build FrontEnd Docker Image
    - Test FrontEnd Docker image by using curl to test the API
    - Stop the FrontEnd container
    - Push the FrontEnd Docker Image to Docker Hub

**Use this section to document your automated build and deployment process.**

    - Log into Docker Hub - User and Password are secret and are configured in my GitHub (secrets.DOCKER_USERNAME &  secrets.DOCKER_PASSWORD)
    - Build BackEnd Docker Image
    - Test BackEnd Docker image by using curl to test the API
    - Stop the BackEnd container
    - Push the Backend Docker Image to Docker Hub
    - Build FrontEnd Docker Image
    - Test FrontEnd Docker image by using curl to test the API
    - Stop the FrontEnd container
    - Push the FrontEnd Docker Image to Docker Hub


### Assumptions

- List any assumptions you made while creating the Dockerfiles, `docker-compose.yml`, or CI/CD pipeline. 


### Lessons Learned

- What challenges did you encounter while working with Docker and CI/CD?
    - Push the image in my Docker Hub without publishing my credentials.
    - When I created the docker-compose, I had some problems when I tried to create the containers based on 
      the Dockerfiles, the container of the frontend had problems to be showed in the right way. The configuration with
      nginx helps me to fix the issue.
- What did you learn about containerization and automation?
    - I put in practice my knowledge about docker, dockercompose
    - I learned how to work with GitHub Actions

**Use this section to reflect on your experience and learnings when implementing this project.**

- I learned to work in this practical case since I guess this is a template for my personal projects in Java
- I would like to have more time to try to deploy the containers on the cloud but this is somethig that I would try in the future.

### Future Improvements

- How could you improve your Dockerfiles, `docker-compose.yml`, or CI/CD pipeline? 
    - Ports could be variables in the Backend and FrontEnd.
- (Optional-Just for personal reflection) Are there any additional functionalities you would like to consider for the calculator application to crate more stages in the CI/CD pipeline or add additional configuration in the Dockerfiles?
    - For the CI/CD I would like to deploy the images in containers on the cloud.

**Use this section to brainstorm ways to enhance your project.**

- The deployment in a server seems to be like a good idea to finish the process of Continuous Deployment
- Use other technology like Java could be interesting as well

<!-- BEST OF LUCK! -->
