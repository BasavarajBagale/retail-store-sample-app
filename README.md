Retail Store Sample App - GitOps with Amazon EKS Auto Mode

!Banner

<div align="center">

![Stars](https://img.shields.io/github/stars/BasavarajBagale/retail-store-sample-app) !GitHub License

<h2>AWS Containers Retail Sample</h2>

Author: Basavaraj Bagale

</div>

This project demonstrates a modern retail store application deployed on Amazon EKS using Terraform, Docker, Kubernetes, Helm, ArgoCD, and GitHub Actions.

Table of Contents
Overview
Architecture
Prerequisites
Quick Start
Getting Started
Infrastructure Components
GitOps Workflow
CI/CD Pipeline
Monitoring
Cleanup
Troubleshooting
Overview

The Retail Store Sample App is a microservices-based application that provides an online shopping experience.

The application includes:

UI Service: Java-based frontend.
Catalog Service: Go-based product catalog API.
Cart Service: Java-based shopping cart API.
Orders Service: Java-based order management API.
Checkout Service: Node.js-based checkout API.
Application Architecture

!Architecture

Component	Language	Description
UI	Java	Store frontend
Catalog	Go	Product catalog
Cart	Java	Shopping cart
Orders	Java	Order management
Checkout	Node.js	Checkout processing
Infrastructure Architecture

This project uses:

Amazon VPC
Amazon EKS Auto Mode
Amazon EC2
AWS IAM
AWS ECR
Terraform
Docker
Kubernetes
Helm
ArgoCD
NGINX Ingress Controller
Cert Manager
GitHub Actions

!EKS Architecture

Prerequisites

Install the following tools before deployment.

Tool	Version
AWS CLI	v2+
Terraform	1.0+
kubectl	Compatible with EKS
Docker	20.0+
Helm	3.0+
Git	2.0+
VS Code	Latest
Installation Links
AWS CLI
Terraform
kubectl
Docker Desktop
Helm
Git
VS Code
Quick Start
Step 1: Configure AWS CLI

Configure AWS credentials using an IAM identity with the permissions required for this deployment.

bash
aws configure


Verify AWS authentication:

bash
aws sts get-caller-identity

Step 2: Clone Repository
bash
git clone https://github.com/BasavarajBagale/retail-store-sample-app.git


Navigate to the project:

bash
cd retail-store-sample-app

Step 3: Configure Terraform

Navigate to the Terraform directory:

bash
cd terraform


Initialize Terraform:

bash
terraform init


Format Terraform files:

bash
terraform fmt


Validate configuration:

bash
terraform validate


Preview infrastructure:

bash
terraform plan


Deploy infrastructure after reviewing the plan:

bash
terraform apply


Type yes when prompted.

This deployment is expected to provision the infrastructure defined in your Terraform configuration.

Step 4: Configure kubectl

After the EKS cluster is created, configure kubeconfig:

bash
aws eks update-kubeconfig --name retail-store --region ap-south-1


Check cluster connectivity:

bash
kubectl get nodes


Check Kubernetes namespaces:

bash
kubectl get namespaces

Step 5: Verify Application

Check the ingress controller:

bash
kubectl get svc -n ingress-nginx


Check application pods:

bash
kubectl get pods -n retail-store


Check ingress:

bash
kubectl get ingress -n retail-store


Use the ingress load balancer address in your browser.

GitOps Workflow

This project uses GitOps principles to manage Kubernetes application deployment.

ArgoCD continuously monitors the configured Git repository and synchronizes Kubernetes resources.

Main workflow:

Developer updates application code.
Changes are pushed to GitHub.
GitHub Actions builds application images when configured.
Docker images are pushed to Amazon ECR.
ArgoCD synchronizes Kubernetes manifests.
Application is deployed on Amazon EKS.
CI/CD Pipeline

GitHub Actions can automate the following tasks:

Application build.
Docker image creation.
Docker image publishing to Amazon ECR.
Kubernetes deployment updates.
Automated application delivery.
GitHub Actions Secrets

Configure repository secrets under:

GitHub Repository → Settings → Secrets and variables → Actions.

Secret	Description
AWS_ACCESS_KEY_ID	AWS access key
AWS_SECRET_ACCESS_KEY	AWS secret key
AWS_REGION	AWS region
AWS_ACCOUNT_ID	AWS account ID

Prefer GitHub Actions OIDC federation with an IAM role instead of long-lived AWS access keys.

ArgoCD Deployment

Verify ArgoCD pods:

bash
kubectl get pods -n argocd


Get the initial admin password:

bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d


Port-forward ArgoCD:

bash
kubectl port-forward svc/argocd-server -n argocd 8080:443


Open:

https://localhost:8080

Default username:

text
admin


Password: Use the password retrieved from the previous command.

Monitoring and Observability

Check Kubernetes nodes:

bash
kubectl get nodes


Check all pods:

bash
kubectl get pods -A


Check services:

bash
kubectl get svc -A


Check application logs:

bash
kubectl logs -n retail-store <pod-name>


Check ArgoCD applications:

bash
kubectl get applications -n argocd

Cleanup

To remove infrastructure managed by Terraform:

Navigate to the Terraform directory:

bash
cd terraform


Run:

bash
terraform destroy


Review the proposed deletions and confirm.

Important: Check for remaining AWS resources such as ECR repositories, load balancers, and persistent storage. Some resources may require manual cleanup depending on the Terraform configuration.

Troubleshooting
AWS Authentication Issues
bash
aws sts get-caller-identity


Verify that your AWS identity has the required permissions.

Terraform Errors
bash
terraform init -upgrade
terraform validate
terraform plan

Kubernetes Connection Issues
bash
aws eks update-kubeconfig --name retail-store --region ap-south-1
kubectl get nodes

Docker Issues
bash
docker version
docker ps

Helm Issues
bash
helm version
helm list -A

ArgoCD Issues
bash
kubectl get pods -n argocd
kubectl get applications -n argocd

Project Repository

GitHub:

https://github.com/BasavarajBagale/retail-store-sample-app

Technologies Used
AWS
Amazon EKS Auto Mode
Terraform
Docker
Kubernetes
Helm
ArgoCD
GitHub Actions
Git and GitHub
License

This project retains the license and attribution applicable to the original AWS sample application. Refer to the LICENSE file.

<div align="center">

Developed and maintained by Basavaraj Bagale

⭐ If you find this project useful, consider giving it a star!

</div>
