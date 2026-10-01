# Node.js CI/CD Pipeline using GitHub Actions and Docker

## Project Overview

This project demonstrates a basic CI/CD pipeline for a Node.js web application.

The application is automatically tested, containerized using Docker, and the Docker image is pushed to Docker Hub using GitHub Actions.

The pipeline is triggered whenever code is pushed to the `main` branch.

## Objective

The main objective of this project is to understand and implement a complete CI/CD automation process using:

- Node.js
- GitHub
- GitHub Actions
- Docker
- Docker Hub

The pipeline follows:

**Test → Build → Push**

---

## Technologies Used

| Technology | Purpose |
|---|---|
| Node.js | Runtime environment for the application |
| Express.js | Used to create the web application |
| Git | Version control |
| GitHub | Source code repository |
| GitHub Actions | CI/CD automation |
| Docker | Application containerization |
| Docker Hub | Docker image registry |
| YAML | GitHub Actions workflow configuration |

---

## Project Structure

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
```

### File Description

- **app.js** - Contains the Node.js Express application.
- **test.js** - Contains the application test.
- **package.json** - Contains project information, dependencies, and npm scripts.
- **package-lock.json** - Maintains the dependency versions.
- **Dockerfile** - Contains instructions to build the Docker image.
- **.dockerignore** - Specifies files that should not be copied into the Docker image.
- **main.yml** - Defines the GitHub Actions CI/CD pipeline.
- **README.md** - Project documentation.

---

## Application

The application is built using Node.js and Express.js.

The server runs on port `3000`.

### Home Endpoint

```text
GET /
```

Response:

```text
Hello from Node.js CI/CD Pipeline!
```

### Health Check Endpoint

```text
GET /health
```

Response:

```json
{
  "status": "OK"
}
```

The health endpoint is used to verify whether the application is running correctly.

---

## Run the Application Locally

Install dependencies:

```bash
npm install
```

Run tests:

```bash
npm test
```

Start the application:

```bash
npm start
```

The application will be available at:

```text
http://localhost:3000
```

Health check:

```text
http://localhost:3000/health
```

---

## Testing

The project uses the Node.js built-in testing module.

The test is executed using:

```bash
npm test
```

If the test passes, the CI/CD pipeline can continue to the Docker stages.

If the test fails, the pipeline stops and the Docker image is not pushed.

---

## Docker

Docker is used to containerize the Node.js application.

### Build Docker Image

```bash
docker build -t nodejs-demo-app .
```

Check the image:

```bash
docker images
```

### Run Docker Container

```bash
docker run -d -p 3000:3000 --name nodejs-demo-container nodejs-demo-app
```

Check the running container:

```bash
docker ps
```

Open the application:

```text
http://localhost:3000
```

### Stop Container

```bash
docker stop nodejs-demo-container
```

### Remove Container

```bash
docker rm nodejs-demo-container
```

---

## GitHub Actions CI/CD

The GitHub Actions workflow is located at:

```text
.github/workflows/main.yml
```

The workflow is triggered whenever code is pushed to the `main` branch.

### CI/CD Flow

```text
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
Login to Docker Hub
    ↓
Build Docker Image
    ↓
Push Docker Image
    ↓
Docker Hub
```

---

## GitHub Actions Pipeline Steps

### 1. Checkout Code

The `actions/checkout` action downloads the repository code into the GitHub Actions runner.

### 2. Setup Node.js

The `actions/setup-node` action configures the required Node.js environment.

### 3. Install Dependencies

The pipeline installs the required Node.js packages:

```bash
npm install
```

### 4. Run Tests

The application tests are executed:

```bash
npm test
```

### 5. Login to Docker Hub

GitHub Actions authenticates with Docker Hub using GitHub Secrets.

### 6. Build Docker Image

The Docker image is built using the Dockerfile.

### 7. Push Docker Image

The Docker image is pushed to Docker Hub.

---

## GitHub Secrets

Docker Hub credentials are not hardcoded in the workflow.

The following GitHub Actions Secrets are used:

```text
DOCKER_USERNAME
DOCKER_TOKEN
```

### DOCKER_USERNAME

Contains the Docker Hub username.

### DOCKER_TOKEN

Contains the Docker Hub access token.

The workflow accesses them using:

```yaml
${{ secrets.DOCKER_USERNAME }}
```

and:

```yaml
${{ secrets.DOCKER_TOKEN }}
```

Using GitHub Secrets helps keep sensitive credentials outside the source code.

---

## Docker Hub

Docker Hub is used as the container image registry.

After the pipeline successfully completes, the Docker image is pushed to Docker Hub.

Image format:

```text
YOUR_DOCKER_USERNAME/nodejs-demo-app:latest
```

The `latest` tag represents the latest image pushed by the pipeline.

---

## CI/CD Explanation

### Continuous Integration

Continuous Integration means automatically validating code changes when they are integrated into the shared repository.

In this project, CI includes:

```text
Code Push
    ↓
Checkout
    ↓
Install Dependencies
    ↓
Run Tests
```

### Continuous Delivery / Deployment

After the tests pass, the application is packaged as a Docker image and pushed to Docker Hub.

```text
Tests Pass
    ↓
