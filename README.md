# Backstage Service Example

A Java web application example demonstrating CI/CD pipeline integration with GitLab, SonarQube analysis, Docker containerization, and Kubernetes deployment.

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Building the Application](#building-the-application)
- [Docker Support](#docker-support)
- [Kubernetes Deployment](#kubernetes-deployment)
- [CI/CD Pipeline](#cicd-pipeline)
- [Code Quality](#code-quality)
- [Configuration](#configuration)
- [Contributing](#contributing)

## 🌟 Overview

This project serves as a template for Java web applications with modern DevOps practices including:

- **Java 11** with Maven build system
- **Tomcat 9** as the servlet container
- **Docker** containerization
- **Kubernetes** deployment manifests
- **GitLab CI/CD** pipeline with multiple stages
- **SonarQube** integration for code quality analysis
- **AWS EKS** deployment support

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Source Code   │───▶│   Build & Test  │───▶│   Docker Image  │
│   (Java WAR)    │    │   (Maven)       │    │   (Tomcat)      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                       │
                                                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Load Balancer  │◀───│   Kubernetes    │◀───│  Container      │
│   (Service)     │    │   (Deployment)  │    │  Registry       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 📚 Prerequisites

- **Java 11** or higher
- **Maven 3.6+**
- **Docker** (for containerization)
- **kubectl** (for Kubernetes deployment)
- **AWS CLI** (for EKS deployment)
- **GitLab** account (for CI/CD pipeline)

## 📁 Project Structure

```
backstage-service-example/
├── src/                          # Java source code
├── target/                       # Maven build output
├── .gitlab-ci.yml               # GitLab CI/CD pipeline configuration
├── Application.yaml             # Kubernetes deployment manifests
├── Dockerfile                   # Docker image configuration
├── pom.xml                      # Maven project configuration
└── README.md                    # Project documentation
```

## 🚀 Getting Started

### Local Development

1. **Clone the repository:**
   ```bash
   git clone https://github.com/harihar3/backstage-service-example.git
   cd backstage-service-example
   ```

2. **Build the application:**
   ```bash
   mvn clean package
   ```

3. **Run tests:**
   ```bash
   mvn test
   ```

4. **Deploy to local Tomcat:**
   ```bash
   cp target/my-webapp.war $TOMCAT_HOME/webapps/
   ```

## 🔨 Building the Application

### Maven Commands

```bash
# Clean and compile
mvn clean compile

# Run tests
mvn test

# Package WAR file
mvn clean package

# Skip tests during build
mvn clean package -DskipTests=true

# Run code quality checks
mvn checkstyle:check
```

## 🐳 Docker Support

### Build Docker Image

```bash
# Build the Docker image
docker build -t my-webapp:latest .

# Run the container
docker run -p 8080:8080 my-webapp:latest
```

### Access the Application

- **Local URL:** http://localhost:8080
- **Container Port:** 8080

## ☸️ Kubernetes Deployment

### Deploy to Kubernetes

```bash
# Apply Kubernetes manifests
kubectl apply -f Application.yaml

# Check deployment status
kubectl get deployments
kubectl get services
kubectl get pods

# Access the service
kubectl port-forward service/project-k8s-service 8080:80
```

### Kubernetes Resources

- **Deployment:** `project-k8s-deployment` (2 replicas)
- **Service:** `project-k8s-service` (LoadBalancer type)
- **Port:** 8080 (container) → 80 (service)
- **NodePort:** 30080

## 🔄 CI/CD Pipeline

The GitLab CI/CD pipeline includes the following stages:

### Pipeline Stages

1. **Lint** - Code style checking with Checkstyle
2. **Build** - Maven clean package
3. **Test** - Unit tests execution
4. **SonarQube Check** - Code quality analysis
5. **SonarQube Vulnerability Report** - Security scan export
6. **Dockerize** - Docker image build and push
7. **Deploy** - Kubernetes deployment to AWS EKS

### Required Variables

Set these variables in your GitLab project settings:

```bash
# Docker Registry
CI_REGISTRY_USER=<gitlab-username>
CI_REGISTRY_PASSWORD=<gitlab-token>

# SonarQube
SONAR_TOKEN=<sonar-token>
SONAR_HOST_URL=<sonar-server-url>

# AWS EKS
AWS_ACCESS_KEY_ID=<aws-access-key>
AWS_SECRET_ACCESS_KEY=<aws-secret-key>
AWS_DEFAULT_REGION=<aws-region>
```

## 📊 Code Quality

### SonarQube Integration

- **Project Key:** `hariharpanda3_gitlab-poc_2eb50b77-dee9-4ab8-98a0-39f70686ecbe`
- **Quality Gate:** Enabled
- **Coverage Reports:** Generated from Maven Surefire
- **Security Scanning:** SAST reports exported

### Code Standards

- **Java Version:** 11
- **Code Style:** Checkstyle validation
- **Testing:** JUnit 4.13.2 with Mockito 3.12.4
- **Build Tool:** Maven 3 with Eclipse Temurin 17

## ⚙️ Configuration

### Application Configuration

- **Artifact ID:** `my-webapp`
- **Group ID:** `com.example`
- **Version:** 1.0
- **Packaging:** WAR
- **Final Name:** `my-webapp`

### Dependencies

- **Servlet API:** 4.0.1 (provided)
- **JUnit:** 4.13.2 (test)
- **Mockito:** 3.12.4 (test)

### Deployment Configuration

- **Base Image:** tomcat:9.0-jdk11-openjdk
- **Exposed Port:** 8080
- **Context Path:** ROOT (deployed as ROOT.war)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is created for educational and verification purposes.

## 🆘 Support

For questions and support, please refer to the project documentation or create an issue in the repository.

---

**Note:** This repository serves as a template for cross-verifying project files after completion of development projects.
