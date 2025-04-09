Devops Internship Day-2

TASK -2
# 🚀 CI/CD Pipeline with Jenkins on AWS

This project demonstrates how to set up a Continuous Integration and Continuous Deployment (CI/CD) pipeline using **Jenkins**, hosted on an **AWS EC2 instance**, to automate the build and deployment process of a full-stack application.

## 🧰 Tech Stack

- **Frontend:** React (client)
- **Backend:** Node.js + Express (backend)
- **CI/CD Tool:** Jenkins
- **Hosting:** AWS EC2 (Ubuntu)

## 🔧 Setup Overview

### 1. Jenkins on AWS

- Launched Jenkins on an EC2 Ubuntu instance
- Installed Jenkins and started the service on port 8080
- Configured security groups to allow web access

### 2. GitHub Integration

- Forked the [simple-react-full-stack](https://github.com/crsandeep/simple-react-full-stack) repository
- Added a `Jenkinsfile` to define pipeline stages
- Configured Jenkins to pull from GitHub and run pipeline on push

### 3. Jenkins Pipeline Stages

The `Jenkinsfile` includes:

```groovy
pipeline {
    agent any

    environment {
        BACKEND_DIR = 'backend'
        FRONTEND_DIR = 'client'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir("${env.BACKEND_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir("${env.FRONTEND_DIR}") {
                    sh 'npm install'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir("${env.FRONTEND_DIR}") {
                    sh 'npm run build'
                }
            }
        }

        stage('Test Backend') {
            steps {
                dir("${env.BACKEND_DIR}") {
                    sh 'npm test || true'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deployment placeholder (can be replaced with S3, EC2, Docker, etc.)'
            }
        }
    }
}
