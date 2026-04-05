# Flask App — Docker & Jenkins CI/CD Pipeline

A simple Python Flask app containerized with Docker and automated through a Jenkins pipeline.

## Pipeline Stages

1. **Clone** — pulls the repo from GitHub
2. **Build** — builds the Docker image (`rawdaessamrou/flask-app:latest`)
3. **Push** — pushes the image to Docker Hub

## Files

| File | Description |
|------|-------------|
| `hello.py` | Flask application |
| `Dockerfile` | Container image definition |
| `Jenkinsfile` | CI/CD pipeline definition |
| `jenkins-shared-lib/` | Reusable Jenkins shared library |
| `requirements.txt` | Python dependencies |

## Prerequisites

- Docker
- Jenkins with Docker plugin and `docker-credentials` configured
