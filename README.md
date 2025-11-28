# Infrastructure CI/CD Automation - RgfShop/Fruit Shop

## Project Overview

This project demonstrates a comprehensive **Infrastructure as Code (IaC) and CI/CD automation** setup for a Spring Boot application (RgfShop/Fruit Shop). It provides end-to-end automation from infrastructure provisioning to application deployment, monitoring, and observability.

### Architecture Highlights

- **Multi-tier Infrastructure**: VPC, subnets, load balancers, auto-scaling groups, managed databases
- **Automated CI/CD**: Jenkins-based pipelines with quality gates and artifact management
- **Container Orchestration**: Kubernetes deployment across EKS, Kind, or Kubeadm clusters
- **Full Observability**: Integrated monitoring (Prometheus/Grafana) and logging (ELK Stack)
- **Security & Quality**: SonarQube code analysis, security scanning, artifact versioning

---

## Table of Contents

1. [Features](#features)
2. [Architecture Diagram](#architecture-diagram)
3. [Technology Stack](#technology-stack)
4. [Project Structure](#project-structure)
5. [Prerequisites](#prerequisites)
6. [Quick Start](#quick-start)
7. [Infrastructure Setup](#infrastructure-setup)
8. [CI/CD Pipeline](#cicd-pipeline)
9. [Kubernetes Deployment](#kubernetes-deployment)
10. [Monitoring & Logging](#monitoring--logging)
11. [Configuration Guide](#configuration-guide)
12. [Troubleshooting](#troubleshooting)
13. [Contributing](#contributing)

---

## Features

### Infrastructure Automation
- ✅ **VPC & Networking**: Multi-AZ VPC with public/private subnets, NAT gateways, route tables
- ✅ **Load Balancing**: Application Load Balancer (ALB) with target groups and health checks
- ✅ **Auto Scaling**: ASG with dynamic scaling policies based on CPU/memory metrics
- ✅ **Database**: RDS MySQL with Multi-AZ, automated backups, read replicas
- ✅ **DNS Management**: Route53 hosted zones and record sets
- ✅ **Security**: Security groups, NACLs, IAM roles and policies

### CI/CD Pipeline
- ✅ **Automated Builds**: Maven-based compilation and packaging
- ✅ **Code Quality**: SonarQube static analysis with quality gates
- ✅ **Security Scanning**: Dependency vulnerability checks
- ✅ **Artifact Management**: Nexus repository for versioned artifacts
- ✅ **Automated Testing**: Unit tests, integration tests, smoke tests
- ✅ **Multi-stage Deployment**: Dev → Staging → Production pipelines

### Containerization
- ✅ **Docker Images**: Optimized multi-stage Dockerfile
- ✅ **Docker Compose**: Local development environment with all services
- ✅ **Image Registry**: Private registry integration (ECR/DockerHub)
- ✅ **Image Scanning**: Trivy/Clair vulnerability scanning

### Kubernetes Orchestration
- ✅ **Cluster Management**: Support for EKS, Kind, Kubeadm
- ✅ **Workload Deployment**: Deployments, StatefulSets, DaemonSets
- ✅ **Service Discovery**: ClusterIP, NodePort, LoadBalancer services
- ✅ **Configuration**: ConfigMaps and Secrets management
- ✅ **Persistence**: PersistentVolumes for stateful applications
- ✅ **Ingress**: NGINX Ingress Controller with TLS

### Monitoring & Observability
- ✅ **Metrics**: Prometheus for metrics collection and alerting
- ✅ **Visualization**: Grafana dashboards for infrastructure and application metrics
- ✅ **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana) for centralized logs
- ✅ **Tracing**: Distributed tracing integration ready
- ✅ **Alerting**: Alert rules for critical infrastructure and application events

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                          AWS Cloud (VPC)                         │
│                                                                   │
│  ┌──────────────┐         ┌──────────────┐                      │
│  │ Public Subnet│         │ Public Subnet│                      │
│  │   AZ-1       │         │   AZ-2       │                      │
│  │              │         │              │                      │
│  │  ┌────────┐  │         │  ┌────────┐  │                      │
│  │  │  ALB   │◄─┼─────────┼─►│  ALB   │  │                      │
│  │  └───┬────┘  │         │  └───┬────┘  │                      │
│  └──────┼───────┘         └──────┼───────┘                      │
│         │                        │                               │
│  ┌──────▼───────┐         ┌──────▼───────┐                      │
│  │Private Subnet│         │Private Subnet│                      │
│  │   AZ-1       │         │   AZ-2       │                      │
│  │              │         │              │                      │
│  │ ┌──────────┐ │         │ ┌──────────┐ │                      │
│  │ │   ASG    │ │         │ │   ASG    │ │                      │
│  │ │ EC2/K8s  │ │         │ │ EC2/K8s  │ │                      │
│  │ └────┬─────┘ │         │ └────┬─────┘ │                      │
│  └──────┼───────┘         └──────┼───────┘                      │
│         │                        │                               │
│  ┌──────▼─────────────────────────▼───────┐                     │
│  │        RDS MySQL (Multi-AZ)             │                     │
│  └─────────────────────────────────────────┘                     │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
                              │
                    ┌─────────▼──────────┐
                    │    CI/CD Layer     │
                    │                    │
                    │  ┌──────────────┐  │
                    │  │   Jenkins    │  │
                    │  ├──────────────┤  │
                    │  │   SonarQube  │  │
                    │  ├──────────────┤  │
                    │  │    Nexus     │  │
                    │  └──────────────┘  │
                    └────────────────────┘
                              │
                    ┌─────────▼──────────┐
                    │  Monitoring Layer  │
                    │                    │
                    │  ┌──────────────┐  │
                    │  │  Prometheus  │  │
                    │  ├──────────────┤  │
                    │  │   Grafana    │  │
                    │  ├──────────────┤  │
                    │  │  ELK Stack   │  │
                    │  └──────────────┘  │
                    └────────────────────┘
```

---

## Technology Stack

| Component | Technology | Version | Purpose |
|-----------|-----------|---------|---------|
| **IaC** | Terraform | 1.6+ | Infrastructure provisioning |
| **Cloud Provider** | AWS | - | Cloud infrastructure |
| **Version Control** | Git/GitHub | - | Source code management |
| **CI/CD** | Jenkins | 2.400+ | Continuous integration/deployment |
| **Build Tool** | Maven | 3.8+ | Java project build automation |
| **Language** | Java/Spring Boot | 17/3.x | Application development |
| **Artifact Repository** | Nexus | 3.x | Artifact management |
| **Code Quality** | SonarQube | 9.x+ | Static code analysis |
| **Containerization** | Docker | 24+ | Container runtime |
| **Orchestration** | Docker Compose | 2.x | Local multi-container setup |
| **Kubernetes** | EKS/Kind/Kubeadm | 1.28+ | Container orchestration |
| **Monitoring** | Prometheus | 2.45+ | Metrics collection |
| **Visualization** | Grafana | 10.x | Metrics dashboards |
| **Logging** | ELK Stack | 8.x | Centralized logging |
| **Database** | MySQL | 8.0 | Application database |

---

## Project Structure

```
.
├── compose.yml                      # Docker Compose for local development
├── Dockerfile                       # Multi-stage Docker build
├── Jenkinsfile                      # Jenkins pipeline definition
├── pom.xml                          # Maven project configuration
│
├── package-management/
│   ├── CICD/
│   │   ├── jenkins/
│   │   │   ├── jenkins-setup.sh    # Jenkins installation script
│   │   │   ├── plugins.txt          # Required Jenkins plugins
│   │   │   └── pipeline-configs/    # Pipeline configurations
│   │   ├── maven/
│   │   │   ├── settings.xml         # Maven settings (Nexus integration)
│   │   │   └── pom-templates/       # POM templates
│   │   ├── nexus/
│   │   │   ├── nexus-setup.sh       # Nexus installation
│   │   │   └── repository-config/   # Repository configurations
│   │   └── sonarqube/
│   │       ├── sonar-setup.sh       # SonarQube installation
│   │       └── quality-profiles/    # Quality profiles & rules
│   │
│   ├── docker/
│   │   ├── docker-compose/
│   │   │   ├── dev/                 # Development environment
│   │   │   ├── staging/             # Staging environment
│   │   │   └── production/          # Production setup
│   │   └── Dockerfile/
│   │       ├── app.Dockerfile       # Application container
│   │       └── nginx.Dockerfile     # NGINX reverse proxy
│   │
│   ├── k8s/
│   │   ├── kubernetes-workload/
│   │   │   ├── deployment.yaml      # Application deployment
│   │   │   ├── service.yaml         # Kubernetes services
│   │   │   ├── ingress.yaml         # Ingress rules
│   │   │   ├── configmap.yaml       # Configuration data
│   │   │   ├── secrets.yaml         # Sensitive data
│   │   │   ├── mysql/               # MySQL StatefulSet
│   │   │   └── hpa.yaml             # Horizontal Pod Autoscaler
│   │   └── monitoring/
│   │       ├── prometheus/          # Prometheus configs
│   │       ├── grafana/             # Grafana dashboards
│   │       └── elk/                 # ELK Stack manifests
│   │
│   └── terraform/
│       └── vpc-projects/
│           ├── main.tf              # Main Terraform config
│           ├── variables.tf         # Input variables
│           ├── outputs.tf           # Output values
│           ├── providers.tf         # Provider configuration
│           ├── modules/
│           │   ├── vpc/             # VPC module
│           │   ├── alb/             # Load balancer module
│           │   ├── asg/             # Auto scaling module
│           │   ├── rds/             # Database module
│           │   ├── route53/         # DNS module
│           │   └── security/        # Security groups module
│           └── environments/
│               ├── dev/             # Development environment
│               ├── staging/         # Staging environment
│               └── production/      # Production environment
│
├── src/
│   ├── main/
│   │   ├── java/com/example/rgfshop/
│   │   │   ├── RgfShopApplication.java
│   │   │   ├── controller/
│   │   │   ├── service/
│   │   │   ├── repository/
│   │   │   ├── model/
│   │   │   └── config/
│   │   └── resources/
│   │       ├── application.yml      # Application configuration
│   │       ├── application-dev.yml
│   │       ├── application-prod.yml
│   │       └── static/              # Frontend assets
│   └── test/
│       └── java/com/example/rgfshop/
│
├── scripts/
│   ├── setup.sh                     # One-click setup script
│   ├── deploy.sh                    # Deployment automation
│   ├── backup.sh                    # Backup utilities
│   └── cleanup.sh                   # Resource cleanup
│
├── docs/
│   ├── ARCHITECTURE.md              # Architecture documentation
│   ├── DEPLOYMENT.md                # Deployment guide
│   ├── MONITORING.md                # Monitoring setup guide
│   └── API.md                       # API documentation
│
└── README.md                        # This file
```

---

## Prerequisites

### Required Software

1. **AWS Account** with appropriate IAM permissions
2. **Terraform** >= 1.6.0
3. **Docker** >= 24.0
4. **Docker Compose** >= 2.0
5. **kubectl** >= 1.28
6. **Java JDK** >= 17
7. **Maven** >= 3.8
8. **Git** >= 2.30

### AWS IAM Permissions

Your AWS user/role needs permissions for:
- VPC, Subnets, Internet Gateway, NAT Gateway
- EC2, Auto Scaling Groups, Launch Templates
- RDS (MySQL), Security Groups
- Application Load Balancer, Target Groups
- Route53 (if using DNS)
- EKS (if using managed Kubernetes)
- ECR (for Docker image registry)
- IAM roles and policies

### Local Environment Setup

```bash
# Install Terraform
wget https://releases.hashicorp.com/terraform/1.6.6/terraform_1.6.6_linux_amd64.zip
unzip terraform_1.6.6_linux_amd64.zip
sudo mv terraform /usr/local/bin/

# Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER

# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Verify installations
terraform --version
kubectl version --client
docker --version
docker-compose --version
```

---

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/infra-cicd-automation.git
cd infra-cicd-automation
```

### 2. Configure AWS Credentials

```bash
aws configure
# Enter your AWS Access Key ID, Secret Access Key, Region, and Output format
```

### 3. Run Local Development Environment

```bash
# Start all services with Docker Compose
docker-compose up -d

# Access services:
# - Application: http://localhost:8080
# - Jenkins: http://localhost:8081
# - SonarQube: http://localhost:9000
# - Nexus: http://localhost:8082
# - Grafana: http://localhost:3000
```

### 4. Deploy Infrastructure

```bash
cd package-management/terraform/vpc-projects

# Initialize Terraform
terraform init

# Review the plan
terraform plan

# Apply infrastructure
terraform apply -auto-approve
```

### 5. Deploy to Kubernetes

```bash
cd package-management/k8s/kubernetes-workload

# Apply Kubernetes manifests
kubectl apply -f configmap.yaml
kubectl apply -f secrets.yaml
kubectl apply -f mysql/
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml

# Check deployment status
kubectl get pods
kubectl get svc
kubectl get ingress
```

---

## Infrastructure Setup

### Terraform Configuration

1. **Configure Variables**

Create `terraform.tfvars`:

```hcl
# General
project_name = "rgfshop"
environment  = "production"
aws_region   = "us-east-1"

# VPC Configuration
vpc_cidr = "10.0.0.0/16"
availability_zones = ["us-east-1a", "us-east-1b"]
public_subnet_cidrs  = ["10.0.1.0/24", "10.0.2.0/24"]
private_subnet_cidrs = ["10.0.10.0/24", "10.0.11.0/24"]

# RDS Configuration
db_instance_class    = "db.t3.medium"
db_allocated_storage = 100
db_engine_version    = "8.0"
db_name              = "rgfshop"
db_username          = "admin"

# ASG Configuration
instance_type     = "t3.medium"
min_size          = 2
max_size          = 10
desired_capacity  = 2

# Tags
tags = {
  Project     = "RgfShop"
  Environment = "Production"
  ManagedBy   = "Terraform"
}
```

2. **Initialize and Deploy**

```bash
cd package-management/terraform/vpc-projects/environments/production

# Initialize
terraform init

# Validate configuration
terraform validate

# Plan deployment
terraform plan -out=tfplan

# Apply
terraform apply tfplan

# View outputs
terraform output
```

3. **Terraform Modules**

Each module is self-contained and reusable:

```bash
# VPC Module
terraform/vpc-projects/modules/vpc/
├── main.tf          # VPC, subnets, IGW, NAT
├── variables.tf     # Input variables
└── outputs.tf       # VPC ID, subnet IDs, etc.

# ALB Module
terraform/vpc-projects/modules/alb/
├── main.tf          # ALB, target groups, listeners
├── variables.tf
└── outputs.tf       # ALB DNS, ARN

# RDS Module
terraform/vpc-projects/modules/rds/
├── main.tf          # RDS instance, parameter group
├── variables.tf
└── outputs.tf       # DB endpoint, connection string
```

---

## CI/CD Pipeline

### Jenkins Pipeline Stages

The `Jenkinsfile` defines a multi-stage pipeline:

```groovy
pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/yourusername/rgfshop.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        
        stage('Publish to Nexus') {
            steps {
                sh 'mvn deploy -DskipTests'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t rgfshop:${BUILD_NUMBER} .'
                sh 'docker tag rgfshop:${BUILD_NUMBER} rgfshop:latest'
            }
        }
        
        stage('Push to Registry') {
            steps {
                sh 'docker push your-registry/rgfshop:${BUILD_NUMBER}'
                sh 'docker push your-registry/rgfshop:latest'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/rgfshop rgfshop=your-registry/rgfshop:${BUILD_NUMBER}'
                sh 'kubectl rollout status deployment/rgfshop'
            }
        }
    }
    
    post {
        success {
            slackSend color: 'good', message: "Build ${BUILD_NUMBER} succeeded"
        }
        failure {
            slackSend color: 'danger', message: "Build ${BUILD_NUMBER} failed"
        }
    }
}
```

### Pipeline Setup

1. **Install Jenkins Plugins**

```bash
# Navigate to Jenkins plugin directory
cd package-management/CICD/jenkins

# Install plugins
cat plugins.txt | xargs -I {} jenkins-cli install-plugin {}
```

Required plugins:
- Git plugin
- Maven Integration
- Docker Pipeline
- Kubernetes CLI
- SonarQube Scanner
- Nexus Artifact Uploader

2. **Configure Jenkins Credentials**

- AWS credentials for deployment
- Docker registry credentials
- Kubernetes cluster config
- SonarQube token
- Nexus credentials

3. **Create Pipeline Job**

- New Item → Pipeline
- Configure SCM → Git
- Pipeline script from SCM
- Point to Jenkinsfile

---

## Kubernetes Deployment

### Cluster Setup Options

#### Option 1: Amazon EKS

```bash
# Create EKS cluster
eksctl create cluster \
  --name rgfshop-cluster \
  --region us-east-1 \
  --nodegroup-name standard-workers \
  --node-type t3.medium \
  --nodes 3 \
  --nodes-min 2 \
  --nodes-max 5 \
  --managed

# Configure kubectl
aws eks update-kubeconfig --region us-east-1 --name rgfshop-cluster
```

#### Option 2: Kind (Local Development)

```bash
# Create Kind cluster
kind create cluster --name rgfshop --config package-management/k8s/kind-config.yaml

# Verify
kubectl cluster-info --context kind-rgfshop
```

#### Option 3: Kubeadm (Self-managed)

```bash
# Initialize master node
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

# Setup kubectl for user
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Install network plugin (Calico)
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

# Join worker nodes
kubeadm join <master-ip>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

### Deploy Application

```bash
cd package-management/k8s/kubernetes-workload

# Create namespace
kubectl create namespace rgfshop

# Apply configurations
kubectl apply -f configmap.yaml -n rgfshop
kubectl apply -f secrets.yaml -n rgfshop

# Deploy MySQL
kubectl apply -f mysql/ -n rgfshop

# Wait for MySQL to be ready
kubectl wait --for=condition=ready pod -l app=mysql -n rgfshop --timeout=300s

# Deploy application
kubectl apply -f deployment.yaml -n rgfshop
kubectl apply -f service.yaml -n rgfshop
kubectl apply -f ingress.yaml -n rgfshop

# Enable autoscaling
kubectl apply -f hpa.yaml -n rgfshop

# Check status
kubectl get all -n rgfshop
```

### Access Application

```bash
# Port forward (local testing)
kubectl port-forward -n rgfshop svc/rgfshop 8080:80

# Get LoadBalancer IP (cloud)
kubectl get svc -n rgfshop rgfshop -o jsonpath='{.status.loadBalancer.ingress[0].ip}'

# Get Ingress URL
kubectl get ingress -n rgfshop
```

---

## Monitoring & Logging

### Prometheus Setup

```bash
cd package-management/k8s/monitoring/prometheus

# Install Prometheus
kubectl apply -f namespace.yaml
kubectl apply -f prometheus-config.yaml
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f prometheus-service.yaml

# Access Prometheus UI
kubectl port-forward -n monitoring svc/prometheus 9090:9090
# Open http://localhost:9090
```

### Grafana Setup

```bash
cd package-management/k8s/monitoring/grafana

# Install Grafana
kubectl apply -f grafana-deployment.yaml
kubectl apply -f grafana-service.yaml

# Get admin password
kubectl get secret -n monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode

# Access Grafana
kubectl port-forward -n monitoring svc/grafana 3000:3000
# Open http://localhost:3000
```

**Import Dashboards:**
- Node Exporter Dashboard (ID: 1860)
- Kubernetes Cluster Monitoring (ID: 7249)
- Spring Boot Dashboard (ID: 12900)

### ELK Stack Setup

```bash
cd package-management/k8s/monitoring/elk

# Deploy Elasticsearch
kubectl apply -f elasticsearch-deployment.yaml
kubectl apply -f elasticsearch-service.yaml

# Deploy Logstash
kubectl apply -f logstash-config.yaml
kubectl apply -f logstash-deployment.yaml

# Deploy Kibana
kubectl apply -f kibana-deployment.yaml
kubectl apply -f kibana-service.yaml

# Access Kibana
kubectl port-forward -n monitoring svc/kibana 5601:5601
# Open http://localhost:5601
```

---

## Configuration Guide

### Environment Variables

Create `.env` files for each environment:

```bash
# .env.dev
SPRING_PROFILES_ACTIVE=dev
DB_HOST=localhost
DB_PORT=3306
DB_NAME=rgfshop_dev
DB_USERNAME=dev_user
DB_PASSWORD=dev_password
NEXUS_URL=http://localhost:8082
SONAR_URL=http://localhost:9000

# .env.prod
SPRING_PROFILES_ACTIVE=production
DB_HOST=prod-rds-endpoint.amazonaws.com
DB_PORT=3306
DB_NAME=rgfshop
DB_USERNAME=admin
DB_PASSWORD=${DB_PASSWORD}  # Use secrets management
NEXUS_URL=https://nexus.yourdomain.com
SONAR_URL=https://sonar.yourdomain.com
```

### Application Configuration

`src/main/resources/application.yml`:

```yaml
spring:
  application:
    name: rgfshop
  datasource:
    url: jdbc:mysql://${DB_HOST}:${DB_PORT}/${DB_NAME}
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
  
management:
  endpoints:
    web:
      exposure:
        include: health,metrics,prometheus
  metrics:
    export:
      prometheus:
        enabled: true

logging:
  level:
    root: INFO
    com.example.rgfshop: DEBUG
```

---

## Troubleshooting

### Common Issues

**Issue: Terraform state lock**
```bash
# Force unlock (use carefully)
terraform force-unlock <LOCK_ID>
```

**Issue: Pod stuck in Pending**
```bash
# Check events
kubectl describe pod <pod-name> -n rgfshop

# Check resources
kubectl top nodes
kubectl top pods -n rgfshop
```

**Issue: Image pull errors**
```bash
# Check secret
kubectl get secret -n rgfshop

# Create registry secret
kubectl create secret docker-registry regcred \
  --docker-server=your-registry \
  --docker-username=your-username \
  --docker-password=your-password \
  -n rgfshop
```

**Issue: Database connection failures**
```bash
# Test from pod
kubectl exec -it <app-pod> -n rgfshop -- mysql -h <db-host> -u <user> -p

# Check security groups (AWS)
# Ensure port 3306 is open between app and RDS
```

### Logs and Debugging

```bash
# Application logs
kubectl logs -f <pod-name> -n rgfshop

# Previous container logs
kubectl logs <pod-name> -n rgfshop --previous

# Multiple containers
kubectl logs <pod-name> -c <container-name> -n rgfshop

# Stream all pods
kubectl logs -f -l app=rgfshop -n rgfshop

# Jenkins logs
docker-compose logs -f jenkins

# Check events
kubectl get events -n rgfshop --sort-by='.lastTimestamp'
```

---

## Best Practices

### Security
- Use AWS Secrets Manager or Kubernetes Secrets for sensitive data
- Enable encryption at rest for RDS
- Use TLS/SSL for all external endpoints
- Implement network policies in Kubernetes
- Regular security scanning with Trivy/Clair

### High Availability
- Multi-AZ deployments
- RDS Multi-AZ with read replicas
- Auto-scaling based on metrics
- Health checks and liveness probes
- Circuit breakers and retry logic

### Cost Optimization
- Use spot instances for non-critical workloads
- Right-size EC2 instances
- Enable S3 lifecycle policies
- Use AWS Cost Explorer
- Implement resource tagging

### Monitoring
- Set up alerts for critical metrics
- Monitor application performance (APM)
- Track deployment success rates
- Log aggregation and analysis
- Distributed tracing


## License

This project is licensed under the MIT License - see the LICENSE file for details.

--
**Happy Deploying! 🚀**








































































