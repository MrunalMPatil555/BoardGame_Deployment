**Board Game CI/CD Pipeline**



This repository demonstrates a complete CI/CD pipeline implementation for a Board Game application. The project includes application source code, containerization, automated build pipelines, and deployment configuration.



The repository also contains a detailed PDF guide explaining the entire CI/CD process step-by-step with screenshots.



**Repository Contents**
This repository contains the following components:



1\. Source Code
The src/ directory contains the source code of the Board Game application.



2\. Jenkins Pipeline
The Jenkinsfile defines the CI/CD pipeline stages used to automate the build and deployment process.
Typical pipeline stages include:
* Code checkout from Git repository
* Build process
* Docker image creation
* Image push to container registry
* Deployment to the target environment



3\. Dockerfile
The Dockerfile is used to containerize the Board Game application.
It defines the base image, application dependencies, and instructions required to build the Docker image.



4\. Deployment Configuration
The deployment file contains the configuration used to deploy the application to the target platform.



5\. CI/CD Documentation
A PDF document is included in this repository which explains the entire CI/CD workflow in detail.
The document contains:
* Complete pipeline architecture
* Step-by-step setup instructions
* Configuration details
* Screenshots of each stage of the process
* CI/CD Workflow Overview



**Technologies Used**



* Jenkins
* Docker
* Git
* CI/CD Pipelines
* Containerized Application Deployment

