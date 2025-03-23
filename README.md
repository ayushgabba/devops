# FastAPI Deployment with GitHub Actions & Docker

## Overview
This project demonstrates the Continuous Integration and Continuous Deployment (CI/CD) pipeline for a FastAPI application using GitHub Actions and Docker. The pipeline automates building a Docker image, pushing it to Docker Hub, and deploying it.

## Technologies Used
- **FastAPI** - Web framework for building APIs in Python
- **Docker** - Containerization platform
- **GitHub Actions** - CI/CD automation tool
- **Docker Hub** - Container registry for storing Docker images

## Prerequisites
Before running the project, ensure you have:
1. **GitHub Repository** - The source code is hosted on GitHub.
2. **Docker Installed** - Install Docker on your local machine.
3. **Docker Hub Account** - To store and manage container images.
4. **GitHub Secrets Configured**:
   - `DOCKER_USERNAME` - Your Docker Hub username
   - `DOCKER_PASSWORD` - Your Docker Hub password

## Project Structure
```
fastapi-github-actions/
│── app/
│   ├── main.py      # FastAPI application entry point
│── Dockerfile       # Docker build configuration
│── .github/
│   ├── workflows/
│   │   ├── DockerBuild.yml  # GitHub Actions workflow
│── README.md        # Project documentation
```

## Setting Up GitHub Actions Workflow

### `.github/workflows/DockerBuild.yml`
The workflow automates the process of building and pushing the Docker image.

```yaml
name: Docker Image Build

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Login to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Build and Push Docker Image
        run: |
          docker build -t ayushgabba16/fastapi-app:latest .
          docker push ayushgabba16/fastapi-app:latest
```

## Running the Project Locally
1. Clone the repository:
   ```sh
   git clone https://github.com/ayushgabba/devops.git
   cd devops
   ```
2. Build and run the Docker container:
   ```sh
   docker build -t fastapi-app .
   docker run -p 8000:8000 fastapi-app
   ```
3. Open `http://localhost:8000/docs` in your browser to test the FastAPI app.

## Deployment
- Each commit to the `main` branch triggers GitHub Actions to:
  1. Build the Docker image
  2. Push it to Docker Hub

## Docker Hub Image URL
```
docker.io/ayushgabba16/fastapi-app:latest
```

## Conclusion
This experiment successfully integrates FastAPI with GitHub Actions and Docker for automated deployment. 🚀

