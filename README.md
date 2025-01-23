# Sports API Management System

## Project Overview
This project focuses on building a containerized API management system for querying real-time sports data. By leveraging **Amazon ECS (Fargate)** for running containers, **Amazon API Gateway** for exposing REST endpoints, and an external **Sports API**, it showcases advanced cloud computing practices like API management, container orchestration, and secure AWS integrations.

---

## Features
- Provides a REST API for real-time sports data queries.
- Uses Amazon ECS (Fargate) for a containerized backend.
- Implements a scalable and serverless architecture.
- Employs Amazon API Gateway for API management and routing.

---

## Prerequisites
1. **Sports API Key**: Obtain your API key by signing up at [SerpAPI](https://serpapi.com).
2. **AWS Account**: Ensure an AWS account is ready with a basic understanding of ECS, API Gateway, Docker, and Python.
3. **AWS CLI**: Install and configure the AWS CLI for programmatic interaction.
4. **SerpAPI Library**: Install the SerpAPI library:
   ```bash
   pip install google-search-results
   ```
5. **Docker**: Ensure Docker CLI and Desktop are installed for building and pushing container images.

---

## Technical Architecture
![Technical Architecture](https://github.com/user-attachments/assets/32e49fe6-df16-40cb-b262-af1478cf01d5)

---

## Technologies
- **Cloud Provider**: AWS
- **Core Services**: Amazon ECS (Fargate), API Gateway, CloudWatch
- **Programming Language**: Python 3.x
- **Containerization**: Docker
- **Security**: IAM policies with the least privilege for ECS and API Gateway

---

## Project Structure

```bash
sports-api-management/
├── app.py           # Flask application for querying sports data
├── Dockerfile       # Dockerfile for containerizing the Flask app
├── requirements.txt # Python dependencies
├── .gitignore
└── README.md        # Project documentation
```

---

## Setup Instructions

### Clone the Repository
```bash
git clone https://github.com/ifeanyiro9/containerized-sports-api.git
cd containerized-sports-api
```

### Create an ECR Repository
```bash
aws ecr create-repository --repository-name sports-api --region us-east-1
```

### Build and Push the Docker Image
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com

docker build --platform linux/amd64 -t sports-api .
docker tag sports-api:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:latest
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:latest
```

### Set Up an ECS Cluster with Fargate
1. **Create a Cluster**:
   - Navigate to the ECS Console.
   - Create a new cluster named `sports-api-cluster`.
   - Select the **Fargate** option for infrastructure.

2. **Define a Task**:
   - Go to Task Definitions → Create New Task Definition.
   - Name the task `sports-api-task`.
   - Use the Fargate launch type and specify the container details:
     - **Name**: sports-api-container
     - **Image URI**: `<AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:latest`
     - **Port**: 8080 (Protocol: TCP)
   - Add an environment variable for the Sports API key:
     - **Key**: `SPORTS_API_KEY`
     - **Value**: `<YOUR_API_KEY>`

3. **Deploy the Service**:
   - Create a new service in the ECS cluster.
   - Use an Application Load Balancer (ALB) for traffic routing.
   - Configure the ALB:
     - Health check path: `/sports`

4. **Test the Service**:
   - Retrieve the ALB DNS name (e.g., `sports-api-alb-<AWS_ACCOUNT_ID>.us-east-1.elb.amazonaws.com`).
   - Access the API by navigating to `http://<ALB_DNS_NAME>/sports`.

### Configure API Gateway
1. **Create a REST API**:
   - Navigate to the API Gateway Console and create a new REST API.
   - Name the API `Sports API Gateway`.

2. **Set Up Integration**:
   - Add a resource `/sports` with a GET method.
   - Use the ALB DNS name as the endpoint.

3. **Deploy the API**:
   - Deploy to a stage (e.g., `prod`).
   - Note the API Gateway endpoint URL.

### Test the System
Use `curl` or a browser to test the API:
```bash
curl https://<api-gateway-id>.execute-api.us-east-1.amazonaws.com/prod/sports
```

---

## Lessons Learned
- Setting up scalable, containerized applications with ECS.
- Managing public APIs using API Gateway.

---

## Future Enhancements
1. **Caching**: Use Amazon ElastiCache for frequent API requests.
2. **Data Storage**: Integrate DynamoDB to store user-specific queries.
3. **Security**: Implement API Gateway authentication using API keys or IAM.
4. **Automation**: Introduce CI/CD pipelines for container deployment.
