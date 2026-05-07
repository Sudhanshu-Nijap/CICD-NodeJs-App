# CI/CD NodeJs app

This repository contains a simple, premium-looking Node.js application built with Express. It serves as a demonstration for implementing a complete CI/CD pipeline using Docker and GitHub Actions, specifically deploying to an AWS EC2 instance.

## 🚀 Features
- **Modern UI**: A dark-themed, responsive web interface tailored for video content (HTML/CSS/JS).
- **Express Backend**: A lightweight Node.js API to serve static files and video metadata.
- **Dockerized**: Includes a `Dockerfile` and `docker-compose.yml` for easy containerization.
- **Automated CI/CD**: A fully configured GitHub Actions workflow (`.github/workflows/deploy.yml`) that builds, pushes to DockerHub, and deploys to an EC2 instance.

## 🛠️ How to Run Locally

You can run this project locally using either standard Node.js or Docker.

### Option 1: Using Node.js
Ensure you have Node.js installed.

1. Install dependencies:
   ```bash
   npm install
   ```
2. Start the server:
   ```bash
   npm start
   ```
3. Open your browser and navigate to `http://localhost:3000`.

### Option 2: Using Docker
Ensure you have Docker and Docker Compose installed.

1. Build and run the container:
   ```bash
   docker-compose up --build
   ```
2. Open your browser and navigate to `http://localhost:3000`.

## 🔄 CI/CD Pipeline

The GitHub Actions pipeline is triggered automatically on pushes to the `main` branch. 

**Workflow Steps:**
1. **Checkout Code**: Grabs the latest code from the repository.
2. **DockerHub Login**: Authenticates using repository secrets.
3. **Build & Push**: Builds the Docker image and pushes it to DockerHub.
4. **Deploy to EC2**: SSHs into your EC2 server, dynamically generates the `docker-compose.yml`, pulls the latest image, and restarts the container.

### 🔑 Required GitHub Secrets
To make the deployment pipeline work, you must add the following secrets in your GitHub repository settings (**Settings > Secrets and variables > Actions**):

| Secret Name | Description |
| :--- | :--- |
| `DOCKERHUB_USERNAME` | Your DockerHub account username. |
| `DOCKERHUB_TOKEN` | A Personal Access Token (PAT) from DockerHub. |
| `EC2_HOST` | The public IP address or DNS of your target EC2 instance. |
| `EC2_USERNAME` | The SSH user for your EC2 instance (e.g., `ubuntu` or `ec2-user`). |
| `EC2_SSH_KEY` | The raw contents of your private SSH key (`.pem` file) used to access the instance. |

## 📝 License
This project is open-source and available for educational purposes.
