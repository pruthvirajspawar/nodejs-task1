# Node.js CI/CD Pipeline using GitHub Actions and Docker

## 📌 Project Overview

This project demonstrates a complete CI/CD pipeline for a Node.js web application using GitHub Actions and Docker.

The main objective is to automate the process of:

1. Getting the source code from GitHub
2. Setting up the Node.js environment
3. Installing application dependencies
4. Running automated tests
5. Building a Docker image
6. Authenticating with Docker Hub
7. Pushing the Docker image to Docker Hub

The pipeline is automatically triggered whenever code is pushed to the `main` branch.

---

## 🎯 Project Objective

The objective of this project is to understand and implement a basic CI/CD workflow using GitHub Actions.

Instead of manually performing every deployment step, the pipeline automates the process from code commit to Docker image publishing.

### Manual Process

Without CI/CD:

Developer
   ↓
Write Code
   ↓
Run Tests
   ↓
Build Docker Image
   ↓
Login to Docker Hub
   ↓
Push Docker Image

### Automated Process

With GitHub Actions:

Developer
   ↓
Git Push
   ↓
GitHub Repository
   ↓
GitHub Actions
   ↓
Checkout Code
   ↓
Setup Node.js
   ↓
Install Dependencies
   ↓
Run Tests
   ↓
Build Docker Image
   ↓
Login to Docker Hub
   ↓
Push Image
   ↓
Docker Hub

---

# 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Node.js | Application runtime |
| Express.js | Web application framework |
| Git | Version control |
| GitHub | Source code repository |
| GitHub Actions | CI/CD automation |
| Docker | Application containerization |
| Docker Hub | Docker image registry |
| YAML | GitHub Actions workflow configuration |

---

# 📂 Project Structure

```text
nodejs-demo-app/
│
├── .github/
│   └── workflows/
│       └── main.yml
│
├── app.js
├── test.js
├── package.json
├── package-lock.json
├── Dockerfile
├── .dockerignore
└── README.md
