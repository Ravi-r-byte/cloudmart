# CloudMart — E-Commerce Platform on AWS

A production-grade e-commerce web application deployed on AWS using 
Kubernetes and a fully automated CI/CD pipeline.

## Live Architecture

GitHub → CodePipeline → CodeBuild → Amazon ECR → Amazon EKS → CloudMart Live

## Tech Stack

### Frontend
- React + Vite + Tailwind CSS
- Dockerized container

### AWS Infrastructure
- Amazon EKS (Kubernetes v1.34) — Container orchestration
- Amazon ECR — Docker image registry
- AWS CodePipeline — CI/CD automation
- AWS CodeBuild — Build and Deploy stages
- Amazon VPC — Networking
- IAM — Security and permissions

## CI/CD Pipeline Flow

1. Developer pushes code to GitHub main branch
2. CodePipeline auto-triggers
3. CodeBuild (Build stage):
   - Builds Docker image
   - Pushes image to Amazon ECR
4. CodeBuild (Deploy stage):
   - Installs kubectl
   - Connects to EKS cluster
   - Runs kubectl apply → deploys to Kubernetes
5. CloudMart is live on EKS

## Project Structure

cloudmart/
├── src/                        # React frontend source code
├── Dockerfile                  # Container build instructions
├── cloudmart-frontend.yaml     # Kubernetes deployment manifest
├── buildspec-build.yml         # CodeBuild build stage instructions
├── buildspec-deploy.yml        # CodeBuild deploy stage instructions
└── README.md                   # Project documentation

## AWS Resources

| Service         | Resource                        |
|-----------------|---------------------------------|
| EKS Cluster     | cloudmart-v2 (ap-south-1)       |
| ECR Frontend    | cloudmart-frontend              |
| ECR Backend     | cloudmart-backend               |
| CodePipeline    | cloudmart-cicd-pipeline         |
| CodeBuild Build | cloudmartbuild                  |
| CodeBuild Deploy| cloudmartDeployToProduction     |
| Node Group      | standard-workers (t3.medium)    |

## Problems Solved

| Problem                              | Solution                          |
|--------------------------------------|-----------------------------------|
| CodePipeline missing IAM permissions | Added inline policy for CodeBuild |
| kubectl not found in CodeBuild       | Added install commands to buildspec|
| Wrong Kubernetes manifest path       | Fixed path to cloudmart-frontend.yaml |
| BatchGetBuilds permission missing    | Updated IAM inline policy         |

## What I Learned

- Containerizing a React app with Docker
- Pushing Docker images to Amazon ECR
- Creating and managing an EKS Kubernetes cluster
- Writing Kubernetes deployment manifests
- Building a full CI/CD pipeline with CodePipeline + CodeBuild
- Debugging IAM permission errors in AWS
- Connecting CodePipeline to GitHub via AWS CodeConnections
- Deploying to Kubernetes using kubectl in a CI/CD pipeline

## Author

Ravi — Cloud & DevOps Engineer
GitHub: Ravi-r-byte
