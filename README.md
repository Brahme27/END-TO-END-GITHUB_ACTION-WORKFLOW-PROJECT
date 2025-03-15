# CI/CD for Dockerized Flask App

This repository contains a simple Flask application with a CI/CD pipeline using GitHub Actions. The application is containerized using Docker and automatically built, tested, and pushed to Docker Hub.

## Project Overview

This project demonstrates how to set up a **CI/CD workflow** for a **Flask application** using:
- **GitHub Actions** for automation
- **Docker** for containerization
- **Pytest** for testing
- **Docker Hub** for container registry

## Folder Structure
```
/
├── app.py               # Flask Application
├── test_app.py          # Pytest for testing the Flask app
├── Dockerfile           # Docker configuration file
├── requirements.txt     # Python dependencies (Flask, pytest)
├── .github/workflows/
│   ├── ci-cd.yml       # GitHub Actions workflow
└── README.md            # Project documentation
```

## Setup and Installation

### Prerequisites
Ensure you have the following installed:
- Python 3.9+
- Docker
- Git

### Clone the Repository
```sh
git clone https://github.com/Brahme27/END-TO-END-GITHUB_ACTION-WORKFLOW-PROJECT.git
cd END-TO-END-GITHUB_ACTION-WORKFLOW-PROJECT
```

### Install Dependencies
```sh
pip install -r requirements.txt
```

### Run the Flask Application Locally
```sh
python app.py
```
The application will be available at `http://localhost:5000`.

## Running Tests
To run unit tests using Pytest:
```sh
pytest
```

## Docker Setup

### Build Docker Image
```sh
docker build -t flasktest-app .
```

### Run Docker Container
```sh
docker run -p 5000:5000 flasktest-app
```

## CI/CD Pipeline with GitHub Actions
This repository is configured with a **CI/CD workflow** that automates the following steps:
1. **Build and Test** - On every push or pull request to `main`:
   - Checkout the code
   - Set up Python and install dependencies
   - Run tests using Pytest
2. **Build and Publish Docker Image** - If tests pass:
   - Set up Docker Buildx
   - Authenticate to Docker Hub
   - Build and push the Docker image

### Workflow File (`.github/workflows/ci-cd.yml`)
```yaml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```

## Deploying to Docker Hub
Ensure you have set up GitHub Secrets:
- `DOCKER_USERNAME`: Your Docker Hub username
- `DOCKER_PASSWORD`: Your Docker Hub password or access token

Once the workflow runs successfully, you can pull the latest image from Docker Hub:
```sh
docker pull <DOCKER_USERNAME>/flasktest-app:latest
docker run -p 5000:5000 <DOCKER_USERNAME>/flasktest-app
```