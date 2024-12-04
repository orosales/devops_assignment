## Multi-Container Docker Application with CI/CD: Calculator App Project

#### Complete Project Instructions: [DevOps Foundations Course/Project](https://github.com/shiftkey-labs/DevOps-Foundations-Course/tree/master/Project)

#### Submission by - Omar Rosales

### Project Overview

- **Brief project description:** What is the purpose of your application?

This project is a practical case study using the knowledge gained from the DevOps Course. The objectives are:
    - Create a Docker image for a backend application developed in Python.
    - Create a Docker image for a frontend application developed in React.
    - Set up a GitHub workflow to publish the images to Docker Hub.
    - Use Docker Compose for local deployment.

- **Which files are you implmenting? and why?:**

    - backend/Dockerfile ->  Creates the Docker image for the backend in Python.
    - frontend/Dockerfile -> Creates the Docker image for the frontend in React.
    - github/workflows/github-ci.yml -> Defines the pipeline for building and publishing images to Docker Hub.
    - docker-compose.yml -> Configures containers for local deployment.


- _**Any other explanations for personal note taking.**_

Steps in Assigment.txt is a file I created that includes the commands used for creating local images and validating the Dockerfiles.


### Docker Implementation

**Explain your Dockerfiles:**

- **Backend Dockerfile** (Python API):
    - Based on the python:3.9-slim image.
    - /app is the application directory inside the container.
    - Copies the application files into the /app directory.
    - Installs dependencies listed in requirements.txt.
    - Adds the flask-cors library for CORS support.
    - Exposes port 5000 for the API.
    - Run app.py 


- **Frontend Dockerfile** (React App):
    - Based on the node:23.3.0-slim image.
    - /app is the application directory inside the container.
    - Copies package.json and package-lock.json to /app.
    - Installs dependencies using npm install.
    - Copies the public and src folders to /app.
    - Builds the application with npm run build.
    - Uses the build output as input for an Nginx container.
    - Copies React build files to Nginx's default directory.
    - Configures Nginx to listen on port 3000 instead of the default port 80.
    - Runs Nginx.


**Use this section to document your choices and steps for building the Docker images.**


### Docker Compose YAML Configuration

**Break down your `docker-compose.yml` file:**

- **Services:** 
  backend ->  Python API.
  frontend -> React App.
- **Networking:** Configured with the app-network bridge type.
- **Volumes:** No volumes are used.
- **Environment Variables:** 
  FrontEnd
  REACT_APP_BACKEND_URL -> Specifies the backend URL for the frontend.
- Command to start the local environment:: docker-compose up -d


**Use this section to explain how your services interact and are configured within `docker-compose.yml`.**

    - The backend runs on port 5000, and the frontend runs on port 3000. Both use the app-network for communication.


### CI/CD Pipeline (YAML Configuration)

**Explain your CI/CD pipeline:**

- Trigger: 
    - The pipeline runs on push and pull_request events.
- Stages: 
    - Build Docker images.
    - Test Docker images.
    - Push Docker images to Docker Hub.
- Steps for pushing images to Docker Hub:
    - Log into Docker Hub using credentials stored as GitHub secrets (secrets.DOCKER_USERNAME & secrets.DOCKER_PASSWORD).
    - Build the backend Docker image.
    - Test the backend Docker image using curl to verify the API.
    - Stop the backend container.
    - Push the backend image to Docker Hub.
    - Build the frontend Docker image.
    - Test the frontend Docker image using curl to verify the application.
    - Stop the frontend container.
    - Push the frontend image to Docker Hub.

**Use this section to document your automated build and deployment process.**

    - Log into Docker Hub using credentials stored as GitHub secrets (secrets.DOCKER_USERNAME & secrets.DOCKER_PASSWORD).
    - Build the backend Docker image.
    - Test the backend Docker image using curl to verify the API.
    - Stop the backend container.
    - Push the backend image to Docker Hub.
    - Build the frontend Docker image.
    - Test the frontend Docker image using curl to verify the application.
    - Stop the frontend container.
    - Push the frontend image to Docker Hub.


### Assumptions

- List any assumptions you made while creating the Dockerfiles, `docker-compose.yml`, or CI/CD pipeline. 
    - The frontend runs on port 3000.
    - The backend runs on port 5000.


### Lessons Learned

- What challenges did you encounter while working with Docker and CI/CD?
    - Pushing images to Docker Hub without exposing credentials.
    - Resolving frontend container issues during local deployment. Configuring Nginx helped resolve these issues.
- What did you learn about containerization and automation?
    - Improved understanding of Docker and Docker Compose.
    - Learned how to work with GitHub Actions for CI/CD automation.

**Use this section to reflect on your experience and learnings when implementing this project.**

    - This project served as a template for personal projects, including those in Java. In the future, I aim to deploy containers to the cloud to complete the CI/CD process.



### Future Improvements

- How could you improve your Dockerfiles, `docker-compose.yml`, or CI/CD pipeline? 
    - Add stages in the CI/CD pipeline for deploying containers to the cloud.
- (Optional-Just for personal reflection) Are there any additional functionalities you would like to consider for the calculator application to crate more stages in the CI/CD pipeline or add additional configuration in the Dockerfiles?
    - Explore using Java for similar projects.


**Use this section to brainstorm ways to enhance your project.**

- Deploy the application to a server for complete continuous deployment.
- Use other technology like Java could be interesting as well.

<!-- BEST OF LUCK! -->
