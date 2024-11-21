```
Overview
This pipeline automates the process of building Docker images for the backend and frontend applications, pushing these images to Amazon Elastic Container Registry (ECR), and deploying the updated applications to an EC2 instance when changes are pushed to the main branch.

Workflow Trigger
Event: Push to the main branch in the GitHub repository.
Branches Monitored: main.
Pipeline Workflow
Build Docker Images

Build separate Docker images for the backend and frontend applications using their respective Dockerfiles.
Tag the Docker images with a version number or latest.
Push Docker Images to ECR

Authenticate to ECR using AWS CLI.
Push the backend and frontend Docker images to their respective repositories in ECR.
Deploy to EC2

SSH into the EC2 instance.
Pull the latest Docker images from ECR.
Stop existing containers and run updated ones.
