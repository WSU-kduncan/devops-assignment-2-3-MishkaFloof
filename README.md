# Devops Assignment 2 - GitHub Actions & DockerHub

[Assignment Description](https://github.com/pattonsgirl/CS3900-AppSoftwareDev/blob/main/DevOps/Assignment2/Assignment2.md)

[Edit this file with your assignment documentation deliverables](build-pipeline.md)

Changelog:
- emptied `workorderpro` service folder into parent folder
- Dockerfile in parent repo
    - simplified taskings, focuses on apps primary needs.
    - Do not build with Dockerfile in `.devcontainer` - that Dockerfile will only be referenced in VSCode Open as DevContainer context
- Added `gradlew` script to parent repo
- `build.gradle` moved to partent folder

## **actionsWorkflow.yml**

### Workflow Summary

This GitHub Actions workflow automates the process of building and pushing a Docker image of the WorkOrder Pro Spring application to DockerHub. The workflow is triggered on any commit pushed to the main branch and performs the following tasks:

1. Build Job:
    * **Checkout Code**: The workflow first checks out the code from the repository.
    * **Java Setup**: Installs Java (Temurin 17 distribution) to build the application.
    * **Gradle Build**: Executes the ./gradlew build command to compile the application into a JAR file.
    * **Prepare JAR for Docker**: Renames the JAR file as app.jar for consistency and accessibility in the next job.
    * **Upload Artifacts**: The JAR file and Dockerfile are uploaded as artifacts to be shared with the next job.
2. Build and Push Docker Image Job:
    * **Download Artifacts**: Retrieves the JAR file and Dockerfile from the previous job.
    * **Set up Docker Buildx**: Prepares the Docker CLI with Buildx for enhanced compatibility.
    * **Docker Login**: Logs into DockerHub using secure secrets (DOCKERHUB_USERNAME and DOCKERHUB_TOKEN).
    * **Build and Push Docker Image**: Builds a Docker image from the JAR file and Dockerfile, tags it with the unique commit SHA for tracking, and pushes it to the DockerHub repository.

### Links
DockerHub Repository: [sutton-wopro-service](https://hub.docker.com/repository/docker/mishkafloof/sutton-wopro-service/general) 


Workflow Action Run Results Summary: [GitHub Actions](https://github.com/WSU-kduncan/devops-assignment-2-3-MishkaFloof/actions)
