# Infra CI/CD Automation

## Project Overview
This project demonstrates a full **Infrastructure as Code (IaC) and CI/CD automation** setup for a sample application (`RgfShop / Fruit Shop`). It includes automated provisioning of cloud infrastructure, containerized services, Kubernetes workloads, CI/CD pipelines, monitoring, and artifact management.

The stack integrates **Terraform, Docker, Jenkins, Maven, Nexus, SonarQube, Kubernetes (EKS / Kind / Kubeadm), Prometheus, Grafana, and ELK stack**, providing an end-to-end DevOps solution.

---

## Features

- **Infrastructure as Code (IaC)**: Automate VPC, subnets, NAT gateways, ALB, ASG, RDS, Route53, and security groups using Terraform.
- **CI/CD Pipelines**: Jenkins pipelines for automated build, test, code quality, and deployment.
- **Containerization**: Dockerized application and services with `docker-compose`.
- **Artifact Management**: Nexus repository to manage built artifacts (JARs, packages).
- **Code Quality & Security**: SonarQube integration for static code analysis.
- **Kubernetes Orchestration**: Deploy applications and MySQL database on EKS, Kind, or Kubeadm clusters.
- **Monitoring & Logging**: Full ELK stack and Prometheus/Grafana setup for observability.

---

## Tools & Technologies

| Component             | Technology / Tool                              |
|-----------------------|-----------------------------------------------|
| Version Control       | Git / GitHub                                  |
| Infrastructure        | Terraform, AWS VPC, ALB, RDS, ASG, Route53   |
| CI/CD                 | Jenkins, GitHub Actions (optional)           |
| Build Tools           | Maven                                         |
| Artifact Repository   | Nexus Repository                              |
| Code Quality          | SonarQube                                     |
| Containerization      | Docker, Docker Compose                        |
| Kubernetes            | EKS / Kind / Kubeadm                           |
| Monitoring & Logging  | Prometheus, Grafana, ELK Stack (Elasticsearch, Logstash, Kibana) |
| Programming Language  | Java / Spring Boot                             |

---

## Project Structure

```text
.
├── compose.yml
├── Dockerfile
├── Jenkinsfile
├── package-management
│   ├── CICD
│   │   ├── jenkins
│   │   ├── maven
│   │   ├── nexus
│   │   └── sonarqube
│   ├── docker
│   │   ├── docker-compose
│   │   └── Dockerfile
│   ├── k8s
│   │   ├── kubernetes-workload
│   │   └── monitoring
│   └── terraform
│       └── vpc-projects
├── pom.xml
├── src
│   ├── main/java/com/example/rgfshop
│   └── resources/static
├── target
└── README.md

Setup Instructions
Prerequisites

Java JDK 17+

Docker & Docker Compose

Terraform

AWS CLI configured

Kubernetes cluster (EKS, Kind, or Kubeadm)

Git installed

Steps

Clone the repository

git clone https://github.com/19sparkz/infra-ci-cd-automation.git
cd infra-ci-cd-automation


Provision infrastructure (Terraform)

cd package-management/terraform/vpc-projects
terraform init
terraform plan
terraform apply


Build Docker images

docker build -t rgfshop-app .
docker-compose -f package-management/docker/docker-compose/compose.yml up -d


Setup Jenkins & CI/CD

cd package-management/CICD/jenkins
bash Jenkins-ubuntuinstallation.sh
bash jenkins.sh


Configure pipeline via Jenkinsfile.

Deploy to Kubernetes

cd package-management/k8s/kubernetes-workload/fruitapp-deployment
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml


Monitoring & Logging

Apply Prometheus, Grafana, and ELK manifests from package-management/k8s/monitoring.

CI/CD Pipeline Overview
Source Code -> Git -> Jenkins -> Build (Maven) -> Test -> SonarQube Analysis
 -> Package -> Push to Nexus -> Deploy to Kubernetes -> Monitor via Prometheus/Grafana

Architecture Diagram
                       +-----------------+
                       |   GitHub Repo    |
                       +--------+--------+
                                |
                                v
                         +-------------+
                         |   Jenkins   |
                         +------+------+  
                                |
             +------------------+------------------+
             v                                     v
      +------------+                       +----------------+
      |   Maven    |                       |  SonarQube     |
      +------------+                       +----------------+
             |
             v
      +------------+
      |   Nexus    |
      +------------+
             |
             v
      +----------------+
      | Kubernetes /   |
      |  Dockerized    |
      |   Services     |
      +----------------+
             |
   +---------+---------+
   v                   v
Prometheus/Grafana   ELK Stack (Logs)
(Monitoring)          (Observability)

Notes

Use .tfvars in Terraform to configure environment-specific variables.

Docker images can be tagged with Git commit hash for traceability.

SonarQube quality gates prevent bad code from being deployed.

Prometheus & Grafana dashboards provide metrics and alerts.


























































































