# infra-ci-cd-automation
End-to-end Infrastructure, CI/CD & DevOps Automation Platform

This project is a complete DevOps automation stack designed to provision infrastructure, deploy containerized applications, implement CI/CD, enable code quality scanning, manage artifacts, and support cloud-native workloads on Kubernetes.
It includes Terraform, Docker, Jenkins, Maven, SonarQube, Nexus, Kubernetes manifests, and Monitoring/Logging stacks.

🚀 Project Overview

This repository demonstrates a full DevOps workflow:

🔹 Infrastructure as Code (IaC)

Provision and manage AWS resources using Terraform:

VPC, Subnets, NAT Gateways

Application Load Balancer

Auto Scaling Groups

RDS Database

Route53 DNS

Security Groups

SNS for notifications

🔹 CI/CD Automation

Automated pipeline using Jenkins:

Build Java application with Maven

Run unit tests

Perform static code analysis with SonarQube

Build Docker image

Push image to registry (Nexus or DockerHub)

Deploy to Kubernetes (EKS / Kind / Kubeadm)

🔹 Containerization & Deployment

Full Docker and Docker-Compose support:

Application Dockerfiles

Local development via Compose

Automated startup scripts

🔹 Kubernetes Orchestration

Deploy workloads on:

EKS

Self-hosted clusters (Kubeadm / Kind)

Includes:

Deployments

Services

Ingress

NFS storage

Monitoring components

🔹 Monitoring & Logging Stack

Includes templates for:

Prometheus

Elasticsearch

Logging storage classes

Metrics and logging dashboards

📁 Repository Structure
├── compose.yml
├── Dockerfile
├── Jenkinsfile
├── package-management
│   ├── CICD
│   │   ├── jenkins/ (install scripts, config)
│   │   ├── maven/ (setup scripts)
│   │   ├── nexus/ (deployment scripts)
│   │   └── sonarqube/ (setup automation)
│   ├── docker/ (docker setup, compose, Dockerfiles)
│   ├── k8s/
│   │   ├── kubernetes-workload/ (eks, deployments, nfs, etc.)
│   │   └── monitoring/ (logs, metrics)
│   ├── monitoring/ (Elasticsearch configs)
│   └── terraform/
│       └── vpc-projects/ (full AWS infra IaC)
├── src/ (Java application)
├── pom.xml
└── sonar-project.properties

🛠️ Tools & Technologies
DevOps & CI/CD

Jenkins

Maven

SonarQube

Nexus Repository Manager

GitHub

Cloud & IaC

Terraform

AWS (VPC, RDS, ALB, EC2, Route53, EKS, SNS)

Containers

Docker

Docker Compose

Kubernetes

EKS / Kubeadm / Kind

Deployments, Services, Ingress

NFS Persistent Storage

Monitoring & Logging

Prometheus (optional)

Elasticsearch

Storage Classes (PVC/SC)

🧪 CI/CD Pipeline Flow (Jenkins)

Checkout code from GitHub

Build & test Java app via Maven

Run SonarQube analysis

Package application JAR

Build Docker image

Push image to registry

Trigger Kubernetes deployment

Send SNS/Slack notification (optional)

☁️ Terraform Infrastructure Flow

Terraform modules provision:

VPC with public/private subnets

NAT & IGW

Load Balancer

Auto-Scaling Group

RDS (MySQL/PostgreSQL)

Route53 DNS

Security Groups

SNS topic
