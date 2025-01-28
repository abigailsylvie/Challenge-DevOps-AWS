# Sports API Management System

Build a scalable, containerized API management system for real-time sports data using **AWS ECS (Fargate)**, **API Gateway**, and an external **Sports API**.

---

## Features
- REST API for real-time sports data.
- Containerized backend powered by Amazon ECS (Fargate).
- Serverless architecture with API Gateway.

---

## Requirements
1. **Sports API Key**: Sign up at [SerpAPI](https://serpapi.com).
2. **AWS Account**: Basic knowledge of ECS, API Gateway, Docker, and Python.
3. **AWS CLI**: Installed and configured.
4. **SerpAPI Library**: Install:
   ```bash
   pip install google-search-results
   ```
5. **Docker**: CLI and Desktop installed.

---

## Setup Steps

### 1. Clone the Repository
```bash
git clone https://github.com/ifeanyiro9/containerized-sports-api.git
cd containerized-sports-api
```

### 2. Create ECR Repository and Push Docker Image
```bash
aws ecr create-repository --repository-name sports-api --region us-east-1
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com

docker build --platform linux/amd64 -t sports-api .
docker tag sports-api:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:latest
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:latest
```

### 3. Set Up ECS with Fargate
1. **Create a Cluster**: Name it `sports-api-cluster` (Fargate launch type).
2. **Task Definition**:
   - Name: `sports-api-task`
   - Container:
     - **Image**: `<ECR_URI>`
     - **Port**: 8080 (TCP)
     - **Env Variable**: `SPORTS_API_KEY=<YOUR_API_KEY>`
3. **Service**:
   - Use Application Load Balancer (ALB).
   - Health check path: `/sports`.

Retrieve ALB DNS: `sports-api-alb-<AWS_ACCOUNT_ID>.us-east-1.elb.amazonaws.com`

### 4. Configure API Gateway
1. Create a REST API: Name it `Sports API Gateway`.
2. Resource `/sports` (GET method): Integrate with ALB DNS.
3. Deploy to stage (e.g., `prod`).

---

## Test the API
Access the endpoint:
```bash
curl https://<api-gateway-id>.execute-api.us-east-1.amazonaws.com/prod/sports
```

---

## Future Enhancements
1. Add caching with ElastiCache.
2. Store user queries in DynamoDB.
3. Secure API Gateway with authentication.
4. Automate deployments using CI/CD.

---