Docker Build
    ↓
Docker Push
    ↓
Docker Hub
```

---

## GitHub Actions Runner

A runner is the machine or environment where GitHub Actions executes the workflow.

This project uses:

```yaml
runs-on: ubuntu-latest
```

Therefore, the workflow runs on a GitHub-hosted Ubuntu environment.

The runner executes commands such as:

```bash
npm install
npm test
docker build
docker push
```

---

## Jobs and Steps

A **job** is a collection of related tasks executed on a runner.

Example:

```yaml
jobs:
  build-and-deploy:
```

A **step** is an individual task inside a job.

Examples:

```text
Checkout Code
Setup Node.js
Install Dependencies
Run Tests
Login to Docker Hub
Build Docker Image
Push Docker Image
```

The basic structure is:

```text
Workflow
    ↓
Job
    ↓
Steps
```

---

## Error Handling

If an important step fails, GitHub Actions normally stops the remaining steps of that job.

For example:

```text
Install Dependencies
        ↓
      Success
        ↓
     Run Tests
        ↓
      Failed
        ↓
   Pipeline Stops
```

Therefore, if the test fails, the Docker image will not be pushed.

---

## Security

Sensitive credentials should never be directly written inside:

```text
main.yml
Dockerfile
app.js
README.md
```

Instead, GitHub Actions Secrets are used.

Example:

```yaml
username: ${{ secrets.DOCKER_USERNAME }}
password: ${{ secrets.DOCKER_TOKEN }}
```

This prevents Docker Hub credentials from being exposed in the source code.

---

## Troubleshooting

### Docker Hub Login Error

If GitHub Actions shows:

```text
Error: Password required
```

check the following GitHub repository secrets:

```text
DOCKER_USERNAME
DOCKER_TOKEN
```

Make sure `DOCKER_TOKEN` contains a valid Docker Hub access token.

### Test Failure

Run the test locally:

```bash
npm test
```

Fix the issue and push the changes again.

### Docker Build Failure

Check:

- Dockerfile syntax
- Dockerfile location
- `package.json`
- Application files
- Docker image name

### Container Not Running

Check:

```bash
docker ps
```

View container logs:

```bash
docker logs nodejs-demo-container
```

---

## Interview Explanation

> I created a simple Node.js application using Express.js and implemented a CI/CD pipeline using GitHub Actions and Docker.
>
> The pipeline is triggered whenever code is pushed to the main branch. GitHub Actions first checks out the source code, sets up Node.js, installs the dependencies, and runs the application tests.
>
> If the tests pass, the workflow logs into Docker Hub using GitHub Secrets, builds the Docker image using the Dockerfile, and pushes the image to Docker Hub.
>
> Through this project, I learned how GitHub Actions can automate testing, Docker image creation, and delivery of an application image.

---

## Interview Questions

### 1. What is CI/CD?

CI/CD is a software development practice used to automate activities such as code integration, testing, building, and delivering applications.

### 2. How does GitHub Actions work?

GitHub Actions uses YAML workflow files to define automated tasks. The workflow is triggered by events such as a push to a branch and executes jobs on a runner.

### 3. What is a runner?

A runner is the machine or environment where GitHub Actions executes workflow jobs.

In this project:

```yaml
runs-on: ubuntu-latest
```

is used.

### 4. What is the difference between a job and a step?

A job is a collection of related tasks executed on a runner, while a step is an individual task inside a job.

### 5. How did you secure Docker Hub credentials?

I stored the Docker Hub username and access token as GitHub Actions Secrets instead of hardcoding them in the workflow.

### 6. What happens if the test fails?

The pipeline stops at the testing stage, so the Docker image is not built or pushed.

### 7. Explain the Docker build-push workflow.

After the tests pass, GitHub Actions builds the Docker image using the Dockerfile, authenticates with Docker Hub, and pushes the image to the Docker Hub repository.

### 8. How can you test the CI/CD pipeline?

I can test the application locally using:

```bash
npm test
```

Then I can push the code to the `main` branch and verify the workflow from the GitHub Actions tab.

### 9. Why did you use Docker?

Docker packages the application and its dependencies into a portable container image, making the application easier to run consistently in different environments.

---

## Learning Outcomes

Through this project, I learned:

- Git and GitHub
- GitHub Actions
- CI/CD concepts
- GitHub Actions runners
- Jobs and steps
- GitHub Secrets
- Node.js and npm
- Dockerfile
- Docker image building
- Docker containers
- Docker Hub
- CI/CD troubleshooting

---

## Final Result

The final automated process is:

```text
Developer
    ↓
Git Push
    ↓
GitHub
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
Docker Login
    ↓
Docker Build
    ↓
Docker Push
    ↓
Docker Hub
```

The project demonstrates how a Node.js application can be integrated with a CI/CD pipeline to automate testing, Docker image creation, and pushing the image to Docker Hub.

---

## Conclusion

This project provided practical experience with Node.js, Git, GitHub, GitHub Actions, Docker, Docker Hub, and CI/CD concepts.

The main goal was to reduce manual work by automating the process from code push to Docker image delivery.
