# Node.js CI/CD Pipeline

## Overview

This project demonstrates a CI/CD pipeline using GitHub Actions
for a Node.js application.

## Technologies Used

- Node.js
- Express.js
- Git
- GitHub
- GitHub Actions
- Docker
- Docker Hub

## CI/CD Workflow

The pipeline is triggered whenever code is pushed to the main branch.

Pipeline:

1. Checkout source code
2. Setup Node.js
3. Install dependencies
4. Run tests
5. Login to Docker Hub
6. Build Docker image
7. Push Docker image to Docker Hub

## Project Structure

```text
nodejs-demo-app/
├── .github/
│   └── workflows/
│       └── main.yml
├── app.js
├── test.js
├── package.json
├── package-lock.json
├── Dockerfile
├── .dockerignore
└── README.md
