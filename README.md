# 🚀 Flask App CI/CD Pipeline using GitHub Actions, Docker, Trivy & EC2 Self-Hosted Runner

A complete end-to-end DevOps CI/CD project demonstrating automated Docker image building, security scanning, and deployment of a Flask application to an AWS EC2 Ubuntu server using GitHub Actions and a Self-Hosted Runner.

---

## 📌 Project Overview

This project implements a production-style CI/CD pipeline for a containerized Flask application.

The pipeline automatically:

* Builds a Docker image
* Pushes the image to DockerHub
* Performs vulnerability scanning using Trivy
* Uses Composite Actions and Reusable Workflows
* Deploys the latest image to an EC2 Ubuntu Self-Hosted Runner
* Replaces the old container with the new version
* Makes the Flask application available on the EC2 Public IP

---

# 🏗 Architecture

```text
Developer Push
        ↓
GitHub Actions (GitHub-hosted Runner)
        ↓
Reusable Workflow
        ↓
Composite Action
        ↓
Docker Build
        ↓
DockerHub Push
        ↓
Trivy Security Scan
        ↓
Self-Hosted Runner (EC2 Ubuntu)
        ↓
docker pull latest image
        ↓
stop old container
        ↓
remove old container
        ↓
run new container
        ↓
Flask Application Live on EC2 Public IP
```

---

# 🛠 Tech Stack

* Python Flask
* Docker
* DockerHub
* GitHub Actions
* Composite Actions
* Reusable Workflows
* Trivy Security Scanner
* AWS EC2 Ubuntu
* Self-Hosted GitHub Runner
* Linux
* Git & GitHub

---

# 📁 Project Structure

```text
flask-app-gitactions
│
├── app.py
├── run.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
│
└── .github
    ├── actions
    │   └── docker-build-push
    │       └── action.yml
    │
    └── workflows
        ├── docker-build.yml
        ├── reusable-docker-build.yml
        ├── caller-docker-build.yml
        └── deploy-ec2.yml
```

---

# ⚙️ CI Pipeline

### Stage 1 – Docker Build

* Checkout repository
* Build Docker image
* Validate Dockerfile and application packaging

### Stage 2 – DockerHub Push

* Login using GitHub Secrets
* Tag Docker image
* Push latest image to DockerHub

### Stage 3 – Build Artifact

* Generate build report
* Upload artifact to GitHub Actions

### Stage 4 – Composite Action

Created custom action:

```text
.github/actions/docker-build-push/action.yml
```

Encapsulated:

* Docker Build
* DockerHub Login
* Docker Push

### Stage 5 – Reusable Workflow

Created reusable workflow:

```text
reusable-docker-build.yml
```

Caller workflow invokes the reusable workflow and passes:

* Image Name
* DockerHub Username
* DockerHub Password

### Stage 6 – Trivy Security Scan

* Install Trivy
* Scan Docker image
* Generate vulnerability report
* Upload report as GitHub Artifact

---

# 🚀 CD Pipeline

Deployment runs on an AWS EC2 Ubuntu Self-Hosted Runner.

Deployment Steps:

```text
DockerHub Login
↓
Pull Latest Image
↓
Stop Existing Container
↓
Remove Existing Container
↓
Run New Container
↓
Verify Container Status
```

Deployment command:

```bash
docker pull <dockerhub-user>/flask-app-gitactions:latest

docker stop flask-app-gitactions || true
docker rm flask-app-gitactions || true

docker run -d \
  --name flask-app-gitactions \
  -p 80:80 \
  <dockerhub-user>/flask-app-gitactions:latest
```

---

# 🔐 GitHub Secrets Used

Repository → Settings → Secrets and Variables → Actions

```text
DOCKER_USER
DOCKER_PASSWORD
```

---

# ☁️ AWS Infrastructure

### EC2 Configuration

* Ubuntu Server 24.04 LTS
* Self-Hosted GitHub Runner
* Docker Engine Installed
* Security Group:

| Port | Purpose           |
| ---- | ----------------- |
| 22   | SSH               |
| 80   | Flask Application |

---

# 📷 Project Screenshots

## Repository Setup

* 01_project_files_verified.png
* 02_dockerfile_verified.png
* 03_workflows_folder_created.png
* 04_docker_build_workflow_created.png
* 05_docker_build_workflow_pushed.png

## Docker Build Pipeline

* 06_workflow_run_started.png
* 07_docker_build_success.png

## DockerHub Integration

* 08_docker_user_and_password_secret_created.png
* 09_dockerhub_push_workflow_created.png
* 10_dockerhub_workflow_pushed.png
* 11_dockerhub_workflow_started.png
* 12_dockerhub_push_success.png
* 13_dockerhub_image_uploaded.png

## Build Artifacts

* 14_artifact_step_added.png
* 15_artifact_workflow_pushed.png
* 16_build_artifact_uploaded.png
* 17_build_report_verified.png

## Composite Actions

* 18_composite_action_created.png
* 19_workflow_using_composite_action.png
* 20_composite_action_workflow_success.png
* 21_composite_action_artifact_uploaded.png

## Reusable Workflows

* 22_reusable_workflow_created.png
* 23_caller_workflow_created.png
* 24_reusable_workflow_pushed.png
* 25_caller_workflow_manual_trigger.png
* 26_reusable_workflow_called_successfully.png

## Trivy Security Scanning

* 27_trivy_steps_added.png
* 28_trivy_artifact_step_added.png
* 29_trivy_workflow_pushed.png
* 30_trivy_workflow_running.png
* 31_trivy_report_artifact_uploaded.png
* 32_trivy_report_verified.png

## EC2 Self-Hosted Runner

* 33_ec2_instance_created.png
* 34_ec2_ssh_connected.png
* 35_docker_installed_permission_granted_on_ec2.png
* 36_runner_files_downloaded.png
* 37_github_runner_setup_page.png
* 38_runner_configured.png
* 39_runner_listening_for_jobs.png
* 40_runner_online_in_github.png

## Deployment

* 40_deploy_ec2_workflow_created.png
* 41_deploy_workflow_pushed.png
* 42_deploy_workflow_triggered.png
* 43_deployment_job_success.png
* 44_container_running_on_ec2.png
* 45_flask_app_live_on_ec2.png

---

# 🎯 Key DevOps Concepts Demonstrated

✅ GitHub Actions CI/CD

✅ Docker Containerization

✅ DockerHub Image Registry

✅ GitHub Secrets Management

✅ Composite Actions

✅ Reusable Workflows

✅ Trivy Security Scanning

✅ Build Artifacts

✅ AWS EC2 Self-Hosted Runner

✅ Automated Container Deployment

✅ Zero Manual Deployment Process

---

# 🌐 Final Result

Every push to GitHub can automatically:

```text
Build Application
↓
Create Docker Image
↓
Push to DockerHub
↓
Scan for Vulnerabilities
↓
Deploy on EC2
↓
Replace Existing Container
↓
Serve Flask Application Live
```

This project demonstrates an end-to-end modern DevOps CI/CD implementation using GitHub Actions, Docker, Trivy, and AWS EC2 Self-Hosted Runners.
