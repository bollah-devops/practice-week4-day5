# Week 4 Day 5 - Jenkins Pipeline to AWS EKS

## What this project does
A complete CI/CD pipeline that automatically builds a Docker image and
deploys it to AWS EKS using Helm, triggered by a git push. No manual
kubectl or helm commands needed after the initial setup.

## Pipeline stages
1. Checkout - pulls code from GitHub
2. Build and push - builds Docker image and pushes to Docker Hub
3. Deploy to EKS staging - helm upgrade --install to staging namespace
4. Deploy to EKS production - helm upgrade --install to production namespace

## Tech stack
- Jenkins - CI/CD automation
- Docker - containerization
- AWS EKS - managed Kubernetes
- Helm - Kubernetes package management
- eksctl - EKS cluster provisioning

## How to run

Step 1 - Create EKS cluster

    eksctl create cluster \
      --name week4-eks \
      --region us-east-1 \
      --nodegroup-name standard-workers \
      --node-type t3.medium \
      --nodes 2 \
      --managed

Step 2 - Create namespaces

    kubectl create namespace staging
    kubectl create namespace production

Step 3 - Push code to GitHub to trigger the pipeline automatically

## IMPORTANT - delete the cluster after every session

    eksctl delete cluster --name week4-eks --region us-east-1

## Docker image
tawa123/k8s-practice:latest
